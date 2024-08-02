# IAM Access Management

IAM Access Management lets you control who can access your cloud resources and what actions they can perform on those resources. IAM Policies are JSON documents that define resource access rights and rules for IAM identities (IAM User Accounts, User Groups, and Service Accounts). This guide will walk you through creating and managing IAM Policies to effectively control access to your resources.

**Concepts and Terms**&#x20;

* **Permissions and Policy**: Permissions define specific actions that a recipient is allowed to perform on a resource. Policies are sets of permissions represented as JSON documents. These policies are associated with IAM user accounts, groups, and service accounts to grant or deny access to various resources. Each policy contains declarations that define actions that are allowed or denied, resources, and optional conditions.&#x20;
* **Access control:** Access control is the implementation of permissions based on policies. When a recipient initiates a request to perform an action, the system checks the relevant policies to determine whether the requested action is allowed. If the policies grant the required permissions, the action is authorized; otherwise, it is denied.&#x20;
* **Resource-Based Authorization:** In IAM, authorization is often resource-based, meaning that permissions are defined in relation to specific resources. These resources can be specific services, buckets, databases, files, or any other digital asset in the system. Resource-based authorization ensures that recipients can only access resources for which they have been explicitly authorized.
* **Granular Control:** IAM provides granular control over authorization. Administrators can define specific Permissions and Policies, not only the types of actions an entity can perform, but also the conditions under which that action is allowed in a given case.&#x20;
* **Dynamic Authorization:** Permissions and Policies can be dynamically adjusted to adapt to changing requirements and situations. This allows administrators to easily grant or revoke access as needed, without the need for complex manual intervention.&#x20;
* **Least Privilege Principle:** The principle of least privilege is a fundamental concept in IAM authorization. It states that entities should only be granted the minimum permissions necessary to perform their actions. This minimizes the potential impact of security breaches and limits the exposure of sensitive resources.

#### Hiểu về IAM Policy <a href="#iamaccessmanagement-hieuveiampolicy" id="iamaccessmanagement-hieuveiampolicy"></a>

Mỗi chính sách bao gồm một hoặc nhiều câu lệnh, và mỗi câu lệnh chứa các phần tử "Effect" (Cho phép hoặc Từ chối), "Action" (Các hành động trên Resource), "Resource" (Các tài nguyên VNG Cloud) và các phần tử "Condition" tùy chọn.

**Product/Service**

Việc chỉ định Product/Service khi khởi tạo một Policy là bắt buộc, giúp bạn giới hạn tập quyền lên một nhóm Resources thuộc một Prodcut/Service nhất định, giúp việc vận hành hoạt động một cách mượt mà và an toàn.

Các sản phẩm/service thuộc VNG Cloud như: vServer, vStorage, vMonitor, vLB, vConsole, IAM,...

**Action**

Tại mục Action, bạn có thể chỉ định các hành động (**được cấp phép** hoặc **từ chối truy cập**) trên các tài nguyên được áp dụng:

* Để **cấp phép truy cập** các Action trên Resource, chọn **Allow Permission**
* Để **từ chối truy cập** các Action trên Resource, chọn **Deny Permission**

**Có ba loại cấp độ truy cập, bao gồm:**

* **List:** Cấp độ này liệt kê tất cả các quyền liên quan đến xem danh sách tài nguyên thuộc Product đã chọn. Bạn có thể chọn **Tất cả / các hành động cụ thể**.
* **Write**: Cấp độ này liệt kê tất cả các quyền liên quan đến các hành động thay đổi tài nguyên thuộc Product đã chọn, chẳng hạn như Tạo, Cập nhật, Tải lên, Gia hạn và các hành động khác. Bạn có thể chọn tất cả / các hành động cụ thể ở cấp độ này.
* **Read**: Cấp độ này liệt kê tất cả các quyền liên quan đến xem thông tin chi tiết của tài nguyên thuộc Product đã chọn. Bạn có thể chọn tất cả / các hành động cụ thể ở cấp độ này.

**Resource**

Có một số cách linh hoạt để bạn chỉ định các tài nguyên được áp dụng các Action (được cấp phép hoặc từ chối truy cập), bao gồm:

* Tất cả các tài nguyên
* Các tài nguyên cụ thể: Đối với mỗi loại tài nguyên thuộc Product đã chọn, bạn có thể chọn tất cả / các tài nguyên cụ thể (dựa trên ID tài nguyên) thuộc loại đó.

**Request conditions**

Các Request conditions trong Policy là các điều kiện tùy chọn mà bạn có thể đặt để quy định Policy đó sẽ áp dụng như thế nào cho trên các đối tượng (IAM User Account, Service Account, Group). Có nhiều loại điều kiện bạn có thể cài đặt để áp dụng lên Policy của mình, và điều chỉnh thời gian áp dụng chính sách là một trong số đó. Điều này cho phép bạn điều chỉnh khi nào chính sách sẽ có hiệu lực và khi nào nó sẽ bị hủy bỏ đối với một hoặc nhiều hành động cụ thể mà người dùng hoặc dịch vụ đang thực hiện.

Ví dụ, bạn có thể sử dụng Request conditions để quy định rằng một chính sách chỉ sẽ áp dụng vào các ngày cụ thể hoặc chỉ trong khoảng thời gian nhất định. Điều này có thể hữu ích trong việc quản lý quyền truy cập dựa trên thời gian, ngày lễ, sự kiện đặc biệt hoặc các tình huống cụ thể khác mà bạn muốn kiểm soát.

**Rules**

Một chính sách (Policies) sẽ bao gồm nhiều Rule. Mỗi Rule sẽ bao gồm đầy đủ các thành phần như Product, Action, Resource và Request conditions. Việc có nhiều Rule trong một Policy giúp bạn áp dụng các tập quyền hạn khác nhau, lên từng tập resource khác nhau.

#### Phân loại Chính Sách (Policy) <a href="#iamaccessmanagement-phanloaichinhsach-policy" id="iamaccessmanagement-phanloaichinhsach-policy"></a>

Tại VNG Cloud Service, chúng tôi hỗ trợ 2 loại Chính Sách (Policy), bao gồm:

* **VNG Managed Policy:** Là các Chính Sách IAM (IAM Policy) được tạo mặc định bởi hệ thống IAM VNG Cloud. Các Chính Sách này được quản lý bởi chính VNG Cloud nhằm mục đích hỗ trợ người dùng trong việc cài đặt nhanh chóng các quyền truy cập cần thiết cho các tài khoản người dùng IAM đối với các tài nguyên của từng Product cụ thể
* **Customer Policy:** Là các Chính Sách IAM (IAM Policy) được tạo bởi Root user (hoặc IAM user nếu có quyền). Các Chính Sách này được quản lý trực tiếp bởi người dùng và có thể điều chỉnh bất cứ lúc nào tùy thuộc vào nhu cầu sử dụng.
* Tìm hiểu thêm và 2 loại Policy tại đây:
  * [VNG Managed Policy](https://docs.vngcloud.vn/display/ONVINA/VNG+Cloud+Manage+Policies)
  * [Customer Managed Policy](https://docs.vngcloud.vn/display/ONVINA/Customer+Managed+Policies)
