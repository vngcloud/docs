# Cấu hình DNS cho dịch vụ vWAF

Sau khi khởi tạo ứng dụng trên vWAF, lưu lượng chỉ thực sự đi qua WAF khi **domain dịch vụ của Quý Khách hàng đã được trỏ DNS về hệ thống vWAF**. Nếu chưa cấu hình DNS, ứng dụng vẫn hiển thị trạng thái _Active_ trên giao diện nhưng WAF **chưa bảo vệ** lưu lượng thực tế.

GreenNode hỗ trợ **song song hai phương thức** cấu hình DNS:

|                                          | **CNAME** _(khuyến nghị)_                                           | **A Record**                                                          |
| ---------------------------------------- | ------------------------------------------------------------------- | --------------------------------------------------------------------- |
| Bản ghi trỏ về                           | Domain DNS riêng do GreenNode cấp                                   | Địa chỉ IP public của vWAF                                            |
| Điều chỉnh định tuyến giữa các zone vWAF | GreenNode chủ động thực hiện, **không cần Quý Khách hàng thao tác** | Quý Khách hàng phải tự cập nhật lại DNS                               |
| Thời gian xử lý khi cần đổi định tuyến   | Nhanh (theo TTL bản ghi do GreenNode quản lý)                       | Phụ thuộc thời gian Quý Khách hàng cập nhật + TTL phía Quý Khách hàng |
| Áp dụng cho Root Domain (Apex)           | Chỉ khi DNS Provider hỗ trợ ALIAS / ANAME / CNAME Flattening        | Áp dụng được cho mọi trường hợp                                       |
| Áp dụng cho subdomain                    | Có                                                                  | Có                                                                    |

> **Khuyến nghị:** GreenNode khuyến nghị Quý Khách hàng chủ động rà soát cấu hình DNS hiện tại và cân nhắc chuyển sang phương thức **CNAME** nếu DNS Provider hỗ trợ. Phương thức này giúp tăng tính linh hoạt và khả năng chủ động trong việc điều phối lưu lượng khi vận hành dịch vụ vWAF.

***

### 1. Phương thức CNAME (khuyến nghị)

#### 1.1. Nguyên lý hoạt động

Với phương thức CNAME, GreenNode bổ sung một **lớp trung gian DNS do GreenNode quản lý**:

* GreenNode cấp cho **mỗi Quý Khách hàng một domain DNS riêng** (gọi là _domain định tuyến vWAF_).
* Quý Khách hàng cấu hình **CNAME Record** của domain dịch vụ trỏ đến domain DNS do GreenNode cung cấp.
* Domain định tuyến này trỏ tới zone vWAF đang phục vụ Quý Khách hàng. Khi cần tối ưu hoặc điều chỉnh định tuyến, GreenNode **chủ động cập nhật DNS phía GreenNode** để chuyển lưu lượng sang zone vWAF phù hợp, **mà không yêu cầu Quý Khách hàng thay đổi cấu hình DNS**.

```
           Quý Khách hàng cấu hình                   GreenNode quản lý
             (một lần duy nhất)                     (chủ động cập nhật)
                      │                                      │
                      ▼                                      ▼
www.example.com ────CNAME────▶ opnclhqr.waf.greennode.vn ────A────▶ Zone vWAF (IP)
```

Nhờ đó, việc điều phối lưu lượng giữa các zone vWAF được thực hiện chủ động ở phía GreenNode, giúp **rút ngắn thời gian xử lý** trong các tình huống cần thay đổi định tuyến.

#### 1.2. Lấy domain định tuyến vWAF

Domain định tuyến là **duy nhất cho mỗi tài khoản** và **không thay đổi** trong suốt quá trình sử dụng dịch vụ (kể cả khi Quý Khách hàng thêm, sửa hoặc xóa ứng dụng). Quý Khách hàng chỉ cần cấu hình CNAME một lần cho mỗi domain dịch vụ.

Domain có dạng `<mã-định-tuyến>.waf.greennode.vn`, trong đó `<mã-định-tuyến>` là chuỗi 8 ký tự do GreenNode sinh tự động và gắn với tài khoản của Quý Khách hàng.

**Ví dụ:**

```
opnnqpqr.waf.greennode.vn
```

Để xem domain định tuyến được cấp cho tài khoản của mình, Quý Khách hàng truy cập **Portal GreenNode → vWAF → Ứng dụng**. Domain được hiển thị ngay tại khung thông báo phía trên danh sách ứng dụng:

