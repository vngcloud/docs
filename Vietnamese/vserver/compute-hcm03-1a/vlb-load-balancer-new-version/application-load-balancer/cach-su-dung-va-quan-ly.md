# Cách sử dụng và quản lý

Trong phần này, chúng ta sẽ tìm hiểu về cách sử dụng và quản lý một Application Load Balancer (ALB) theo cách cơ bản nhất, từ đó cung cấp cái nhìn tổng quan hơn về việc sử dụng Application Load Balancer.

#### Trước khi bắt đầu <a href="#gettingstarted-truockhibatdau" id="gettingstarted-truockhibatdau"></a>

* Để bắt đầu sử dụng Application Load Balancer, bạn cần có ít nhất **một Virtal Private Cloud (VPC)**, tham khảo hướng dẫn [Virtual Private Cloud (VPC)](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648039).
* Tìm hiểu cách **truy cập VNG Cloud Portal** với Root User Account hoặc IAM User Account, tham khảo hướng dẫn [How to Login into VNG Cloud](https://docs.vngcloud.vn/display/ONVINA/How+to+Login+into+VNG+Cloud).
* Trong trường hợp người dùng muốn bắt đầu với IAM User Account, tham khảo hướng dẫn [IAM for vServer](https://docs.vngcloud.vn/display/ONVINA/IAM+for+vServer).
* Đối với Application Load Balancer, yêu cầu có ít nhất một chứng chỉ TLS/SSL khi **cấu hình HTTPS Listener**, tham khảo hướng dẫn [Upload a certificate](https://docs.vngcloud.vn/display/vServer/Upload+a+certificate).&#x20;

#### 1. Truy cập vLB Console <a href="#gettingstarted-1.truycapvlbconsole" id="gettingstarted-1.truycapvlbconsole"></a>

vLB Console là giao diện người dùng dựa trên web, cho phép bạn quản lý các Load Balancers trong môi trường điện toán đám mây của bạn. Nó cung cấp giao diện một cách trực quan để kiểm soát và quản lý Load Balancer của bạn.

**Cách truy cập Bảng điều khiển vLB**

* Truy cập từ trang chủ vConsole: [https://dashboard.console.vngcloud.vn/](https://dashboard.console.vngcloud.vn/)
  * Tại mục **"VNG Cloud Service"** trên giao diện, click **chọn "vServer"**, sau đó click **chọn "vLB"** từ danh sách sản phẩm/dịch vụ tương ứng bên phải
* Truy cập từ trang chủ vServer: [https://hcm-3.console.vngcloud.vn/vserver/](https://hcm-3.console.vngcloud.vn/vserver/)
  * Tại trang chủ vServer, điều hướng đến vLB portal bằng cách click **chọn "Load Balancers" trong mục "Load Balancing"** tại thanh menu bên trái.
* Truy cập trực tiêp đến vLB Portal thông qua đường dẫn: [https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb](https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb)

#### 2. Khởi tạo ALB <a href="#gettingstarted-2.khoitaoalb" id="gettingstarted-2.khoitaoalb"></a>

**Cách khởi tạo một Application Load Balancer**

1. **Tại trang chủ Load Balancer, click chọn "Create a Load Balancer".**
2. **Chọn cấu hình Load Balancer**
   * _**Tên Load Balancer**_**:** Trường hợp người dùng không chủ động điền tên Load Balancer, hệ thống sẽ tự động sinh ra tên Load Balancer.
   * _**Layer**_**:** Chọn **"Application - HTTP/HTTPS"**
   * _**Cơ chế/Scheme**_:
     * Chọn **Internet facing** nếu: Cho phép truy cập từ Internet
     * Chọn **Internal** nếu: Chỉ cho phép truy cập với mạng nội bộ
   * _**Load Balancer Package**_: Chọn gói khởi tạo phù hợp với nhu cầu và mục đích sử dụng, lưu ý rằng gói này là yếu tố chính dùng để tính chi phí khởi tạo và vận hành Load Balancer của bạn
   * _**Cài đặt Network**_**: Chọn Virtual Private Cloud (VPC) và Subnet** có sẵn từ danh sách VPC của bạn, trường hợp chưa khởi tạo VPC, tham khảo hướng dẫn [Virtual Private Cloud (VPC)](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648039).
3. **Chọn cấu hình Listener**
   * **Tên Listener:** Trường hợp người dùng không chủ động điền tên Listener, hệ thống sẽ tự động sinh ra tên Listener.
   * **Giao thức & Cổng (Protocol & Port)**
     * Trường hợp chọn Giao thức (Protocol) = **HTTP**: Người dùng cần **chọn Port** (mặc định điền sẵn Port **80**) và **Header** (mặc định điền sẵn X-Fowarded-For, X-Forwarded-Proto, X-Fowarded-Port, có thể bỏ chọn Header nếu không có nhu cầu).
     * Trường hợp chọn Giao thức (Protocol) = **HTTPS**: Người dùng cần **chọn Port** (mặc định điền sẵn Port **443**) và **Certificate** (tham khảo hướng dẫn [Upload a certificate](https://docs.vngcloud.vn/display/vServer/Upload+a+certificate) nếu chưa có Certificate).
4. **Chọn cấu hình Pool mặc định**
   * **Tên Pool**: Trường hợp người dùng không chủ động điền tên Pool, hệ thống sẽ tự động sinh ra tên Pool.
   * **Giao thức HTTP mặc định**
   * **Thuật toán:** Chọn thuật toán cân bằng tải phù hợp
   * **Cài đặt Health Check**: Giao thức: TCP / HTTP (nhập đường dẫn mặc định trong trường hợp chọn Giao thức HTTP)
5. **Chọn Pool Member: Thêm các máy chủ backend vào Pool**
   * **Chọn Pool Member** từ một danh sách các máy chủ backend khả dụng thuộc Load Balancer Network (cùng subnet với LB)
   * **Click nút "Gắn / Attach"** để thực hiện việc thêm máy chủ thành viên
6. **Kiểm tra thông tin khởi tạo: Người dùng có thể kiểm tra thông tin cấu hình và đơn giá trước khi hoàn tất khởi tạo, phần thông tin này sẽ được hiển thị phía bên phải màn hình nhập liệu**
   * **Tab "Tóm tắt / Summary"**: Kiểm tra làn lượt các thông tin cấu hình Load Balancer, Listener, Pool và Pool Member
   * **Tab " Danh sách / Item list":** Kiểm tra thông tin Load Balancer Package và Chi phí
7. **Hoàn tất khởi tạo: Sau khi hoàn tất việc cấu hình và kiểm tra thông tin, click nút "Tạo load Balancer / Create Load Balancer" để hoàn tất việc khởi tạo.**
   * Đối với người dùng trả trước, bạn sẽ được điều hướng đến trang thanh toán, tại đây bạn cần cung cấp một phương thức thanh toán khả dụng để hoàn tất việc khởi tạo Application Load Balancer. Tham khảo thêm hướng dẫn [Thanh toán trực tuyến](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49649313)

#### 3. Quan sát và kiểm tra ALB <a href="#gettingstarted-3.quansatvakiemtraalb" id="gettingstarted-3.quansatvakiemtraalb"></a>

* Sau khi hoàn tất khởi tạo thành công, hệ thống sẽ điều hướng người dùng đến trang danh sách Load Balancer, tại đây người dùng có thể theo dõi trạng thái khởi tạo Load Balancer từ **Creating (đang khởi tạo)** đến khi **Active (Khởi tạo thành công).**
* Sau khi khởi tạo thành công, người dùng có thể truy cập vào trang chi tiết Load Balancer để quan sát và kiểm tra tính đúng đắn của Load Balancer.

Trên đây là các hướng dẫn cơ bản trong việc khởi tạo Application Load Balancer một cách nhanh chóng nhất. Ngoài ra, còn có các cấu hình nâng cao cho từng nhu cầu sử dụng Load Balancer khác nhau. Cùng tìm hiểu chi tiết cách hoạt động cũng như các tính năng nâng cao của một Application Load Balancer thông qua chuỗi bài viết đưới đây:



Chủ đề liên quan

* [Manage Load balancer](https://docs.vngcloud.vn/display/vServer/Manage+Load+balancer)
* [Listener](https://docs.vngcloud.vn/display/vServer/Listener)
* [Pool](https://docs.vngcloud.vn/display/vServer/Pool)
* [Certificate](https://docs.vngcloud.vn/display/vServer/Certificate)
* [Monitor your load balancers](https://docs.vngcloud.vn/display/vServer/Monitor+your+load+balancers)