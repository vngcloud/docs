# Migrate from Postgres Single to Postgres Cluster

This guide walks you through exporting data from a **Postgres Single Node** instance and restoring it to a **Postgres Cluster** on vDB. Two scenarios are covered: **Section A** for instances with a single database, and **Section B** for instances with multiple databases.

{% hint style="info" %}
**Note:** vDB does not support changing the Deployment Type of an existing database. Migration requires creating a new Postgres Cluster and transferring data manually using the steps below.
{% endhint %}

***

## Prerequisites

Before you begin, make sure:

* `psql`, `pg_dump` or `pg_dumpall`, and `pg_restore` are installed on the machine running the migration (version must match the PostgreSQL version on the source instance).
* You have credentials (host, username, password) for both the Postgres Single Node and the Postgres Cluster.

***

## A. Single-Database Migration (pg\_dump)

Use this section when your Postgres Single Node instance contains **one database** that you want to migrate.


### Step 1 — Verify Connectivity

Before starting, confirm that both your Postgres Single Node instance and your Postgres Cluster are running and reachable.

```bash
# Test Postgres Single Node
psql -h <IP_single> -U <username_single> -d <database_single> -c "SELECT 1;"

# Test Postgres Cluster
psql -h <IP_cluster> -U <username_cluster> -d <database_cluster> -c "SELECT 1;"
```

***

### Step 2 — Export the Database

Use `pg_dump` to export the source database. Choose the format that matches your preferred restore method.

**Option A — Custom format** (recommended; for use with `pg_restore`):

```bash
pg_dump -h <IP_single> -U <username_single> -d <database_single> \
        -Fc -f backup.dump
```

**Option B — Plain SQL format** (for use with `psql`):

```bash
pg_dump -h <IP_single> -U <username_single> -d <database_single> \
        -Fp > backup.sql
```

{% hint style="info" %}
**Tip — Choosing a format:**
The custom format (`-Fc`) produces a compressed binary file and supports multi-job restore with `pg_restore`. The plain SQL format (`-Fp`) produces a human-readable file that is easier to inspect or edit before restoring. Use custom format for large databases.
{% endhint %}

***

### Step 3 — Restore on Postgres Cluster

Restore the dump to the target cluster using the method that matches your export format.

**If you exported in custom format**, use `pg_restore`:

```bash
pg_restore -h <IP_cluster> -U <username_cluster> -d <database_cluster> \
           --no-owner --no-privileges backup.dump
```

**If you exported in plain SQL format**, use `psql`:

```bash
psql -h <IP_cluster> -U <username_cluster> -d <database_cluster> \
     -f backup.sql
```

{% hint style="warning" %}
**Superuser errors during restore:**
Postgres Cluster does not grant superuser access. You may see errors such as `ERROR: must be superuser` or warnings about `ALTER TABLE ... OWNER TO`. These are expected and safe to ignore.

The flags `--no-owner` and `--no-privileges` (shown above for `pg_restore`) suppress the most common ones. Any error related to table creation or actual data should be investigated before proceeding.
{% endhint %}

***

### Step 4 — Verify the Restored Data

After the restore completes, validate the data on Postgres Cluster before cutting over traffic. Recommended checks:

* Compare table counts between source and target.
* Compare row counts for critical tables.
* Spot-check a sample of rows in key tables.
* Test application queries against the restored database.

***

## B. Multi-Database Migration (pg\_dumpall / pg\_dump)

Use this section when your Postgres Single Node instance contains **more than one database**.

***

### Step 1 — Verify Connectivity

Confirm that both instances are running and accessible before proceeding.

```bash
# Test Postgres Single Node
psql -h <IP_single> -U <username_single> -c "\l"

# Test Postgres Cluster
psql -h <IP_cluster> -U <username_cluster> -c "\l"
```

***

### Step 2 — Export All Databases

Choose one of the two export approaches below.

**Option A — pg\_dumpall** (exports all databases in a single file):

```bash
pg_dumpall -h <IP_single> -U <username_single> \
           --no-role-passwords > alldb.sql
```

