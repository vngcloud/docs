# Tạo kết nối VPC

**Thực hiện các bước sau để thực hiện việc tạo một kết nối VPC giữa hai region:**

**Bước 1:** Truy cập thành công vào VNG Cloud, tại màn hình Console chọn đến dịch vụ vNetwork;

**Bước 2:** Tại thanh menu bên trái của giao diện vNetwork, chọn mục Cross Connect;

**Bước 3:** Màn hình được điều hướng tới màn hình Danh sách Cross Connect;

**Bước 4:** Tại màn hình danh sách các Cross Connect, nhấn chọn vào Cross Connect đã tạo trước;

**Bước 5:** Tại màn hình xem chi tiết Cross Connect, ở Tab Connections, nhấn chọn "<mark style="color:blue;">**Thêm kết nối**</mark>" để thực hiện việc tạo kết nói VPC giữ hai vùng;

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

**Bước 6:** Tại màn hình Add VPC's Connections:

* Người dùng phải chọn trước <mark style="color:blue;">**"VPC của Requester Region"**</mark> ;
* Hệ thống dựa vào VPC vừa chọn của Requester Region sẽ [kiểm tra điều kiện kết nối](kiem-tra-dieu-kien-ket-noi-vpc.md) và hiển thị các <mark style="color:blue;">**"VPC của Accepter Region"**</mark> mà người dùng có thể tạo kết nối;

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

**Bước 7**: Sau khi chọn cặp VPC kết nối, hẫy nhấn "<mark style="color:blue;">**Thêm**</mark>" để thêm mới cặp kết nối VPC.&#x20;

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Ghi chú:**

* **Requester Region** và **Accepter Region** được hiểu là hai region độc lập để tạo thành một kết nối Cross Connect. (Requester Region được mặc định chọn theo region đang được chọn khi truy cập vào vServer)
* VPC của mỗi Region phải được tạo từ trước tại vServer; ( xem [Tạo VPC](../../vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc.md#virtualprivatecloud-vpc-taovpc)).
{% endhint %}

