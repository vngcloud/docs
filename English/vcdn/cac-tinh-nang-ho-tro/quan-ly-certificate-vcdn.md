# Manage Certificate vCDN

Hỗ trợ khách hàng upload SSL Cert và SSL Key bao gồm key ChainCA

<figure><img src="../../.gitbook/assets/image (203).png" alt=""><figcaption></figcaption></figure>

Sau khi đăng nhập, click vào mục “Certificate” như hình bên.

<figure><img src="../../.gitbook/assets/image (204).png" alt=""><figcaption></figcaption></figure>

Giao diện quản lý Certificate hiện ra với danh sách các certificate gồm các cột:

* Domain,
* Issuer (Tên nhà cấp phát chứng chỉ),
* Valid From (Thời gian hiệu lực của chứng chỉ),
* Expires On (Thời hạn của chứng chỉ),
* CDN Using (Số lượng CDN đang dùng chứng chỉ này, click vào để xem chi tiết),
* Status: Trạng thái của chứng chỉ đang được kích hoạt hay hủy kích hoạt
* Các nút Action gồm Edit (Cập nhật chứng chỉ) và Delete (Xóa chứng chỉ)
* Đầu trang, thông tin tóm tắt về số lượng chứng chỉ (Total), số certificate đang được kích hoạt để sẳn sàng sử dụng (Active) và số chứng chỉ đã tạm hủy kích hoạt (Inactive).
* Để thêm mới/upload certificate, click vào nút “Upload” , giao diện upload ceritificate sẽ như sau:

<figure><img src="../../.gitbook/assets/image (205).png" alt=""><figcaption></figcaption></figure>

(1): Click vào Upload Private Key để tải lên private key của Certificate, hoặc cũng có thể paste private key vào khung textbox bên dưới.

(2): Upload Certificate để tải lên file CRT/PEM của Certificate.

(3): Upload CA Root Chain để tải lên thông tin certificate của nhà cung cấp chứng chỉ. Có thể để trống nếu không có thông tin.\*

_\* Một số trình duyệt phiên bản cũ có thể báo lỗi Certificate không hợp lệ nếu thiếu thông tin CA Root Chain._

Sau khi nhập/upload đầy đủ thông tin, click “Save and Deploy”(5) để lưu và kích hoạt certificate, sẳn sàng cho các CDN sử dụng.

Nếu chứng chỉ chưa sẳn sàng để dùng ngay, click “Save as Draf”(4) để lưu trữ.

{% hint style="info" %}
**Chú ý:**

* vCDN do VNG Cloud cung cấp là dịch vụ phân phối nội dung thông qua giao thức HTTP có hỗ trợ TLS/SSL (HTTPS). Do vậy, các TLS Certificate - được tải lên bởi khách hàng nhằm mục đích mã hóa kênh truyền HTTP giữa người dùng và hệ thống máy chủ CDN - đồng thời được lưu trữ và quản lý bởi khách hàng và VNG Cloud cho đến khi khách hàng thực hiện lệnh xóa thông qua giao diện Web Portal/API.
* VNG Cloud cam kết không chia sẻ các TLS Certificate này cho bên thứ ba bất kỳ.
{% endhint %}
