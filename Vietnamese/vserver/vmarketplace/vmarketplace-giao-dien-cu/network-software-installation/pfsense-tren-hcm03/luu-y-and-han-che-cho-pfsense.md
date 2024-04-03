# Lưu ý & hạn chế cho Pfsense

## Default MTU: <a href="#luuy-and-hanchechopfsense-defaultmtu" id="luuy-and-hanchechopfsense-defaultmtu"></a>

Default MTU của Pfsense là **1500**. Bạn cần chỉnh thông số này cho phù hợp cấu hình của VNG Cloud là **1450**.

Để update thông số này, bạn truy cập vào WebGUI. Bạn tham khảo link sau để bật WebGUI: [Khởi tạo Pfsense trên HCM03](khoi-tao-pfsense-tren-hcm03.md).

Tại WebGui:

* **Bước 1:** Truy cập vào giao diện quản lý của pfsense, chọn tab interfaces và cấu hình lần lượt cho mạng WAN (hoặc LAN đang sử dụng).



<figure><img src="https://docs.vngcloud.vn/download/attachments/59807039/image2023-7-28_15-29-10.png?version=1&#x26;modificationDate=1690532951000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* **Bước 2:** Tại mục MTU, bạn điền thông số 1450.



Cuối cùng, nhấn _**Save**_ để lưu lại cấu hình.

Bạn thực hiện lần lượt cho các Interfaces đang sử dụng.

Nếu có khó khăn trong quá trình sử dụng, vui lòng liên hệ VNGCloud Support.
