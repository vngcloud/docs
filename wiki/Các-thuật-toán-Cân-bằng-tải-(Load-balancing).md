Load balancing hay "Cân bằng tải" là một trong những tính năng chính của dịch vụ Load Balancer (LB) của VNG CLOUD. Nó là quá trình nhận yêu cầu của khách hàng ở Listener và phân phối chúng cho một số Member (server) theo các thuật toán đã được thiết lập. Nhờ vào tính năng này dịch vụ của người dùng được gia tăng năng lực xử lý với việc tạo nhiều hoặc một cụm server đứng sau LB.

Thuật toán Cân bằng tải sẽ xác định Member (server) nào được chọn khi cân bằng tải. Load Balancer của VNG CLOUD cung cấp ba loại thuật toán Cân bằng tải và tính năng Weight nâng cao có khả năng xử lý theo cấu hình của từng Member (server)  với nhiều mục đích khác nhau cho người dùng:

 **1. Round Robin** 







Round Robin là thuật toán lựa chọn các Member (server) theo trình tự. Theo đó, Load Balancer sẽ bắt đầu đi từ Member (server) số 1 trong danh sách của nó ứng với yêu cầu đầu tiên. Tiếp đó, nó sẽ di chuyển dần xuống trong danh sách theo thứ tự và bắt đầu lại ở đầu trang khi đến Member (server) cuối cùng.

 **2. Least Connection** 

Các request sẽ được chuyển vào server có ít kết nối (active connection) nhất trong hệ thống tại thời điểm hiện tại. Thuật toán này được coi như thuật toán động, vì nó phải đếm số kết nối đang hoạt động của server.

Ví dụ:

Chúng ta có 6 client request đến LB đang cân bằng tải cho 2 server bên dưới.





Step 1: Cả 6 client đều gửi request và chia đều cho 2 server.

Step 2: Giả sử client 1 và 3 ngắt kết nối trước khi client 6 gửi request, thì lúc này request của client 6 sẽ được chuyển đến server 1.











 **3. Source IP** 

Thuật toán này kết hợp địa chỉ IP nguồn và đích của client và server để tạo ra hash key duy nhất. Key này được sử dụng để phân bổ client đến một server cụ thể, và nó có thể được tạo lại nếu session bị timeout hay ngắt kết nối do một lý do nào đó. Khi đó request của client vẫn được chuyển đến cùng một server mà nó đã sử dụng trước đó. Đây là một phương pháp để đảm bảo rằng người dùng sẽ kết nối với cùng một server. Ví dụ: để giữ lại các mặt hàng trong giỏ hàng giữa các phiên.

 **Tính năng Weight** 

Weight hay "Trọng số" có khả năng xử lý theo cấu hình của từng Member (server) đích. Mỗi server được đánh giá bằng một số nguyên (giá trị trọng số Weight – mặc định giá trị là 1). Một server có khả năng xử lý gấp đôi server khác sẽ được đánh số lớn hơn gấp đôi và nhận được số request gấp đôi từ Load Balancer. Tính năng này thường sẽ kết hợp với các thuật toán bên trên để tạo ra nhiều mục đích sử dụng cho Khách hàng.

Ví dụ: Server 1 có khả năng xử lý gấp 5 lần Server 2. Chúng ta sẽ đánh "Weight = 5" cho server 1 và "Weight = 1" cho server 2.

![](images/storage/image2020-5-24_22-34-57.png)



*****

[[category.storage-team]] 
[[category.confluence]] 
