# Khởi tạo một OpenSearch Cluster

Để khởi tạo một OpenSearch Cluster Database trên hệ thống vDB, bạn có thể làm theo các bước sau:

**Bước 1:** Truy cập vào [https://vdb.console.vngcloud.vn/](https://vdb.console.vngcloud.vn/)

**Bước 2:** Chọn mục **Cluster** trên mục **OpenSearch**, sau đó chọn **Create a cluster..**

**Bước 3:** Tại màn hình khởi tạo OpenSearch Cluster, bạn cần nhập/ chọn:

* **Basic configuration:**
  * **OpenSearch Cluster name:** tên gợi nhớ của cluster. Tên cluster cần dài từ 5 tới 50 ký tự và có thể bao gồm các ký tự a-z, A-Z, 0-9, '-'.
  * **Tag:** bạn có thể thêm các tag để đánh dầu cluster theo nhu cầu.

<figure><img src="../../../.gitbook/assets/image (952).png" alt=""><figcaption></figcaption></figure>

* **Cluster specification**
  * **OpenSearch Version:** lựa chọn phiên bản OpenSearch Cluster mà bạn muốn sử dụng. Hiện tại chúng tôi đang hỗ trợ 2 phiên bản v2.15 và v2.17
  * **Instance**: lựa chọn loại CPU và package tương ứng mà bạn muốn cấu hình cho tất cả các VM (node) trong mỗi cluster.
  * **Number of nodes:** lựa chọn số lượng node (VM) mà bạn mong muốn sử dụng cho cluster. Hiện tại chúng tôi đang cung cấp các lựa chọn 3, 5, 7, 9 node. Nếu bạn muốn tạo một cluster có nhiều hơn 9 node, vui lòng liên hệ GreenNode để chúng tôi có thể hỗ trợ bạn.&#x20;
  * **Encryption volume:** lựa chọn có/ không sử dụng dịch vụ mã hóa các volume được sử dụng trên cluster. Nếu bạn chọn sử dụng phương án này, bạn cần chi trả thêm chi phí cho việc encryption.&#x20;
  * **Storage type:** lựa chọn loại ổ đĩa và IOPS mà bạn mong muốn sử dụng.
  * **Storage size:** lựa chọn kích thước ổ đĩa tương ứng.

<figure><img src="../../../.gitbook/assets/image (953).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (954).png" alt=""><figcaption></figcaption></figure>

* **Network settings:**
  * **VPC:** lựa chọn một VPC mà bạn muốn sử dụng. VPC được chọn chính là dải địa chỉ IP mà các node của Cluster sẽ sử dụng để giao tiếp.
  * **Subnet:** lựa chọn một Subnet trong VPC mà bạn đã lựa chọn. Đây là dải địa chỉ IP nhỏ hơn thuộc VPC. Mỗi node trong Cluster sẽ được gán một IP từ Subnet này.
  * **Public Allow CIDRs:** nhập CIDR bạn cho phép truy cập vào OpenSearch Dashboard và đẩy logs vào OpenSearch Received Logs.

<figure><img src="../../../.gitbook/assets/image (955).png" alt=""><figcaption></figcaption></figure>

* **Access control methods:**
  * **Master user password:** hệ thống sẽ tự động tạo username `master-user`, bạn cần nhập master user password và ghi nhớ sử dụng tài khoản này để truy cập vào OpenSearch Dashboard cũng như đẩy log vào Received log.

<figure><img src="../../../.gitbook/assets/image (956).png" alt=""><figcaption></figcaption></figure>

* **Cluster options:**
  * **Configuration group**: mặc định, tương ứng với mỗi OpenSearch version, chúng tôi sẽ tạo sẵn một **Default Configuration Group**. Bạn sẽ không thể thay đổi các tham số trong Default Configuration Group này. Nếu bạn muốn thay đổi tham số default, hãy thực hiện tự tạo Configuration Group mới và chỉnh sửa theo mong muốn của bạn.

<figure><img src="../../../.gitbook/assets/image (957).png" alt=""><figcaption></figcaption></figure>

* **Plugins**
  * **Plugin:** hiện tại, vDB đã tự động cài đặt trong OpenSearch Cluster của bạn các plugin phổ biến trong mục **Bundled Plugins**, ví dụ kNN. Bạn có thể tham khảo danh sách các plugin mặc định có sẵn tại [đây](../cac-tinh-nang-cua-opensearch-cluster/lam-viec-voi-plugin.md). Ngoài ra, bạn cũng có thể lựa chọn cài đặt thêm các plugin khác bằng cách chọn plugin tại mục **Additional Plugins**. Tham khảo danh sách các plugin có thể cài đặt theo lựa chọn của bạn tại [đây](../cac-tinh-nang-cua-opensearch-cluster/lam-viec-voi-plugin.md).

<figure><img src="../../../.gitbook/assets/image (958).png" alt=""><figcaption></figcaption></figure>

**Bước 5:** Chọn **Create Cluster.**

**Bước 6:** Thực hiện các bước thanh toán nếu bạn là người dùng trả trước.
