# Number

### Tổng quan

**Number chart** với chỉ số tóm tắt là một loại biểu đồ thể hiện các số được tính toán từ một bộ dữ liệu, thay vì thể hiện các số gốc.

![](http://docs.vngcloud.vn/download/attachments/59806972/image2023-8-9\_14-35-7.png?version=1\&modificationDate=1691566508000\&api=v2)

***

### Cấu hình biểu đồ

<figure><img src="http://docs.vngcloud.vn/download/attachments/59806972/image2023-8-1_13-17-44.png?version=1&#x26;modificationDate=1690870665000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### 1. Choose graph style&#x20;

Đối với biểu đồ dạng number, tại mục này bạn chọn Style là ![](http://docs.vngcloud.vn/download/thumbnails/59806972/image2023-8-9\_14-35-24.png?version=1\&modificationDate=1691566524000\&api=v2)

\


![](http://docs.vngcloud.vn/download/attachments/59806972/image2023-8-9\_14-35-39.png?version=1\&modificationDate=1691566540000\&api=v2)

#### 2. Graph your data

Chọn loại dữ liệu để vẽ Widget:

* Metrics: xem [Metric query](http://docs.vngcloud.vn/display/VPV/Metric+query) để cấu hình cho loại dữ liệu Metrics.
* Logs: xem [Log Query](http://docs.vngcloud.vn/display/VPV/Log+Query) để cấu hình cho loại dữ liệu Logs.

Alias: Bạn có thể đặt Alias cho mỗi câu query, alias này sẽ được hiển thị trên graph và legend, điều này rất hữu ích cho những tên metric, logs hay những câu query có filter (bộ lọc) dài.&#x20;

#### 3. Fixed time range&#x20;

Khung thời gian cố định là một thuộc tính của Widget mà bạn có thể thiết lập để lọc dữ liệu trên Widget theo một khung thời gian cố định mà không phụ thuộc với khung thời gian (time range) của Dashboard. Mỗi Widget đều có thể thiết lập Fixed time range riêng biệt, bạn có thể chọn một trong các khung thời gian được mô tả ở bảng bên dưới. Ví dụ: nếu bạn chọn Global time thì khoảng thời gian lấy dữ liệu trên Widget được hiển thị sẽ được bằng khoảng thời gian mà bạn chọn trên Dashboard. Tức là khi thay đổi thời gian lấy dữ liệu trên Dashboard thì thời gian lấy dữ liệu của Widget sẽ thay đổi theo. Khuyến khích sử dụng lựa chọn này. Nếu bạn chọn Pass N minutes (N = 5,10,...) thì khoảng thời gian lấy dữ liệu trên Widget cố định (không thay đổi) luôn là 5, 10,...phút trước.&#x20;

Chọn **Create** để tạo Widget, nếu có nhu cầu thay đổi tên widget thì bạn có thể thực hiện chỉnh sửa tại **Widget name**.
