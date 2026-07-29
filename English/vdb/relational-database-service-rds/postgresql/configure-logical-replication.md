# Configure Logical Replication

> This guide helps you set up **PostgreSQL Logical Replication** — replicating data changes in real time from a source cluster (Publisher) to a destination cluster (Subscriber). One or both clusters can be hosted on GreenNode vDB.

***

## Prerequisites

* At least one of the two clusters (Publisher or Subscriber) must be a PostgreSQL Cluster on GreenNode vDB (**version 16 or 17**).
* Both clusters must run the **same major version** of PostgreSQL.
* The user running SQL commands must be the **owner** of the tables to replicate (to create a Publication).

{% hint style="info" %}
GreenNode vDB supports Logical Replication for **PostgreSQL 16 and 17** only.
{% endhint %}

***

## How Logical Replication Works

![Logical Replication architecture](../../../.gitbook/assets/vdb-logical-replication-architecture.png)

* **Publisher**: the source cluster holding the original data. You create a `PUBLICATION` to define which tables are replicated.
* **Subscriber**: the destination cluster receiving changes. You create a `SUBSCRIPTION` to connect to the Publisher and pull data.

***

## Part A: vDB PostgreSQL Cluster as Publisher

> Follow the steps in this section if your GreenNode vDB cluster is the **data source** (Publisher).

### Step A.1: Request Logical Replication Activation

Contact **GreenNode Support** to request Logical Replication activation on your cluster. GreenNode Support will grant the `REPLICATION` privilege, along with any other privileges needed, directly to your cluster's existing admin account.

{% hint style="warning" %}
When managing Subscriptions, do not delete or modify replication slots that do not belong to you. These slots may belong to the system or other Subscriptions — accidentally dropping one will cause replication loss immediately.
{% endhint %}

### Step A.2: Configure PostgreSQL Parameters

Logical Replication requires three PostgreSQL parameters to be correctly configured on the **Publisher cluster**.

| Parameter               | Required value         | Description                                                                      |
| ----------------------- | ---------------------- | -------------------------------------------------------------------------------- |
| `wal_level`             | `logical`              | Required — default is `replica`, which is not sufficient for logical replication |
| `max_replication_slots` | ≥ total slots needed   | Total replication slots for all replicas, subscriptions, and CDC connectors      |
| `max_wal_senders`       | ≥ total senders needed | Total WAL sender processes (typically equals `max_replication_slots`)            |

**How to calculate `max_replication_slots` and `max_wal_senders`:**

| Component                               | Slots + senders needed |
| --------------------------------------- | ---------------------- |
| Each replica node in the cluster        | 1 slot + 1 sender      |
| Each Subscription (logical replication) | 1 slot + 1 sender      |
| Each CDC connector (Debezium)           | 1 slot + 1 sender      |

**Example:** 3-node cluster (2 replicas) + 1 subscription → `max_replication_slots = 3`, `max_wal_senders = 3`.

{% hint style="warning" %}
Changing `wal_level`, `max_replication_slots`, and `max_wal_senders` requires a **cluster restart**. See [PostgreSQL Cluster Parameters](https://github.com/vngcloud/docs/blob/main/English/vdb/relational-database-service-rds/postgresql/postgresql-cluster-parameters.md) for instructions.
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

***

## Part B: vDB PostgreSQL Cluster as Subscriber

> Follow the steps in this section if your GreenNode vDB cluster is the **data destination** (Subscriber).

### Step B.1: Request Logical Replication Activation

Contact **GreenNode Support** to request Logical Replication activation on your cluster. GreenNode Support will grant the `REPLICATION` privilege, along with any other privileges needed, directly to your cluster's existing admin account.

{% hint style="warning" %}
When managing Subscriptions, do not delete or modify replication slots that do not belong to you. These slots may belong to the system or other Subscriptions — accidentally dropping one will cause replication loss immediately.
{% endhint %}

### Step B.2: Create Tables on Subscriber

Logical Replication **does not create tables automatically** on the Subscriber. You must create the schema and tables on the Subscriber before creating the Subscription.

{% hint style="warning" %}
The schema and data types of tables on the Subscriber must **exactly match** the Publisher. A mismatch will cause the Subscription to fail when applying changes.
{% endhint %}

You can create the tables using one of the following methods:

#### Create the table manually

Write the CREATE TABLE statement directly, matching the Publisher's schema. Suitable when only a few simple tables need to be replicated.

```sql
-- Example: create the orders table on Subscriber
CREATE TABLE orders (
    id      serial PRIMARY KEY,
    product text   NOT NULL,
    qty     int    NOT NULL,
    ts      timestamptz DEFAULT now()
);
```

#### Create the table using `pg_dump`

Instead of writing DDL by hand, use `pg_dump --schema-only` to dump the table structure from the Publisher, review the file, then apply it to the Subscriber with `psql -f`.

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

# Step 3: apply to Subscriber
psql \
  -h <subscriber_hostname> \
  -U <username> \
  -d <database_name> \
  -f schema.sql
```

To dump multiple tables, repeat `--table` for each one. Omit `--table` to dump the entire schema.

### Step B.3: Create a Subscription

1. Connect to the **Subscriber cluster** using the admin account granted `REPLICATION` in Step B.1.
2. Create the Subscription:

```sql
CREATE SUBSCRIPTION my_subscription
    CONNECTION 'host=<host> port=5432 dbname=<dbname> user=<user> password=<password> sslmode=require'
    PUBLICATION <publication_name>;
```

| Parameter          | Description                                   |
| ------------------ | --------------------------------------------- |
| `host`             | Publisher hostname                            |
| `port`             | PostgreSQL connection port                    |
| `dbname`           | Source database name on Publisher             |
| `user`             | Username with replication rights on Publisher |
| `password`         | Password with replication rights on Publisher |
| `sslmode`          | SSL encryption mode                           |
| `publication_name` | Publication name on Publisher                 |

{% hint style="warning" %}
The `user`/`password` in the CONNECTION string above is the **Publisher's account**, not the Subscriber account you used to connect and run the CREATE SUBSCRIPTION command.
{% endhint %}

By default, PostgreSQL performs an **initial sync**: copying all existing data from the Publisher to the Subscriber before switching to streaming new changes.

If the Subscriber already has data (for example, restored earlier via `pg_dump`), you can skip the initial sync:

```sql
CREATE SUBSCRIPTION my_subscription
    CONNECTION 'host=<host> port=5432 dbname=<dbname> user=<user> password=<password> sslmode=require'
    PUBLICATION <publication_name>
    WITH (copy_data = false);
```

When `copy_data = false`, the Subscriber only receives changes that occur after the Subscription is created.

***

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

***

## Result

Once complete, data from the tables in your Publication on the Publisher will be continuously synchronized to the Subscriber in real time. All changes (INSERT, UPDATE, DELETE) are applied automatically.

| I want to...                          | Go to                                                                                                                                                               |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Set up CDC with Debezium              | [Set Up CDC with Debezium](set-up-cdc-with-debezium.md)                                                                                                             |
| View cluster configuration parameters | [PostgreSQL Cluster Parameters](https://github.com/vngcloud/docs/blob/main/English/vdb/relational-database-service-rds/postgresql/postgresql-cluster-parameters.md) |
