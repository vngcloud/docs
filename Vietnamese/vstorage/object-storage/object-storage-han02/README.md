# Object storage (HAN02)

VNGCloud giới thiệu tới bạn **Region HAN02** mới cho dịch vụ vStorage. Những tính năng nổi bật tại region này bao gồm.

* **Hiệu suất cao**: Region HAN02 được thiết kế để đáp ứng nhu cầu xử lý khối lượng truy cập lớn, điều này mang lại hiệu suất vượt trội, giúp tối ưu hóa hoạt động của các ứng dụng và dịch vụ của bạn.
* **Bảo mật nâng cao**: Region HAN02 cung cấp các cơ chế mã hóa như SSE-S3, SSE-C đảm bảo an toàn tuyệt đối cho dữ liệu của khách hàng.
* **Đa dạng gói cước:** Đặc biệt, tại region HAN02, chúng tôi cung cấp đa dạng các gói lưu trữ như Gold, Instant Archive,.. đáp ứng đầy đủ nhu cầu cho việc lưu trữ của bạn.

Bắt đầu với vStorage tại Region HAN02 theo các hướng dẫn sau đây.

***

## **Farm**

Farm là một thuật ngữ dùng riêng cho vStorage, farm được chúng tôi định nghĩa là một hệ thống bao gồm cơ sở hạ tầng, dịch vụ, v.v. được triển khai tại một vị trí cụ thể thuộc 2 region Hà Nội và Hồ Chí Minh với mục đích cung cấp dịch vụ lưu trữ vStorage. Đối với farm HAN02, các thông số của farm như sau:

<table data-full-width="true"><thead><tr><th width="107.80000000000001">Farm</th><th width="211">Farm ID</th><th width="319">vStorage endpoint</th><th>Mục đích sử dụng</th></tr></thead><tbody><tr><td>HAN02</td><td>5d10c8ba-7187-4acc-b8c5-2d67d71c9202</td><td>https://han02.vstorage.vngcloud.vn</td><td>Farm phục vụ đa mục đích với hiệu suất cao và được dùng chung cho dữ liệu lưu trữ tại Region Hà Nội.</td></tr></tbody></table>

***

## Hạn mức tài nguyên

Các bảng sau đây liệt kê các giá trị tối đa cho tài nguyên lưu trữ trên vStorage của bạn.

### Bandwidth

<table data-full-width="true"><thead><tr><th width="113">Farm</th><th width="210">Download BW Domestic</th><th width="238">Download BW International</th><th width="198">Upload BW Domestic</th><th>Upload BW International</th></tr></thead><tbody><tr><td>HAN02</td><td>10Gbps shared</td><td>TBA</td><td>10Gbps shared</td><td>TBA</td></tr></tbody></table>

### Request per limit

* Per IP

<table data-full-width="true"><thead><tr><th width="167">Storage Class</th><th width="187.091064453125">Request all types</th><th width="174.45458984375">Put request</th><th width="188.364013671875">Get request</th><th>Delete request</th></tr></thead><tbody><tr><td>Gold</td><td>5000  request/s/IP</td><td>2000  request/s/IP</td><td>3000  request/s/IP</td><td>1000  request/s/IP</td></tr><tr><td>Instant Archive</td><td>2500  request/s/IP</td><td>1000  request/s/IP</td><td>1500  request/s/IP</td><td>500  request/s/IP</td></tr><tr><td>Archive</td><td>1000 request/s/IP</td><td>500 request/s/IP</td><td>500  request/s/IP</td><td>100  request/s/IP</td></tr></tbody></table>

* Per path

<table data-full-width="true"><thead><tr><th width="164.1817626953125">Storage Class</th><th width="203.13629150390625">Request all types</th><th width="194.9090576171875">Put request</th><th width="194.0906982421875">Get request</th><th>Delete request</th></tr></thead><tbody><tr><td>Gold</td><td>5000 request/s/path</td><td>2000 request/s/path</td><td>3000 request/s/path</td><td>1000 request/s/path</td></tr><tr><td>Instant Archive</td><td>2500 request/s/path</td><td>1000 request/s/path</td><td>1500 request/s/path</td><td>500 request/s/path</td></tr><tr><td>Archive</td><td>1000 request/s/path</td><td>500 request/s/path</td><td>500 request/s/path</td><td>100 request/s/path</td></tr></tbody></table>

### Các hạn mức khác

<table data-full-width="true"><thead><tr><th>Item</th><th>Limit</th></tr></thead><tbody><tr><td>Số lượng object tối đa được lưu trữ trên một bucket</td><td>600 triệu objects</td></tr><tr><td>Số lượng container/ bucket tối đa có thể tạo trên một project</td><td>Không giới hạn</td></tr></tbody></table>

***

## **Gói lưu trữ**

Bên dưới là bảng mô tả các thông số của mỗi storage class mà chúng tôi đang hỗ trợ:

<table data-full-width="true"><thead><tr><th>Item</th><th>Gold Class</th><th>Instant Archive</th><th>Archive</th></tr></thead><tbody><tr><td><strong>Designed for</strong></td><td>For frequently accessed data that requires low latency and high throughput with retrieval in <strong>milliseconds (10m object/ 1H)</strong>.</td><td>For long-term storing data with retrieval in <strong>miliseconds (5m object/ 1H)</strong>.</td><td>For long-term data archiving that is accessed once or twice in a year with retrieval within <strong>hour (5m object/ 12H and 10m object/ 24H).</strong></td></tr><tr><td><strong>Durability</strong></td><td>99.999999999%</td><td>99.999999999%</td><td>99.999999999%</td></tr><tr><td><strong>Availability</strong></td><td>99.99%</td><td>99.99%</td><td>99.99%</td></tr><tr><td><strong>Min storage quota</strong></td><td>No</td><td>No</td><td>5 TB</td></tr><tr><td><strong>Min storage duration</strong></td><td>No</td><td>No</td><td>90 days</td></tr><tr><td><strong>Min billable object size</strong></td><td>0</td><td>0</td><td>128 KB</td></tr><tr><td><strong>Free traffic</strong></td><td>Quota x 10</td><td>Quota x 2</td><td>Quota x1</td></tr><tr><td><strong>Free request</strong></td><td>Free request on Gold Class performance</td><td>Free request on Instant Archive Class performance</td><td>Free request on Archive Class performance</td></tr></tbody></table>
