# Origin

Hiện tại, vCDN đang hỗ trợ Multi Origin với các Thuật toán kết nối: **Round Robin, Least Connection, IP Hash và tự động chạy fail-over.**

Khi bạn tạo 1 Web Accelerator CDN, màn hình khởi tạo CDN sẽ bao gồm các thông tin sau:

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045477/image2021-11-17_13-56-23.png?version=1&#x26;modificationDate=1637132184000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Trong đó:

(1): Domain name: nhập Tên domain

(2): CNAMEs: nhập danh sách CNAMEs mong muốn.

(3): Lựa chọn phương thức Origin Load Balancing:

* Round Robin: Hệ thống sẽ tự động điều phối traffic xuống Server Origin của khách hàng với phương thức xoay vòng – đều nhau giữa các servers.
* Least Connected: Hệ thống sẽ chọn Server Origin có lượng connected thấp nhất để điều phối traffic xuống.
* IP Hashing: Hệ thống sẽ dựa vào IP Client để điều phối và duy trì kết nối xuống Server Origin.

(4): Thông tin các mã lỗi Origin Server sẽ phản hồi, dựa vào các mã lỗi này hệ thống sẽ nhận biết và điều phối khách hàng qua các Server Origin khác trong pool.

(5): Nhập địa chỉ IPv4 Server Origin.

(6): Độ ưu tiên (weight) của Server Origin, nhập “0” để thiết lập Server Origin này ở chế độ Backup/Standy, số càng cao độ ưu tiên càng cao.

Sau khi nhập xong thông tin Server Origin và click “Add Server”\*, khung số (8) sẽ hiện ra danh sách các địa chỉ IP Server Origin và thông tin như hình sau:

_\* Khi khách hàng nhập thông tin domain chính, hệ thống sẽ tự động thêm các Server Origin dựa theo các bản ghi DNS có sẳn của tên miền vào khung số (8)._

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045477/image2021-11-17_13-58-35.png?version=1&#x26;modificationDate=1637132316000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Priority – thể hiện mức độ ưu tiên (weight) của Server Origin, số càng cao, độ ưu tiên càng cao.
* Value: Địa chỉ IPv4 của Origin Servers.
* Algorithms: Thuật toán phân tải traffic cho Origin Servers.
* Status: Thể hiện trạng thái ![](https://docs.vngcloud.vn/download/thumbnails/36045477/image2021-11-17\_13-59-15.png?version=1\&modificationDate=1637132356000\&api=v2) (Active) và ![](https://docs.vngcloud.vn/download/thumbnails/36045477/image2021-11-17\_13-59-24.png?version=1\&modificationDate=1637132365000\&api=v2) (Disabled)
  * Active: Origin Server sẽ được đưa vào Pool Origin Servers.
  * Disabled: Origin Server sẽ bị loại bỏ khỏi Pool Origin Servers.
* Hỗ trợ cấu hình các loại mã lỗi để hệ thống tự động thực hiện Fail-Over .
* Origin**:** cho phép khách hàng tự chỉ định các loại mã lỗi khi chạy theo mode Fail-Over.
