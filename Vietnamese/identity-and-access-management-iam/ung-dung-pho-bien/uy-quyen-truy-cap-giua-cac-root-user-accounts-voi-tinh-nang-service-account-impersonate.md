# Uỷ quyền truy cập giữa các root user accounts với tính năng Service Account Impersonate

Khi có nhu cầu phân quyền cho phép IAM User Account của một Root User Account được quyền truy cập các tài nguyên trong một Root User Account khác, bạn cần sử dụng tính năng Impersonate của Service Account. Ví dụ như bạn có các tài nguyên của vServer ở Root User Account B, khi bạn muốn User Account: System1 thuộc Root User Account A được quyền quản lý tất cả tài nguyên vServer của Root User Account B, thì bạn sử dụng tính năng Impersonate của Service Account, mô hình như bên dưới:

Để thiết lập IAM theo mô hình trên chúng ta sẽ có 2 giai đoạn thiết lập ở 2 Root User Account như sau:

**Giai đoạn 1**: Thiết lập tại Root User Account B (người muốn chia sẻ quyền)

* **Bước 1.1**: Tạo Service Account AllowAccessFromRootUserAccountA, gắn quyền vServerFullAccess và thiết lập Trust với Root User Account A

**Giai đoạn 2**: Thiết lập tại Root User Account A (người được uỷ quyền)

* **Bước 2.1**: Tạo User: System1 nếu chưa có User Account (lưu ý rằng nếu đã có sẵn User: System1, cần đảo bảo User: System1 không có quyền gì hoặc không có các quyền chồng lấn với hướng dẫn)
* **Bước 2.2**: Tạo Policy: ImpersonateToRootUserAccountB để cấp quyền impersonate cho Service Account đã tạo ở giai đoạn 1
* **Bước 2.3**: Gắn Policy: ImpersonateToRootUserAccountB cho User: System1 để cho phép System1 có quyền sử dụng Service Account đã tạo ở giai đoạn 1
* **Bước 2.4**: Đăng nhập và kiểm tra quyền của User: System1

Trước tiên để thực hiện theo chi tiết hướng dẫn bạn cần thu thập thông tin user ID của 2 Root User Account, để có thể lấy thông thông tin User ID, bạn nhấn vào tên email ở góc trên bên phải trình duyệt

Thông tin của 2 Root User Account ở hướng dẫn này như sau

**Root User Account A có Email: demoiaas@vng.com.vn, User ID: 53461**

**Root User Account B có Email: iaas.dev4@vng.com.vn, User ID: 60108**

Chi tiết các bước như sau

**Giai đoạn 1: Thiết lập tại Root User Account B (người muốn chia sẻ quyền)**

**Bước 1.1: Tạo Service Account AllowAccessFromRootUserAccountA, gắn quyền vServerFullAccess và thiết lập Trust với Root User Account A**

