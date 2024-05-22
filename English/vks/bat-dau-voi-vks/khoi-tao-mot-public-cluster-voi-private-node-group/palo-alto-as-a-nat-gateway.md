# Palo Alto as a NAT Gateway

Sử dụng hướng dẫn bên dưới dể làm việc với Private Node group thông qua Palo Alto.

## Điều kiện cần

Để có thể sử dụng Palo Alto làm NAT Gateway cho Cluster trên hệ thống VKS, bạn cần có:

* Một **server (VM) Windows** đã được khởi tạo trên hệ thống **vServer** với cấu hình như sau:

<table><thead><tr><th width="240">Item</th><th>Cấu hình</th></tr></thead><tbody><tr><td>Flavor</td><td>2x4</td></tr><tr><td>Volume</td><td>20 GB</td></tr><tr><td>VPC</td><td>10.76.0.0/16</td></tr><tr><td>Subnet</td><td>10.76.0.4/24</td></tr><tr><td>Network Interface 1</td><td>10.76.0.3</td></tr></tbody></table>

* Một **server (VM) Palo Alto** được khởi tạo trên hệ thống **vMarketPlace** theo hướng dẫn bên dưới với cấu hình như sau:

<table><thead><tr><th width="244">Item</th><th>Cấu hình</th></tr></thead><tbody><tr><td>Flavor</td><td>2x8</td></tr><tr><td>Volume</td><td>60 GB</td></tr><tr><td>VPC</td><td>10.76.0.0/16</td></tr><tr><td>Network Interface 1</td><td>10.76.255.4</td></tr><tr><td>Network Interface 2</td><td>10.76.0.4</td></tr></tbody></table>

## Khởi tạo Palo Alto <a href="#toc165621057" id="toc165621057"></a>

