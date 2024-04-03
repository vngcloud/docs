# Web Accelerator

#### **Tổng quan** <a href="#webaccelerator-tongquan" id="webaccelerator-tongquan"></a>

Web Accelerator là giải pháp giúp tăng tốc độ hiển thị nội dung và trải nghiệm người dùng.

#### **Cơ Chế Phân Phối Dữ Liệu** <a href="#webaccelerator-cochephanphoidulieu" id="webaccelerator-cochephanphoidulieu"></a>

Dịch vụ Web Accelerator cache tất cả các đối tượng đi qua nó không chỉ bao gồm các nội dung tĩnh như Image, javascript, css mà còn có cả HTML code và API. Bên cạnh đó còn thực hiện các cơ chế tự động tối ưu hóa source code và hình ảnh.

***

#### **Tính Năng Dịch Vụ** <a href="#webaccelerator-tinhnangdichvu" id="webaccelerator-tinhnangdichvu"></a>

* Hỗ trợ [CNAME](https://docs.vngcloud.vn/display/ONVINA/CNAME).
* Hỗ trở tùy chỉnh [Origin](https://docs.vngcloud.vn/display/ONVINA/Origin).
* Hỗ trợ [tối ưu hóa kích thước file thiết bị đầu cuối](https://docs.vngcloud.vn/pages/viewpage.action?pageId=36045484).
* Hỗ trợ chế độ bảo mật [HSTS](https://docs.vngcloud.vn/pages/viewpage.action?pageId=36045496).
* Hỗ trợ tùy chỉnh các [tính năng cache](https://docs.vngcloud.vn/pages/viewpage.action?pageId=36045500).
* Hỗ trợ [tự động redirect từ HTTP sang HTTPS](https://docs.vngcloud.vn/pages/viewpage.action?pageId=36045505).
* Hỗ trợ [đổi các link HTTP sang HTTPS trong source code](https://docs.vngcloud.vn/pages/viewpage.action?pageId=36045508).
* Hỗ trợ [chỉnh sửa CDN đã tạo](https://docs.vngcloud.vn/pages/viewpage.action?pageId=36045511).

***

#### **Cách Tạo Web accelerator CDN** <a href="#webaccelerator-cachtaowebacceleratorcdn" id="webaccelerator-cachtaowebacceleratorcdn"></a>

* Bước 1: Chọn menu Web accelerator bạn sẽ vô trang thống kê và chỉnh sửa cho Web Accelerator, Chọn button Create để tạo CDN.

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045717/image2023-8-15_11-31-56.png?version=1&#x26;modificationDate=1692073917000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Bước 2: Nhập và tùy chọn tính năng dịch vụ Web Accelerator

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045717/image2023-8-15_11-32-23.png?version=1&#x26;modificationDate=1692073944000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Bước 3: Nhập Domain Name cho CDN khi người dùng nhập domain có sẵn của mình hệ thống sẽ tự tìm và thêm server ở tùy chọn origin. Ví dụ: người dùng có domain “[vnexpress.net](http://vnexpress.net/)” thì khi nhập xong chọn ra một field khác sẽ tự dộng thêm server có IP là “111.65.250.2”.
* Bước 4: Nhập và tùy chỉnh các tính năng dịch vụ.
* Bước 5: Tùy theo người dùng yêu cầu nhập thông [tin chính sách rule cơ bản](https://docs.vngcloud.vn/pages/viewpage.action?pageId=36045518) hoặc [chính sách rule nâng cao](https://docs.vngcloud.vn/pages/viewpage.action?pageId=36045523) cho CDN.
* Bước 6: Khi điền các thông tin đúng và đủ thì nhấn button Submit ở cuối cùng giao diện đợi khoản 5 phút cho hệ thống cái đặt CDN cho người dùng.
* Bước 7: Người dùng có thể truy cập CDN qua vCDN Domain khi đã tạo CDN xong.
