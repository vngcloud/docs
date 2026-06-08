# PostgreSQL Cluster Extensions

PostgreSQL nổi tiếng với tính linh hoạt. Bạn hoàn toàn có thể mở rộng các core-function của PostgreSQL bằng các Extensions.

Mặc định, khi khởi tạo một database với vDB PostgreSQL, bạn đã được bật sẵn một số extension (danh sách bên dưới), ngoài ra bạn cũng có thể chủ động bật thêm một số extension khác tùy theo nhu cầu.

***

## 1. Extension được bật sẵn

Các extension sau đây được cài đặt tự động trên mỗi database của Cluster khi khởi tạo. Bạn không cần chạy `CREATE EXTENSION` để sử dụng.

<table><thead><tr><th>Name</th><th>Version</th><th>Description</th></tr></thead><tbody><tr><td>plpgsql</td><td>1.0</td><td>Ngôn ngữ thủ tục PL/pgSQL</td></tr><tr><td>pg_stat_statements</td><td>1.11</td><td>Ghi nhận thống kê thực thi cho tất cả câu lệnh SQL</td></tr><tr><td>pg_stat_kcache</td><td>2.3.1</td><td>Theo dõi thống kê cache kernel (đọc/ghi) theo từng câu truy vấn</td></tr></tbody></table>

## 2. Danh sách extension bạn có thể tự bật

Bạn có thể tự bật các extension sau bằng `CREATE EXTENSION`.

```sql
CREATE EXTENSION <extension_name>;
```

<table><thead><tr><th>Name</th><th>Version</th><th>Description</th></tr></thead><tbody><tr><td>btree_gin</td><td>1.3</td><td>Hỗ trợ đánh index các kiểu dữ liệu phổ biến với GIN</td></tr><tr><td>btree_gist</td><td>1.7</td><td>Hỗ trợ đánh index các kiểu dữ liệu phổ biến với GiST</td></tr><tr><td>citext</td><td>1.6</td><td>Kiểu dữ liệu chuỗi ký tự không phân biệt hoa thường</td></tr><tr><td>cube</td><td>1.5</td><td>Kiểu dữ liệu lưu điểm hoặc khoảng trong không gian nhiều chiều</td></tr><tr><td>dict_int</td><td>1.0</td><td>Template từ điển tìm kiếm văn bản cho kiểu số nguyên</td></tr><tr><td>dict_xsyn</td><td>1.0</td><td>Template từ điển hỗ trợ tìm kiếm mở rộng qua các từ đồng nghĩa</td></tr><tr><td>earthdistance</td><td>1.2</td><td>Tính khoảng cách địa lý giữa hai điểm trên bề mặt Trái Đất</td></tr><tr><td>fuzzystrmatch</td><td>1.2</td><td>Đo độ tương đồng và khoảng cách giữa các chuỗi ký tự</td></tr><tr><td>hstore</td><td>1.8</td><td>Kiểu dữ liệu lưu trữ key-value linh hoạt trong một trường</td></tr><tr><td>intarray</td><td>1.5</td><td>Hàm, toán tử và hỗ trợ index cho mảng số nguyên một chiều</td></tr><tr><td>isn</td><td>1.2</td><td>Kiểu dữ liệu cho các chuẩn mã số sản phẩm quốc tế</td></tr><tr><td>lo</td><td>1.1</td><td>Quản lý đối tượng lớn (Large Object)</td></tr><tr><td>ltree</td><td>1.3</td><td>Kiểu dữ liệu biểu diễn cấu trúc cây phân cấp</td></tr><tr><td>pg_partman</td><td>5.4.3</td><td>Quản lý phân vùng bảng theo thời gian hoặc theo chuỗi số</td></tr><tr><td>pg_permissions</td><td>1.3</td><td>Xem và kiểm tra quyền truy cập đối tượng theo trạng thái mong muốn</td></tr><tr><td>pg_repack</td><td>1.5.3</td><td>Tổ chức lại bảng với thời gian khóa tối thiểu</td></tr><tr><td>pg_trgm</td><td>1.6</td><td>Đo độ tương đồng chuỗi và tìm kiếm index theo trigram</td></tr><tr><td>pgaudit</td><td>17.1</td><td>Ghi nhật ký kiểm toán chi tiết theo phiên làm việc và theo đối tượng</td></tr><tr><td>pgcrypto</td><td>1.3</td><td>Tập hàm mã hóa dữ liệu</td></tr><tr><td>pltcl</td><td>1.0</td><td>Ngôn ngữ thủ tục PL/Tcl</td></tr><tr><td>postgis</td><td>3.6.3</td><td>Kiểu dữ liệu và hàm không gian của PostGIS (geometry, geography, raster)</td></tr><tr><td>postgis_raster</td><td>3.6.3</td><td>Kiểu dữ liệu raster và các hàm không gian của PostGIS</td></tr><tr><td>postgis_tiger_geocoder</td><td>3.6.3</td><td>Geocoder và reverse geocoder kiểu Tiger của PostGIS</td></tr><tr><td>postgis_topology</td><td>3.6.3</td><td>Kiểu dữ liệu và hàm không gian topology của PostGIS</td></tr><tr><td>postgres_fdw</td><td>1.1</td><td>Foreign-data wrapper kết nối đến máy chủ PostgreSQL từ xa</td></tr><tr><td>seg</td><td>1.4</td><td>Kiểu dữ liệu lưu khoảng giá trị số thực</td></tr><tr><td>set_user</td><td>4.1.0</td><td>Chuyển đổi người dùng trong phiên làm việc với tùy chọn ghi nhật ký</td></tr><tr><td>tablefunc</td><td>1.0</td><td>Các hàm xây dựng bảng pivot (crosstab) và xử lý bảng</td></tr><tr><td>tcn</td><td>1.0</td><td>Tự động gửi NOTIFY khi có thay đổi dữ liệu trong bảng</td></tr><tr><td>timescaledb</td><td>2.27.1</td><td>Tối ưu hóa lưu trữ và truy vấn dữ liệu time-series</td></tr><tr><td>tsm_system_rows</td><td>1.0</td><td>Phương thức lấy mẫu TABLESAMPLE theo số lượng hàng</td></tr><tr><td>tsm_system_time</td><td>1.0</td><td>Phương thức lấy mẫu TABLESAMPLE theo thời gian (mili giây)</td></tr><tr><td>unaccent</td><td>1.1</td><td>Loại bỏ dấu khỏi văn bản, hỗ trợ tìm kiếm không phân biệt dấu</td></tr><tr><td>uuid-ossp</td><td>1.1</td><td>Sinh UUID theo chuẩn RFC 4122</td></tr><tr><td>vector</td><td>0.8.2</td><td>Kiểu dữ liệu vector với hỗ trợ index ivfflat và hnsw</td></tr></tbody></table>

***