{% hint style="info" %}
**pg\_dumpall limitations:**
`pg_dumpall` only produces plain SQL output, so you must restore with `psql`. It also attempts to export global objects (roles, tablespaces) that require superuser access. Errors like `ERROR: must be superuser` during export are expected and safe to skip. The flag `--no-role-passwords` omits hashed passwords, which cannot be restored without superuser access anyway.
{% endhint %}

**Option B — pg\_dump per database** (recommended for most cases):

Run `pg_dump` separately for each database. This avoids global-permission errors entirely and gives you more control over the restore process.

```bash
# Repeat for each database
pg_dump -h <IP_single> -U <username_single> -d <db_name> \
        -Fc -f <db_name>.dump
```

{% hint style="info" %}
`pg_dump` does not export global objects such as roles and tablespaces. You must recreate these manually on Postgres Cluster before restoring. See Step 3 for details.
{% endhint %}

***

### Step 3 — Recreate Roles and Tablespaces (if needed)

If your databases rely on specific roles or custom tablespaces, recreate them on Postgres Cluster before restoring. Roles created here will need passwords set manually.

```sql
-- Recreate a role
CREATE ROLE <role_name> WITH LOGIN;
ALTER ROLE <role_name> WITH PASSWORD '<new_password>';
```

If you used `pg_dumpall`, the SQL file contains role definitions, but some statements may fail due to missing superuser access. Review the file and apply role statements manually as needed.

***

### Step 4 — Restore on Postgres Cluster

**If you used pg\_dumpall (Option A)**, restore with `psql` connecting to the default `postgres` database:

```bash
psql -h <IP_cluster> -U <username_cluster> -d postgres \
     -f alldb.sql
```

**If you used pg\_dump per database (Option B)**, restore each dump individually:

```bash
# Repeat for each database
pg_restore -h <IP_cluster> -U <username_cluster> -d <db_name> \
           --no-owner --no-privileges <db_name>.dump
```

{% hint style="warning" %}
**Role passwords after restore:**
`pg_dumpall` exports role definitions but not their passwords (the `--no-role-passwords` flag omits them, and encrypted passwords cannot be restored without superuser access). After the restore, you must manually set passwords for all roles that require authentication:

```sql
ALTER ROLE <role_name> WITH PASSWORD '<new_password>';
```
{% endhint %}

***

### Step 5 — Verify Each Database

After the restore, verify every database on Postgres Cluster:

* Confirm all expected databases are present.
* Check table counts and row counts in each database.
* Verify that application users can connect and query successfully.

***

## Quick Reference

| Scenario | Export tool | Restore tool | When to use |
| --- | --- | --- | --- |
| Single database | `pg_dump -Fc` | `pg_restore` | Large databases; supports multi-job restore |
| Single database | `pg_dump -Fp` | `psql` | Need to inspect or edit the SQL file before restoring |
| Multiple databases | `pg_dumpall` | `psql` | Want to export all databases into a single file |
| Multiple databases | `pg_dump` (per DB) | `pg_restore` / `psql` | Need per-database control; avoids global permission errors |

***

## Troubleshooting

**`ERROR: must be superuser`**

Errors mentioning superuser access are expected on both Postgres Single Node and Postgres Cluster. Skip them. Use `--no-owner` and `--no-privileges` flags with `pg_restore` to suppress the most common cases.

**Roles or ownership errors after restore**

`pg_dump` and `pg_dumpall` do not carry over role passwords. After restoring, manually set passwords for all roles that need to authenticate.

**Missing tablespaces**

If the source database uses custom tablespaces, the restore may fail because those tablespaces do not exist on the target cluster. Recreate any required tablespaces on Postgres Cluster before running the restore.

**Table creation errors**

Errors unrelated to superuser access (e.g., duplicate tables, type mismatches) should be investigated before proceeding. Do not skip these.

**Large databases**

For very large databases, use `pg_restore --jobs <n>` to enable multi-job restore with the custom format and reduce the total restore time.

***

## Next Steps

After verifying the data successfully:

* Update the connection string in your application to point to the Postgres Cluster (new host, port, and credentials).
* Confirm the application works correctly against the migrated database.
* Delete the old Postgres Single Node on vDB once you have confirmed it is no longer needed.
