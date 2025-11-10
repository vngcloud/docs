# Object storage (HCM04)

VNGCloud giới thiệu tới bạn **Region HCM04** mới cho dịch vụ vStorage. Những tính năng nổi bật tại region này bao gồm:

* **Hiệu suất cao**: Region HCM04 được thiết kế để đáp ứng nhu cầu xử lý khối lượng truy cập lớn, điều này mang lại hiệu suất vượt trội, giúp tối ưu hóa hoạt động của các ứng dụng và dịch vụ của bạn.
* **Bảo mật nâng cao**: Region HCM04 cung cấp các cơ chế mã hóa như SSE-S3, SSE-C đảm bảo an toàn tuyệt đối cho dữ liệu của khách hàng.
* **Gói cước mới - Instant Archive:** Đặc biệt, tại region HCM04, chúng tôi giới thiệu gói cước mới Instant Archive với chi phí thấp hơn, giúp khách hàng tiết kiệm chi phí lưu trữ dữ liệu dài hạn mà không phát sinh chi phí ẩn và vẫn đáp ứng đầy đủ tiêu chí cho việc lưu trữ backup.

Bắt đầu với vStorage tại Region HCM04 theo hướng dẫn tại [đây](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vstorage/object-storage/object-storage-hcm04/bat-dau-voi-object-storage).

***

## **Farm**

Farm là một thuật ngữ dùng riêng cho vStorage, farm được chúng tôi định nghĩa là một hệ thống bao gồm cơ sở hạ tầng, dịch vụ, v.v. được triển khai tại một vị trí cụ thể thuộc 2 region Hà Nội và Hồ Chí Minh với mục đích cung cấp dịch vụ lưu trữ vStorage. Đối với farm HCM04, các thông số như sau:

<table data-full-width="true"><thead><tr><th width="107.80000000000001">Farm</th><th width="211">Farm ID</th><th width="319">vStorage endpoint</th><th>Mục đích sử dụng</th></tr></thead><tbody><tr><td>HCM04</td><td>8b1e9c9b-7123-54a5-ua8f-2d67d71c9204</td><td>https://hcm04.vstorage.vngcloud.vn</td><td>Farm phục vụ đa mục đích với hiệu suất cao và được dùng chung cho dữ liệu lưu trữ tại Region Hồ Chí Minh.</td></tr></tbody></table>

***

## Hạn mức tài nguyên

Các bảng sau đây liệt kê các giá trị tối đa cho tài nguyên lưu trữ trên vStorage của bạn.

### Bandwidth

<table data-full-width="true"><thead><tr><th width="113">Farm</th><th width="210">Download BW Domestic</th><th width="238">Download BW International</th><th width="198">Upload BW Domestic</th><th>Upload BW International</th></tr></thead><tbody><tr><td>HCM04</td><td>10Gbps shared</td><td>TBA</td><td>10Gbps shared</td><td>TBA</td></tr></tbody></table>

### Request per limit

* Per IP

<table data-full-width="true"><thead><tr><th width="167">Storage Class</th><th width="198.45458984375">Request all types</th><th width="229">Put request</th><th>Get request</th><th>Delete request</th></tr></thead><tbody><tr><td>Instant Archive</td><td>2500 request/s/IP</td><td>1000 request/s/IP</td><td>1500 request/s/IP</td><td>500 request/s/IP</td></tr></tbody></table>

* Per path

<table data-full-width="true"><thead><tr><th width="171">Storage Class</th><th width="199.727294921875">Request all types</th><th width="229">Put request</th><th>Get request</th><th>Delete request</th></tr></thead><tbody><tr><td>Instant Archive</td><td>2500 request/s/path</td><td>1000 request/s/path</td><td>1500 request/s/path</td><td>500 request/s/path</td></tr></tbody></table>

### Các hạn mức khác

<table data-full-width="true"><thead><tr><th>Item</th><th>Limit</th></tr></thead><tbody><tr><td>Số lượng object tối đa được lưu trữ trên một bucket</td><td>600 triệu objects</td></tr><tr><td>Số lượng container/ bucket tối đa có thể tạo trên một project</td><td>Không giới hạn</td></tr></tbody></table>

***

## **Gói lưu trữ**

Bên dưới là bảng mô tả các thông số của mỗi storage class mà chúng tôi đang hỗ trợ:

<table data-full-width="true"><thead><tr><th>Item</th><th>Gold Class</th><th>Instant Archive</th><th data-hidden>Archive</th></tr></thead><tbody><tr><td><strong>Designed for</strong></td><td>For frequently accessed data that requires low latency and high throughput with retrieval in <strong>milliseconds (10m object/ 1H)</strong>.</td><td>For long-term storing data with retrieval in <strong>miliseconds (5m object/ 1H)</strong>.</td><td>For long-term data archiving that is accessed once or twice in a year with retrieval within <strong>hour (5m object/ 12H and 10m object/ 24H).</strong></td></tr><tr><td><strong>Durability</strong></td><td>99.999999999%</td><td>99.999999999%</td><td>99.999999999%</td></tr><tr><td><strong>Availability</strong></td><td>99.99%</td><td>99.99%</td><td>99.99%</td></tr><tr><td><strong>Min storage quota</strong></td><td>No</td><td>No</td><td>5 TB</td></tr><tr><td><strong>Min storage duration</strong></td><td>No</td><td>No</td><td>90 days</td></tr><tr><td><strong>Min billable object size</strong></td><td>0</td><td>0</td><td>128 KB</td></tr><tr><td><strong>Free traffic</strong></td><td>Quota x 10</td><td>Quota x 2</td><td>Quota x1</td></tr><tr><td><strong>Free request</strong></td><td>Free request on Gold Class performance</td><td>Free request on Instant Archive Class performance</td><td>Free request on Archive Class performance</td></tr></tbody></table>
