# Farm là gì?

Farm là một thuật ngữ dùng riêng cho vStorage, farm được chúng tôi định nghĩa là một hệ thống bao gồm cơ sở hạ tầng, dịch vụ, v.v. được triển khai tại một vị trí cụ thể thuộc 2 region Hà Nội và Hồ Chí Minh với mục đích cung cấp dịch vụ lưu trữ vStorage. Tương tự như region, bạn có thể chọn một farm làm nơi lưu trữ dữ liệu của bạn, việc chọn farm hợp lý sẽ giảm tải cho hệ thống cũng như tối ưu chi phí hoạt động lưu trữ cho doanh nghiệp của bạn.&#x20;

***

#### Danh sách các farm vStorage cung cấp <a href="#farmlagi-danhsachcacfarmvstoragecungcap" id="farmlagi-danhsachcacfarmvstoragecungcap"></a>

* Hiện tại, chúng tôi cung cấp cho bạn 2 farm được mô tả ở bảng bên dưới:

<table data-header-hidden data-full-width="true"><thead><tr><th width="96"></th><th width="171"></th><th width="141"></th><th width="159"></th><th></th></tr></thead><tbody><tr><td><strong>Farm</strong></td><td><strong>Farm ID</strong></td><td><strong>Authentication endpoint</strong></td><td><strong>vStorage endpoint</strong></td><td><strong>Mục đích sử dụng</strong></td></tr><tr><td>HAN01</td><td>5d10c8ba-7187-4acc-b8c5-2d67d71c9233</td><td>https://han.auth.vstorage.vngcloud.vn/v3</td><td>https://han01.vstorage.vngcloud.vn</td><td>Farm phục vụ đa mục đích và được dùng chung cho dữ liệu khởi tạo project tại Region Hà Nội.</td></tr><tr><td>HCM03</td><td>8b1e9c9b-7123-54a5-ua8f-2d67d71c9212</td><td>https://hcm03.auth.vstorage.vngcloud.vn/v3</td><td>https://hcm03.vstorage.vngcloud.vn</td><td>Farm phục vụ đa mục đích và được dùng chung cho dữ liệu khởi tạo project tại Region Hồ Chí Minh.</td></tr></tbody></table>

* Nếu khách hàng muốn triển khai mã hóa nội dung các tệp tin (object) được lưu trữ trên dịch vụ vStorage của VNGCloud, bạn có thể sử dụng endpoint encrypt để thực hiện tải lên tệp tin. Trong cơ chế này dữ liệu được tự động mã hóa khi tải lên tệp tin thông qua domain enryption. Cụ thể:

<table data-header-hidden data-full-width="true"><thead><tr><th width="96"></th><th width="171"></th><th width="141"></th><th width="159"></th><th></th></tr></thead><tbody><tr><td><strong>Farm</strong></td><td><strong>Farm ID</strong></td><td><strong>Authentication endpoint</strong></td><td><strong>vStorage endpoint</strong></td><td><strong>Mục đích sử dụng</strong></td></tr><tr><td>HCM03</td><td>8b1e9c9b-7123-54a5-ua8f-2d67d71c9212</td><td>https://hcm03.auth.vstorage.vngcloud.vn/v3</td><td><a href="https://hcm03-encrypt-vstorage.vngcloud.vn">https://hcm03-encrypt-vstorage.vngcloud.vn</a></td><td>Khi sử dụng encryption endpoint này, dữ liệu của bạn sẽ được tự động mã hóa khi tải tệp tin lên vStorage theo đúng chuẩn mã hóa AES-256.</td></tr></tbody></table>

{% hint style="info" %}
**Chú ý:**

* Khi bạn đã thực hiện tải tệp tin lên vStorage thông quan encryption domain. Lúc này, nếu bạn thực hiện tải xuống tệp tin này, bạn có thể sử dụng bất kỳ vStorage endpoint nào thuộc farm HCM03 và tệp tin khi tải xuống đã được giải mã.&#x20;
* Việc tải lên tệp tin thông qua encryption domain có thể sẽ bị ảnh hưởng hiệu năng (performance), có thể là tốc độ upload sẽ giảm từ 5% -10%.
{% endhint %}

Đối với mỗi farm, ngoài các tính năng vStorage chung, sẽ có một số tính năng riêng biệt đặc trưng cho farm đó. Chi tiết sẽ được chúng tôi cập nhật sớm nhất tại đây.  Bạn cũng có thể yêu cầu chúng tôi cung cấp một farm đặc biệt nếu dữ liệu bạn cần lưu trữ đủ lớn và là dữ liệu đặc thù. Để liên hệ với chúng tôi, bạn có thể yêu cầu hỗ trợ hay liên hệ trực tiếp tới nhân viên VNG Clou đang hỗ trợ của bạn.
