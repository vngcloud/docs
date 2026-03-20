# Hướng dẫn quản lý địa chỉ nhận hóa đơn

### 1. Giới thiệu <a href="#id-1-gioi-thieu" id="id-1-gioi-thieu"></a>

Tính năng **Quản lý Địa Chỉ Nhận Hóa Đơn** cho phép người dùng:

* Thêm nhiều địa chỉ nhận hóa đơn (cá nhân hoặc doanh nghiệp)
* Đặt một địa chỉ làm **mặc định** để tự động sử dụng khi thanh toán
* Xóa các địa chỉ không còn cần thiết

> ⚠️ **Lưu ý:** Địa chỉ Nhận Hóa Đơn Mặc Định sẽ được ưu tiên hiển thị trong lúc thanh toán.

### 2. Cách truy cập <a href="#id-2-cach-truy-cap" id="id-2-cach-truy-cap"></a>

Truy cập vào màn hình **Quản lý Địa Chỉ Nhận Hóa Đơn** tại [https://register.vngcloud.vn/profile#invoice-address-info](https://register.vngcloud.vn/profile#invoice-address-info)

### 3. Giao diện màn hình chính <a href="#id-3-giao-dien-man-hinh-chinh" id="id-3-giao-dien-man-hinh-chinh"></a>

Màn hình chính hiển thị danh sách tất cả địa chỉ nhận hóa đơn đã được lưu.

#### 3.1. Thông tin hiển thị cho mỗi địa chỉ <a href="#id-31-thong-tin-hien-thi-cho-moi-dia-chi" id="id-31-thong-tin-hien-thi-cho-moi-dia-chi"></a>

Mỗi địa chỉ trong danh sách hiển thị đầy đủ các thông tin sau:

<table><thead><tr><th width="196.625">Trường</th><th>Mô tả</th></tr></thead><tbody><tr><td><strong>Tên</strong></td><td>Tên người nhận (Cá nhân) hoặc Tên doanh nghiệp</td></tr><tr><td><strong>Loại</strong></td><td>Nhãn <code>CÁ NHÂN</code> hoặc <code>DOANH NGHIỆP</code></td></tr><tr><td><strong>Email</strong></td><td>Địa chỉ email nhận hóa đơn</td></tr><tr><td><strong>Số Điện Thoại</strong></td><td>Số điện thoại liên lạc (kèm mã vùng quốc gia)</td></tr><tr><td><strong>Mã số thuế</strong></td><td>Mã số thuế doanh nghiệp hoặc Số CCCD (cá nhân)</td></tr><tr><td><strong>Quốc tịch</strong></td><td>Quốc gia</td></tr><tr><td><strong>Địa chỉ</strong></td><td>Địa chỉ cụ thể</td></tr></tbody></table>

#### 3.2. Nhãn trạng thái <a href="#id-32-nhan-trang-thai" id="id-32-nhan-trang-thai"></a>

* **`MẶC ĐỊNH`** — Hiển thị bên cạnh tên của địa chỉ đang được dùng làm mặc định. Địa chỉ này sẽ tự động được chọn khi thanh toán.
* **`CÁ NHÂN`** — Địa chỉ thuộc loại cá nhân.
* **`DOANH NGHIỆP`** — Địa chỉ thuộc loại doanh nghiệp.

#### 3.3. Các nút hành động <a href="#id-33-cac-nut-hanh-dong" id="id-33-cac-nut-hanh-dong"></a>

* **Sử dụng làm địa chỉ mặc định** — Chỉ hiện với địa chỉ chưa phải mặc định. Nhấn để đặt địa chỉ này thành địa chỉ mặc định.
* **Xóa** _(nút đỏ)_ — Chỉ hiện với địa chỉ chưa phải mặc định. Nhấn để xóa địa chỉ này.
* **Thêm Địa Chỉ Nhận Hóa Đơn** _(nút xanh lá, cuối trang)_ — Mở form để thêm địa chỉ mới.

### 4. Thêm địa chỉ nhận hóa đơn mới <a href="#id-4-them-dia-chi-nhan-hoa-don-moi" id="id-4-them-dia-chi-nhan-hoa-don-moi"></a>

#### Bước 1: Mở form thêm mới <a href="#buoc-1-mo-form-them-moi" id="buoc-1-mo-form-them-moi"></a>

Cuộn xuống cuối danh sách và nhấn nút **"Thêm Địa Chỉ Nhận Hóa Đơn"** (màu xanh lá).

Cửa sổ popup **"Thêm Địa Chỉ Nhận Hóa Đơn"** sẽ xuất hiện.

> _(Các trường được đánh dấu `*` là bắt buộc nhập)_

#### Bước 2: Chọn loại chủ thể nhận hóa đơn <a href="#buoc-2-chon-loai-chu-the-nhan-hoa-don" id="buoc-2-chon-loai-chu-the-nhan-hoa-don"></a>

Ở đầu form, chọn một trong hai loại:

* 🔘 **Doanh nghiệp** — Dành cho khách hàng là tổ chức, công ty, doanh nghiệp
* 🔘 **Cá nhân** — Dành cho khách hàng cá nhân

> Lựa chọn này ảnh hưởng đến các trường thông tin hiển thị trong form bên dưới.

#### Bước 3: Điền thông tin <a href="#buoc-3-dien-thong-tin" id="buoc-3-dien-thong-tin"></a>

**Trường hợp chọn Doanh nghiệp**

<table><thead><tr><th width="192.703125">Trường</th><th width="112.2734375" align="center">Bắt buộc</th><th>Ghi chú</th></tr></thead><tbody><tr><td>Tên Doanh Nghiệp</td><td align="center">✅</td><td>Tên đầy đủ của doanh nghiệp</td></tr><tr><td>Email</td><td align="center">✅</td><td>Email nhận hóa đơn điện tử</td></tr><tr><td>Số Điện Thoại</td><td align="center">❌</td><td>Chọn mã vùng quốc gia từ dropdown, sau đó nhập số điện thoại</td></tr><tr><td>Mã Số Thuế</td><td align="center">✅</td><td>Mã số thuế của doanh nghiệp</td></tr><tr><td>Quốc Tịch</td><td align="center">✅</td><td>Chọn quốc gia từ danh sách thả xuống</td></tr><tr><td>Địa chỉ</td><td align="center">✅</td><td>Địa chỉ đầy đủ (số nhà, đường, phường/xã, quận/huyện, tỉnh/thành phố)</td></tr></tbody></table>

**Trường hợp chọn Cá nhân**

<table><thead><tr><th width="199.8828125">Trường</th><th width="123.3125" align="center">Bắt buộc</th><th>Ghi chú</th></tr></thead><tbody><tr><td>Tên Người Nhận</td><td align="center">✅</td><td>Họ và tên đầy đủ của người nhận</td></tr><tr><td>Email</td><td align="center">✅</td><td>Email nhận hóa đơn điện tử</td></tr><tr><td>Số Điện Thoại</td><td align="center">❌</td><td>Chọn mã vùng quốc gia từ dropdown, sau đó nhập số điện thoại</td></tr><tr><td>Mã Số Thuế (Số Căn Cước Công Dân 12 số)</td><td align="center">✅</td><td>Nhập đầy đủ 12 chữ số CCCD</td></tr><tr><td>Quốc Tịch</td><td align="center">✅</td><td>Chọn quốc gia từ danh sách thả xuống</td></tr><tr><td>Địa chỉ</td><td align="center">✅</td><td>Địa chỉ đầy đủ</td></tr></tbody></table>

#### Bước 4: Xác nhận thông tin <a href="#buoc-4-xac-nhan-thong-tin" id="buoc-4-xac-nhan-thong-tin"></a>

Tích vào ô checkbox bắt buộc:

> ☑️ **"Tôi xác nhận rằng những thông tin trên là đúng sự thật và đã được người nhận đồng ý"** _(bắt buộc)_

Nếu không tích xác nhận này, hệ thống sẽ không cho phép lưu địa chỉ.

#### Bước 5 (Tùy chọn): Đặt làm địa chỉ mặc định ngay <a href="#buoc-5-tuy-chon-dat-lam-dia-chi-mac-dinh-ngay" id="buoc-5-tuy-chon-dat-lam-dia-chi-mac-dinh-ngay"></a>

Nếu muốn địa chỉ vừa thêm trở thành địa chỉ mặc định, tích vào ô:

> ☑️ **"Sử dụng làm địa chỉ mặc định"**

#### Bước 6: Lưu địa chỉ <a href="#buoc-6-luu-dia-chi" id="buoc-6-luu-dia-chi"></a>

* Nhấn nút **"Thêm Địa Chỉ Nhận Hóa Đơn"** (màu xanh, góc dưới phải) để lưu.
* Nhấn **"Đóng"** để hủy bỏ và quay lại danh sách.

### 5. Đặt địa chỉ mặc định <a href="#id-5-dat-dia-chi-mac-dinh" id="id-5-dat-dia-chi-mac-dinh"></a>

Địa chỉ mặc định là địa chỉ được hệ thống tự động điền khi người dùng tiến hành thanh toán.

#### Cách thực hiện <a href="#cach-thuc-hien" id="cach-thuc-hien"></a>

1. Trong danh sách địa chỉ, tìm địa chỉ muốn đặt làm mặc định.
2. Nhấn nút **"Sử dụng làm địa chỉ mặc định"** ở bên phải của địa chỉ đó.
3. Hệ thống cập nhật ngay lập tức — địa chỉ được chọn sẽ hiển thị nhãn **`MẶC ĐỊNH`**.

> ⚠️ **Lưu ý quan trọng:** - Mỗi tài khoản chỉ có **một** địa chỉ mặc định tại một thời điểm. - Địa chỉ đang là mặc định **không hiển thị** nút "Sử dụng làm địa chỉ mặc định". - Địa chỉ đang là mặc định **không thể bị xóa** trực tiếp.

### 6. Xóa địa chỉ nhận hóa đơn <a href="#id-6-xoa-dia-chi-nhan-hoa-don" id="id-6-xoa-dia-chi-nhan-hoa-don"></a>

#### Cách thực hiện <a href="#cach-thuc-hien-1" id="cach-thuc-hien-1"></a>

1. Trong danh sách, tìm địa chỉ muốn xóa.
2. Nhấn nút **"Xóa"** (màu đỏ) bên phải địa chỉ đó.
3. Hộp thoại xác nhận xuất hiện với tiêu đề **"Xác nhận xóa Địa Chỉ Nhận Hóa Đơn"** và nội dung:

> _"Quý Khách muốn xóa Địa Chỉ Nhận Hóa Đơn \[Tên địa chỉ]?"_

1. Chọn một trong hai:
   * Nhấn **"Xóa Địa Chỉ Nhận Hóa Đơn"** (màu xanh) để xác nhận xóa vĩnh viễn.
   * Nhấn **"Đóng"** để hủy bỏ, giữ lại địa chỉ.

> ⚠️ **Lưu ý:** Không thể xóa địa chỉ đang được đặt là **mặc định**. Hãy đặt địa chỉ khác làm mặc định trước, sau đó mới có thể xóa địa chỉ cũ.
