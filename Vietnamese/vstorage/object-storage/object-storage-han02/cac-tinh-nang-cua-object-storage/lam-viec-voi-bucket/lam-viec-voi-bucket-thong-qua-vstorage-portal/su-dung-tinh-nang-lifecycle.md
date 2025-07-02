# Sử dụng tính năng Lifecycle

## **Tổng quan**

**Lifecycle** trên vStorage là tính năng giúp bạn quản lý vòng đời của các object trong bucket, từ đó giúp tối ưu chi phí lưu trữ. Với Lifecycle, bạn có thể định cấu hình các quy tắc (rules) theo 2 loại:

* **Transition rule:** Rule hỗ trợ di chuyển object giữa các storage class. Bạn có thể thực hiện thiết lập một hoặc nhiều lifecycle rule di chuyển object nếu trong vòng N ngày mà object không được thay đổi.
* **Expiration rule**: Rule hỗ trợ xóa các object theo điều kiện ràng buộc. Bạn có thể thực hiện thiết lập một hoặc nhiều lifecycle rule xóa object sau một khoảng thời gian nhất định kể từ ngày object tồn tại trên hệ thống vStorage.&#x20;

<figure><img src="../../../../../../.gitbook/assets/image (1091).png" alt=""><figcaption></figcaption></figure>

Tham khảo thêm bảng bên dưới để hiểu cách hoạt động của mỗi storage class:

<table data-full-width="true"><thead><tr><th>Item</th><th>Gold Class</th><th>Instant Archive</th><th>Archive</th></tr></thead><tbody><tr><td><strong>Designed for</strong></td><td>For frequently accessed data that requires low latency and high throughput with retrieval in <strong>milliseconds (10m object/ 1H)</strong>.</td><td>For long-term storing data with retrieval in <strong>miliseconds (5m object/ 1H)</strong>.</td><td>For long-term data archiving that is accessed once or twice in a year with retrieval within <strong>hour (5m object/ 12H and 10m object/ 24H).</strong></td></tr><tr><td><strong>Durability</strong></td><td>99.999999999%</td><td>99.999999999%</td><td>99.999999999%</td></tr><tr><td><strong>Availability</strong></td><td>99.99%</td><td>99.99%</td><td>99.99%</td></tr><tr><td><strong>Min storage quota</strong></td><td>No</td><td>No</td><td>5 TB</td></tr><tr><td><strong>Min storage duration</strong></td><td>No</td><td>No</td><td>90 days</td></tr><tr><td><strong>Min billable object size</strong></td><td>0</td><td>0</td><td>128 KB</td></tr><tr><td><strong>Free traffic</strong></td><td>Quota x 10</td><td>Quota x 2</td><td>Quota x1</td></tr><tr><td><strong>Free request</strong></td><td>Free request on Gold Class performance</td><td>Free request on Instant Archive Class performance</td><td>Free request on Archive Class performance</td></tr></tbody></table>

***

## Với Transition rule

Thực hiện theo hướng dẫn bên dưới để thiết lập transition rule:

1\. Đăng nhập vào [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list), sau đó chọn Region **HAN02**

2\. Chọn **project** chứa **bucket** bạn muốn thiết lập lifecycle. Giả sử tôi có một bucket `demo-project` đã được khởi tạo tạo Storage Class Gold như hình dưới

<figure><img src="../../../../../../.gitbook/assets/image (1093).png" alt=""><figcaption></figcaption></figure>

3\. Chọn biểu tượng **Action** và chọn **Configure Lifecycle.**

<figure><img src="../../../../../../.gitbook/assets/image (1095).png" alt=""><figcaption></figcaption></figure>

4\. Màn hình **Lifecycle** được hiển thị. Chọn **Create a lifecycle rule**.

<figure><img src="../../../../../../.gitbook/assets/image (1094).png" alt=""><figcaption></figcaption></figure>

5\. Nhập **Rule name**. Rule name mà chúng tôi cho phép bạn nhập bao gồm các chữ cái (a-z, A-Z, 0-9, '\_', '-', space). Độ dài **Rule name** của bạn phải nằm trong khoảng từ 5 đến 50.

6\. Chọn **Rule type**: **Transition**

<figure><img src="../../../../../../.gitbook/assets/image (1096).png" alt=""><figcaption></figcaption></figure>

7\. Nhập **Filter**. Filter này được áp dụng cho một lifecycle rule cụ thể. **Mỗi lifecycle rule chỉ được đặt 1 filter duy nhất, nếu bạn muốn áp dụng quy tắc lifecycle mà bạn đang tạo lên tất cả các object thuộc bucket này, hãy để trống trường thông tin này.** Hoặc bạn có thể lọc các object mong muốn áp dụng lifecycle rule thông qua prefix.

8\. Chọn hành động xảy ra với object tại bucket mà bạn chọn, bao gồm:

* **Transition current version of objects:**
  * Khi kích hoạt, rule này sẽ tự động di chuyển object từ lớp lưu trữ hiện tại xuống lớp lưu trữ thấp hơn tùy chọn sau một khoảng thời gian nhất định.
  * Bạn có thể nhập số ngày trong phần "**After \_\_\_ days from object modified**" để định nghĩa số ngày object được di chuyển nếu không có thay đổi.

