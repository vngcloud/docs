# vDB PostgreSQL - Các extension được hỗ trợ

PostgreSQL nổi tiếng với tính linh hoạt. Bạn hoàn toàn có thể mở rộng các core-function của PostgreSQL bằng các Extensions.

Mặc định, khi khởi tạo một database với vDB PostgreSQL, bạn đã được bật sẵn một số extension (danh sách bên dưới), ngoài ra bạn cũng có thể chủ động bật thêm một số extension khác tùy theo nhu cầu.

{% hint style="info" %}
vDB PostgreSQL hỗ trợ hai loại deployment: **Standalone** (Single Node) và **Cluster** (1 Writer + N Readers). Danh sách extension được hỗ trợ có thể khác nhau tùy theo loại deployment.
{% endhint %}

***

## 1. Danh sách các extension được bật sẵn

Đối với PostgreSQL, các database được tạo mới sẽ được bật sẵn các Extension như trong database **template1.**

Sau khi tạo database, bạn có thể dùng lệnh:

```sql
\dx
```

hoặc

```sql
select * from pg_extension;
```

để xem danh sách các extension đã được bật trên database.

Dưới đây là danh sách các extension đã được bật sẵn:

<table><thead><tr><th>No</th><th>Name</th><th>Description</th><th>Standalone</th><th>Cluster</th></tr></thead><tbody><tr><td>1</td><td>plpgsql</td><td>PL/pgSQL procedural language</td><td>✅</td><td>✅</td></tr><tr><td>2</td><td>btree_gin</td><td>Support for indexing common datatypes in GIN</td><td>✅</td><td>✅</td></tr><tr><td>3</td><td>btree_gist</td><td>Support for indexing common datatypes in GiST</td><td>✅</td><td>✅</td></tr><tr><td>4</td><td>citext</td><td>Data type for case-insensitive character strings</td><td>✅</td><td>✅</td></tr><tr><td>5</td><td>cube</td><td>Data type for multidimensional cubes</td><td>✅</td><td>✅</td></tr><tr><td>6</td><td>dict_int</td><td>Text search dictionary template for integers</td><td>✅</td><td>✅</td></tr><tr><td>7</td><td>dict_xsyn</td><td>Text search dictionary template for extended synonym processing</td><td>✅</td><td>✅</td></tr><tr><td>8</td><td>hstore</td><td>Data type for storing sets of (key, value) pairs</td><td>✅</td><td>✅</td></tr><tr><td>9</td><td>isn</td><td>Data types for international product numbering standards</td><td>✅</td><td>✅</td></tr><tr><td>10</td><td>lo</td><td>Large Object maintenance</td><td>✅</td><td>✅</td></tr><tr><td>11</td><td>ltree</td><td>Data type for hierarchical tree-like structures</td><td>✅</td><td>✅</td></tr><tr><td>12</td><td>pg_trgm</td><td>Text similarity measurement and index searching based on trigrams</td><td>✅</td><td>✅</td></tr><tr><td>13</td><td>postgis</td><td>PostGIS geometry, geography, and raster spatial types and functions</td><td>✅</td><td>✅</td></tr><tr><td>14</td><td>postgres_fdw</td><td>Foreign-data wrapper for remote PostgreSQL servers</td><td>✅</td><td>✅</td></tr><tr><td>15</td><td>unaccent</td><td>Text search dictionary that removes accents</td><td>✅</td><td>✅</td></tr><tr><td>16</td><td>vector</td><td>Vector data type and ivfflat and hnsw access methods</td><td>✅</td><td>✅</td></tr><tr><td>17</td><td>chkpass</td><td>Data type for auto-encrypted passwords</td><td>✅</td><td>❌</td></tr></tbody></table>

**Lưu ý:** Nếu bạn muốn tạo database trắng hoàn toàn, hãy dùng **template0.**

```sql
CREATE DATABASE dbname TEMPLATE template0;
```

***

## 2. Danh sách các extension bạn có thể tự bật

Bạn có thể tự bật một Extension bằng cách chạy lệnh:

```sql
CREATE EXTENSION <extension_name>;
```

### 2.1. Extension dùng chung (Standalone & Cluster)

