# PostgreSQL Cluster Extensions

PostgreSQL is renowned for its flexibility. You can extend its core functionality with various Extensions.

By default, when you create a database with vDB PostgreSQL, several extensions are already enabled (listed below). You can also manually enable additional extensions as needed.

***

## 1. Extensions Enabled by Default

The following extensions are automatically installed on every database in the Cluster upon initialization. You do not need to run `CREATE EXTENSION` to use them.

<table><thead><tr><th>Name</th><th>Version</th><th>Description</th></tr></thead><tbody><tr><td>plpgsql</td><td>1.0</td><td>PL/pgSQL procedural language</td></tr><tr><td>pg_stat_statements</td><td>1.11</td><td>Track execution statistics of all SQL statements executed</td></tr><tr><td>pg_stat_kcache</td><td>2.3.1</td><td>Track kernel-level cache statistics (reads, writes) per query</td></tr></tbody></table>

## 2. Extensions You Can Enable Manually

You can enable the following extensions with `CREATE EXTENSION` without superuser privileges.

```sql
CREATE EXTENSION <extension_name>;
```

<table><thead><tr><th>Name</th><th>Version</th><th>Description</th></tr></thead><tbody><tr><td>btree_gin</td><td>1.3</td><td>Support for indexing common datatypes in GIN</td></tr><tr><td>btree_gist</td><td>1.7</td><td>Support for indexing common datatypes in GiST</td></tr><tr><td>citext</td><td>1.6</td><td>Data type for case-insensitive character strings</td></tr><tr><td>cube</td><td>1.5</td><td>Data type for multidimensional cubes</td></tr><tr><td>dict_int</td><td>1.0</td><td>Text search dictionary template for integers</td></tr><tr><td>dict_xsyn</td><td>1.0</td><td>Text search dictionary template for extended synonym processing</td></tr><tr><td>earthdistance</td><td>1.2</td><td>Calculate great-circle distances on the surface of the Earth</td></tr><tr><td>fuzzystrmatch</td><td>1.2</td><td>Determine similarities and distance between strings</td></tr><tr><td>hstore</td><td>1.8</td><td>Data type for storing sets of (key, value) pairs</td></tr><tr><td>intarray</td><td>1.5</td><td>Functions, operators, and index support for 1-D arrays of integers</td></tr><tr><td>isn</td><td>1.2</td><td>Data types for international product numbering standards</td></tr><tr><td>lo</td><td>1.1</td><td>Large Object maintenance</td></tr><tr><td>ltree</td><td>1.3</td><td>Data type for hierarchical tree-like structures</td></tr><tr><td>pg_partman</td><td>5.4.3</td><td>Manage time-based and serial-based table partition sets</td></tr><tr><td>pg_permissions</td><td>1.3</td><td>View object permissions and compare them with the desired state</td></tr><tr><td>pg_repack</td><td>1.5.3</td><td>Reorganize tables in PostgreSQL databases with minimal locks</td></tr><tr><td>pg_trgm</td><td>1.6</td><td>Text similarity measurement and index searching based on trigrams</td></tr><tr><td>pgaudit</td><td>17.1</td><td>Provides detailed session and/or object audit logging</td></tr><tr><td>pgcrypto</td><td>1.3</td><td>Cryptographic functions</td></tr><tr><td>pltcl</td><td>1.0</td><td>PL/Tcl procedural language</td></tr><tr><td>postgis</td><td>3.6.3</td><td>PostGIS geometry, geography, and raster spatial types and functions</td></tr><tr><td>postgis_raster</td><td>3.6.3</td><td>PostGIS raster types and functions</td></tr><tr><td>postgis_tiger_geocoder</td><td>3.6.3</td><td>PostGIS tiger geocoder and reverse geocoder</td></tr><tr><td>postgis_topology</td><td>3.6.3</td><td>PostGIS topology spatial types and functions</td></tr><tr><td>postgres_fdw</td><td>1.1</td><td>Foreign-data wrapper for remote PostgreSQL servers</td></tr><tr><td>seg</td><td>1.4</td><td>Data type for representing line segments or floating-point intervals</td></tr><tr><td>set_user</td><td>4.1.0</td><td>Set user session context with optional logging</td></tr><tr><td>tablefunc</td><td>1.0</td><td>Functions that manipulate whole tables, including crosstab</td></tr><tr><td>tcn</td><td>1.0</td><td>Triggered change notifications</td></tr><tr><td>timescaledb</td><td>2.27.1</td><td>Enables scalable inserts and complex queries for time-series data</td></tr><tr><td>tsm_system_rows</td><td>1.0</td><td>TABLESAMPLE method which accepts number of rows as a limit</td></tr><tr><td>tsm_system_time</td><td>1.0</td><td>TABLESAMPLE method which accepts time in milliseconds as a limit</td></tr><tr><td>unaccent</td><td>1.1</td><td>Text search dictionary that removes accents</td></tr><tr><td>uuid-ossp</td><td>1.1</td><td>Generate universally unique identifiers (UUIDs)</td></tr><tr><td>vector</td><td>0.8.2</td><td>Vector data type and ivfflat and hnsw access methods</td></tr></tbody></table>

***