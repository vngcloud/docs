Cloud Audit Logs là tính năng ghi lại tất cả các hoạt động quản trị và truy cập trên tài nguyên VNG Cloud của bạn. Audit Logs sẽ giúp bạn trả lời những câu hỏi: " **Ai đã làm gì, nơi nào và khi nào?** "  trên các tài nguyên VNG Cloud cùng với mức độ minh bạch như trên môi trường On-premise của bạn. Việc bật tính năng Audit Logs sẽ giúp bạn theo dõi, rà soát và đảm bảo bảo mật cho các tài nguyên trên VNG Cloud.

 **1. Các loại Audit Logs** Cloud Audit Logs cung cấp các loại Audit Logs như bên dưới đây, tuỳ vào các products hay services mà sẽ hỗ trợ loại audit logs nào:


*  **Admin Activity Audit Logs** : chứa tất cả các logs cho những hành động mà thay đổi tài nguyên (Create, Update, Delete) trên VNG Cloud. Ví dụ như là: những logs khi người dùng tạo vServer hay xoá security group. Gọi tắt là  **ADMIN_WRITE** 
*  **Data Access Audit Logs**  (coming soon): chứa tất cả các logs cho những hành động mà đọc thông tin cấu hình của tài nguyên, cũng như những hành động mà tạo, xoá, sửa và đọc dữ liệu của tài nguyên. Dữ liệu của tài nguyên là những dữ liệu của người dùng đưa lên trên VNG Cloud, ví dụ như là các object của vStorage. Cụ thể chia 3 loại như bên dưới: 
    *  **ADMIN_READ** : hành động đọc thông tin cấu hình của tài nguyên. Ví dụ như là: liệt kê danh sách vServer hay xem chi tiết một vServer
    *  **DATA_WRITE** : hành động tạo, xoá, sửa dữ liệu của tài nguyên. Ví dụ như là: tải object lên vStorage hay là xoá object trên vStorage
    *  **DATA_READ** : hành động đọc dữ liệu của tài nguyên. Ví dụ như là: liệt kê danh sách objects của vStorage

    
*  **System Event Audit Logs** : chứa tất cả các logs cho những hành động mà thay đổi tài nguyên trên VNG Cloud; tuy nhiên nó là những hành động mà được tạo ra bởi VNG Cloud systems, mà không phải được thực hiện trực tiếp từ người dùng. Ví dụ những dòng logs khi VNG Cloud systems tự động mở rộng (autoscale) node group của vContainer, hay những hành động tự động tạo bản daily backup cho vDB. Gọi tắt là  **SYSTEM_EVENT** 
*  **Policy Denied Audit Logs**  (coming soon): chứa tất cả các logs khi mà VNG Cloud products/services từ chối truy cập của IAM user account hay service accounts bởi vì vi phạm các Policy. Gọi tắt là  **POLICY_DENIED** 

 **2. Danh sách các Products/Services hỗ trợ các loại Audit Logs** 

| Products/Service Name | Admin Activity Audit Logs | Data Access Audit Logs   | System Event Audit Logs | Policy Denied Audit Logs | 
|  --- |  --- |  --- |  --- |  --- | 
| ADMIN_WRITE | ADMIN_READ | DATA_WRITE | DATA_READ | SYSTEM_EVENT | POLICY_DENIED | 
| vServer | YES

 | COMING SOON | N/A

 | N/A

 | N/A

 | COMING SOON

 | 
| vLB | YES

 | COMING SOON

 | N/A

 | N/A

 | N/A

 | COMING SOON

 | 
| vDB | COMING SOON

 | COMING SOON

 | N/A

 | N/A

 | COMING SOON

 | COMING SOON

 | 
| vContainer | YES

 | COMING SOON

 | N/A

 | N/A

 | YES

 | COMING SOON

 | 
| vMonitor | YES

 | COMING SOON

 | N/A

 | N/A

 | N/A

 | COMING SOON

 | 
| vStorage | YES | YES | YES | YES | N/A

 | COMING SOON

 | 


*  **Ý nghĩa các trạng thái** 

YES : đã hỗ trợ đầy đủ loại audit logs này

PARTIAL YES :  đã hỗ trợ nhưng chưa đầy đủ 

COMING SOON : có loại audit logs này và sẽ hỗ trợ sắp tới

N/A : không hỗ trợ loại audit logs này

 **3. Kích hoạt Audit Logs** Mặc định VNG Cloud sẽ không bật sẵn tính năng Audit Logs, khách hàng cần thực hiện các bước dưới đây để kích hoạt:


