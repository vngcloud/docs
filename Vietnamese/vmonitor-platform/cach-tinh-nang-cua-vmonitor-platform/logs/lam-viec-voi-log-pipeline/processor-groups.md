# Processor Groups

### Tổng quan

Processor Group: cho phép bạn chỉ định nơi lấy dữ liệu log (source log project), nơi lưu trữ dữ liệu đã parse (destination log project) và những log nào sẽ được parse khi thoả mãn filter.&#x20;

***

### Khởi tạo Processor Groups

Processor Group: cho phép bạn chỉ định nơi lấy dữ liệu log (source log project), nơi lưu trữ dữ liệu đã parse (destination log project) và những log nào sẽ được parse khi thoả mãn filter.&#x20;

Để tạo processor group, hãy làm theo hướng dẫn bên dưới:

1\. Đăng nhập vào [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor/).

2\. Chọn thư mục **Log**, sau đó chọn menu **Log pipeline**.

3\. Chọn một **Log pipeline** đã được tạo trước đó.

4\. Chọn **Create a processor group** hoặc **Process Group Library** trong đó:&#x20;

* **Create a processor group**: tạo mới hoàn toàn processor group.
* **Process Group Library**: tạo processor group từ những thư viện có sẵn do VNG Cloud hỗ trợ.

| <ol><li>Nhập tên processor <strong>Group name</strong>. Tên Group name phải tuân thủ theo quy định của chúng tôi.</li><li>Nhập <strong>Description</strong> cho processor group này.</li><li>Chọn <strong>Source</strong> và <strong>Destination log project</strong> mà bạn muốn thực hiện pipeline trong danh sách các log project đang tồn tại trên account của bạn. <strong>Source log project và Destination log project không thể là cùng một log project mà bắt buộc bạn phải chọn chúng là những log project khác biệt. Nếu Destination log project đã có dữ liệu thì việc tạo luồng pipeline cho project này có thể gây mất đồng bộ dữ liệu.</strong></li><li>Nhập điều kiện <strong>Filter</strong> cho log nếu có. Bạn có thể nhập điều kiện lọc cho log bằng một trong 2 cách: <strong>Suggestion mode</strong> hoặc <strong>Editor mode</strong>. Cách sử dụng 2 phương thức này và chuyển đổi qua lại giữa 2 phương thức đã được chúng tôi mô tả ở các tính năng <a href="../lam-viec-voi-log-search/search-logs.md">Search logs</a>.</li><li>Chọn <strong>Create.</strong></li></ol><p><img src="http://docs.vngcloud.vn/download/attachments/49650043/image2023-7-31_14-9-40.png?version=1&#x26;modificationDate=1690787381000&#x26;api=v2" alt=""></p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

***

