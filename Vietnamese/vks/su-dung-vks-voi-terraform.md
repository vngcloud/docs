# Sử dụng VKS với Terraform

### Terraform là gì?

Terraform là một cơ sở hạ tầng nguồn mở dưới dạng công cụ mã cho phép người dùng quản lý cơ sở hạ tầng của họ một cách dễ dàng và hiệu quả trên các nền tảng đám mây khác nhau, chẳng hạn như VNG Cloud, AWS, Google Cloud và Azure. Máy chủ Terraform đề cập đến phiên bản của công cụ Terraform đang chạy trên một máy chủ hoặc máy cụ thể. Đây là nơi mã cơ sở hạ tầng được viết và thực thi, cho phép người dùng tạo, sửa đổi và hủy tài nguyên trên nền tảng đám mây.

Bản thân Terraform không có giao diện người dùng đồ họa, thay vào đó người dùng tương tác với nó bằng giao diện dòng lệnh. Terraform yêu cầu tài khoản và khóa của nhà cung cấp đám mây được định cấu hình cùng với tệp cấu hình Terraform để thực thi cơ sở hạ tầng dưới dạng mã. Ngoài ra, Terraform có thể hoạt động trong môi trường nhóm nơi nhiều người dùng có thể cộng tác trên cùng một cơ sở mã cơ sở hạ tầng, khiến nó trở thành một công cụ mạnh mẽ và linh hoạt để quản lý cơ sở hạ tầng đám mây.

***

#### Để sử dụng VKS với Terraform, bạn cần làm các bước sau đây: <a href="#quanlyvcontainervoiterraform-dequanlyvcontainervoiterraform-bancanlamcacbuocsauday" id="quanlyvcontainervoiterraform-dequanlyvcontainervoiterraform-bancanlamcacbuocsauday"></a>

### **Cài đặt Terraform CLI** <a href="#quanlyvcontainervoiterraform-caidatterraformcli" id="quanlyvcontainervoiterraform-caidatterraformcli"></a>

Để có thể quản lý vContainer với Terraform bạn cần cài đặt Terraform CLI theo hướng dẫn [tại đây](../vserver/compute-hcm03-1a/terraform/cai-dat-terraform.md).

***

### **Cấp quyền IAM cho việc sử dụng**  <a href="#quanlyvcontainervoiterraform-capquyeniamchoviecsudung" id="quanlyvcontainervoiterraform-capquyeniamchoviecsudung"></a>

Để có thể thực hiện quản lý VKS với Terraform, bạn cần khởi tạo hoặc sử dụng một **service account** đã tạo trên IAM và gắn policy: **VKSFullAccess**. Để tạo service account bạn truy cập tại [đây](https://hcm-3.console.vngcloud.vn/iam/service-accounts) và thực hiện theo các bước sau:

* Chọn "**Create a Service Account**", điền tên cho Service Account và nhấn **Next Step** để gắn quyền cho Service Account.&#x20;
* Tìm và chọn **Policy:** **VKSFullAccess** sau đó nhấn "**Create a Service Account**" để tạo Service Account, **Policy: VKSFullAccess** do VNG Cloud tạo ra, bạn không thể xóa các policy này.
* Sau khi tạo thành công bạn cần phải lưu lại **Client\_ID** và **Secret\_Key** của Service Account để thực hiện bước tiếp theo.

***

### **Tạo thư mục chứa Terraform file** trên thiết bị của bạn <a href="#quanlyvcontainervoiterraform-taothumucchuaterraformfilevataiexamplefiletuvngcloudrepo" id="quanlyvcontainervoiterraform-taothumucchuaterraformfilevataiexamplefiletuvngcloudrepo"></a>

Sau khi tạo một **Service Account** với policy: **VKSFullAccess,** bạn cần tạo một thư mục trên thiết bị của bạn chứa các terraform file (main.tf, variable.tf) mà bạn có thể tải về từ VNG Cloud repo của chúng tôi tại [đây](https://github.com/vngcloud/terraform-provider-vngcloud/tree/main/examples).

***

### **Cài đặt thông số trong Terraform file** <a href="#quanlyvcontainervoiterraform-caidatthongsotrongterraformfile" id="quanlyvcontainervoiterraform-caidatthongsotrongterraformfile"></a>

* Trên file variable.tf, bạn cầm thêm thông tin Client\_ID và Client\_Secret đã tạo bên trên. Cụ thể, file variable.tf sẽ có cấu trúc như sau:

```markup
variable "client_id" {
  type = string
  default = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
variable "client_secret" {
  type = string
  default = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```

* Trên file main.tf, bạn cần có thể thêm data theo mẫu để tạo Cluster/ Node Group:
  * Tạo Cluster my-vks-cluster và Node Group my-vks-node-group:

```
resource "vngcloud_vks_cluster" "primary" {
  name      = "my-vks-cluster"
  cidr      = "172.16.0.0/16"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  name= "my-vks-node-group"
  ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  cluster_id= vngcloud_vks_cluster.primary.id
}
```

* Tạo Cluster với Default Node Group

```
resource "vngcloud_vks_cluster" "primary" {
  name      = "my-vks-cluster"
  cidr      = "172.16.0.0/16"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  node_group {
    name= "my-vks-node-group"
    ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  }
}
```

* Tạo Node Group

```
resource "vngcloud_vks_cluster" "primary" {
  name      = "my-vks-cluster"
  cidr      = "172.16.0.0/16"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  name= "my-vks-node-group"
  ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  cluster_id= vngcloud_vks_cluster.primary.id
}
```

***

### **Khởi chạy Terraform command** <a href="#quanlyvcontainervoiterraform-khoichayterraformcommand" id="quanlyvcontainervoiterraform-khoichayterraformcommand"></a>

* Sau khi hoàn tất các thông tin trên, để terraform khởi tạo và tải VNG Cloud provider về đồng thời thiết lập các thông tin cần thiết chạy lệnh bên dưới, lưu ý khi chạy cần đứng tại thư mục terraform-provider-vngcloud/ [**examples**](https://github.com/vngcloud/terraform-provider-vngcloud/tree/main/examples)/:&#x20;

```
terraform init
```

* Sau đó, bạn để xem những thay đổi sẽ được áp dụng trên những resource mà terraform đang quản lý bạn có thể chạy

```
terraform plan
```

* Cuối cùng bạn chọn chạy dòng lệnh:

```
terraform apply
```

* Chọn **YES** để thực hiện việc khởi tạo Cluster, Node Group thông qua Terraform

***

### **Kiểm tra Cluster vừa tạo trên giao diện VNG Cloud Portal** <a href="#quanlyvcontainervoiterraform-kiemtracontainervuataotrengiaodienvngcloudportal" id="quanlyvcontainervoiterraform-kiemtracontainervuataotrengiaodienvngcloudportal"></a>

Sau khi khởi tạo thành công Terraform, bạn có thể lên VKS Portal để xem thông tin Cluster vừa tạo.
