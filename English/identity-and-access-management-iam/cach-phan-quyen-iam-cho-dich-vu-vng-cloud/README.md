# IAM for GreenNode's Services

1. **How IAM Works**&#x20;

IAM works by authenticating a user's identity and then authorizing access based on the Policies associated with IAM User Accounts, User Groups, and Service Accounts. When a user submits a request to access a specific resource or perform an action, IAM checks the associated policies to determine whether the user is authorized to perform that action.&#x20;

The principle of least privilege is fundamental to IAM, ensuring that users and services have only the minimum permissions necessary to perform their tasks, minimizing the risk of unauthorized access. IAM's centralized approach optimizes access management, enhances security, and helps organizations comply with regulatory requirements in cloud computing environments. This access management model consists of five main parts:

1. **Principal**

An entity (principal) refers to an object that can request access to resources in the GreenNode system. An entity can represent different types of objects such as User Account, Service Account, and IDP (Identity Provider).

* User Account: IAM User Account represents individual identities associated with a Root User Account. Each user has a unique set of security credentials such as a username and password or access key. Users are authenticated to access cloud resources and services.
* Service Account: A Service Account is an identity you can create in your Root User account with specific permissions. Unlike User Accounts, Service Accounts are identities used by applications or computers, not users, to make authorized API calls and access specific resources. IDP: Identity Provider allows you to manage resources on GreenNode with a set of users on the enterprise authentication system, helping enterprises centrally manage users and without having to create additional IAM User Accounts on GreenNode User Group: User Group is a collection of User Accounts with similar access requirements. Grouping User Accounts simplifies permission management by granting permissions to a group instead of each individual User Account. This improves consistency and efficiency in access control.

**2. Request**

The concept of "Request" refers to the specific operational requests that an entity is trying to perform on resources in the system. Each request consists of the following main parts: "Actions", "Resources", "Principal" and "Request Information".&#x20;

* Actions: These are the specific operations that an entity can perform on a resource. Actions can be interactions with the resource such as reading, writing, updating, deleting and many other actions.
* Resources: These are the objects or assets affected by the above actions. Resources can be specific services such as servers, load balancers, metrics, ... or any other digital assets in the system. The definition of a resource determines the scope that the action can impact.&#x20;
* Principal: When an entity initiates a request, the system checks to see if the requested action is allowed based on the Policies associated with that entity and the resource. If the Policies allow it, the request is carried out; otherwise, the request is denied. This helps ensure that access to resources is controlled and secured in the most optimal way.&#x20;
* Request information: This is information related to the request that the entity is making. This information may include information such as the requester's IP address, the time the request was sent, and other additional data relevant to the context of the request.

**3. Policy**

IAM Policies are JSON documents that define permissions and access rules for resources. Policies are attached to entities to control the actions they can perform on specific resources. These Policies follow the "allow" or "deny" principle and specify the actions that are allowed or denied for a specific entity.

**4. Authentication**

Authentication is the process of authenticating an entity using its credentials to send a request to GreenNode. The entity needs to provide authentication information, such as a username and password, to prove their identity. The authentication information required for authentication from the IAM Console side for each entity includes:

* Root User Account: Email address and password&#x20;
* IAM User Account: Identifier and password&#x20;
* Service Account: Client ID and Secret key&#x20;
* IDP: Log in via the link and be granted the same access as an IAM User Account

**5. Authorization**

After successful authentication, the system performs the authorization process, or decides whether an entity has the right to perform a particular action on a particular resource. This process ensures that only authorized entities can perform actions on the resource.

* Root User Account: By default, it has full (unlimited) access to all products/services and resources under those products/services.&#x20;
* IAM User Account: By default, it has no rights (denies access) on resources under GreenNode products/services. The subject must be authorized based on the attached Policies set to perform specific actions on specific resources.&#x20;
* Service Account: Similar to IAM User Account, Service Account by default has no rights (denies access) on resources under GreenNode products/services. The subject must be authorized based on the attached Policies set to perform specific actions on specific resources.&#x20;
* IDP: When Identity is successfully established between GreenNode (Service Provider) and the third party (Identity Providers), the subject can access the GreenNode system through the login link. Access objects are considered as IAM User Accounts and by default have no rights (denied access) on resources of GreenNode products/services. Objects must be authorized based on the attached Policies set to perform specific actions on specific resources.

#### 2. Services in GreenNode System  <a href="#howiamsupportsvngcloudservices-2.cacdichvutronghethongvngcloud" id="howiamsupportsvngcloudservices-2.cacdichvutronghethongvngcloud"></a>

#### There are three main product lines in GreenNode system, please navigate to detailed instructions to know how to apply IAM with specific products: <a href="#howiamsupportsvngcloudservices-2.cacdichvutronghethongvngcloud" id="howiamsupportsvngcloudservices-2.cacdichvutronghethongvngcloud"></a>

1. **vServer:** [IAM cho vServer](iam-cho-vserver.md)
2. **vStorage:**[ IAM cho vStorage](iam-cho-vstorage.md)
3. **vMonitor:** [IAM cho vMonitor](iam-cho-vmonitor.md)
