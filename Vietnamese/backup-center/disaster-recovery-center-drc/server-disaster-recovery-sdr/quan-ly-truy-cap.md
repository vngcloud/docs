# Quản lý truy cập

Khi triển khai và quản lý Server Disaster Recovery (SDR) trên VNG Cloud, việc thiết lập chính sách truy cập và phân quyền (IAM) là rất quan trọng để đảm bảo an ninh và kiểm soát chặt chẽ các hoạt động liên quan đến DR. Tham khảo bài viết dưới đây để tiến hành quản lý truy cập và phân quyền trên SDR

## Danh sách endpoint



<table><thead><tr><th width="138">Level</th><th>Action</th><th>Mô tả</th></tr></thead><tbody><tr><td>Write</td><td>DrPairAttachServer</td><td>Thêm máy chủ chính vào DRC</td></tr><tr><td>Write</td><td>DrPairStartReplication</td><td>Khởi tạo quá trình sao chép</td></tr><tr><td>Write</td><td>DrPairTestFailover</td><td>Kiểm tra chuyển đổi dự phòng</td></tr><tr><td>Write</td><td>DrPairChangeRecoveryPoint</td><td>Thay đổi Recovery Point</td></tr><tr><td>Write</td><td>DrPairCleanTestEnvironment</td><td>Xóa môi trường kiểm tra chuyển đổi dự phòng</td></tr><tr><td>Write</td><td>DrPairCommitFailover</td><td>Xác nhận chuyển đổi dự phòng</td></tr><tr><td>Write</td><td>DrPairDetachServer</td><td>Xóa thông tin pairing</td></tr><tr><td>Write</td><td>DrPairFailover</td><td>Chuyển đổi dự phòng</td></tr><tr><td>Write</td><td>DrPairRestartReplication</td><td>Khởi tạo lại quá trình sao chép</td></tr><tr><td>Write</td><td>DrPairResumeReplication</td><td>Tiếp tục sao chép </td></tr><tr><td>Write</td><td>DrPairStopReplication</td><td>Tạm dừng sao chép</td></tr><tr><td>List</td><td>ListDrPairs</td><td>Xem danh sách pairing</td></tr><tr><td>Get</td><td>GetDrPair</td><td>Xem thông tin chi tiết pairing</td></tr><tr><td>Get</td><td>GetDrPairHistory</td><td>Xem lịch sử thao tác trên pairing</td></tr><tr><td>Get</td><td>GetDrPairRecoveryPoints</td><td>Xem danh sách recovery point</td></tr></tbody></table>
