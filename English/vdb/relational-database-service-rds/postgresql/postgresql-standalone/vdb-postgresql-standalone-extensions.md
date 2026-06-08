# PostgreSQL Standalone Extensions

PostgreSQL is renowned for its flexibility. You can extend its core functionality with various Extensions.

By default, when you create a database with vDB PostgreSQL, several extensions are already enabled (listed below). You can also manually enable additional extensions as needed.

***

## 1. Extensions Enabled by Default

For PostgreSQL, newly created databases will have extensions enabled from the **template1** database.

After creating a database, you can check the enabled extensions by running:

```sql
\dx
```

or

```sql
select * from pg_extension;
```

Below is the list of extensions enabled by default:

<table><thead><tr><th>No</th><th>Name</th><th>Description</th></tr></thead><tbody><tr><td>1</td><td>plpgsql</td><td>PL/pgSQL procedural language</td></tr><tr><td>2</td><td>btree_gin</td><td>Support for indexing common datatypes in GIN</td></tr><tr><td>3</td><td>btree_gist</td><td>Support for indexing common datatypes in GiST</td></tr><tr><td>4</td><td>citext</td><td>Data type for case-insensitive character strings</td></tr><tr><td>5</td><td>cube</td><td>Data type for multidimensional cubes</td></tr><tr><td>6</td><td>dict_int</td><td>Text search dictionary template for integers</td></tr><tr><td>7</td><td>dict_xsyn</td><td>Text search dictionary template for extended synonym processing</td></tr><tr><td>8</td><td>hstore</td><td>Data type for storing sets of (key, value) pairs</td></tr><tr><td>9</td><td>isn</td><td>Data types for international product numbering standards</td></tr><tr><td>10</td><td>lo</td><td>Large Object maintenance</td></tr><tr><td>11</td><td>ltree</td><td>Data type for hierarchical tree-like structures</td></tr><tr><td>12</td><td>pg_trgm</td><td>Text similarity measurement and index searching based on trigrams</td></tr><tr><td>13</td><td>postgis</td><td>PostGIS geometry, geography, and raster spatial types and functions</td></tr><tr><td>14</td><td>postgres_fdw</td><td>Foreign-data wrapper for remote PostgreSQL servers</td></tr><tr><td>15</td><td>unaccent</td><td>Text search dictionary that removes accents</td></tr><tr><td>16</td><td>vector</td><td>Vector data type and ivfflat and hnsw access methods</td></tr></tbody></table>

**Note:** If you want to create a completely blank database, use **template0**.

```sql
CREATE DATABASE dbname TEMPLATE template0;
```

## 2. Extensions You Can Enable Manually

You can enable an Extension by running:

```sql
CREATE EXTENSION <extension_name>;
```

<table><thead><tr><th>Name</th><th>Description</th></tr></thead><tbody><tr><td>fuzzystrmatch</td><td>Determine similarities and distance between strings</td></tr><tr><td>intarray</td><td>Functions, operators, and index support for 1-D arrays of integers</td></tr><tr><td>pgcrypto</td><td>Cryptographic functions</td></tr><tr><td>postgis_tiger_geocoder</td><td>PostGIS tiger geocoder and reverse geocoder (requires fuzzystrmatch to be enabled first)</td></tr><tr><td>seg</td><td>Data type for representing line segments or floating-point intervals</td></tr><tr><td>tablefunc</td><td>Functions that manipulate whole tables, including crosstab</td></tr><tr><td>tcn</td><td>Triggered change notifications</td></tr><tr><td>tsm_system_rows</td><td>TABLESAMPLE method which accepts number of rows as a limit</td></tr><tr><td>tsm_system_time</td><td>TABLESAMPLE method which accepts time in milliseconds as a limit</td></tr><tr><td>uuid-ossp</td><td>Generate universally unique identifiers (UUIDs)</td></tr></tbody></table>

***

## 3. Notes

* The **vector** extension is only available for vDB instances created from **01/08/2024** onwards.
* To enable it on instances created before that date, please contact **GreenNode Cloud Support**.
