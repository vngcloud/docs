# Use Terraform to create a Cluster and Node Group

## Overview <a href="#tong-quan" id="tong-quan"></a>

Terraform is an open source tool used to automate the provisioning and management of infrastructure such as virtual machines, networking, storage, and Kubernetes.

With Terraform, you can describe your desired infrastructure in code, then Terraform will perform the necessary operations to create or update the infrastructure to match your description.

***

## **Initialize Cluster and Node Group** <a href="#khoi-tao-cluster-va-node-group" id="khoi-tao-cluster-va-node-group"></a>

To initialize a Kubernetes Cluster using Terraform, you need to perform the following steps:

1. **Access the IAM Portal** here , create a Service Account with [VKS ](https://iam.console.vngcloud.vn/)**Full Access** authority . Specifically, at the IAM site, you can:
   * Select " **Create a Service Account** ", enter a name for the Service Account and click **Next Step** to assign permissions to the Service Account.
   * Find and select **Policy: VKSFullAccess** then click " **Create a Service Account** " to create a Service Account, **Policy: VKSFullAccess** is created by VNG Cloud, you cannot delete these policies.
   * After successful creation, you need to save **the Client\_ID** and **Secret\_Key** of the Service Account to perform the next step.
2. **Access the VKS Portal** here **, Activate** [the](https://vks.console.vngcloud.vn/overview) VKS service on the **Overview tab.** Please wait until we successfully create your VKS account.
3. **Install Terraform:**
   * Download and install Terraform for your operating system from [https://developer.hashicorp.com/terraform/install](https://developer.hashicorp.com/terraform/install) .
4. **Initialize Terraform configuration:**
   * Create a file `variable.tf`and declare Service Account information in this file.
   * Create a file `main.tf`and define the Kubernetes Cluster resources you want to create.

For example:

* The file `variable.tf:`you need to replace the Client ID and Client Secret created in step 1 in this file.

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

* The file `main.tf:`in this example I initialize a Cluster and a Node Group has the following information:
  * Cluster name: my-cluster
  * K8S Version: v1.28.8
  * Mode: Public Cluster and Public Node Group
  * Node Group name: my-nodegroup
  * Turn on AutoScaling: scale from 0 to 5 nodes

**Attention:**

* In the main.tf file, to initialize a cluster with a node group, you must pass in the following parameters:

```
  vpc_id    = "net-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  subnet_id = "sub-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
  ssh_key_id= "ssh-xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"
```

* The sample file `main.tf`helps you create Cluster and Node Group according to the configuration above:

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
  num_nodes
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

1. **Initialize Terraform:**

* Run the command `terraform init.`This command will download the necessary plugins and initialize the Terraform state.

1. **Apply Terraform configuration:**

* Run command `terraform apply.`This command will create a Kubernetes Cluster as described in the `main.tf`.

See more about how to use Terraform to work with VKS [here](https://registry.terraform.io/providers/vngcloud/vngcloud/latest/docs/resources/vks\_cluster) .
