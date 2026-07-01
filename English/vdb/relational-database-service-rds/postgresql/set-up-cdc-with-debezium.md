# Set Up CDC with Debezium

> This guide helps you configure **Change Data Capture (CDC)** from a vDB PostgreSQL Cluster to external systems — Kafka, data pipelines, search indexes — using the **Debezium PostgreSQL Connector**.

---

## Prerequisites

- A PostgreSQL Cluster on vDB (**version 16 or 17**).
- The user creating the Publication must be the owner of the tables, or contact GreenNode Support to create a `FOR ALL TABLES` Publication.

---

## What is CDC and How Does it Differ from Logical Replication?

CDC captures all data changes (INSERT, UPDATE, DELETE) from PostgreSQL and streams them to external systems in real time.

![CDC architecture with Debezium](../../../../.gitbook/assets/vdb-cdc-debezium-architecture.png)

| | Logical Replication | CDC (Debezium) |
|---|---|---|
| Data destination | Another PostgreSQL Cluster | Kafka, data pipeline, etc. |
| Who creates Replication Slot? | PostgreSQL automatically | Debezium on startup |
| Slot cleanup on stop | PostgreSQL automatically | **Must clean up manually** |

---

## Step 1: Request CDC Activation and Receive Credentials

Contact **GreenNode Support** to request CDC activation on your cluster. GreenNode Support will create a dedicated user and provide you with a **username** and **password** to configure the Debezium connector.

To change the replication user password, run the following command on the cluster:

```sql
ALTER USER <username> PASSWORD '<new_password>';
```

{% hint style="warning" %}
When managing replication slots, do not delete or modify replication slots that do not belong to you. These slots may belong to the system or other Subscriptions — accidentally dropping one may impact the system.
{% endhint %}

---

## Step 2: Check and Configure PostgreSQL Parameters

CDC requires three PostgreSQL parameters to be correctly configured on the source cluster. If not configured, Debezium will fail to connect and adding new replicas from the portal may also fail.

| Parameter | Required value | Description |
|---|---|---|
| `wal_level` | `logical` | Required — default is `replica`, which is not sufficient for CDC |
| `max_replication_slots` | ≥ total slots needed | Total replication slots for all replicas, subscriptions, and CDC connectors |
| `max_wal_senders` | ≥ total senders needed | Total WAL sender processes (typically equals `max_replication_slots`) |

**How to calculate `max_replication_slots` and `max_wal_senders`:**

| Component | Slots + senders needed |
|---|---|
| Each replica node in the cluster | 1 + 1 |
| Each Subscription (logical replication) | 1 + 1 |
| Each CDC connector (Debezium) | 1 + 1 |

**Example:** 3-node cluster (2 replicas) + 1 CDC connector → `max_replication_slots = 3`, `max_wal_senders = 3`.

{% hint style="warning" %}
Changing `wal_level`, `max_replication_slots`, and `max_wal_senders` requires a **cluster restart**. Update all three parameters at the same time to trigger only one restart. See [PostgreSQL Cluster Parameters](postgresql-cluster-parameters.md) for instructions.
{% endhint %}

---

## Step 3: Create a Publication

A **Publication** defines the set of tables that Debezium will monitor. You must create it before configuring the connector.

1. Connect to the PostgreSQL Cluster using an account with owner rights on the tables to capture.
2. Create a Publication for the tables to capture:

```sql
CREATE PUBLICATION my_cdc_pub FOR TABLE public.orders, public.products;
```

{% hint style="info" %}
To use `FOR ALL TABLES`, contact **GreenNode Support** — this requires superuser privileges on the cluster.
{% endhint %}

3. Verify the Publication:

```sql
SELECT pubname, puballtables, pubinsert, pubupdate, pubdelete
FROM pg_publication;
```

---

## Step 4: Configure the Debezium Connector

**Kafka Connect** is the framework (bundled with Kafka) for running *connectors* — processes that move data between Kafka and external systems. Connectors are loaded into Kafka Connect as JSON configuration and managed via **REST API**.

The **Debezium PostgreSQL Connector** runs as a *source connector* inside Kafka Connect: it maintains a connection to the source cluster, watches for data changes in the database, and pushes each change as an event to the corresponding Kafka topic.

