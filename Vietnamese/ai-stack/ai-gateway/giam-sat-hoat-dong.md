# Giám sát hoạt động

Để theo dõi và phân tích hoạt động của một AI Gateway đang hoạt động, bạn có thể giám sát thông qua:

## Metric

Tại giao diện chi tiết của một Gateway, chọn tab **Monitor** để theo dõi các chỉ số thời gian thực được thể hiện qua biểu đồ bao gồm:

* **Requests**: Tổng số lượng request đã được gửi tới AI Gateway.
* **Errors**: Số request đã được gửi tới AI Gateway và được nhận kết quả lỗi.
* **Tokens**: Số lượng token đã sử dụng, bao gồm:
  * `input`: token đầu vào (câu hỏi của bạn).
  * `output`: token đầu ra (kết quả từ LLM Model).

Bạn có thể tùy chỉnh khoảng thời gian quan sát (15m, 30m, 1h, 2h, v.v.) và lọc theo Provider hoặc Model cụ thể.

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Logs

Tại giao diện chi tiết của một Gateway, chọn tab **Log** để xem danh sách tất cả các request đã gửi qua Gateway.

Tại đây, bạn có thể danh sách request được gửi tới AI Gateway bao gồm:&#x20;

* **Time:** thời gian gửi request.
* **Status:** trạng thái của request, bao gồm **Success**, **Error** hoặc **Timeout**.
* **Model:** tên model được sử dụng.
* **Tokens:** số lượng token input/ output.
* **Duration:** tổng thời gian xử lý request.

Bạn có thể tùy chỉnh khoảng thời gian quan sát (24h, 1d, 2d,...) và lọc theo Status cụ thể.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Ngoài ra, bạn có thể xem chi tiết một request bằng cách:

* Nhấn vào biểu tượng **Detail** cột **Action** để mở **Detail Log**.
* Tại đây bạn sẽ thấy:
  * **Input**: Nội dung câu hỏi hoặc prompt gốc bạn gửi vào.
  * **Output**: Kết quả trả về từ LLM Model.
  * **Thông tin bổ sung**: host, model, thời gian phản hồi,...

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Các metrics đo lường latencies trong một request cũng được hiển thị cụ thể tại đây:

latencies.receive: Thời gian bắt đầu nhận response(byte đầu tiên) tới kết thúc nhận response (byte cuối cùng) từ LLM

latencies.gateway: Thời gian xử lý nội bộ tại Gateway (không tính thời gian proxy)

latencies.proxy: Thời gian GW gửi request lên LLM và nhận response từ LLM về (byte đầu tiên)

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
