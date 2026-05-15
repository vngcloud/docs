# Migrate từ Postgres Single sang Postgres Cluster

Hướng dẫn này mô tả các bước export dữ liệu từ **Postgres Single Node** và restore sang **Postgres Cluster** trên vDB. Tài liệu bao gồm hai tình huống: **Phần A** cho instance có một database, và **Phần B** cho instance có nhiều database.

{% hint style="info" %}
**Lưu ý:** vDB không hỗ trợ thay đổi Deployment Type của database hiện có. Việc migrate yêu cầu tạo mới một Postgres Cluster và chuyển dữ liệu thủ công theo các bước dưới đây.
{% endhint %}

***

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy đảm bảo:

* `psql`, `pg_dump` hoặc `pg_dumpall`, và `pg_restore` đã được cài đặt trên máy thực hiện migrate (phiên bản khớp với PostgreSQL trên instance nguồn).
* Bạn có credentials (host, username, password) cho cả Postgres Single Node và Postgres Cluster.

***

## A. Migrate một database (pg\_dump)

Sử dụng phần này khi Postgres Single Node của bạn chứa **một database** cần migrate.


### Bước 1 — Kiểm tra kết nối

Trước khi bắt đầu, hãy xác nhận rằng cả Postgres Single Node và Postgres Cluster đều đang chạy và có thể kết nối được. 

```bash
# Kiểm tra Postgres Single Node
psql -h <IP_single> -U <username_single> -d <database_single> -c "SELECT 1;"

# Kiểm tra Postgres Cluster
psql -h <IP_cluster> -U <username_cluster> -d <database_cluster> -c "SELECT 1;"
```

***

### Bước 2 — Xuất dữ liệu

Dùng `pg_dump` để xuất database nguồn. Chọn định dạng phù hợp với phương thức restore bạn muốn sử dụng.

**Tùy chọn A — Custom format** (khuyến nghị; dùng với `pg_restore`):

```bash
pg_dump -h <IP_single> -U <username_single> -d <database_single> \
        -Fc -f backup.dump
```

**Tùy chọn B — Plain SQL format** (dùng với `psql`):

```bash
pg_dump -h <IP_single> -U <username_single> -d <database_single> \
        -Fp > backup.sql
```

{% hint style="info" %}
**Gợi ý — Chọn định dạng phù hợp:**
Custom format (`-Fc`) tạo ra file binary được nén và hỗ trợ restore multi-job với `pg_restore`. Plain SQL format (`-Fp`) tạo ra file có thể dễ dàng đọc được, dễ kiểm tra hoặc chỉnh sửa trước khi restore. Nên dùng custom format cho database có dung lượng lớn.
{% endhint %}

***

### Bước 3 — Restore trên Postgres Cluster

Restore dữ liệu lên cluster đích theo đúng định dạng đã export.

**Nếu export bằng custom format**, dùng `pg_restore`:

```bash
pg_restore -h <IP_cluster> -U <username_cluster> -d <database_cluster> \
           --no-owner --no-privileges backup.dump
```

**Nếu export bằng plain SQL format**, dùng `psql`:

```bash
psql -h <IP_cluster> -U <username_cluster> -d <database_cluster> \
     -f backup.sql
```

{% hint style="warning" %}
**Lỗi superuser trong quá trình restore:**
Postgres Cluster không cấp quyền superuser. Bạn có thể gặp lỗi như `ERROR: must be superuser` hoặc cảnh báo về `ALTER TABLE ... OWNER TO`. Đây là hành vi bình thường và có thể bỏ qua.

Các flag `--no-owner` và `--no-privileges` (dùng với `pg_restore`) sẽ ngăn các lỗi phổ biến nhất. Bất kỳ lỗi nào liên quan đến việc tạo bảng hoặc dữ liệu thực cần được xem xét kỹ trước khi tiếp tục.
{% endhint %}

***

### Bước 4 — Xác minh dữ liệu sau restore

Sau khi restore hoàn tất, hãy kiểm tra dữ liệu trên Postgres Cluster trước khi chuyển traffic sang. Khuyến nghị một số kiểm tra:

* So sánh số lượng bảng giữa nguồn và đích.
* So sánh số lượng bản ghi trong các bảng quan trọng.
* Kiểm tra thủ công một số bản ghi trong các bảng chính.
* Chạy thử các câu truy vấn của ứng dụng với database vừa restore.

***

## B. Migrate nhiều database (pg\_dumpall / pg\_dump)

Sử dụng phần này khi Postgres Single Node của bạn chứa **nhiều hơn một database**.

***

### Bước 1 — Kiểm tra kết nối

Xác nhận cả hai instance đang chạy và có thể kết nối được trước khi tiến hành.

```bash
# Kiểm tra Postgres Single Node
psql -h <IP_single> -U <username_single> -c "\l"

# Kiểm tra Postgres Cluster
psql -h <IP_cluster> -U <username_cluster> -c "\l"
```

***

### Bước 2 — Xuất toàn bộ database

Chọn một trong hai cách xuất dữ liệu dưới đây.

**Tùy chọn A — pg\_dumpall** (xuất tất cả database vào một file):

```bash
pg_dumpall -h <IP_single> -U <username_single> \
           --no-role-passwords > alldb.sql
```

{% hint style="info" %}
**Giới hạn của pg\_dumpall:**
`pg_dumpall` chỉ tạo output dạng plain SQL, do đó bạn phải restore bằng `psql`. Lệnh này cũng cố gắng export các global object (role, tablespace) yêu cầu quyền superuser. Lỗi `ERROR: must be superuser` trong quá trình export là bình thường và có thể bỏ qua. Flag `--no-role-passwords` bỏ qua các mật khẩu đã được mã hóa vì không thể restore chúng mà không có quyền superuser.
{% endhint %}

