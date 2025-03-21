# Truy cập và làm việc trên OpenSearch Dashboard

Sau khi một OpenSearch Cluster đã được khởi tạo, bạn có thể truy cập vào OpenSearch Dashboard để **thêm data, sử dụng các công cụ phân tích, thực hiện truy vấn, tạo dashboard, quản lý index, quản lý người dùng**...Chi tiết, các bước để thực hiện như sau:

## Truy cập vào OpenSearch Dashboard

**Bước 1:** Trên màn hình chứa danh sách các OpenSearch Cluster, chọn vào OpenSearch Cluster mà bạn muốn truy cập.

**Bước 2:** Tại màn hình chi tiết cluster, chọn mục **Connectivity & Security**

**Bước 3**: Tại mục **Accessibility**, thực hiện lấy thông tin **Dashboard Endpoint**

**Bước 4**: Thực hiện mở URL này và đăng nhập bằng:

* **Tên đăng nhập**: `master-user`
* **Mật khẩu**: là **Master user password** bạn đã nhập khi khởi tạo Cluster

Sau khi đã đăng nhập thành công, lúc này, bạn có thể làm việc với OpenSearch Cluster thông qua OpenSearch Dashboard. Tham khảo thêm các mục bên dưới để xem hướng dẫn thực hiện một số tác vụ chính trên OpenSearch Dashboard.

## Làm việc với OpenSearch Dashboard

### Thêm data

{% embed url="https://opensearch.org/docs/latest/dashboards/quickstart/#adding-sample-data" %}

### Sử dụng các công cụ phân tích

{% embed url="https://opensearch.org/docs/latest/dashboards/discover/index-discover/" %}

### Thực hiện truy vấn

{% embed url="https://opensearch.org/docs/latest/dashboards/query-workbench/" %}

### Tạo Dashboard

{% embed url="https://opensearch.org/docs/latest/dashboards/dashboard/index/" %}

### Quản lý index

{% embed url="https://opensearch.org/docs/latest/dashboards/im-dashboards/index/" %}
