# Working VKS with Terraform

### What is Terraform?

Terraform itself does not have a graphical user interface; instead, users interact with it via the command line interface. Terraform requires cloud provider accounts and keys to be configured along with a Terraform configuration file to execute infrastructure as code. Additionally, Terraform can operate in a team environment where multiple users can collaborate on the same infrastructure codebase, making it a powerful and flexible tool for managing cloud infrastructure. Terraform is an open-source infrastructure as code tool that enables users to manage their infrastructure easily and efficiently across different cloud platforms such as VNG Cloud, AWS, Google Cloud, and Azure. The Terraform server refers to an instance of the Terraform tool running on a specific server or machine. This is where the infrastructure code is written and executed, allowing users to create, modify, and destroy resources on the cloud platform.

***

## Steps to create a Kubernetes Cluster using Terraform

### Create `main.tf`

Define the Kubernetes Cluster resources you want to create.

### Create `variable.tf`

Declare the Service Account information in this file.

### Initialize Terraform configuration

Download and install Terraform for your operating system: [Install Terraform](https://developer.hashicorp.com/terraform/install)

### Activate VKS Service

Go to the **Overview** tab and wait until we successfully initialize your VKS account.

### Access VKS Portal

After successful creation, save the **Client\_ID** and **Secret\_Key** of the Service Account for the next step.

### Create a Service Account with VKS Full Access

1. Access IAM Portal.
2. Select **Policy: VKSFullAccess**.
3. Click **Create a Service Account**.
4. Enter a name for the Service Account and click **Next Step** to attach permissions.

Now you’re ready to create a Kubernetes Cluster using Terraform.

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

***

*   To create `my-vks-cluster` and independent `my-nodegroup`:

    In the `main.tf` file, you need to add the resources to create the Cluster/Node Group.

```markup
resource "vngcloud_vks_cluster" "primary" {
  name      = "my-cluster"
  cidr      = "172.16.0.0/16"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  name= "my-nodegroup"
  ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  cluster_id= vngcloud_vks_cluster.primary.id
}
```

* Tạo Cluster với Default Node Group

```markup
resource "vngcloud_vks_cluster" "primary" {
  name      = "my-cluster"
  cidr      = "172.16.0.0/16"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  node_group {
    name= "my-nodegroup"
    ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  }
}
```

{% hint style="info" %}
**Note:**

* We recommend creating and managing Clusters and Node Groups separately as resources, as in the example below. This allows you to add or remove Node Groups without recreating the entire Cluster. If you directly declare the Default Node Group in the `vngcloud_vks_cluster` resource, you cannot delete them without recreating the entire Cluster.
* In the `main.tf` file, to successfully initialize a cluster with a node group, you must enter the information for the following 4 fields:
* <pre><code><strong>  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  </strong>  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
    ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  </code></pre>
{% endhint %}

Enable AutoScaling: scale from 0 to 5 nodes Node Group Name: my-nodegroup Mode: Public Cluster and Public Node Group K8S Version: v1.28.8 Cluster Name: my-cluster

Below is the `main.tf` file I use to create the Cluster with the specified parameters:

<mark style="color:blue;">Example 1</mark>

```
terraform {
  required_providers {
    vngcloud = {
      source  = "vngcloud/vngcloud"
      version = "1.2.2"
    }
  }
}

provider "vngcloud" {
  token_url        = "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token"
  client_id        = var.client_id
  client_secret    = var.client_secret
  vserver_base_url = "https://hcm-3.api.vngcloud.vn/vserver/vserver-gateway"
  vlb_base_url     = "https://hcm-3.api.vngcloud.vn/vserver/vlb-gateway"
}

resource "vngcloud_vks_cluster" "primary" {
  name      = "my-cluster"
  description = "VNGCLOUD uses terraform"
  version = "v1.28.8"
  cidr      = "172.16.0.0/16"
  enable_private_cluster = false
  network_type = "CALICO"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  enabled_load_balancer_plugin = true
  enabled_block_store_csi_plugin = true
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  cluster_id= vngcloud_vks_cluster.primary.id
  name= "my-nodegroup"
  auto_scale_config {
    min_size = 0
    max_size = 5
  }
  upgrade_config {
    strategy = "SURGE"
    max_surge = 1
	max_unavailable = 0
  }
  image_id = "img-983d55cf-9b5b-44cf-aa72-23f3b25d43ce"
  flavor_id = "flav-9e88cfb4-ec31-4ad4-8ba5-243459f6dc4b"
  disk_size = 20
  disk_type = "vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018"
  enable_private_nodes = false
  ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  labels = {
    "mylabel" = "vngcloud"
  }
  taint {
    key    = "mykey"
    value  = "myvalue"
    effect = "PreferNoSchedule"
  }
}
```

First, you need to apply the main file with the following configuration:

* Enable AutoScaling: scale from 0 to 5 nodes
* Node Group Name: my-nodegroup
* Mode: Public Cluster and Private Node Group
* K8S Version: v1.29.1
* Cluster Name: my-cluster

Below is the main.tf file I used to create the Cluster with the parameters: \*\*Example 2

```
terraform {
  required_providers {
    vngcloud = {
      source  = "vngcloud/vngcloud"
      version = "1.2.2"
    }
  }
}

provider "vngcloud" {
  token_url        = "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token"
  client_id        = var.client_id
  client_secret    = var.client_secret
  vserver_base_url = "https://hcm-3.api.vngcloud.vn/vserver/vserver-gateway"
  vlb_base_url     = "https://hcm-3.api.vngcloud.vn/vserver/vlb-gateway"
}

resource "vngcloud_vks_cluster" "primary" {
  name      = "my-cluster"
  description = "VNGCLOUD uses terraform"
  version = "v1.29.1"
  cidr      = "172.16.0.0/16"
  enable_private_cluster = false
  network_type = "CALICO"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  enabled_load_balancer_plugin = true
  enabled_block_store_csi_plugin = true
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  cluster_id= vngcloud_vks_cluster.primary.id
  name= "my-nodegroup"
  auto_scale_config {
    min_size = 0
    max_size = 5
  }
  upgrade_config {
    strategy = "SURGE"
    max_surge = 1
	max_unavailable = 0
  }
  image_id = "img-108b3a77-ab58-4000-9b3e-190d0b4b07fc"
  flavor_id = "flav-9e88cfb4-ec31-4ad4-8ba5-243459f6dc4b"
  disk_size = 20
  disk_type = "vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018"
  enable_private_nodes = true
  ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  labels = {
    "mylabel" = "vngcloud"
  }
  taint {
    key    = "mykey"
    value  = "myvalue"
    effect = "PreferNoSchedule"
  }
}
```

Sau đó, nếu bạn cần thêm Whitelist IP cho Control Plane, hãy thêm field này vào file main.tf và thực hiện apply lại file này:

```
terraform {
  required_providers {
    vngcloud = {
      source  = "vngcloud/vngcloud"
      version = "1.2.2"
    }
  }
}

provider "vngcloud" {
  token_url        = "https://iamapis.vngcloud.vn/accounts-api/v2/auth/token"
  client_id        = var.client_id
  client_secret    = var.client_secret
  vserver_base_url = "https://hcm-3.api.vngcloud.vn/vserver/vserver-gateway"
  vlb_base_url     = "https://hcm-3.api.vngcloud.vn/vserver/vlb-gateway"
}

resource "vngcloud_vks_cluster" "primary" {
  name      = "my-cluster"
  description = "VNGCLOUD uses terraform"
  version = "v1.29.1"
  cidr      = "172.16.0.0/16"
  white_list_node_cidr = "172.25.32.1/16"
  enable_private_cluster = false
  network_type = "CALICO"
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  enabled_load_balancer_plugin = true
  enabled_block_store_csi_plugin = true
}

resource "vngcloud_vks_cluster_node_group" "primary" {
  cluster_id= vngcloud_vks_cluster.primary.id
  name= "my-nodegroup"
  auto_scale_config {
    min_size = 0
    max_size = 5
  }
  upgrade_config {
    strategy = "SURGE"
    max_surge = 1
	max_unavailable = 0
  }
  image_id = "img-108b3a77-ab58-4000-9b3e-190d0b4b07fc"
  flavor_id = "flav-9e88cfb4-ec31-4ad4-8ba5-243459f6dc4b"
  disk_size = 20
  disk_type = "vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018"
  enable_private_nodes = true
  ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  labels = {
    "mylabel" = "vngcloud"
  }
  taint {
    key    = "mykey"
    value  = "myvalue"
    effect = "PreferNoSchedule"
  }
}
```

{% hint style="info" %}
**Note**

To get the flavor\_id you want to use for your Node group, please obtain the ID from here. To get the image\_id you wish to use, you can visit the VKS Portal, navigate to the System Image menu, and retrieve the desired ID, or obtain this information here..
{% endhint %}

Select **YES** to initiate Cluster and Node Group creation using Terraform Finally, select to run the command: `terraform apply` Then, to see the changes that will be applied to the resources managed by Terraform, you can run: `terraform plan` After completing the above information, proceed with running the command below: \*\*Execute Terraform command

***

### Check the newly created Cluster on the VNG Cloud Portal interface

Refer to how to use Terraform to work with VKS. After successfully initializing Terraform, you can visit the VKS Portal to view the newly created Cluster.