1. Truy cập vào trang Audit Logs của IAM Portal: [https://hcm-3.console.vngcloud.vn/iam/audit-logs](https://hcm-3.console.vngcloud.vn/iam/audit-logs)
1. Chọn  **Set default configuration, ** popup thiết lập sẽ hiển thị cho phép bạn chọn bật ADMIN_WRITE hay SYSTEM_EVENT
1. Chọn kích hoạt bật loại audit logs ADMIN_WRITE hay SYSTEM_EVENT mà bạn mong muốn
1. Nhấn nút  **Save ** để kích hoạt

Ví dụ bạn chọn cả 2 loại Audit Logs đang được hỗ trợ, bạn sẽ thấy màn hình như bên dưới, đối với 2 loại ADMIN_WRITE và SYSTEM_EVENT khi được kích hoạt sẽ áp dụng cho tất cả product/services đang được hỗ trợ theo như bảng trên

![](images/storage/image2023-6-19_17-31-59.png)Khi đã kích hoạt Audit Logs, hệ thống sẽ bắt đầu lưu các Audit Logs kể từ thời điểm kích hoạt (không có quá khứ), và tự động tạo  **Log Project: required**  bên phía  **vMonitor Logs**  để lưu trữ, ** Log Project: required**  sẽ hoàn toàn miễn phí và lưu trữ các Audit Logs trong vòng  **90 ngày** . Đồng thời khi đã kích hoạt 2 loại Audit Logs: ADMIN_WRITE VÀ SYSTEM_EVENT, thì bạn sẽ không thể tắt tính năng này đi, hệ thống sẽ luôn luôn lưu trữ tất cả hành động thuộc 2 loại Audit Logs này.

 **4. Xem các Audit Logs đã kích hoạt** Để xem các Audit Logs đã kích hoạt, bạn cần làm theo các hướng dẫn sau:


1. Truy cập mục Log Search của vMonitor Logs: [https://hcm-3.console.vngcloud.vn/vmonitor/log/search](https://hcm-3.console.vngcloud.vn/vmonitor/log/search)
1. Chọn  **Log Project: required**  để xem các Audit Logs đã được lưu trữ. Ví dụ như hình dưới đây là hành động 1 root user account tạo Security Group thuộc vServer tại thời điểm 19/06/2023 17:51:57 đã được ghi nhận lại.

![](images/storage/image2023-6-19_18-8-35.png)



 **3. Cấu trúc và định dạng các Audit Logs** Mỗi dòng Audit Logs sẽ có thể có các field như bên dưới


*  **timestamp** : thời gian logs được sinh ra
*  **logId** : UUID để phân biệt từng dòng log
*  **source** : nơi sinh ra dòng log, và đặc tả rõ đó là loại logs gì, ví dụ nếu dòng logs được sinh ra từ audit logs và loại là ADMIN_WRITE thì nội dung sẽ là source: cloud_audit/admin_write
*  **serviceName** : thông tin sản phẩm/dịch vụ được theo dõi, ví dụ dòng Audit Logs này là của vServer thì nội dung sẽ là serviceName: vserver
*  **resource** : thông tin chi tiết và cụ thể tài nguyên nào được theo dõi, sẽ gồm 2 fields con là: type và labels 
    *  **type** : thông tin resource nào của product, ví dụ nếu là dòng logs liên quan server sẽ là type: vserver_server
    *  **labels** : tên và ID của resource hay các thông tin khác của resource
    * Ví dụ ở dưới là resource server của vServer có serverID: ins-b019f5d0-1234-41ba-1234-851f9ef39003



    



| "resource":{"labels":{"serverVRN":"vserver::12345:server/ins-b019f5d0-1234-41ba-1234-851f9ef39003","serverId":"ins-b019f5d0-1234-41ba-1234-851f9ef39003"},"type":"vserver:server"}, | 


*  **JsonPayload** : chứa thông tin cụ thể hành động là gì, ai đã tạo ra hành động này (root user account, IAM user account hay service account), request metadata và các request/response body nếu có. Ví dụ ở bên dưới bạn có thể thấy userType: root-user là root user account với ID: 12345 đang thực hiện hành động DeleteServer với server có ID: ins-b019f5d0-1234-41ba-1234-851f9ef39003



| "jsonPayload":{"authenticationInfo":{"rootUserAccountId":12345,"userType":"root-user"},"serviceName":"vserver""action":"vserver:DeleteServer","resource":"vserver::12345:server/ins-b019f5d0-1234-41ba-1234-851f9ef39003","request":{},"requestMetadata":{},"response":{}}, | 


*  Với ví dụ bên dưới, bạn có thể thấy userType: iam-user là IAM user account có ID: e6d39955-e4c3-1234-1234-84d82ea554bf thuộc root user account có ID: 12345 đang thực hiện hành động SearchLogs với Log Project có ID: bbb5f6ef-1234-49a1-1234-b41332376fef. Tương tự với serviceAccount bạn cũng sẽ thấy userType: user-sa.



| "jsonPayload":{"authenticationInfo":{"userType":"iam-user","rootUserAccountId":12345,"userAccount":"e6d39955-e4c3-1234-1234-84d82ea554bf"},"serviceName":"vmonitor","action":"vmonitor:SearchLogs","resource":"vmonitor::12345:log-project/bbb5f6ef-1234-49a1-1234-b41332376fef","request":{},"requestMetadata":{},"response":{}}, | 


* Ngoài ra bạn cũng có thể thấy thêm các thông tin về requestMetadata, request và response của hành động này (tuỳ vào loại action sẽ có hay không)



| "jsonPayload":{"authenticationInfo":{"userType":"iam-user","rootUserAccountId":12345,"userAccount":"e6d39955-e4c3-1234-1234-84d82ea554bf"},"serviceName":"vmonitor","action":"vmonitor:SearchLogs","resource":"vmonitor::12345:log-project/bbb5f6ef-1234-49a1-1234-b41332376fef","request":{"method":"POST","path":"/v1/projects/bbb5f6ef-1234-49a1-1234-b41332376fef/search-logs","httpVersion":"HTTP/1.1"},"requestMetadata":{"callerIp":"103.1.208.50","userAgent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36"},"response":{"duration":272,"status":200}}, | 





*****

[[category.storage-team]] 
[[category.confluence]] 
