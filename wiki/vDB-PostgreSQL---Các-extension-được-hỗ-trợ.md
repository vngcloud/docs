PostgreSQL nổi tiếng với tính linh hoạt. Bạn hoàn toàn có thể mở rộng các core-function của Postgresql bằng các Extensions.

Mặc định, khi khởi tạo một database với vDB PostgreSQL, bạn đã được bật sẵn một số extension (danh sách bên dưới), ngoài ra bạn cũng có thể chủ động bật thêm một số extension khác tùy theo nhu cầu (danh sách bên dưới).

 **1.Danh sách các extension được bật sẵn:** Đối với PostgreSQL, các database được tạo mới sẽ được bật sẵn các Extension như trong database  **template1. ** 

Sau khi tạo database, bạn có thể dùng lệnh:


```
 \dx
```
hoặc


```
select * from pg_extension; 
```
để xem danh sách các extension đã được bật trên database.



Dưới đây là danh sách các extension đã được bật sẵn:



|  **Name**  |  **Version**  |  **Description**  | 
| btree_gin | 1.2 | support for indexing common datatypes in GIN | 
| btree_gist | 1.5 | support for indexing common datatypes in GiST | 
| chkpass | 1 | data type for auto-encrypted passwords | 
| citext | 1.4 | data type for case-insensitive character strings | 
| cube | 1.2 | data type for multidimensional cubes | 
| dict_int | 1 | text search dictionary template for integers | 
| dict_xsyn | 1 | text search dictionary template for extended synonym processing | 
| hstore | 1.4 | data type for storing sets of (key, value) pairs | 
| isn | 1.1 | data types for international product numbering standards | 
| lo | 1.1 | Large Object maintenance | 
| ltree | 1.1 | data type for hierarchical tree-like structures | 
| plpgsql | 1 | PL/pgSQL procedural language | 
| postgis | 2.5.4 | PostGIS geometry, geography, and raster spatial types and functions | 



 **Lưu ý:** N **ế** u bạn muốn tạo database trắng hoàn toàn, hãy dùng  **template0.** 

VD:


```
CREATE DATABASE dbname TEMPLATE template0;
```




 **2. Danh sách các extension bạn có thể tự bật:** Bạn có thể tự bật một Extension bằng cách chạy lệnh:


```
Create Extension <extension_name>;
```




|  **Name**  |  **Version**  |  **Description**  | 
| address_standardizer | 2.5.4 | Used to parse an address into constituent elements. Generally used to support geocoding address normalization step. | 
| address_standardizer_data_us | 2.5.4 | Address Standardizer US dataset example | 
| amcheck | 1 | functions for verifying relation integrity | 
| autoinc | 1 | functions for autoincrementing fields | 
| earthdistance | 1.1 | calculate great-circle distances on the surface of the Earth | 
| fuzzystrmatch | 1.1 | determine similarities and distance between strings | 
| insert_username | 1 | functions for tracking who changed a table | 
| intagg | 1.1 | integer aggregator and enumerator (obsolete) | 
| intarray | 1.2 | functions, operators, and index support for 1-D arrays of integers | 
| moddatetime | 1 | functions for tracking last modification time | 
| pageinspect | 1.6 | inspect the contents of database pages at a low level | 
| pg_buffercache | 1.3 | examine the shared buffer cache | 
| pg_freespacemap | 1.2 | examine the free space map (FSM) | 
| pg_prewarm | 1.1 | prewarm relation data | 
| pg_stat_statements | 1.6 | track execution statistics of all SQL statements executed | 
| pg_trgm | 1.3 | text similarity measurement and index searching based on trigrams | 
| pg_visibility | 1.2 | examine the visibility map (VM) and page-level visibility info | 
| pgcrypto | 1.3 | cryptographic functions | 
| pgrouting | 3.0.0 | pgRouting Extension | 
| pgrowlocks | 1.2 | show row-level locking information | 
| pgstattuple | 1.5 | show tuple-level statistics | 
| postgis_sfcgal | 2.5.4 | PostGIS SFCGAL functions | 
| postgis_tiger_geocoder | 2.5.4 | PostGIS tiger geocoder and reverse geocoder | 
| postgis_topology | 2.5.4 | PostGIS topology spatial types and functions | 
| refint | 1 | functions for implementing referential integrity (obsolete) | 
| sslinfo | 1.2 | information about SSL certificates | 
| tablefunc | 1 | functions that manipulate whole tables, including crosstab | 
| tcn | 1 | Triggered change notifications | 
| timetravel | 1 | functions for implementing time travel | 
| tsm_system_rows | 1 | TABLESAMPLE method which accepts number of rows as a limit | 
| tsm_system_time | 1 | TABLESAMPLE method which accepts time in milliseconds as a limit | 
| unaccent | 1.1 | text search dictionary that removes accents | 
| uuid-ossp | 1.1 | generate universally unique identifiers (UUIDs) | 



bạn có thể dùng lệnh sau để kiểm tra danh sách các extension đang được hỗ trợ trên vDB của mình:




```
select * from pg_available_extensions;
```


Nếu bạn cần extension nào chưa được hỗ trợ, vui lòng liên hệ với  **VNG Cloud Support** để được hỗ trợ.



*****

[[category.storage-team]] 
[[category.confluence]] 