| <p>Hiện tại VNG Cloud hỗ trợ thư viện cho 2 ứng dụng phổ biến là <strong>Apache, Nginx</strong>. Khi bạn chọn <strong>Process Group Library</strong>, tiếp tục thực hiện các bước dưới đây để hoàn thành tạo processor group</p><ol><li>Chọn <img src="http://docs.vngcloud.vn/download/thumbnails/49650043/image2023-3-27_9-48-38.png?version=1&#x26;modificationDate=1679885318000&#x26;api=v2" alt="">(<strong>Duplicate this group)</strong> để tạo Processor Group từ Library này.</li></ol><p><img src="http://docs.vngcloud.vn/download/attachments/49650043/image2023-8-2_15-6-24.png?version=1&#x26;modificationDate=1690963585000&#x26;api=v2" alt=""></p><ol><li><p>Nhập các thông tin bao gồm: </p><ul><li><strong>Group name</strong>: nhập tên processor group. Tên group phải tuân thủ theo quy định của chúng tôi.</li><li><strong>Description</strong>: nhập mô tả processor group này</li><li>Chọn <strong>Source</strong> và <strong>Destination log project</strong> mà bạn muốn thực hiện pipeline trong danh sách các log project đang tồn tại trên account của bạn. <strong>Source log project và Destination log project không thể là cùng một log project mà bắt buộc bạn phải chọn chúng là những log project khác biệt. Nếu Destination log project đã có dữ liệu thì việc tạo luồng pipeline cho project này có thể gây mất đồng bộ dữ liệu.</strong></li><li>Nhập điều kiện <strong>Filter</strong> cho log nếu có. Bạn có thể nhập điều kiện lọc cho log bằng một trong 2 cách: <strong>Suggestion mode</strong> hoặc <strong>Editor mode</strong>. Cách sử dụng 2 phương thức này và chuyển đổi qua lại giữa 2 phương thức đã được chúng tôi mô tả ở các tính năng <a href="../lam-viec-voi-log-search/search-logs.md">Search logs</a>.</li></ul></li><li>Chọn <strong>Duplicate</strong>.</li></ol><p><img src="http://docs.vngcloud.vn/download/attachments/49650043/image2023-8-2_15-2-28.png?version=1&#x26;modificationDate=1690963350000&#x26;api=v2" alt="" data-size="original"></p><p>Sau khi bạn sao chép thành công:</p><ul><li>Đối với thư viện <strong>Apache</strong>, hệ thống sẽ tự tạo một <strong>3 Processor</strong> loại: <strong>Grok Parser, GeoIP Parse, User-Agent Parser</strong>. Nếu các cấu hình parser này chưa như bạn mong muốn, bạn có thể chỉnh sửa các <strong>Processor</strong> này theo hướng dẫn tại <a href="processor/">Processor</a>.</li><li>Đối với thư viện <strong>Nginx</strong>, hệ thống sẽ tự tạo một <strong>4 Processor</strong> loại: <strong>Grok Parser, Field Remapper Parser, GeoIP Parse, Date Parser</strong>. Nếu các cấu hình parser này chưa như bạn mong muốn, bạn có thể chỉnh sửa các <strong>Processor</strong> này theo hướng dẫn tại <a href="processor/">Processor</a>.</li></ul><p><img src="http://docs.vngcloud.vn/download/attachments/49650043/image2023-8-2_15-8-35.png?version=1&#x26;modificationDate=1690963717000&#x26;api=v2" alt="" data-size="original"></p><p><img src="http://docs.vngcloud.vn/download/attachments/49650043/image2023-8-2_15-9-10.png?version=1&#x26;modificationDate=1690963751000&#x26;api=v2" alt="" data-size="original"></p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

***

### Chỉnh sửa Processor Groups

Để chỉnh sửa Processor group trong Log pipeline, hãy làm theo hướng dẫn bên dưới

1. Đăng nhập vào [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). Nếu bạn chưa có tài khoản, đăng ký miễn phí tại [tại đây](https://register.vngcloud.vn/signup).
2. Chọn thư mục **Log.**
3. Chọn **Log pipeline.**
4. Trong danh sách log pipeline đang có, chọn **Log pipeline** chứa **Processor group** mà bạn muốn chỉnh sửa.
5. Tại **Processor group** mà bạn muốn chỉnh sửa, chọn ![](http://docs.vngcloud.vn/download/thumbnails/49650043/image2023-5-8\_10-2-24.png?version=1\&modificationDate=1690787355000\&api=v2).&#x20;
6. Chọn **Edit group**.
7. Chỉnh sửa các thông số cho **Processor group** mà bạn mong muốn. Bạn có thể chỉnh sửa tất cả các trường thông tin trong cấu hình một processor group. Việc chỉnh sửa này tương tự như khi bạn thực hiện tạo mới một Processor group theo hướng dẫn bên trên.
8. Chọn **Save.**

***

### Xóa Processor Groups

Khi bạn không có nhu cầu sử dụng một Processor group tùy chỉnh nữa, bạn có thể thực hiện xóa Processor group khỏi hệ thống theo hướng dẫn bên dưới:&#x20;

1. Đăng nhập vào [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor). Nếu bạn chưa có tài khoản, đăng ký miễn phí tại [tại đây](https://register.vngcloud.vn/signup).
2. Chọn thư mục **Log.**
3. Chọn **Log pipeline** chứa processor group mà bạn muốn thực hiện xóa.
4. Chọn **Processor group.**
5. Tại **Processor group** mà bạn muốn xóa, chọn ![](http://docs.vngcloud.vn/download/thumbnails/49650043/image2023-4-19\_15-31-39.png?version=1\&modificationDate=1690787655000\&api=v2).
6. Chọn **Delete**.
7. Tại màn hình xác nhận xóa Processor group, chọn **Delete**.

Sau khi bạn thực hiện xóa thành công thì Processor group của bạn sẽ bị xóa hoàn toàn khỏi hệ thống của chúng tôi đồng thời tất cả các processor bên trong một processor group cũng sẽ bị xóa. Bạn không thể khôi phục lại Processor group đã xóa nên hãy lưu ý cẩn thận khi sử dụng tính năng này.&#x20;

\