<table><thead><tr><th>Name</th><th>Description</th></tr></thead><tbody><tr><td>earthdistance</td><td>Calculate great-circle distances on the surface of the Earth</td></tr><tr><td>fuzzystrmatch</td><td>Determine similarities and distance between strings</td></tr><tr><td>pg_stat_statements</td><td>Track execution statistics of all SQL statements executed</td></tr><tr><td>pgcrypto</td><td>Cryptographic functions</td></tr><tr><td>postgis_topology</td><td>PostGIS topology spatial types and functions</td></tr><tr><td>tablefunc</td><td>Functions that manipulate whole tables, including crosstab</td></tr><tr><td>uuid-ossp</td><td>Generate universally unique identifiers (UUIDs)</td></tr></tbody></table>

### 2.2. Extension chỉ có trên Cluster

<table><thead><tr><th>Name</th><th>Version</th><th>Description</th></tr></thead><tbody><tr><td>pg_cron</td><td>1.6</td><td>Job scheduler for PostgreSQL</td></tr><tr><td>timescaledb</td><td>2.24.0</td><td>Enables scalable inserts and complex queries for time-series data</td></tr><tr><td>postgis_raster</td><td>3.6.1</td><td>PostGIS raster types and functions</td></tr><tr><td>pgaudit</td><td>17.1</td><td>Auditing functionality</td></tr><tr><td>pg_partman</td><td>5.4.0</td><td>Manage partitioned tables (time/ID-based)</td></tr><tr><td>pg_repack</td><td>1.5.3</td><td>Reorganize tables with minimal locks</td></tr></tbody></table>

### 2.3. Extension chỉ có trên Standalone

<table><thead><tr><th>Name</th><th>Description</th></tr></thead><tbody><tr><td>address_standardizer</td><td>Used to parse an address into constituent elements for geocoding</td></tr><tr><td>address_standardizer_data_us</td><td>Address Standardizer US dataset example</td></tr><tr><td>amcheck</td><td>Functions for verifying relation integrity</td></tr><tr><td>autoinc</td><td>Functions for autoincrementing fields</td></tr><tr><td>insert_username</td><td>Functions for tracking who changed a table</td></tr><tr><td>intagg</td><td>Integer aggregator and enumerator (obsolete)</td></tr><tr><td>intarray</td><td>Functions, operators, and index support for 1-D arrays of integers</td></tr><tr><td>moddatetime</td><td>Functions for tracking last modification time</td></tr><tr><td>pageinspect</td><td>Inspect the contents of database pages at a low level</td></tr><tr><td>pg_buffercache</td><td>Examine the shared buffer cache</td></tr><tr><td>pg_freespacemap</td><td>Examine the free space map (FSM)</td></tr><tr><td>pg_prewarm</td><td>Prewarm relation data</td></tr><tr><td>pg_visibility</td><td>Examine the visibility map (VM) and page-level visibility info</td></tr><tr><td>pgrouting</td><td>pgRouting Extension</td></tr><tr><td>pgrowlocks</td><td>Show row-level locking information</td></tr><tr><td>pgstattuple</td><td>Show tuple-level statistics</td></tr><tr><td>postgis_sfcgal</td><td>PostGIS SFCGAL functions</td></tr><tr><td>postgis_tiger_geocoder</td><td>PostGIS tiger geocoder and reverse geocoder</td></tr><tr><td>refint</td><td>Functions for implementing referential integrity (obsolete)</td></tr><tr><td>sslinfo</td><td>Information about SSL certificates</td></tr><tr><td>tcn</td><td>Triggered change notifications</td></tr><tr><td>timetravel</td><td>Functions for implementing time travel</td></tr><tr><td>tsm_system_rows</td><td>TABLESAMPLE method which accepts number of rows as a limit</td></tr><tr><td>tsm_system_time</td><td>TABLESAMPLE method which accepts time in milliseconds as a limit</td></tr></tbody></table>

***

Bạn có thể dùng lệnh sau để kiểm tra danh sách các extension đang được hỗ trợ trên vDB của mình:

```sql
SELECT * FROM pg_available_extensions;
```

Nếu bạn cần extension nào chưa được hỗ trợ, vui lòng liên hệ với **GreenNode Cloud Support** để được hỗ trợ.

***

## 3. Lưu ý

* Extension **vector** chỉ available cho các vDB khởi tạo từ **01/08/2024**.
* Để sử dụng trên các vDB đã khởi tạo trước đó, bạn vui lòng liên hệ **GreenNode Cloud Support** để được hỗ trợ enable.
* Danh sách extension trên Cluster có thể được cập nhật thêm trong các phiên bản tiếp theo.