**Bước 1:** Truy cập vào [https://marketplace.console.vngcloud.vn/](https://marketplace.console.vngcloud.vn/)

**Bước 2:** Tại màn hình chính, thực hiện tìm kiếm **Palo Alto**, tại dịch vụ **Palo Alto**, chọn **Launch**.

**Bước 3:** Lúc này, bạn cần thiết lập cấu hình cho **Palo Alto.** Cụ thể, bạn có thể chọn **Volume, IOPS, Network, Security Group** mong muốn. **Bạn cần lựa chọn VPC và Subnet giống với VPC và Subnet mà bạn lựa chọn sử dụng cho Cluster của bạn.** Ngoài ra bạn cũng cần chọn Một Server Group đã tồn tại hoặc chọn **Dedicated SOFT ANTI AFFINITY group** để chúng tôi tự động tạo một server group mới.

**Bước 4:** Tiến hành thanh toán như các tài nguyên bình thường trên VNG Cloud.

***

## Cấu hình thông số cho Palo Alto <a href="#toc165621058" id="toc165621058"></a>

**Bước 1:** Sau khi khởi tạo Palo Alto từ vMarketPlace theo hướng dẫn bên trên, bạn có thể truy cập vào giao diện vServer tại [đây](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) để kiểm tra server chạy Palo Alto đã được khởi tạo xong chưa.

**Bước 2: Sau khi server chạy Palo Alto được khởi tạo thành công**. Để vào GUI của Palo Alto bạn cần có 1 vServer chạy Windows. Sau đó bạn truy cập vào bằng IP Internal Interface với tên đăng nhập và mật khẩu mặc định là: **admin/admin**

Lưu ý: Về phần Network của vServer Windows để truy cập vào GUI của Palo Alto. Bạn cần tạo cùng VPC và sử dụng subnet khác với subnet có priority là 1 khi khởi tạo Palo Alto

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

**Bước 3**: Sau khi đăng nhập xong, bạn cần thực hiện thay đổi mật khẩu lần đầu. Hãy nhập mật khẩu mới theo mong muốn của bạn.

**Bước 4:** Bạn cần tiến hành khởi tạo 1 Zone Inside và 1 Zone Outside theo hướng dẫn bên dưới:

* Chọn bút **Add**

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Đặt tên cho **Zone**: **Inside** sau đó chọn **OK**

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

* Làm tương tự đối với **Zone Outside**

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

**Bước 5**: Cấu hình cho **External Interface**

* Interface Type: **Layer 3**
* Virtual Router: **default**
* Security Zone: **Outside**

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

* Chuyển sang **Tab IPv4** và chọn **Add** để nhập **Static IP** cho **External Interface**

<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

* Để lấy thông tin IP này bạn vào phần **Network Interface** của **Palo Alto** để xem thông tin

<figure><img src="../../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

* Chuyển sang tab **Advanced**, ở phần **MTU** bạn cần chỉnh thành **1400**

<figure><img src="../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

**Bước 6:** Thực hiện cấu hình tương tự cho các **Internal Interface**

<figure><img src="../../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

* Tại tab **IPv4:** bạn tiến hành thiết lập **Static IP**

<figure><img src="../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

* Chuyển sang tab **Advanced**, ở phần **MTU** bạn chỉnh thành 1400

<figure><img src="../../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

**Bước 7:** Tạo **static route**

* Vào phần **Network** -> **Virtual Routers**-> Chọn **default**-> Chuyển sang mục **Static Routes**

<figure><img src="../../../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

* Thực hiện tạo 1 **route** như hình bên dưới

<figure><img src="../../../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>

**Bước 8:** Tạo **Security Policy Rule**

* Vào phần **Policies** -> **Security** ->**Add**
* Tại tab **General**, bạn cần đặt tên cho rule

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

* Tại tab **Source**, thiết lập các thông tin như **Source Zone**, **Source Address**, **Source User, Source Device**

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

* Tại tab **Destination**, thiết lập các thông tin như **Destination Zone, Destination Address, Destination Device**

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

* Tại tab **Application**, thiết lập các thông tin như **Application, Depend On**

<figure><img src="../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

* Tại tab **Service/URL Category**, thiết lập các thông tin như **Service, URL Category**

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

* Tại tab **Actions**, thiết lập các thông tin như **Action, Log, Profile, Other Settings**

**Bước 9**: Tạo **rule NAT** để các VM có thể đi ra Internet

* Vào phần **Policies** -> **NAT** -> **Add**

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

* Tại tab **General** đặt tên cho **NAT rule**

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

* Tại tab **Original Packe**t chọn **Source Zone, Destination Zone, Destination Interface, Service, Source Address, Destination Address**

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

* Tạo tab **Translated Packet** thực hiện cấu hình như hình bên dưới

Lưu ý: Cần thay đổi **IP Address** thành địa chỉ **Static IP** mà bạn đã cấu hình ở bước 6

<figure><img src="../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

**Bước 10**: Tiến hành **Commit**

<figure><img src="../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

***

## Khởi tạo Route Table <a href="#khoitaomotpublicclustervoiprivatenodegroup-khoitaoroutetable" id="khoitaomotpublicclustervoiprivatenodegroup-khoitaoroutetable"></a>

Sau khi Palo Alto được khởi tạo và cấu hình thành công, bạn cần tạo một Route table để kết nối tới các mạng khác nhau. Cụ thể thực hiện theo các bước sau để tạo Route table:

**Bước 1:** Truy cập vào [https://hcm-3.console.vngcloud.vn/vserver/network/route-table](https://hcm-3.console.vngcloud.vn/vserver/network/route-table)

**Bước 2:** Tại thanh menu điều hướng, chọn **Tab Network/ Route table.**

**Bước 3:** Chọn **Create Route table.**

**Bước 4:** Nhập tên mô tả cho Route table. Tên Route table có thể bao gồm các chữ cái (a-z, A-Z, 0-9, '\_', '-'). Độ dài dữ liệu đầu vào nằm trong khoảng từ 5 đến 50. Nó không được bao gồm khoảng trắng ở đầu hoặc ở cuối.

**Bước 5:** Chọn **VPC** cho Route table của bạn, nếu chưa có VPC cần tạo mới một VPC theo hướng dẫn tại [Trang VPC](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648039). **VPC sử dụng để thiết lập Route table phải là VPC được chọn sử dụng cho Palo Alto và Cluster của bạn.**

**Bước 6**: Chọn **Create** để tạo mới Route table.

**Bước 7:** Chọn <img src="https://docs-admin.vngcloud.vn/download/thumbnails/73762068/image2024-4-16_15-40-3.png?version=1&#x26;modificationDate=1713256805000&#x26;api=v2" alt="" data-size="line">tại Route table vừa tạo sau đó chọn **Edit Routes.**

**Bước 8:** Tại phần thêm mới **Route** hãy nhập vào các thông tin:

* Đối với Destination, hãy nhập **Destination CIDR là 0.0.0.0/0**
* Đối với Target, hãy nhập **Target CIDR là địa chỉ IP Network Interface 2 của Palo Alto.**

Ví dụ:

<figure><img src="../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

***

## **Kiểm tra kết nối**

* Tiến hành ping 8.8.8.8 hoặc google.com

<figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>