Để tạo Service Account bạn qua tab Service Account ở trang IAM tại [đây](https://iam.console.vngcloud.vn/service-accounts), nhấn **Create a Service Account**, **đặt tên** cho Service Account: AllowAccessFromRootUserAccountA và nhấn vào **Add a root user account** để thiết lập Trust với Root User Account A

Điền thông tin User ID của Root User Account A để thiết lập **Trust** giữa Root User Account A và Service Account này, nhấn **Next step**

Tìm kiếm và **chọn policy: vServerFullAccess, nhấn Create Service Account** để tạo

Lưu lại thông tin Client ID và Secret Key của Service Account nếu có nhu cầu sử dụng trực tiếp Service Account này.

Lưu lại thông tin Service Account ID để thiết lập ở giai đoạn 2

Như vậy là bạn đã tạo thành công Service Account: **AllowAccessFromRootUserAccountA,** có quyền vServerFullAccess và thiết lập **Trust** với Root User Account A, với việc thiết lập Trust này, Root User Account A có thể cấp quyền cho 1 IAM User thuộc Root User Account A có quyền sử dụng Service Account: **AllowAccessFromRootUserAccountA** để quản lý vServer thuộc Root User Account B.

**Giai đoạn 2: Thiết lập tại Root User Account A (người được uỷ quyền)**

**Bước 2.1: Tạo User: System1 nếu chưa có User Account (lưu ý rằng nếu đã có sẵn User: System1, cần đảo bảo User: System1 không có quyền gì hoặc không có các quyền chồng lấn với hướng dẫn)**

Tiến hành tạo User Account bằng cách truy cập vào tab User Account ở trang quản lý IAM tại [đây](https://iam.console.vngcloud.vn/user-accounts), nhấn **Create a User Account,** điền thông tin Username và Password, sau đó nhấn **Create User Account**&#x20;

Sau khi tạo thành công User Account, sẽ được liệt kê ở trang User Account.

**Bước 2.2: Tạo Policy: ImpersonateToRootUserAccountB để cấp quyền impersonate cho Service Account đã tạo ở giai đoạn 1**

Để tạo Policy bạn qua tab Policy ở trang IAM tại [đây](https://iam.console.vngcloud.vn/policies), nhấn **Create a Policy**, **đặt tên** cho Policy: **ImpersonateToRootUserAccountB** và nhấn **Next step**

Chọn **Product**: **iam, tìm kiếm và chọn action: ImpersonateServiceAccount**

Sau đó tại mục **Resource,** nhấn vào **mũi tên chỗ Resource** để chọn thông tin Resource, nhấn **Add a service-account** để thêm User ID của Root User Account B và Service Account ID của AllowAccessFromRootUserAccountA mà đã thu thập ở giai đoạn 1

**Điền thông tin User ID** của Root User Account B và **Service Account ID** của AllowAccessFromRootUserAccountA mà đã thu thập ở giai đoạn 1 vào Popup đc hiển thị lên

Sau đó nhấn **Create Policy** để tạo Policy&#x20;

Như vậy bạn đã hoàn thành việc tạo Policy cho phép Impersonate Service Account: AllowAccessFromRootUserAccountA của User Account B

**Bước 2.3: Gắn Policy: ImpersonateToRootUserAccountB cho User: System1 để cho phép System1 có quyền sử dụng Service Account đã tạo ở giai đoạn 1**

Sau khi tạo thành công Policy: ImpersonateToRootUserAccountB, bạn tiến hành gắn Policy này cho User: System1, bạn có thể thực hiện ở User Account hoặc Policy, ở đây chúng tôi sẽ hướng dẫn ở Policy, **nhấn vào tên của Policy** để vào trang chi tiết Policy

**Chọn tab Policy usage** và **nhấn Attach** để thêm User: System1

**Chọn User: System1** và **nhấn Add**

Sau khi thêm User: System1 vào Policy: ImpersonateToRootUserAccountB, lúc này User: System1 đã có quyền để có thể Impersonate Service Account: AllowAccessFromRootUserAccountA để quản lý các Server thuộc User Account B

**Bước 2.4: Đăng nhập và thực hiện Impersonate để kiểm tra quyền của User: System1**

Lúc này bạn có thể đăng nhập vào User: System1 để kiểm tra quyền

Truy cập vào vServer tại [đây](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server), khi chưa đăng nhập bất kì tài khoản nào bạn sẽ được chuyển hướng sang trang sign-in chọn "**Sign-in With IAM User Account**"

Điền thông tin root user account email mà User: System1 trước đó đã được tạo, thông tin IAM username và password của User: System1, nhấn **Sign-in with IAM User Account**

Thực hiện Impersonate qua Service Account: AllowAccessFromRootUserAccountA bằng cấp **nhấn vào email** ở góc trên bên phải và chọn **Impersonate service account**

**Điền Service account ID** của Service Account: AllowAccessFromRootUserAccountA và **tên hiển thị khi Impersonate**, **chọn Go** để thực hiện Impersonate

Lúc này bạn thấy User: System1 đã thực hiện thành công việc Impersonate qua Root User Account B (thông tin email: iaas.dev4@vng.com.vn, Account ID: 60108) với Service Account: AllowAccessFromRootUserAccountA

Và có đầy đủ quyền trên vServer, ở bên dưới là System1 đang tắt 1 server

Như vậy là bạn đã thực hiện thành công việc thiết lập cho phép User: System1 thuộc Root User Account A có đầy đủ quyền quản lý vServer của Root User Account B.
