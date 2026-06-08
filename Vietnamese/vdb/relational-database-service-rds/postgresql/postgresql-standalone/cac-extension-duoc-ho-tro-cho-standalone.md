# PostgreSQL Standalone Extensions

PostgreSQL nổi tiếng với tính linh hoạt. Bạn hoàn toàn có thể mở rộng các core-function của PostgreSQL bằng các Extensions.

Mặc định, khi khởi tạo một database với vDB PostgreSQL, bạn đã được bật sẵn một số extension (danh sách bên dưới), ngoài ra bạn cũng có thể chủ động bật thêm một số extension khác tùy theo nhu cầu.

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

<table><thead><tr><th>No</th><th>Name</th><th>Description</th></tr></thead><tbody><tr><td>1</td><td>plpgsql</td><td>Ngôn ngữ thủ tục PL/pgSQL</td></tr><tr><td>2</td><td>btree_gin</td><td>Hỗ trợ đánh index các kiểu dữ liệu phổ biến với GIN</td></tr><tr><td>3</td><td>btree_gist</td><td>Hỗ trợ đánh index các kiểu dữ liệu phổ biến với GiST</td></tr><tr><td>4</td><td>citext</td><td>Kiểu dữ liệu chuỗi ký tự không phân biệt hoa thường</td></tr><tr><td>5</td><td>cube</td><td>Kiểu dữ liệu lưu điểm hoặc khoảng trong không gian nhiều chiều</td></tr><tr><td>6</td><td>dict_int</td><td>Template từ điển tìm kiếm văn bản cho kiểu số nguyên</td></tr><tr><td>7</td><td>dict_xsyn</td><td>Template từ điển hỗ trợ tìm kiếm mở rộng qua các từ đồng nghĩa</td></tr><tr><td>8</td><td>hstore</td><td>Kiểu dữ liệu lưu trữ key-value linh hoạt trong một trường</td></tr><tr><td>9</td><td>isn</td><td>Kiểu dữ liệu cho các chuẩn mã số sản phẩm quốc tế</td></tr><tr><td>10</td><td>lo</td><td>Quản lý đối tượng lớn (Large Object)</td></tr><tr><td>11</td><td>ltree</td><td>Kiểu dữ liệu biểu diễn cấu trúc cây phân cấp</td></tr><tr><td>12</td><td>pg_trgm</td><td>Đo độ tương đồng chuỗi và tìm kiếm index theo trigram</td></tr><tr><td>13</td><td>postgis</td><td>Kiểu dữ liệu và hàm không gian của PostGIS (geometry, geography, raster)</td></tr><tr><td>14</td><td>postgres_fdw</td><td>Foreign-data wrapper kết nối đến máy chủ PostgreSQL từ xa</td></tr><tr><td>15</td><td>unaccent</td><td>Loại bỏ dấu khỏi văn bản, hỗ trợ tìm kiếm không phân biệt dấu</td></tr><tr><td>16</td><td>vector</td><td>Kiểu dữ liệu vector với hỗ trợ index ivfflat và hnsw</td></tr></tbody></table>

**Lưu ý:** Nếu bạn muốn tạo database trắng hoàn toàn, hãy dùng **template0.**

```sql
CREATE DATABASE dbname TEMPLATE template0;
```

## 2. Danh sách các extension bạn có thể tự bật

Bạn có thể tự bật một Extension bằng cách chạy lệnh:

```sql
CREATE EXTENSION <extension_name>;
```

<table><thead><tr><th>Name</th><th>Description</th></tr></thead><tbody><tr><td>fuzzystrmatch</td><td>Đo độ tương đồng và khoảng cách giữa các chuỗi ký tự</td></tr><tr><td>intarray</td><td>Hàm, toán tử và hỗ trợ index cho mảng số nguyên một chiều</td></tr><tr><td>pgcrypto</td><td>Tập hàm mã hóa dữ liệu</td></tr><tr><td>postgis_tiger_geocoder</td><td>Geocoder và reverse geocoder kiểu Tiger của PostGIS (yêu cầu fuzzystrmatch đã được bật trước)</td></tr><tr><td>seg</td><td>Kiểu dữ liệu cho đoạn thẳng hoặc khoảng số thực</td></tr><tr><td>tablefunc</td><td>Các hàm xây dựng bảng pivot (crosstab) và xử lý bảng</td></tr><tr><td>tcn</td><td>Tự động gửi NOTIFY khi có thay đổi dữ liệu trong bảng</td></tr><tr><td>tsm_system_rows</td><td>Phương thức lấy mẫu TABLESAMPLE theo số lượng hàng</td></tr><tr><td>tsm_system_time</td><td>Phương thức lấy mẫu TABLESAMPLE theo thời gian (mili giây)</td></tr><tr><td>uuid-ossp</td><td>Sinh UUID theo chuẩn RFC 4122</td></tr></tbody></table>

***

## 3. Lưu ý

* Extension **vector** chỉ available cho các vDB khởi tạo từ **01/08/2024**.
* Để sử dụng trên các vDB đã khởi tạo trước đó, bạn vui lòng liên hệ **GreenNode Cloud Support** để được hỗ trợ enable.
