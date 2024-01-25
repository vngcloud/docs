Service Account là một danh tính mà bạn có thể tạo trong tài khoản Root User của bạn và có các quyền cụ thể. Nó có một số điểm tương đồng với IAM User Account. Để làm rõ hơn, Service Account và IAM User Account đều là các danh tính có chính sách quyền xác định những gì danh tính đó có thể và không thể làm với tài nguyên VNG Cloud. Tuy nhiên,Service Account được sử dụng bởi một ứng dụng hoặc máy móc, không phải là một người, để thực hiện các cuộc gọi API được ủy quyền và truy cập vào các tài nguyên được chỉ định.

![](images/storage/Identities-Service Account.drawio (1).png)


### 1. Cách Tạo Service Account?
Để tạo một Service Account mới:


1. Truy cập vào IAM Console: [https://hcm-3.console.vngcloud.vn/iam/](https://hcm-3.console.vngcloud.vn/iam/)
1. Nhấp vào  **"Service account"**  trong menu bên trái.
1. Nhấp vào  **"Create service account."** 
1. Nhập thông tin Service Account, bao gồm tên và mô tả tùy chọn.
1. Gắn các  **Policies**  cần thiết
1. Xem lại các thiết lập và nhấp  **"Create service account"**  ở góc phải trên cùng.
1. Lưu thông tin  **Client Secret Key** 



TipsHãy nhớ lưu Client Secret ở một nơi khác vì nó chỉ hiển thị một lần duy nhất.


### 2. Gán Quyền cho Service Account
Để gán Policies vào Service Account:


1. Truy cập vào IAM - Trang Service Acocunt với URL: [https://hcm-3.console.vngcloud.vn/iam/service-accounts](https://hcm-3.console.vngcloud.vn/iam/service-accounts)
1. Đăng nhập với tư cách là tài khoản Người dùng Gốc (Root User Account) hoặc User Account được cấp quyền truy cập. Bạn cần cung cấp tên người dùng/email và mật khẩu khi đăng nhập.
1. Tìm kiếm Service Account bằng cách nhập tên người dùng vào ô tìm kiếm và chọn kết quả đúng trong kết quả tìm kiếm.
1. Mặc định, bạn sẽ thấy tab " **Permission** " tại trang thông tin chi tiết của Service Account.
1. Nhấp vào nút " **Attach Policies** ", sau đó bạn sẽ thấy một cửa sổ nhảy lên chứa tất cả Policies.
1. Tìm kiếm các Policies hiện có bằng cách nhập chính xác tên Policies vào ô tìm kiếm.
1. Chọn Policies trong kết quả tìm kiếm và nhấp vào nút " **Attach** " ở góc dưới bên phải của cửa sổ nhảy lên.
1. Bây giờ, Service Account của bạn sẽ có tất cả các quyền hạn nằm trong các Policies đã gắn vào.

3. Cách Tạo Mối Quan Hệ Tin Cậy (Trusted Relationships) **Trusted Relationship**  là tính năng chia sẻ quyền giữa các  **Root User Accounts**  khác nhau, cho phép việc ủy quyền truy cập được điều chỉnh và bảo mật trên các thực thể quản trị riêng biệt. Với tính năng này, các  **Root User Accounts**  khác nhau có thể hợp tác trong khi vẫn duy trì tính riêng tư và ranh giới bảo mật. Tính năng này đặc biệt hữu ích trong các tình huống khi nhiều tổ chức hoặc nhóm cần làm việc cùng nhau trên các tài nguyên chia sẻ, đảm bảo sự hợp tác hiệu quả mà không đánh đổi tính bảo mật.

Tìm hiểu thêm về Trusted Relationship tại đây:
* [[Trusted Relationship|Trusted-Relationship]]

4. Quản lý thông tin xác thực Service AccountMột Service Account bao gồm thông tin xác thực (Client ID và Secret Key). Bạn cần lưu trữ Secret Key hoặc tải xuống sau khi tạo Service Account. Tuy nhiên, bạn cũng có thể tạo lại Secret Key bất kỳ lúc nào.


1. Truy cập trang Service account trong Bảng điều khiển IAM: [https://hcm-3.console.vngcloud.vn/iam/service-accounts](https://hcm-3.console.vngcloud.vn/iam/service-accounts)
1. Đăng nhập với tư cách là tài khoản Người dùng Gốc (Root User Account) hoặc User Account được cấp quyền truy cập. Bạn cần cung cấp tên người dùng/email và mật khẩu khi đăng nhập.
1. Tìm kiếm Service Account bằng cách nhập tên vào ô tìm kiếm và chọn đúng kết quả trong danh sách.
1. Nhấp vào tab " **Security credentials** " (Thông tin xác thực bảo mật) trong thông tin chi tiết của Service Account. Bạn sẽ thấy thông tin như hình dưới đây và bạn có thể thực hiện các hành động sau:
    1. Sao chép Client ID.
    1. Đặt lại Client Secret và nhớ lưu lại Secret mới.
    1. Kích hoạt/Tắt kích hoạt Service Account thông qua việc thay đổi Status

    

![](images/storage/image2023-7-27_13-51-21.png)


### 5. Gắn S3 keys và Swift users vào Service Account
Để gắn S3 Key và Swift user chúng tôi khuyến nghị bạn nên tuân theo các hướng dẫn dưới đây:


* [Understand how vStorage Credential works](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59804855)
* [Learn how to create a S3 key with IAM](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59804857)
* [Learn how to create a Swift user with IAM](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59804859)
* [Learn how to attach S3 Keys & Swift users to a Service Account](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59804923)


### 6. Xóa Service Account?
Bạn có thể xóa Service Account bằng cách tuân theo 2 tùy chọn dưới đây:


1.  **Xóa nhiều Service Account cùng một lúc:** 


    * Truy cập vào IAM với Tài khoản người dùng Gốc.
    * Nhấp vào  **"Service account"**  (Tài khoản Dịch vụ) trong menu bên trái.
    * Chọn các Service Account mà bạn muốn xóa (một nút " **Delete** " sẽ được bật ở góc trên bên phải khi bạn chọn ít nhất một tài khoản).
    * Nhấp vào nút " **Delete** " (Xóa), một hộp thoại xác nhận sẽ xuất hiện để đảm bảo bạn không xóa nhầm tài khoản, sau đó nhấp vào nút " **Confirm** " (Xác nhận) để hoàn tất quy trình.

    
1.  **Xóa một Service Account: ** Chúng tôi khuyến nghị bạn nên truy cập vào thông tin chi tiết của Service Account và thực hiện xóa từ đó để đảm bảo bạn không xóa nhầm tài khoản.





*****

[[category.storage-team]] 
[[category.confluence]] 
