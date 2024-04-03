# Chính Sách Rule Cơ Bản (PageRule)

Cho phép khách hàng tùy chọn tạo ra các chính sách Rules thông qua giao diện Portal. Một Rules sẽ được thực thi khi mà có URI request đúng với điều kiện đã được định nghĩa trong Rule.

&#x20;   &#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045518/image2021-11-17_14-18-15.png?version=1&#x26;modificationDate=1637133496000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Chức năng “Pagerules” sẽ giúp khách hàng tối ưu các điều kiện và các tùy chọn để giúp website thể hiện được nhiều mục đích khác nhau.

Để tạo “Pagerules”, click “Create Page Rule”, popup sẽ hiện ra như sau:

&#x20;   &#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/36045518/image2021-11-17_14-18-55.png?version=1&#x26;modificationDate=1637133536000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Tại mục số (1), nhập “URL pattern” cần áp dụng pagerule, hỗ trợ kiểu khai báo “\*” đại diện cho một chuỗi nhiều ký tự. Ví dụ: /trang\_landing\_cu.html.

Các hành động khi thỏa điều kiện**:** Mỗi Rules khi thỏa điệu kiện đúng URI được request sẽ có thể tùy chọn thực thi một trong khác hành động sau:

* Always Use HTTPS&#x20;
* Auto Minify&#x20;
* Automatic HTTPS Rewrites&#x20;
* Server Cache TTL&#x20;
* Browser Cache TTL&#x20;
* Bypass Cache by Cookie&#x20;
* Bypass Cache By Device Type
* Forwarding URL&#x20;
* Add Response Header&#x20;
* Brotli&#x20;
* Gzip
* Origin Override

Mỗi “Rule” sẽ có các hành động “action” khác nhau được thể hiện ở bảng dưới đây.

“Order” nhằm sắp xếp vị trí các rule, số càng nhỏ, ưu tiên thực hiện càng lớn.

<figure><img src="https://docs.vngcloud.vn/download/thumbnails/36045518/image2021-11-17_14-21-31.png?version=1&#x26;modificationDate=1637133692000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Sau khi tạo xong, click “Save changes” để cập nhật thay đổi.

***

Bảng mô tả các loại hành động:

<table data-header-hidden><thead><tr><th width="79"></th><th width="160"></th><th width="197"></th><th></th></tr></thead><tbody><tr><td>STT</td><td>Rule</td><td>Action</td><td>Mô tả</td></tr><tr><td>1</td><td>Always Use HTTPS</td><td>ON/OFF</td><td>Bật/Tắt tùy chọn “Luôn sử dụng giao thức HTTPS” trên trang chỉ định.</td></tr><tr><td>2</td><td>Auto Minify</td><td>Javascript / CSS / HTML</td><td>Tùy chọn ghi đè chức năng minify trên trang chỉ định.</td></tr><tr><td>3</td><td>Automatic HTTPS Rewrites</td><td>ON/OFF</td><td>Bật tắt tính năng tự động replace các URL HTTP thành HTTPS trong trang chỉ định.</td></tr><tr><td>4</td><td>Server Cache TTL</td><td><br></td><td>Tùy chọn lại thời gian lưu cache trên các Edge Servers hoặc “Bypass Cache” trên trang chỉ định.</td></tr><tr><td>5</td><td>Browser Cache TTL</td><td><br></td><td>Tương tự “Server Cache TTL”, nhưng là quy định thời gian cache trên trình duyệt End-user.</td></tr><tr><td>6</td><td>Bypass Cache By Cookie</td><td>Nhập giá trị “cookie_name” và “cookie_value”</td><td><p>Nếu có cookie được chỉ định từ end-user gửi lên, hệ thống sẽ thực hiện lệnh bypass cache trên trang chỉ định.</p><p>Nếu giá trị “cookie_value” là rỗng, hệ thống chỉ xét nếu tồn tại “cookie_name” và không quan tâm giá trị của “cookie_value”</p></td></tr><tr><td>7</td><td>Bypass Cache By Device Type</td><td>Nhập các giá trị “Agent Text”, hỗ trợ nhiều giá trị, phân cách bởi dấu “Tab” hoặc “Enter”</td><td>Nếu trình duyệt end-user sử dụng có thông tin giống một trong các Agent Text, hệ thống sẽ tự bypass cache trên trang chỉ định.</td></tr><tr><td>8</td><td>Forwarding URL</td><td>Mã chuyển hướng (301/302) và URL đích.</td><td>Tự chuyển hướng URL được chỉ định về URL đích mới.</td></tr><tr><td>9</td><td>Host Header Override</td><td>Header_name và header_value</td><td>Tự động add thêm header trả về cho trình duyệt end-user trên trang được chỉ định.</td></tr><tr><td>10</td><td>Brotli</td><td>ON/OFF</td><td>Tùy chọn bật/tắt Brotli trên trang được chỉ định.</td></tr><tr><td>11</td><td>Gzip</td><td>ON/OFF</td><td>Tùy chọn bật/tắt Gzip trên trang được chỉ định.</td></tr><tr><td>12</td><td>Resolve Origin Override</td><td>IP New Origin</td><td>Tùy chọn thay đổi IP Server Origin ở trang chỉ định.*</td></tr></tbody></table>
