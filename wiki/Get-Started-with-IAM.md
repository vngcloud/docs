Trong phần này, chúng ta sẽ tìm hiểu về các khái niệm cơ bản về Quản lý Định Danh và Truy cập (Identity and Access Management - IAM) và cách bắt đầu quản lý quyền truy cập vào các tài nguyên đám mây một cách an toàn.


### 1. Truy cập IAM Console
Trước khi bắt đầu, mời bạn tham khảo hướng dẫn đăng nhập với Root User Account và IAM User Account tại đây:


* [[How to Login into VNG Cloud|How-to-Login-into-VNG-Cloud]]

IAM Console là giao diện người dùng dựa trên web, cho phép bạn quản lý IAM User Account, Group, Service Account và Policy trong môi trường điện toán đám mây của bạn. Nó cung cấp giao diện một cách trực quan để kiểm soát quyền truy cập vào các tài nguyên của bạn và cấu hình các thiết lập bảo mật.

Cách truy cập Bảng điều khiển IAM?
1. Mở trình duyệt web của bạn và truy cập vào URL IAM Console: [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/)
1. Đăng nhập với tư cách là tài khoản Người dùng Gốc (Root User Account) hoặc User Account được cấp quyền truy cập. Bạn cần cung cấp tên người dùng/email và mật khẩu khi đăng nhập.
1. Sau khi đăng nhập, bạn sẽ thấy giao diện IAM Console, nơi cung cấp tổng quan về cấu hình IAM của bạn.


### 2. Hiểu về IAM User Account & User Group
Root User AccountRoot User Account là một thực thể bạn tạo đầu tiên trong VNG Cloud và sử dụng, mặc định có quyền truy cập đầy đủ vào tất cả các sản phẩm/dịch vụ và tài nguyên của VNG Cloud trong tài khoản đó.

IAM User AccountIAM User Account đại diện cho các danh tính riêng lẻ liên kết với Root User Account của bạn. Mỗi người dùng có một tập hợp duy nhất các chứng chỉ bảo mật, chẳng hạn như tên người dùng và mật khẩu, hoặc các khóa truy cập, để xác thực danh tính của họ.

IAM User GroupIAM User Group là tập hợp các IAM User Account chia sẻ các yêu cầu truy cập tương tự. Việc nhóm hóa IAM User Account giúp đơn giản hóa quản lý quyền bằng cách cấp quyền cho một nhóm thay vì từng IAM User Account riêng lẻ. Điều này cải thiện tính nhất quán và hiệu quả trong kiểm soát truy cập.

Cách Tạo IAM User Account?Để tạo tài khoản người dùng IAM mới:


1. Truy cập IAM Console.
1. Nhấp vào  **"User account"**  trong menu bên trái.
1. Nhấp vào  **"Create a user account."** 
1. Nhập chi tiết tài khoản người dùng, bao gồm tên người dùng và mật khẩu.
1. Xem lại các thiết lập và nhấp vào  **"Create a user account."**  ở góc trên bên phải.

Đăng nhập VNG Cloud với IAM User Account:


* [[How to Login into VNG Cloud|How-to-Login-into-VNG-Cloud]]

Cách Tạo IAM User Group?Để tạo IAM User Group mới:


1. Truy cập IAM Console.
1. Nhấp vào  **"Group"**  trong menu bên trái.
1. Nhấp vào  **"Create new group."** 
1. Cung cấp tên nhóm và mô tả tùy chọn.
1. Đính kèm các  **IAM Policies**  liên quan vào Group để xác định quyền của nhóm.
1. Thêm các  **User Accounts**  cần quản lý vào Group
1. Xem lại các thiết lập và nhấp vào " **Create group** ."


### 3. IAM Policy và Quyền Truy cập
IAM PolicyIAM Policy là các tài liệu JSON xác định các quyền và quy tắc truy cập tài nguyên. Các Policies này được đính kèm vào IAM User Account, Group hoặc Service Account để kiểm soát hành động mà họ có thể thực hiện trên các tài nguyên cụ thể. IAM Policies tuân thủ nguyên tắc "cho phép" hoặc "từ chối", tức là chúng rõ ràng cấp quyền hoặc từ chối truy cập tài nguyên và hành động.

Quyền Truy cậpQuyền truy cập IAM xác định những hành động mà các thực thể IAM (IAM User Account, Group và Service Account) được phép hoặc từ chối thực hiện trên các tài nguyên VNG Cloud. Các hành động này bao gồm các cấp độ truy cập như xem danh sách, quyền đọc và ghi trên tài nguyên, hoặc quản lý IAM User Account và Group.

Cách Cấu hình Quyền trong IAM Policy?
1. Truy cập IAM Console.
1. Nhấp vào  **"Policy"**  trong menu bên trái.
1. Nhấp vào  **"Create a policy."** 
1. Cung cấp tên Policy và mô tả tùy chọn.
1. Nhấp vào  **"Next step"**  để tiếp tục cấu hình quyền.
1. Chọn một  **Product/Service**  cụ thể trong hệ thống VNG Cloud cần cấu hình.
1. Chỉ định các **Actions**  được phép trên tài nguyên của sản phẩm.
1. Chọn các  **Resources**  áp dụng các hành động (Tất cả các tài nguyên / Tài nguyên cụ thể).
1. Cung cấp các  **Request conditions**  về thời gian áp dụng.
1. Xem lại các thiết lập và nhấp vào  **"Create policy."** 

Cách Gán Quyền cho Thực thể IAM?
1. Tạo một  **IAM Policy**  mới hoặc sử dụng Policy hiện có phù hợp với yêu cầu kiểm soát truy cập của bạn.
1.  **Gắn Policy**  vào IAM User Account, Group và Service Account thích hợp.
1. Xem xét và xác nhận các Policies đã gán để đảm bảo phù hợp với nguyên tắc đặc quyền tối thiểu.

Hãy nhớ tuân thủ nguyên tắc đặc quyền tối thiểu khi gán quyền cho các thực thể IAM, chỉ cấp quyền tối thiểu cần thiết cho IAM User Account, Group và Service Account thực hiện nhiệm vụ của họ.

Xin chúc mừng! Bạn đã nắm được cách cơ bản để bắt đầu sử dụng IAM. Bạn có thể tạo IAM User Account, Group và Service Account, và gán quyền cho họ thông qua các chính sách IAM để kiểm soát quyền truy cập vào các tài nguyên đám mây của bạn. Tiếp theo, chúng ta sẽ tìm hiểu sâu hơn về việc viết các tùy chỉnh cho IAM Policies để kiểm soát truy cập chi tiết hơn.



Chủ đềHướng dẫn đăng nhập VNG Cloud Service: [[How to Login into VNG Cloud|How-to-Login-into-VNG-Cloud]]





*****

[[category.storage-team]] 
[[category.confluence]] 
