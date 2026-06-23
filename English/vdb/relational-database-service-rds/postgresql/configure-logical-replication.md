# Configure Logical Replication for PostgreSQL Cluster

> This guide helps you set up **PostgreSQL Logical Replication** — replicating data changes in real time from a source cluster (Publisher) to a destination cluster (Subscriber). One or both clusters can be hosted on GreenNode vDB.

---

## Prerequisites

- At least one of the two clusters (Publisher or Subscriber) must be a PostgreSQL Cluster on GreenNode vDB (**version 16 or 17**).
- Both clusters must run the **same major version** of PostgreSQL.
- The user running SQL commands must be the **owner** of the tables to replicate (to create a Publication).

{% hint style="info" %}
GreenNode vDB supports Logical Replication for **PostgreSQL 16 and 17** only.
{% endhint %}

---

## How Logical Replication Works

![Logical Replication architecture](../../../../.gitbook/assets/vdb-logical-replication-architecture.png)

- **Publisher**: the source cluster holding the original data. You create a `PUBLICATION` to define which tables are replicated.
- **Subscriber**: the destination cluster receiving changes. You create a `SUBSCRIPTION` to connect to the Publisher and pull data.

**Synchronization happens in two phases:**

1. **Initial sync**: As soon as you create a Subscription, PostgreSQL automatically copies all existing data from Publisher to Subscriber — you do not need to manually dump and restore data. This may take minutes to hours depending on data size.
2. **Streaming**: After the initial sync completes, only incremental changes (INSERT, UPDATE, DELETE) are replicated in real time.

