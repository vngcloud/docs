# IAM Access Management

IAM Access Management lets you control who can access your cloud resources and what actions they can perform on those resources. IAM Policies are JSON documents that define resource access rights and rules for IAM identities (IAM User Accounts, User Groups, and Service Accounts). This guide will walk you through creating and managing IAM Policies to effectively control access to your resources.

**Concepts and Terms**&#x20;

* **Permissions and Policy**: Permissions define specific actions that a recipient is allowed to perform on a resource. Policies are sets of permissions represented as JSON documents. These policies are associated with IAM user accounts, groups, and service accounts to grant or deny access to various resources. Each policy contains declarations that define actions that are allowed or denied, resources, and optional conditions.&#x20;
* **Access control:** Access control is the implementation of permissions based on policies. When a recipient initiates a request to perform an action, the system checks the relevant policies to determine whether the requested action is allowed. If the policies grant the required permissions, the action is authorized; otherwise, it is denied.&#x20;
* **Resource-Based Authorization:** In IAM, authorization is often resource-based, meaning that permissions are defined in relation to specific resources. These resources can be specific services, buckets, databases, files, or any other digital asset in the system. Resource-based authorization ensures that recipients can only access resources for which they have been explicitly authorized.
* **Granular Control:** IAM provides granular control over authorization. Administrators can define specific Permissions and Policies, not only the types of actions an entity can perform, but also the conditions under which that action is allowed in a given case.&#x20;
* **Dynamic Authorization:** Permissions and Policies can be dynamically adjusted to adapt to changing requirements and situations. This allows administrators to easily grant or revoke access as needed, without the need for complex manual intervention.&#x20;
* **Least Privilege Principle:** The principle of least privilege is a fundamental concept in IAM authorization. It states that entities should only be granted the minimum permissions necessary to perform their actions. This minimizes the potential impact of security breaches and limits the exposure of sensitive resources.

#### About IAM Policy <a href="#iamaccessmanagement-hieuveiampolicy" id="iamaccessmanagement-hieuveiampolicy"></a>

Each policy includes one or more statements, and each statement contains the elements "Effect" (Allow or Deny), "Action" (Actions on the Resource), "Resource" (VNG Cloud resources), and optional "Condition" elements.

**Product/Service**

Specifying Product/Service when creating a Policy is mandatory, helping you limit permissions to a group of Resources under a specific Product/Service, ensuring smooth and safe operation.

VNG Cloud products/services include: vServer, vStorage, vMonitor, vLB, vConsole, IAM, etc.

**Action**

In the Action section, you can specify the actions (grant or deny access) on the applied resources:

* To grant access to **Actions on a Resource**, select **Allow Permission**&#x20;
* To deny access to **Actions on a Resource**, select **Deny Permission**

There are three types of access levels, including:&#x20;

* **List**: This level lists all permissions related to viewing the list of resources under the selected Product. You can select All / specific actions.&#x20;
* **Write**: This level lists all permissions related to actions that change resources under the selected Product, such as Create, Update, Upload, Renew and other actions. You can select all / specific actions at this level.&#x20;
* **Read**: This level lists all permissions related to viewing detailed information of resources under the selected Product. You can select all / specific actions at this level.

**Resource**

There are several flexible ways for you to specify the resources to which Actions apply (grant or deny access), including:&#x20;

* All resources
* Specific resources: For each resource type in the selected Product, you can select all / specific resources (based on resource ID) of that type.

**Request conditions**

Request conditions in a Policy are optional conditions that you can set to govern how the Policy will apply to objects (IAM User Account, Service Account, Group). There are many types of conditions you can set to apply to your Policy, and adjusting the policy application time is one of them. This allows you to regulate when the policy will take effect and when it will be revoked for a specific action or actions that a user or service is taking.&#x20;

For example, you can use Request conditions to specify that a policy will only apply on specific days or only during a certain time period. This can be useful for managing access based on time, holidays, special events, or other specific situations that you want to control.

**Rules**

A policy will include many Rules. Each Rule will include all components such as Product, Action, Resource and Request conditions. Having many Rules in a Policy helps you apply different sets of permissions to different sets of resources.

#### Policy <a href="#iamaccessmanagement-phanloaichinhsach-policy" id="iamaccessmanagement-phanloaichinhsach-policy"></a>

At VNG Cloud Service, we support 2 types of Policies, including:

* **VNG Managed Policy:** These are IAM Policies created by default by the VNG Cloud IAM system. These Policies are managed by VNG Cloud itself to support users in quickly setting up the necessary access rights for IAM user accounts to resources of each specific Product&#x20;
* **Customer Policy:** These are IAM Policies created by the Root user (or IAM user if they have permission). These Policies are managed directly by the user and can be adjusted at any time depending on usage needs.
