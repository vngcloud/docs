# PageRule

Allows customers to optionally create Rules policies through the Portal interface. A Rule will be executed when a request URI matches the conditions defined in the Rule.

<figure><img src="../../.gitbook/assets/image (198).png" alt=""><figcaption></figcaption></figure>

The "Pagerules" function will help customers optimize conditions and options to help the website express many different purposes.&#x20;

To create “Pagerules”, click “Create Page Rule”, a popup will appear as follows:

<figure><img src="../../.gitbook/assets/image (199).png" alt=""><figcaption></figcaption></figure>

In item number (1), enter "URL pattern" to which the pagerule needs to be applied, supporting the "\*" declaration type that represents a string of multiple characters. For example: /page\_landing\_cu.html.&#x20;

Actions when conditions are met\*\*:\*\* Each Rule that meets the correct condition of the requested URI will have the option to execute one of the following actions:

* Always Use HTTPS
* Auto Minify
* Automatic HTTPS Rewrites
* Server Cache TTL
* Browser Cache TTL
* Bypass Cache by Cookie
* Bypass Cache By Device Type
* Forwarding URL
* Add Response Header
* Brotli
* Gzip
* Origin Override

Mỗi “Rule” sẽ có các hành động “action” khác nhau được thể hiện ở bảng dưới đây.

<figure><img src="../../.gitbook/assets/image (200).png" alt=""><figcaption></figcaption></figure>

“Order” nhằm sắp xếp vị trí các rule, số càng nhỏ, ưu tiên thực hiện càng lớn.

Sau khi tạo xong, click “Save changes” để cập nhật thay đổi.

***

Bảng mô tả các loại hành động:

<table data-header-hidden><thead><tr><th width="79"></th><th width="115"></th><th width="155"></th><th></th></tr></thead><tbody><tr><td><strong>STT</strong></td><td><strong>Rule</strong></td><td><strong>Action</strong></td><td><strong>Mô tả</strong></td></tr><tr><td>1</td><td>Always Use HTTPS</td><td>ON/OFF</td><td>Bật/Tắt tùy chọn “Luôn sử dụng giao thức HTTPS” trên trang chỉ định.</td></tr><tr><td>2</td><td>Auto Minify</td><td>Javascript / CSS / HTML</td><td>Tùy chọn ghi đè chức năng minify trên trang chỉ định.</td></tr><tr><td>3</td><td>Automatic HTTPS Rewrites</td><td>ON/OFF</td><td>Bật tắt tính năng tự động replace các URL HTTP thành HTTPS trong trang chỉ định.</td></tr><tr><td>4</td><td>Server Cache TTL</td><td><br></td><td>Tùy chọn lại thời gian lưu cache trên các Edge Servers hoặc “Bypass Cache” trên trang chỉ định.</td></tr><tr><td>5</td><td>Browser Cache TTL</td><td><br></td><td>Tương tự “Server Cache TTL”, nhưng là quy định thời gian cache trên trình duyệt End-user.</td></tr><tr><td>6</td><td>Bypass Cache By Cookie</td><td>Nhập giá trị “cookie_name” và “cookie_value”</td><td><p>Nếu có cookie được chỉ định từ end-user gửi lên, hệ thống sẽ thực hiện lệnh bypass cache trên trang chỉ định.</p><p>Nếu giá trị “cookie_value” là rỗng, hệ thống chỉ xét nếu tồn tại “cookie_name” và không quan tâm giá trị của “cookie_value”</p></td></tr><tr><td>7</td><td>Bypass Cache By Device Type</td><td>Nhập các giá trị “Agent Text”, hỗ trợ nhiều giá trị, phân cách bởi dấu “Tab” hoặc “Enter”</td><td>Nếu trình duyệt end-user sử dụng có thông tin giống một trong các Agent Text, hệ thống sẽ tự bypass cache trên trang chỉ định.</td></tr><tr><td>8</td><td>Forwarding URL</td><td>Mã chuyển hướng (301/302) và URL đích.</td><td>Tự chuyển hướng URL được chỉ định về URL đích mới.</td></tr><tr><td>9</td><td>Host Header Override</td><td>Header_name và header_value</td><td>Tự động add thêm header trả về cho trình duyệt end-user trên trang được chỉ định.</td></tr><tr><td>10</td><td>Brotli</td><td>ON/OFF</td><td>Tùy chọn bật/tắt Brotli trên trang được chỉ định.</td></tr><tr><td>11</td><td>Gzip</td><td>ON/OFF</td><td>Tùy chọn bật/tắt Gzip trên trang được chỉ định.</td></tr><tr><td>12</td><td>Resolve Origin Override</td><td>IP New Origin</td><td>Tùy chọn thay đổi IP Server Origin ở trang chỉ định.*</td></tr></tbody></table>
