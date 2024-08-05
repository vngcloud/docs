# Node Groups

Node Group is an important concept in Kubernetes, used to manage groups of nodes (VMs) with the same configuration within a cluster. For a Node Group, you can:

### Create a Node Group <a href="#nodegroups-createanodegroup" id="nodegroups-createanodegroup"></a>

To create a Node Group, follow the steps below:

**Step 1:** Go to [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2:** In the previously created Cluster, select **Create a Node group.**

**Step 3:** On the Node Group creation screen, we have set up the information for your Node Group. You can keep these default values or adjust the desired parameters for your Node Group:

* Node Group Information:
  * **Node Group Name**: A memorable name for your Node Group.
  * **Number of nodes:** Enter the number of Worker nodes for your Cluster, note the number of nodes should be between 1 and 100.
* Node Group Automation Setting:
  * **Auto Healing:** By default, we will enable HA in your Cluster. When a node or pod fails, Kubernetes will automatically restart or create a new pod to replace it, ensuring your application runs uninterrupted.
  * **Auto Scaling:** Enable automatic scaling in your Cluster. Auto scaling automatically adjusts the number of pods based on actual usage needs, preventing resource waste when demand is low or overload when demand is high.
    * **Minimum node**: the minimum number of nodes the Cluster needs.
    * **Maximum node**: the maximum number of nodes the Cluster can scale to.
  * Node Group upgrade strategy: upgrade strategy for the Node Group. When you set **Node Group Upgrade Strategy** through the **Surge upgrade** method for a Node Group in VKS, the VKS system will sequentially update nodes for upgrade, in an undefined order.
    * **Max surge:** limits the number of nodes being upgraded simultaneously (number of new nodes (surge) that can be created at once). Default **Max surge = 1** - only one node is upgraded at a time.
    * **Max unavailable**: limits the number of nodes unavailable during the upgrade (number of current nodes that can be disrupted at once). Default **Max unavailable = 0** - ensures all nodes are accessible during the upgrade.
* Node Group Setting:
  * **Image**: by default, we provide one type of Image - Ubuntu with containerd.
  * **Instance type**: select the suitable configuration type for the Worker node as per your needs.
* Node Group Volume Setting: **Boot Volume Configuration** – Parameters are default set by the system optimized for your Cluster.
* Node Group Network Setting: You can choose **Public Node Group** or **Private Node Group** based on your Cluster requirement.
* Node Group Security Setting: You can select **Security Group and SSH Key** for your Node Group.
* Node Group Metadata Setting: You can enter corresponding **Metadata** for the Node Group.

**Step 5:** Select **Create Node Group.** Wait a few minutes for us to create your Node Group, at which point the Node Group status will be **Creating**.

**Step 6:** When the status of **Node Group** is **Active**, you can view the Node Group information by selecting **Node Group Name** on the main screen.

***

### Chỉnh sửa một Node Group <a href="#nodegroups-chinhsuamotnodegroup" id="nodegroups-chinhsuamotnodegroup"></a>

**Đối với Node Group, bạn có thể chỉnh sửa các thông số: Number of Nodes, Auto Scaling, Upgrade Strategy, Security Group trong từng lần chỉnh sửa riêng biệt**. Cụ thể, bạn có thể thực hiện theo các bước sau đây:

**Bước 1:** Truy cập vào [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Bước 2:** Tại Cluster đã khởi tạo trước đó, hãy chọn **vào Cluster bạn muốn chỉnh sửa Node group.**

**Bước 3:** Tại màn hình chứa danh sách Node Group đang có, tại Node Group bạn muốn chỉnh sửa chọn một trong các phương án:

* Tính năng **Resize:** bạn có thể thay đổi\\
  * Number of nodes: Nhập vào số lượng Worker node cho Cluster của bạn, lưu ý số lượng node cần lớn hơn hoặc bằng 1 và nhỏ hơn hoặc bằng 100.
* Tính năng **Edit Auto Scaling:** bạn có thể thay đổi\\
  * Auto Scaling: Bật tính năng tự động mở rộng trong Cluster của bạn. Auto scaling giúp tự động điều chỉnh số lượng pod (đơn vị triển khai ứng dụng) dựa trên nhu cầu sử dụng thực tế, tránh tình trạng lãng phí tài nguyên khi nhu cầu thấp hoặc quá tải khi nhu cầu cao.
    * Minimum node: số node tối thiểu mà Cluster cần có.
    * Maximum node: số node tối đa mà Cluster có thể scale tới.
* Tính năng **Edit Upgrade Stratetry:** bạn có thể thay đổi
  * Node Group upgrade stratetry: chiến lược upgrade Node Group. Khi bạn thiết lập Node Group Upgrade Strategy thông qua phương thức Surge upgrade cho một Node Group trong VKS, hệ thống VKS sẽ cập nhật tuần tự để nâng cấp các node, theo thứ tự không xác định[.](https://cloud.google.com/kubernetes-engine/docs/concepts/node-pool-upgrade-strategies.)
    * Max surge: giới hạn số lượng node được nâng cấp đồng thời (số lượng node mới (surge) có thể được tạo ra cùng một lúc). Mặc định Max surge = 1 - chỉ nâng cấp một node tại một thời điểm. với maxUnavailable
    * Max unavailable: giới hạn số lượng node không thể truy cập được trong quá trình nâng cấp (số lượng node hiện tại có thể bị gián đoạn cùng một lúc). Mặc định Max unavailable = 0 - đảm bảo tất cả các node đều có thể truy cập được trong quá trình nâng cấp.
* Tính năng **Edit Security Group:** bạn có thể thay đổi
  * Node Group Security Setting: Bạn có thể chọn Security Group và SSH Key cho Node Group của bạn.

***

### Xóa một Node Group <a href="#nodegroups-xoamotnodegroup" id="nodegroups-xoamotnodegroup"></a>

{% hint style="info" %}
Chú ý:

Khi không còn nhu cầu sử dụng Node Group, bạn hãy thực hiện xóa chúng để tiết kiệm chi phí. Khi xoá Node Group, các tài nguyên sau sẽ bị xóa:

* Tất cả các node có trong Node Group (VM)
{% endhint %}

**Bước 1:** Truy cập vào [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Bước 2:** Tại màn hình **Overview**, chọn menu **Kubernetes Cluster.**

**Bước 3:** Tại **Cluster** đã tạo thành công, chọn Node Group bạn muốn xóa và chọn **Delete.**

**Bước 4:** Chọn **Delete** để xóa hoàn toàn **Node Group** của bạn.

\\