> Để đảm bảo toàn bộ lưu lượng được kiểm soát và bảo vệ bởi GreenNode WAF:
>
> * **Khuyến nghị:** Trỏ domain của Quý Khách hàng về CNAME `<mã-định-tuyến>.waf.greennode.vn`.
> * **Phương án thay thế:** Nếu không thể sử dụng CNAME, trỏ bản ghi DNS A của domain về `vwaf_public_ip`.

> **Lưu ý:** `opnnqpqr.waf.greennode.vn` ở trên chỉ là ví dụ minh họa, Quý Khách hàng vui lòng sử dụng đúng domain định tuyến hiển thị trên Portal của tài khoản mình. Nếu không thấy khung thông báo này, vui lòng liên hệ đội ngũ hỗ trợ của GreenNode.

#### 1.3. Các bước cấu hình

1. Đăng nhập vào trang quản trị DNS của nhà cung cấp DNS đang sử dụng cho domain dịch vụ.
2. **Tạo bản ghi CNAME** trỏ về domain định tuyến vWAF.
3. Lưu cấu hình và chờ DNS lan truyền, sau đó kiểm tra theo hướng dẫn tại **mục 4**.

**Ví dụ cấu hình:**

| Type  | Name / Host | Value / Target              | TTL |
| ----- | ----------- | --------------------------- | --- |
| CNAME | @           | `opnnqpqr.waf.greennode.vn` | 300 |
| CNAME | `api`       | `opnnqpqr.waf.greennode.vn` | 300 |

Kết quả: `example.com` và `api.example.com` cùng đi qua vWAF.

***

### 2. Phương thức A Record

Phương thức A Record tiếp tục được GreenNode hỗ trợ và **không có thay đổi** so với hiện tại. Quý Khách hàng cấu hình bản ghi A của domain dịch vụ trỏ trực tiếp đến địa chỉ IP public của vWAF

**Ví dụ cấu hình:**

| Type | Name / Host | Value         | TTL |
| ---- | ----------- | ------------- | --- |
| A    | `www`       | `103.7.174.5` | 300 |
| A    | `@`         | `103.7.174.5` | 300 |

> **Lưu ý về vận hành:** Với phương thức A Record, khi GreenNode cần điều chỉnh định tuyến sang zone vWAF khác, Quý Khách hàng sẽ **phải tự cập nhật lại bản ghi DNS** tại phía mình. Điều này làm tăng thời gian xử lý trong các tình huống cần thay đổi định tuyến gấp.

***

### 3. Trường hợp Root Domain (Apex / Zone Apex)

Theo chuẩn DNS, **không thể tạo bản ghi CNAME tại Root Domain** (ví dụ `example.com`, không có subdomain). Quý Khách hàng có thể xử lý theo một trong các cách sau:

| Trường hợp                                                                                     | Cách xử lý                                                                                                                                     |
| ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| DNS Provider hỗ trợ **ALIAS / ANAME / CNAME Flattening** (Cloudflare, AWS Route 53, DNSimple…) | Tạo bản ghi ALIAS/ANAME/Flattened CNAME tại Root Domain trỏ về `<mã-định-tuyến>.waf.greennode.vn`. Vẫn giữ được lợi ích của phương thức CNAME. |
| DNS Provider **không hỗ trợ**                                                                  | Tiếp tục sử dụng **A Record** trỏ trực tiếp đến IP vWAF `103.7.174.5` như hiện tại.                                                            |

> **Lưu ý:** Với cơ chế ALIAS / CNAME Flattening, tốc độ nhận thay đổi định tuyến phụ thuộc vào cách DNS Provider xử lý và TTL mà Provider áp dụng, có thể chậm hơn so với CNAME thông thường.

GreenNode hỗ trợ song song cả hai phương thức CNAME và A Record, tùy thuộc vào khả năng hỗ trợ của DNS Provider và mô hình triển khai của Quý Khách hàng.

***

### 4. Kiểm tra sau khi cấu hình

**Kiểm tra bản ghi CNAME:**

```bash
dig +short CNAME example.com
# Kết quả mong đợi:
# opnnqpqr.waf.greennode.vn.
```

**Kiểm tra địa chỉ IP đích cuối cùng:**

```bash
dig +short example.com
# Kết quả mong đợi: địa chỉ IP của zone vWAF
```

**Kiểm tra lưu lượng đã đi qua vWAF:**

```bash
curl -I https://example.com
```
