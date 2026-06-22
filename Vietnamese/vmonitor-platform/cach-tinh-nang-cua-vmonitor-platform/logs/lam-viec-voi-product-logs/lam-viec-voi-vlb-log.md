# Làm việc với vLB-Log

Để xem được logs của vLB bạn truy cập vào vMonitor Platform tại [link](https://hcm-3.console.vngcloud.vn/vmonitor), sau đó vào mục **Infrastructure list/vLB Log.** Tại đây, bạn có thể xem danh sách tất cả vLB trên HCM03 của bạn. Tại màn hình này, bạn sẽ thấy các cột thông tin cơ bản như:

* **vLB Project**: tên của vLB.
* **Log Project**: log project sẽ chứa logs của vLB khi bạn enable "Detailed Monitoring".
* **Log Project Usage**: thông tin về mức độ sử dụng của Log Project mà bạn đã gắn vào vLB này.
* **Monitoring Status**: trạng thái monitoring của vLB. Nếu chưa enable "Detailed Monitoring" thì trạng thái sẽ là INACTIVE, nếu đã enable thì trạng thái là ACTIVE, còn nếu vLB đã bị xóa thì sẽ là DELETED.
* **Detailed Monitoring**: kích hoạt hay hủy theo dõi Logs của vLB này.

<figure><img src="../../../../.gitbook/assets/image (332).png" alt=""><figcaption></figcaption></figure>

Để kích hoạt theo dõi, bạn cần nhấn **enable** tại cột **Detailed Monitoring.**

Hệ thống sẽ hiển thị Popup và bạn cần **chọn Log Project** để chứa logs của vLB này, sau đó nhấn "**enable**". Nếu bạn chưa có bất kì Log Project nào, bạn có thể nhấn "Create a log project" ở popup hoặc qua tab Quota & Usage để tạo Log Project trước.

Sau khi enable bạn sẽ thấy status của vLB này chuyển thành **ACTIVE**, và bạn có thể truy cập vào Log Project vừa chọn để xem logs.

Nếu có nhu cầu thay đổi Log Project chứa Logs, bạn có thể chọn nút 3 chấm và chọn "**Edit Log Project**" để thay đổi.

Nếu không còn nhu cầu để xem logs của vLB thì bạn có thể **disable** ở cột **Detailed Monitoring**.

***

## Các fields dữ liệu: <a href="#lamviecvoivlb-log-cacfieldsdulieu" id="lamviecvoivlb-log-cacfieldsdulieu"></a>

Đối với Application Load Balancer, bạn sẽ xem được HTTP Access Logs với các fields:

* httpRequest.clientIp
* httpRequest.clientPort
* httpRequest.requestMethod
* httpRequest.requestUrl
* httpRequest.requestSize
* httpRequest.responseSize
* httpRequest.status
* httpRequest.latency
* httpRequest.userAgent
* httpRequest.referer

Đối với Network Load Balancer, bạn sẽ xem được TCP Connection Logs với các fields:

* jsonPayload.connection.clientIp
* jsonPayload.connection.clientPort
* jsonPayload.connection.requestSize
* jsonPayload.connection.responseSize
* jsonPayload.connection.rtt

***

## Đẩy access log vLB sang vDB

Ngoài việc xem log trên vMonitor Platform, bạn có thể đẩy **access log** của vLB sang cụm **vDB Kafka** hoặc **vDB OpenSearch** của riêng mình để chủ động lưu trữ, tra cứu và phân tích log theo nhu cầu.

Hai đích đến hoạt động độc lập: bạn có thể chỉ đẩy sang Kafka, chỉ đẩy sang OpenSearch, hoặc bật đồng thời cả hai cho cùng một vLB.

Lưu ý: tính năng đang trong giai đoạn Alpha, vui lòng liên hệ Hỗ trợ GreenNode để sử dụng.

### Điều kiện cần

**Nếu đẩy sang vDB Kafka**, trên vDB Kafka cần có sẵn:

* Một Cluster Kafka đang hoạt động và cho phép truy cập công khai.
* Một Topic trong Cluster để chứa access log.
* Một Kafka user đã được phát hành thông tin xác thực và được cấp quyền ghi vào Topic nói trên.

**Nếu đẩy sang vDB OpenSearch**, trên vDB OpenSearch cần có sẵn:

* Một Cluster OpenSearch đang hoạt động và có địa chỉ truy cập công khai dành cho log.
* Một tài khoản (Username/Password) có quyền ghi vào Cluster.

### Bật đẩy access log sang vDB Kafka

1. Mở vLB trong danh sách log mapping, chọn chức năng **Enable log to vDB Kafka**.
2. Gạt công tắc **Enable logging** sang trạng thái bật.
3. Chọn các thông tin:

| Trường      | Ghi chú                                                                                             |
| ----------- | --------------------------------------------------------------------------------------------------- |
| **Cluster** | Cluster Kafka sẽ nhận access log.                                                                   |
| **Topic**   | Topic trong Cluster đã chọn.                                                                        |
| **User**    | Kafka user dùng để ghi log.                                                                         |
| **Mode**    | Cơ chế xác thực — chọn **mTLS** hoặc **SASL** (chọn loại mà cả Cluster và user của bạn đều hỗ trợ). |

4. Nhấn **Save**.

{% hint style="info" %}
Hệ thống tự kết nối tới vDB để lấy thông tin xác thực của Kafka user đã chọn — bạn không cần nhập thêm credential.
{% endhint %}

### Bật đẩy access log sang vDB OpenSearch

1. Mở vLB trong danh sách log mapping, chọn chức năng **Enable log to vDB OpenSearch**.
2. Gạt công tắc **Enable logging** sang trạng thái bật.
3. Chọn và nhập:

| Trường       | Yêu cầu                                                                                            |
| ------------ | -------------------------------------------------------------------------------------------------- |
| **Cluster**  | Cluster OpenSearch sẽ nhận access log.                                                             |
| **Username** | Tài khoản có quyền ghi vào Cluster. Độ dài 3–31 ký tự, gồm chữ, số và các ký tự `_`, `.`, `-`.     |
| **Password** | Tối thiểu 8 ký tự, gồm đủ chữ hoa, chữ thường, chữ số và một ký tự đặc biệt trong `@ $ ! % * ? &`. |

4. Nhấn **Save**.

{% hint style="warning" %}
Hệ thống kiểm tra kết nối tới Cluster OpenSearch ngay khi bạn nhấn **Save**. Nếu Username hoặc Password không đúng, thao tác sẽ bị từ chối tại bước này.
{% endhint %}

### Đổi sang Cluster khác

Mở lại hộp thoại tương ứng, chọn Cluster mới (và cập nhật các thông tin liên quan nếu cần), rồi nhấn **Save**. Hệ thống tự động chuyển việc đẩy access log sang Cluster mới.

### Tắt đẩy access log

Mở lại hộp thoại tương ứng, gạt **Enable logging** sang trạng thái tắt và nhấn **Save**. Hệ thống ngừng đẩy access log sang Cluster đó.

### Xử lý lỗi khi lưu

| Thông báo                                                  | Nguyên nhân & cách xử lý                                                                      |
| ---------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| Lỗi liên quan đến Cluster, Topic, User hoặc quyền truy cập | Thành phần tương ứng ở vDB chưa sẵn sàng. Kiểm tra lại trạng thái và quyền ở vDB rồi thử lại. |
| Lỗi kết nối OpenSearch khi nhấn **Save**                   | Username hoặc Password sai. Nhập lại đúng thông tin xác thực và lưu lại.                      |

***

### Một số chú ý: <a href="#lamviecvoivlb-log-motsochuy" id="lamviecvoivlb-log-motsochuy"></a>

* vLB sau khi được tạo sẽ mất khoảng vào phút (tối đa 10 phút) để có thể đồng bộ về vMonitor Platform.