**Tùy chọn B — pg\_dump theo từng database** (khuyến nghị cho hầu hết các trường hợp):

Chạy `pg_dump` riêng cho từng database. Cách này tránh hoàn toàn các lỗi liên quan đến quyền global và cho bạn kiểm soát tốt hơn trong quá trình restore.

```bash
# Lặp lại cho từng database
pg_dump -h <IP_single> -U <username_single> -d <db_name> \
        -Fc -f <db_name>.dump
```

{% hint style="info" %}
`pg_dump` không export các global object như role và tablespace. Bạn phải tạo lại chúng thủ công trên Postgres Cluster trước khi restore. Xem Bước 3 để biết thêm chi tiết.
{% endhint %}

***

### Bước 3 — Tạo lại Role và Tablespace (nếu cần)

Nếu database của bạn phụ thuộc vào các role hoặc tablespace cụ thể, hãy tạo lại chúng trên Postgres Cluster trước khi restore. Các role được tạo ở đây cần đặt mật khẩu thủ công.

```sql
-- Tạo lại một role
CREATE ROLE <role_name> WITH LOGIN;
ALTER ROLE <role_name> WITH PASSWORD '<new_password>';
```

Nếu bạn dùng `pg_dumpall`, file SQL chứa định nghĩa role nhưng một số câu lệnh có thể thất bại do thiếu quyền superuser. Hãy xem qua file và áp dụng thủ công các câu lệnh quản lý role khi cần.

***

### Bước 4 — Restore trên Postgres Cluster

**Nếu dùng pg\_dumpall (Tùy chọn A)**, restore bằng `psql` kết nối vào database mặc định `postgres`:

```bash
psql -h <IP_cluster> -U <username_cluster> -d postgres \
     -f alldb.sql
```

**Nếu dùng pg\_dump theo từng database (Tùy chọn B)**, restore từng file dump riêng lẻ:

```bash
# Lặp lại cho từng database
pg_restore -h <IP_cluster> -U <username_cluster> -d <db_name> \
           --no-owner --no-privileges <db_name>.dump
```

{% hint style="warning" %}
**Mật khẩu role sau khi restore:**
`pg_dumpall` export định nghĩa role nhưng không bao gồm mật khẩu (flag `--no-role-passwords` bỏ qua chúng, và mật khẩu đã mã hóa không thể restore mà không có quyền superuser). Sau khi restore, bạn phải đặt thủ công mật khẩu cho tất cả role cần xác thực:

```sql
ALTER ROLE <role_name> WITH PASSWORD '<new_password>';
```
{% endhint %}

***

### Bước 5 — Xác minh từng database

Sau khi restore, kiểm tra toàn bộ database trên Postgres Cluster. Khuyến nghị một số kiểm tra:

* Xác nhận tất cả database dự kiến đều hiện diện.
* Kiểm tra số lượng bảng và số lượng bản ghi trong từng database.
* Xác minh rằng người dùng ứng dụng có thể kết nối và truy vấn thành công.

***

## Bảng tham khảo nhanh

| Tình huống | Công cụ export | Công cụ restore | Khi nào dùng |
| --- | --- | --- | --- |
| Một database | `pg_dump -Fc` | `pg_restore` | Database lớn, cần restore nhanh (hỗ trợ multi-job) |
| Một database | `pg_dump -Fp` | `psql` | Cần đọc hoặc chỉnh sửa file SQL trước khi restore |
| Nhiều database | `pg_dumpall` | `psql` | Muốn export tất cả database vào một file duy nhất |
| Nhiều database | `pg_dump` (từng DB) | `pg_restore` / `psql` | Cần kiểm soát riêng từng database, tránh lỗi quyền global |

***

## Một số vấn đề thường gặp

**`ERROR: must be superuser`**

Lỗi về quyền superuser là bình thường trên cả Postgres Single Node và Postgres Cluster. Bỏ qua chúng. Dùng flag `--no-owner` và `--no-privileges` với `pg_restore` để ngăn các lỗi phổ biến nhất.

**Lỗi về role hoặc ownership sau khi restore**

`pg_dump` và `pg_dumpall` không mang theo mật khẩu role. Sau khi restore, đặt thủ công mật khẩu cho tất cả role cần xác thực.

**Thiếu tablespace**

Nếu database nguồn sử dụng custom tablespace, quá trình restore có thể thất bại vì các tablespace đó không tồn tại trên cluster đích. Tạo lại các tablespace cần thiết trên Postgres Cluster trước khi chạy lệnh restore.

**Lỗi tạo bảng**

Các lỗi không liên quan đến quyền superuser (ví dụ: bảng trùng lặp, không khớp kiểu dữ liệu) cần được điều tra trước khi tiếp tục. Không bỏ qua những lỗi này.

**Database dung lượng lớn**

Với database rất lớn, dùng `pg_restore --jobs <n>` để bật chế độ restore multi-job với custom format và giảm thời gian restore tổng thể.

***

## Bước tiếp theo

Sau khi xác minh dữ liệu thành công:

* Cập nhật connection string trong ứng dụng để trỏ sang Postgres Cluster (host, port, credentials mới).
* Kiểm tra ứng dụng hoạt động bình thường với database vừa migrate.
* Xóa Postgres Single Node cũ trên vDB sau khi đã xác nhận không còn cần thiết.
