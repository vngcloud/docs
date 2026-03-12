# Initialize an OpenSearch Cluster

To initialize an OpenSearch Cluster Database on the vDB system, you can follow these steps:

**Step 1:** Access [https://vdb.console.vngcloud.vn/](https://vdb.console.vngcloud.vn/)

**Step 2:** Select **Cluster** under the **OpenSearch** section, then select **Create a cluster..**

**Step 3:** On the OpenSearch Cluster initialization screen, you need to enter/select:

* **Basic configuration:**
  * **OpenSearch Cluster name:** a memorable name for the cluster. The cluster name must be between 5 and 50 characters long and can include characters a-z, A-Z, 0-9, '-'.
  * **Tag:** you can add tags to mark clusters according to your needs.

<figure><img src="../../../.gitbook/assets/image (952).png" alt=""><figcaption></figcaption></figure>

* **Cluster specification**
  * **OpenSearch Version:** select the OpenSearch Cluster version you want to use. Currently we are supporting 2 versions v2.15 and v2.17
  * **Instance**: select the CPU type and corresponding package you want to configure for all VMs (nodes) in each cluster.
  * **Number of nodes:** select the number of nodes (VMs) you want to use for the cluster. Currently we are providing options for 3, 5, 7, 9 nodes. If you want to create a cluster with more than 9 nodes, please contact GreenNode so we can assist you.&#x20;
  * **Encryption volume:** select whether or not to use the encryption service for volumes used on the cluster. If you choose to use this option, you need to pay additional costs for encryption.&#x20;
  * **Storage type:** select the disk type and IOPS you want to use.
  * **Storage size:** select the corresponding disk size.

<figure><img src="../../../.gitbook/assets/image (953).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (954).png" alt=""><figcaption></figcaption></figure>

* **Network settings:**
  * **VPC:** select a VPC you want to use. The selected VPC is the IP address range that the Cluster nodes will use to communicate.
  * **Subnet:** select a Subnet within the VPC you have selected. This is a smaller IP address range belonging to the VPC. Each node in the Cluster will be assigned an IP from this Subnet.
  * **Public Allow CIDRs:** enter the CIDR you allow to access the OpenSearch Dashboard and push logs to OpenSearch Received Logs.

<figure><img src="../../../.gitbook/assets/image (955).png" alt=""><figcaption></figcaption></figure>

* **Access control methods:**
  * **Master user password:** the system will automatically create the username `master-user`, you need to enter the master user password and remember to use this account to access the OpenSearch Dashboard as well as push logs to Received log.

<figure><img src="../../../.gitbook/assets/image (956).png" alt=""><figcaption></figcaption></figure>

* **Cluster options:**
  * **Configuration group**: by default, for each OpenSearch version, we will create a **Default Configuration Group**. You will not be able to change the parameters in this Default Configuration Group. If you want to change the default parameters, please create a new Configuration Group and edit it according to your needs.

<figure><img src="../../../.gitbook/assets/image (957).png" alt=""><figcaption></figcaption></figure>

* **Plugins**
  * **Plugin:** currently, vDB has automatically installed popular plugins in your OpenSearch Cluster under the **Bundled Plugins** section, for example kNN. You can refer to the list of default available plugins [here](../cac-tinh-nang-cua-opensearch-cluster/lam-viec-voi-plugin.md). Additionally, you can also choose to install additional plugins by selecting plugins under the **Additional Plugins** section. Refer to the list of plugins available for installation [here](../cac-tinh-nang-cua-opensearch-cluster/lam-viec-voi-plugin.md).

<figure><img src="../../../.gitbook/assets/image (958).png" alt=""><figcaption></figcaption></figure>

**Step 5:** Select **Create Cluster.**

**Step 6:** Complete the payment steps if you are a prepaid user.
