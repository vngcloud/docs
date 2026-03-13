# vDB PostgreSQL - Supported Extensions

**vDB PostgreSQL - Supported Extensions**

PostgreSQL is renowned for its flexibility, allowing you to extend its core functionalities with various extensions.

By default, when you create a PostgreSQL database with vDB, several extensions are already enabled (listed below). Additionally, you can manually enable other extensions as needed.

#### 1. Extensions Already Enabled by Default:

For PostgreSQL, newly created databases will have extensions enabled from the `template1` database.

Once the database is created, you can check the enabled extensions by running the following commands:

```sql
\dx
```

or

```sql
select * from pg_extension;
```

Here is a list of the extensions that are enabled by default:

| No | Name          | Description                                                         | Version Supported by PostgreSQL |
| -- | ------------- | ------------------------------------------------------------------- | ------------------------------- |
| 1  | btree\_gin    | Support for indexing common datatypes in GIN                        | TBU                             |
| 2  | btree\_gist   | Support for indexing common datatypes in GiST                       | TBU                             |
| 3  | chkpass       | Data type for auto-encrypted passwords                              | TBU                             |
| 4  | citext        | Data type for case-insensitive character strings                    | TBU                             |
| 5  | cube          | Data type for multidimensional cubes                                | TBU                             |
| 6  | dict\_int     | Text search dictionary template for integers                        | TBU                             |
| 7  | dict\_xsyn    | Text search dictionary template for extended synonym processing     | TBU                             |
| 8  | hstore        | Data type for storing sets of (key, value) pairs                    | TBU                             |
| 9  | isn           | Data types for international product numbering standards            | TBU                             |
| 10 | lo            | Large Object maintenance                                            | TBU                             |
| 11 | ltree         | Data type for hierarchical tree-like structures                     | TBU                             |
| 12 | pg\_trgm      | Text similarity measurement and index searching based on trigrams   | TBU                             |
| 13 | plpgsql       | PL/pgSQL procedural language                                        | TBU                             |
| 14 | postgis       | PostGIS geometry, geography, and raster spatial types and functions | TBU                             |
| 15 | postgres\_fdw | Foreign-data wrapper for remote PostgreSQL servers                  | TBU                             |
| 16 | unaccent      | Text search dictionary that removes accents                         | TBU                             |
| 17 | vector        | Vector data type and ivfflat and hnsw access methods                | 14, 15                          |

**Note:** If you want to create a completely blank database, use `template0`.

Example:

```sql
CREATE DATABASE dbname TEMPLATE template0;
```

#### 2. Extensions You Can Enable:

You can manually enable an extension by running the following command:

```sql
CREATE EXTENSION <extension_name>;
```

Here is a list of additional extensions that you can enable:

| Name                            | Description                                                         |
| ------------------------------- | ------------------------------------------------------------------- |
| address\_standardizer           | Used to parse an address into constituent elements for geocoding.   |
| address\_standardizer\_data\_us | US dataset for address standardization.                             |
| amcheck                         | Functions for verifying relation integrity.                         |
| autoinc                         | Functions for autoincrementing fields.                              |
| earthdistance                   | Calculates great-circle distances on Earth's surface.               |
| fuzzystrmatch                   | Determines similarities and distance between strings.               |
| insert\_username                | Functions for tracking table changes by users.                      |
| intagg                          | Integer aggregator and enumerator (obsolete).                       |
| intarray                        | Functions, operators, and index support for 1-D arrays of integers. |
| moddatetime                     | Functions for tracking last modification time.                      |
| pageinspect                     | Inspects database page contents at a low level.                     |
| pg\_buffercache                 | Examines the shared buffer cache.                                   |
| pg\_freespacemap                | Examines the free space map (FSM).                                  |
| pg\_prewarm                     | Prewarms relation data.                                             |
| pg\_stat\_statements            | Tracks execution statistics of SQL statements.                      |
| pg\_trgm                        | Text similarity measurement based on trigrams.                      |
| pg\_visibility                  | Examines visibility map (VM) and page-level visibility info.        |
| pgcrypto                        | Cryptographic functions.                                            |
| pgrouting                       | pgRouting extension for routing.                                    |
| pgrowlocks                      | Shows row-level locking information.                                |
| pgstattuple                     | Shows tuple-level statistics.                                       |
| postgis\_sfcgal                 | PostGIS SFCGAL functions.                                           |
| postgis\_tiger\_geocoder        | PostGIS tiger geocoder and reverse geocoder.                        |
| postgis\_topology               | PostGIS topology spatial types and functions.                       |
| refint                          | Functions for implementing referential integrity (obsolete).        |
| sslinfo                         | Information about SSL certificates.                                 |
| tablefunc                       | Functions that manipulate whole tables, including crosstab.         |
| tcn                             | Triggered change notifications.                                     |
| timetravel                      | Functions for implementing time travel.                             |
| tsm\_system\_rows               | TABLESAMPLE method which accepts number of rows as a limit.         |
| tsm\_system\_time               | TABLESAMPLE method which accepts time in milliseconds as a limit.   |
| unaccent                        | Text search dictionary that removes accents.                        |
| uuid-ossp                       | Generates universally unique identifiers (UUIDs).                   |

You can check the list of supported extensions on your vDB by running the following command:

```sql
SELECT * FROM pg_available_extensions;
```

If an extension you need is not supported, please contact GreenNode Support for assistance.

#### 3. Notes:

* The **vector** extension is only available for vDB instances created after **01/08/2024**.
* To use it on pre-existing vDB instances, please contact GreenNode Support to enable it.