Use the **username and password provided by GreenNode** (replication user) to configure the Debezium PostgreSQL Connector:

```json
{
  "name": "<connector_name>",
  "config": {
    "connector.class": "io.debezium.connector.postgresql.PostgresConnector",
    "database.hostname": "<cluster_hostname>",
    "database.port": "5432",
    "database.user": "<username>",
    "database.password": "<password>",
    "database.dbname": "<database_name>",
    "topic.prefix": "<kafka_topic_prefix>",
    "plugin.name": "pgoutput",
    "publication.name": "my_cdc_pub",
    "slot.name": "<meaningful_slot_name>",
    "table.include.list": "public.orders,public.products",
    "snapshot.mode": "initial"
  }
}
```

| Parameter | Description |
|---|---|
| `database.hostname` | Hostname provided by GreenNode |
| `database.port` | PostgreSQL connection port |
| `database.user` | Username provided by GreenNode |
| `database.password` | Password provided by GreenNode |
| `database.dbname` | Source database name |
| `topic.prefix` | Prefix for Kafka topic names. Each table is published to `<prefix>.<schema>.<table>` — for example: prefix `pg-cdc` → topic `pg-cdc.public.orders` |
| `plugin.name` | Logical decoding plugin (built-in since PG 10, no extension needed) |
| `publication.name` | Name of the Publication created in Step 3 |
| `slot.name` | Replication slot name — use a meaningful name for easier management |
| `table.include.list` | List of tables to capture (format: `schema.table`) |
| `snapshot.mode` | Snapshot mode when the connector starts. In the example, `initial` snapshots all existing data on first startup then switches to streaming WAL. |

See all options at [Debezium PostgreSQL Connector — Snapshot properties](https://debezium.io/documentation/reference/stable/connectors/postgresql.html#postgresql-connector-snapshot-properties).

{% hint style="info" %}
`plugin.name: pgoutput` is built into PostgreSQL since version 10. No additional extension installation is required.
{% endhint %}

---

## Step 5: Register the Connector via Kafka Connect REST API

Register the connector with:

```bash
curl -X POST http://<kafka-connect-host>:8083/connectors \
  -H "Content-Type: application/json" \
  -d @connector-config.json
```

Check the connector status:

```bash
curl -s http://<kafka-connect-host>:8083/connectors/<connector_name>/status
```

The connector is running normally when both the connector and task `state` are `RUNNING`.

---

## Step 6: Monitor the Replication Slot

{% hint style="warning" %}
Unlike Logical Replication, **Debezium does not delete the Replication Slot when it stops**. If the connector crashes or is removed without cleaning up the slot, the slot continues holding WAL indefinitely → disk full → cluster crash.
{% endhint %}

Periodically check the Replication Slot status by connecting to the PostgreSQL Cluster and running:

```sql
SELECT
    slot_name,
    active,
    pg_size_pretty(pg_wal_lsn_diff(pg_current_wal_lsn(), restart_lsn)) AS wal_lag
FROM pg_replication_slots;
```

When you no longer need the connector, **stop or delete the connector first** (so the slot becomes inactive), **then drop the slot** — a slot that is still active cannot be dropped:

```sql
SELECT pg_drop_replication_slot('<slot_name>');
```

---

## Actions to Avoid

{% hint style="warning" %}
The following actions may cause data loss or disrupt the CDC pipeline.
{% endhint %}

| Action | Risk |
|---|---|
| Delete the connector without dropping the Replication Slot first | Inactive slot → WAL accumulates → disk full → cluster crash |
| Run `pg_drop_replication_slot()` on a slot that is not yours | May drop a system slot → replication lost |

---

## Result

Once complete, Debezium captures all changes from tables in your Publication and pushes them to Kafka topics in the following format:

```
<topic.prefix>.<schema>.<table>
```

Example: `my-cdc.public.orders`

Check messages on Kafka using `kafka-console-consumer`:

```bash
kafka-console-consumer \
  --bootstrap-server <kafka-host>:9092 \
  --topic my-cdc.public.orders \
  --from-beginning
```

| I want to... | Go to |
|---|---|
| Configure Logical Replication between two Clusters | [Configure Logical Replication](configure-logical-replication.md) |
| View cluster configuration parameters | [PostgreSQL Cluster Parameters](postgresql-cluster-parameters.md) |
