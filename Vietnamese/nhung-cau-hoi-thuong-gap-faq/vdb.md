# vDB

### \[vDB] Tôi đã tạo vDB MySQL muốn public accessbility thì phải làm sao?

Lúc khởi tạo vDB quý khách click vào Public accessibility. Còn nếu đã tạo rồi thì quý khách xóa đi và tạo lại vDB mới để có thể public accessibility

### \[vDB] Tôi muốn gia hạn vDB thì làm như thế nào?

Quý khách có thể tham khảo link hướng dẫn như sau:\


[https://docs.vngcloud.vn/vng-cloud-document/vn/vdb/relational-database-service-rds/gia-han-rds-instance](https://docs.vngcloud.vn/vng-cloud-document/vn/vdb/relational-database-service-rds/gia-han-rds-instance)

### \[vDB] Tại sao tôi không thể nâng gói MySQL của mình?

Quý khách vui lòng kiểm tra lại thông tin server của quý khách còn hạn sử dụng không . Vì nếu sắp hết hạn sử dụng thì sẽ không được gia hạn. Quý khách cần gia hạn trước rồi sẽ resize lại mysql của mình

### \[vDB] Tại sao tôi sử dụng trial vDB MySQL thì nó lại báo lỗi Please select Network?

Quý khách vui lòng khởi tạo network trước như link hướng dẫn sau:\
[https://docs.vngcloud.vn/pages/viewpage.action?pageId=13009888.](https://docs.vngcloud.vn/pages/viewpage.action?pageId=13009888.).\
Sau khi khởi tạo network xong quý khách có thể tạo được vDB được.

### \[vDB] Để update timezone trên vDB thì tôi làm như thế nào?

Trường hợp này Quý khách vui lòng liên hệ 24/7 để tạo ticket, chúng tôi sẽ hỗ trợ nhanh chóng.

### \[vDB] Resize volume ở vDB có cần restart DB không?

Quý khách không cần restart DB khi resize volume, hệ thống đã tự động restart.

### \[vDB] Tôi muốn sử dụng vDB API thì có API curl để tạo user kafka không?

Quý khách có thể tham khảo tài liệu vDB API tại đây [https://docs.api.vngcloud.vn/service-docs/vdb-api.html#tag/Kafka-Cluster-API/operation/createUser](https://docs.api.vngcloud.vn/service-docs/vdb-api.html#tag/Kafka-Cluster-API/operation/createUser)&#x20;

### \[vDB] vDB đổi cổng kết nối được không?

Hiện tại vDB không cho đổi cổng kết nối. Trường hợp bạn muốn xem thông tin kết nối bạn chọn vào xem chi tiết của DB Instance, sau đó chọn đến tab **Connectivity & Security**, bạn xem thông tin kết nối tại mục **Endpoint & Port**.