{% hint style="info" %}
You **do not need to dump data** — Logical Replication handles that automatically. However, you **must create the table structure (schema) on the Subscriber** before creating the Subscription, because PostgreSQL does not replicate DDL. See [Step B.3](#step-b3-create-tables-on-subscriber) for instructions.
{% endhint %}

---

## Part A: vDB PostgreSQL Cluster as Publisher

> Follow the steps in this section if your GreenNode vDB cluster is the **data source** (Publisher).

### Step A.1: Request Activation

Contact **GreenNode Support** to request Logical Replication activation on your cluster. GreenNode Support will configure the cluster and provide you with a **username** and **password** for the replication user — this information will be used in the connection string when the Subscriber creates its Subscription.

To change the replication user password, run the following command on the cluster:

```sql
ALTER USER <username> PASSWORD '<new_password>';
```

{% hint style="warning" %}
When managing Subscriptions, do not delete or modify replication slots that do not belong to you. These slots may belong to the system or other Subscriptions — accidentally dropping one will cause replication loss immediately.
{% endhint %}

### Step A.2: Configure PostgreSQL Parameters

Logical Replication requires three PostgreSQL parameters to be correctly configured on the **Publisher cluster**.

| Parameter | Required value | Description |
|---|---|---|
| `wal_level` | `logical` | Required — default is `replica`, which is not sufficient for logical replication |
| `max_replication_slots` | ≥ total slots needed | Total replication slots for all replicas, subscriptions, and CDC connectors |
| `max_wal_senders` | ≥ total senders needed | Total WAL sender processes (typically equals `max_replication_slots`) |

**How to calculate `max_replication_slots` and `max_wal_senders`:**

| Component | Slots + senders needed |
|---|---|
| Each replica node in the cluster | 1 + 1 |
| Each Subscription (logical replication) | 1 + 1 |
| Each CDC connector (Debezium) | 1 + 1 |

**Example:** 3-node cluster (2 replicas) + 1 subscription → `max_replication_slots = 3`, `max_wal_senders = 3`.

{% hint style="warning" %}
Changing `wal_level`, `max_replication_slots`, and `max_wal_senders` requires a **cluster restart**. Update all three parameters at the same time to trigger only one restart. See [PostgreSQL Cluster Parameters](postgresql-cluster-parameters.md) for instructions.
{% endhint %}

### Step A.3: Create a Publication

1. Connect to the **Publisher cluster** using an account with **owner** rights on the tables to replicate.
2. Create a Publication for the tables to replicate:

```sql
-- Replicate specific tables
CREATE PUBLICATION <publication_name> FOR TABLE orders, products;
```

{% hint style="info" %}
To use `FOR ALL TABLES`, contact **GreenNode Support** — this requires superuser privileges on the cluster.
{% endhint %}

3. Verify the Publication was created:

```sql
SELECT pubname, puballtables, pubinsert, pubupdate, pubdelete
FROM pg_publication;
```

---

## Part B: vDB PostgreSQL Cluster as Subscriber

> Follow the steps in this section if your GreenNode vDB cluster is the **data destination** (Subscriber).

### Step B.1: Request Logical Replication Activation

Contact **GreenNode Support** to request Logical Replication activation on your cluster. GreenNode Support will configure the cluster and provide you with a **username** and **password** for the replication user — this information will be used in the connection string when the Subscriber creates its Subscription.

To change the replication user password, run the following command on the cluster:

```sql
ALTER USER <username> PASSWORD '<new_password>';
```

{% hint style="warning" %}
When managing Subscriptions, do not delete or modify replication slots that do not belong to you. These slots may belong to the system or other Subscriptions — accidentally dropping one will cause replication loss immediately.
{% endhint %}

### Step B.2: Grant CREATE on Schema and Target Database

Connect to the **Subscriber cluster** using the **owner** account of the target database and schema, then run the following commands:

```sql
-- Grant CREATE on the database (required to run CREATE SUBSCRIPTION)
GRANT CREATE ON DATABASE <database_name> TO <username>;

-- Grant USAGE and CREATE on the schema
GRANT USAGE ON SCHEMA <schema_name> TO <username>;
GRANT CREATE ON SCHEMA <schema_name> TO <username>;
```

{% hint style="info" %}
`<username>` here is the account used to run `CREATE TABLE` (Step B.3) and `CREATE SUBSCRIPTION` (Step B.4) — not the replication user in the CONNECTION string (provided by GreenNode in Step B.1).
{% endhint %}

### Step B.3: Create Tables on Subscriber

Logical Replication **does not create tables automatically** on the Subscriber. You must create the schema and tables on the Subscriber before creating the Subscription.

{% hint style="info" %}
**Tip:** Instead of writing DDL by hand, use `pg_dump --schema-only` to dump the table structure from the Publisher, review the file, then apply it to the Subscriber with `psql -f`.
{% endhint %}

```bash
# Step 1: dump schema from Publisher to a file
pg_dump \
  --schema-only \
  --table=<table_name> \
  -h <publisher_hostname> \
  -U <username> \
  -d <database_name> \
  -f schema.sql

# Step 2: inspect the file before applying (optional)
# cat schema.sql

# Step 3: apply to Subscriber
psql \
  -h <subscriber_hostname> \
  -U <username> \
  -d <database_name> \
  -f schema.sql
```

To dump multiple tables, repeat `--table` for each one. Omit `--table` to dump the entire schema.

**Or create the table manually:**

```sql
-- Example: create the orders table on Subscriber
CREATE TABLE orders (
    id      serial PRIMARY KEY,
    product text   NOT NULL,
    qty     int    NOT NULL,
    ts      timestamptz DEFAULT now()
);
```

{% hint style="warning" %}
The schema and data types of tables on the Subscriber must **exactly match** the Publisher. A mismatch will cause the Subscription to fail when applying changes.
{% endhint %}

### Step B.4: Create a Subscription

1. Connect to the **Subscriber cluster** using the GreenNode-provided account.
2. Create the Subscription:

```sql
CREATE SUBSCRIPTION my_subscription
    CONNECTION 'host=<publisher_hostname> port=5432 dbname=<database_name> user=<username> password=<password> sslmode=require'
    PUBLICATION <publication_name>;
```

| Parameter | Description |
|---|---|
| `host` | Publisher hostname |
| `port` | PostgreSQL connection port |
| `dbname` | Source database name on Publisher |
| `user` | Username with replication rights on Publisher |
| `password` | Password with replication rights on Publisher |
| `sslmode` | SSL encryption mode |
| `publication_name` | Publication name on Publisher |

{% hint style="warning" %}
After creating the Subscription, PostgreSQL performs an **initial sync** — copying all existing data from the Publisher to the Subscriber. This may take minutes to hours depending on data size.
{% endhint %}

---

## Verify Replication Status

**On Publisher** — check connected Subscriptions:

```sql
SELECT application_name, state, sent_lsn, write_lsn, flush_lsn, replay_lsn
FROM pg_stat_replication;
```

**On Subscriber** — check Subscription status:

```sql
SELECT subname, pid, received_lsn, last_msg_receipt_time
FROM pg_stat_subscription;
```

Replication is working correctly when `state = streaming` on the Publisher and, on the Subscriber, `pid` is non-`NULL` with `received_lsn` advancing.

---

## Result

Once complete, data from the tables in your Publication on the Publisher will be continuously synchronized to the Subscriber in real time. All changes (INSERT, UPDATE, DELETE) are applied automatically.

| I want to... | Go to |
|---|---|
| Set up CDC with Debezium | [Set Up CDC with Debezium](set-up-cdc-with-debezium.md) |
| View cluster configuration parameters | [PostgreSQL Cluster Parameters](postgresql-cluster-parameters.md) |