<figure><img src="../../../../../../.gitbook/assets/image (1097).png" alt=""><figcaption></figcaption></figure>

***

## Với Expiration rule

Expiration rule và tập quy định tự động xóa object khi đến thời điểm hết hạn. Thực hiện theo hướng dẫn bên dưới để thiết lập expiration rule:

1\. Đăng nhập vào [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list).

2\. Chọn **project** chứa **bucket** bạn muốn thiết lập lifecycle.

3\. Chọn biểu tượng **Action** và chọn **Configure Lifecycle.**

<figure><img src="../../../../../../.gitbook/assets/image (1099).png" alt=""><figcaption></figcaption></figure>

4\. Màn hình **Lifecycle** được hiển thị. Chọn **Create a lifecycle rule**.

<figure><img src="../../../../../../.gitbook/assets/image (1100).png" alt=""><figcaption></figcaption></figure>

5\. Nhập **Rule name**. Rule name mà chúng tôi cho phép bạn nhập bao gồm các chữ cái (a-z, A-Z, 0-9, '\_', '-', space). Độ dài **Rule name** của bạn phải nằm trong khoảng từ 5 đến 50.

6\. Chọn Rule type: hiện tại, chúng tôi chỉ hỗ trợ 1 loại rule Expiration: Rule hỗ trợ xóa các object theo điều kiện ràng buộc.

7\. Nhập **Filter**. Filter này được áp dụng cho một lifecycle rule cụ thể. **Mỗi lifecycle rule chỉ được đặt 1 filter duy nhất, nếu bạn muốn áp dụng quy tắc lifecycle mà bạn đang tạo lên tất cả các object thuộc bucket này, hãy để trống trường thông tin này.** Hoặc bạn có thể lọc các object mong muốn áp dụng lifecycle rule thông qua prefix.

<figure><img src="../../../../../../.gitbook/assets/image (1101).png" alt=""><figcaption></figcaption></figure>

8\. Chọn hành động xảy ra với object tại bucket mà bạn chọn, bao gồm:

* **Expire current version of objects**:
  * Khi kích hoạt, rule này sẽ tự động xóa **phiên bản hiện tại** của object sau một khoảng thời gian nhất định.
  * Bạn có thể nhập số ngày trong phần "After \_\_\_ days from object creation" để định nghĩa số ngày kể từ khi tạo object mà phiên bản hiện tại sẽ hết hạn và bị xóa.
* **Permanently delete noncurrent versions**:
  * Rule này áp dụng cho các **phiên bản không phải là phiên bản hiện tại** (noncurrent versions) của object nếu bạn đã bật tính năng Versioning.
  * Bạn có thể định cấu hình để xóa các phiên bản cũ sau một số ngày kể từ khi chúng trở thành phiên bản không phải là phiên bản hiện tại, bằng cách điền vào "After \_\_\_ days become noncurrent version".
* **Delete incomplete multipart uploads**:
  * Khi bạn tải lên một object lớn bằng cách chia thành nhiều phần (multipart upload), nhưng quá trình tải lên không hoàn tất, các phần đã tải sẽ bị giữ lại trong S3.
  * Rule này cho phép tự động xóa các phần của **multipart upload không hoàn tất** sau một khoảng thời gian từ khi quá trình tải lên được bắt đầu.
  * Bạn có thể nhập số ngày trong phần "After \_\_\_ days from object creation" để xác định khoảng thời gian trước khi các phần incomplete của multipart upload bị xóa.
* **Delete expired object delete marker**:
  * Rule này chỉ áp dụng khi bạn đã bật Versioning và có các object delete marker trong bucket.
  * Khi kích hoạt, nó sẽ xóa các **delete marker** đã hết hạn, giúp cải thiện hiệu suất bằng cách làm sạch các marker không còn cần thiết. (Tùy chọn này thường chỉ có thể bật khi có delete marker hết hạn trong bucket.)

<figure><img src="../../../../../../.gitbook/assets/image (1102).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Lưu ý:**

* Việc xử lý object trong một lần chạy lifecycle rule phụ thuộc vào **số lượng object** trong bucket được thiết lập lifecycle rule của bạn và **workload** của hệ thống chúng tôi. Nếu bucket có **nhiều object** hoặc hệ thống có tải cao, việc xử lý sẽ **chậm và kéo dài qua các ngày kế tiếp**. Nếu bucket có **ít object** hoặc hệ thống có tải thấp, việc xử lý sẽ **nhanh và có thể hoàn thành trong một ngày**. Để đảm bảo việc xử lý object diễn ra hiệu quả và nhanh chóng, bạn nên chia nhỏ các lần chạy lifecycle rule và sử dụng Bộ lọc (Filter) để giảm thiểu số lượng object cần xử lý.
* Với **Transition rule**: bạn chỉ được phép chuyển dữ liệu xuống lớp lưu trữ thấp hơn, không thể tự động chuyển ngược lên lớp cao hơn.&#x20;
{% endhint %}
