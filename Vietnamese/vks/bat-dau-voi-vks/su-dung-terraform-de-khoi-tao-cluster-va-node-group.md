# Sử dụng Terraform để khởi tạo Cluster và Node Group

### Tổng quan

Terraform là một công cụ mã nguồn mở được sử dụng để tự động hóa việc cung cấp và quản lý cơ sở hạ tầng như máy ảo, mạng, lưu trữ và Kubernetes.

Với Terraform, bạn có thể mô tả cơ sở hạ tầng mong muốn bằng mã, sau đó Terraform sẽ thực hiện các thao tác cần thiết để tạo hoặc cập nhật cơ sở hạ tầng cho phù hợp với mô tả của bạn.

***

### **Khởi tạo Cluster và Node Group**

Để khởi tạo một Cluster Kubernetes bằng Terraform, bạn cần thực hiện các bước sau:

1. **Truy cập IAM Portal** tại [đây](https://iam.console.vngcloud.vn/), thực hiện tạo Service Account với quyền hạn **VKS Full Access**. Cụ thể, tại trang IAM, bạn có thể:
   * Chọn "**Create a Service Account**", điền tên cho Service Account và nhấn **Next Step** để gắn quyền cho Service Account.
   * Tìm và chọn **Policy:** **VKSFullAccess** sau đó nhấn "**Create a Service Account**" để tạo Service Account, **Policy: VKSFullAccess** do GreenNode tạo ra, bạn không thể xóa các policy này.
   * Sau khi tạo thành công bạn cần phải lưu lại **Client\_ID** và **Secret\_Key** của Service Account để thực hiện bước tiếp theo.
2. **Truy cập VKS Portal** tại [đây](https://vks.console.vngcloud.vn/overview)**, thực hiện Activate** dịch vụ VKS ở tab **Overview.** Hãy chờ đợi tới khi chúng tôi khởi tạo thành công tài khoản VKS của bạn.
3. **Cài đặt Terraform:**
   * Tải xuống và cài đặt Terraform cho hệ điều hành của bạn từ [https://developer.hashicorp.com/terraform/install](https://developer.hashicorp.com/terraform/install).
4. **Khởi tạo cấu hình Terraform:**
   * Tạo tệp `variable.tf` và khai báo thông tin Service Account trong file này.
   * Tạo tệp `main.tf` và định nghĩa các tài nguyên Kubernetes Cluster mà bạn muốn tạo.

Ví dụ:

* Tệp `variable.tf:`bạn cần thay thế Client ID và Client Secret đã khởi tạo ở bước 1 ở file này.

```
variable "client_id" {
  type = string
  default = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
variable "client_secret" {
  type = string
  default = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```

* Tệp `main.tf:` trong ví dụ này tôi thực hiện khởi tạo một Private Cluster và một Private Node Group&#x20;

{% hint style="info" %}
**Chú ý:**

* Trong file main.tf, để khởi tạo một cluster với một node group, bạn bắt buộc cần truyền vào các thông số sau: &#x20;

```hcl
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
```
{% endhint %}

* Với **Region HCM:**

```
terraform {
  required_providers {
    vngcloud = {
      source  = "vngcloud/vngcloud"
      version = "1.3.3"
    }
  }
}
provider "vngcloud" {
  token_url        = "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token"
  client_id        = var.client_id
  client_secret    = var.client_secret
  vserver_base_url = "https://hcm-3.api.vngcloud.vn/vserver/vserver-gateway"
  vlb_base_url     = "https://hcm-3.api.vngcloud.vn/vserver/vlb-gateway"
  vks_base_url     = "https://vks.api.vngcloud.vn"
}

resource "vngcloud_vks_cluster" "primary" {
  name      = "cluster-hcm"
  description = "Cluster create via terraform"
  version = "v1.29.13-vks.1740045600"
  enable_private_cluster = true
  network_type = "CILIUM_NATIVE_ROUTING"
  cidr      = "172.16.0.0/16"
  vpc_id    = "net-dc27a89b-e7a8-46eb-bba1-9339fa6bd018"
  subnet_id = "sub-1191201a-4b47-46b8-8049-f18889ff5677"
  secondary_subnets = ["10.111.128.0/20","10.111.144.0/20"]
  node_netmask_size = 25
  enable_service_endpoint = true
  enabled_load_balancer_plugin = true
  enabled_block_store_csi_plugin = true
  lifecycle {
    create_before_destroy = true
  }
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  cluster_id = vngcloud_vks_cluster.primary.id
  name = "nodegroup1"
  num_nodes = 3
  auto_scale_config {
    min_size = 0
    max_size = 5
  }
  upgrade_config {
    strategy = "SURGE"
    max_surge = 1
    max_unavailable = 0
  }
  image_id = "img-53bccbb6-7db5-42c1-bcc2-fef9fd1dccdc"
  flavor_id = "flav-305a67bf-1825-4e3f-bc72-d41afa160d93"
  subnet_id = "sub-1191201a-4b47-46b8-8049-f18889ff5677"
  secondary_subnets = ["10.111.160.0/20"]
  disk_size = 50
  disk_type = "vtype-2fc64a6c-38e3-4f08-93a5-18018cb3ab23"
  enable_private_nodes = true
  ssh_key_id= "ssh-7e899107-b5dd-4b91-9c82-5e20497cb00b"
  labels = {
    "test" = "terraform"
  }
  taint {
    key    = "key1"
    value  = "value1"
    effect = "PreferNoSchedule"
  }
  lifecycle {
    create_before_destroy = true
  }
}



```

* Với **Region HAN:**

```
terraform {
  required_providers {
    vngcloud = {
      source  = "vngcloud/vngcloud"
      version = "1.3.3"
    }
  }
}
provider "vngcloud" {
  token_url        = "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token"
  client_id        = var.client_id
  client_secret    = var.client_secret
  vserver_base_url = "https://han-1.api.vngcloud.vn/vserver/vserver-gateway"
  vlb_base_url     = "https://han-1.api.vngcloud.vn/vserver/vlb-gateway"
  vks_base_url     = "https://vks-han-1.api.vngcloud.vn"
}

resource "vngcloud_vks_cluster" "primary" {
  name      = "cluster-demo"
  description = "Cluster create via terraform"
  version = "v1.29.13-vks.1740045600"
  enable_private_cluster = true
  network_type = "CILIUM_NATIVE_ROUTING"
  cidr      = "172.16.0.0/16"
  vpc_id    = "net-0dc4cf1e-d961-4483-b848-62ed86fa69f1"
  subnet_id = "sub-a39ebafb-4231-4a86-b94e-f78fc6b8778d"
  secondary_subnets = ["192.168.200.0/24"]
  node_netmask_size = 25
  enable_service_endpoint = true
  enabled_load_balancer_plugin = true
  enabled_block_store_csi_plugin = true
  lifecycle {
    create_before_destroy = true
  }
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  cluster_id = vngcloud_vks_cluster.primary.id
  name = "nodegroup1"
  num_nodes = 3
  auto_scale_config {
    min_size = 0
    max_size = 5
  }
  upgrade_config {
    strategy = "SURGE"
    max_surge = 1
    max_unavailable = 0
  }
  image_id = "img-331724e8-326f-4fd0-ac6e-f9bd127f976c"
  flavor_id = "flav-305a67bf-1825-4e3f-bc72-d41afa160d93"
  subnet_id = "sub-a39ebafb-4231-4a86-b94e-f78fc6b8778d"
  secondary_subnets = ["192.168.200.0/24"]
  disk_size = 50
  disk_type = "vtype-7a7a8610-34f5-11ee-be56-0242ac120002"
  enable_private_nodes = true
  ssh_key_id= "ssh-4e765839-4222-444b-bf09-83de37aa7121"
  labels = {
    "test" = "terraform"
  }
  taint {
    key    = "key1"
    value  = "value1"
    effect = "PreferNoSchedule"
  }
  lifecycle {
    create_before_destroy = true
  }
}

```

5. **Khởi tạo Terraform:**

* Chạy lệnh `terraform init.`Lệnh này sẽ tải xuống các plugin cần thiết và khởi tạo trạng thái Terraform.

6. **Áp dụng cấu hình Terraform:**

* Chạy lệnh `terraform apply.` Lệnh này sẽ tạo Cluster Kubernetes theo mô tả trong tệp `main.tf`.

Tham khảo thêm về cách sử dụng Terraform để làm việc với VKS tại [đây](https://registry.terraform.io/providers/vngcloud/vngcloud/latest/docs/resources/vks_cluster).
