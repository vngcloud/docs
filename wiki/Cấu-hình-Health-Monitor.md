Health Monitor là một trong những tính năng rất quan trọng của dịch vụ Load Balancer, giúp chúng ta phát hiện được Server down và remove Server đó ra khỏi Pool của nó.

![](images/storage/image2020-5-12_17-19-56.png)

Thông tin như sau:


*  **Protocol: ** Giao thức monitor, 
    * TCP: đơn thuần chỉ check port server, được sử dụng cho Load Balancer layer 4 và layer 7.
    * HTTP: cho phép người dùng có thể check được status code của HTTP, giúp người dùng có thể check được lỗi ở mức ứng dụng (ví dụ lỗi database), đây là một tính năng nâng cao chỉ có ở Load Balancer layer 7.

    
*  **Path: ** đường dẫn check status code của HTTP, default được set là "/"
*  **HTTP method: ** phương thức gọi của request như GET, PUT, POST. Thông tin này chỉ có ở Load Balancer layer 7.
*  **Healthy threshold: ** số lần health check thành công để Load Balancer quyết định chuyển trạng thái member từ ONLINE sang ERROR.
*  **Unhealthy threshold: ** số lần health check thất bại để Load Balancer quyết định chuyển trạng thái member tử ERROR sang ONLINE.
*  **Timeout: ** thời gian Load Balancer chờ member trả tín hiệu về.
*  **Interval: ** khoảng thời gian bao lâu Load Balancer gửi health check đi một lần.
*  **Success code:**  mã code do người dùng định nghĩa để Load Balancer nhận biết là member đang ONLINE hay ERROR, thông thường là "200". Thông tin này chỉ có ở Load Balancer layer 7.

 **Lỗi thông báo từ Health Monitor** Một số người dùng thường thắc mắc khi nhìn thấy trạng thái  **ERROR ** ở cột  **OPERTATING STATE** . Trong trường hợp này thông thường là do Load Balancer health check phát hiện ra có member bị error trong Pool của Load Balancer, lúc này chúng ta nên kiểm tra lại server ở phía người dùng để tìm ra nguyên nhân khắc phục.

![](images/storage/error.jpg)





*****

[[category.storage-team]] 
[[category.confluence]] 
