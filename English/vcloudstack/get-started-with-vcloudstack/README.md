# Get Started with vCloudStack

Use this guide to get started with **vCloudStack** . You will learn the basic components and scope of operations management that GreenNode's vCloudStack service provides you, so you can better understand and operate your business system.

### Infrastructure <a href="#cau-truc-ha-tang" id="cau-truc-ha-tang"></a>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FzOl7OtlGVLs9JNwToWZU%252Fe87245f2-7905-4126-963a-057504a3c03e.png%3Falt%3Dmedia%26token%3D311ad4ac-efb6-4ae4-9ae4-eadbb7003155&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=cc7cd766&#x26;sv=1" alt=""><figcaption><p>vCloudStack Deployment Infrastructure</p></figcaption></figure>

As introduced, vCloudStack provides cloud computing services right at the customer's local premises, so most of the components will be located and managed at the customer's premises such as:

* Network devices such as **Firewalls** and Routers **(Switches** );
* Devices for virtualization and storage such as **Compute Nodes/Storage Nodes/Backup Nodes** .

The components that vCloudStack will directly operate and manage at GreenNode include:

* The interface ( **Portal** ) for virtualization and internal virtual machine operation is completely consistent with the general interface of GreenNode;
* Middleware ;**​**
* Virtual machine processor and controller ( **Controller** ).

### Administration and operations interface <a href="#giao-dien-quan-tri-va-van-hanh" id="giao-dien-quan-tri-va-van-hanh"></a>

From the infrastructure installed at the enterprise's internal facilities, vCloudStack provides operational management interfaces with necessary functions for system administrators and operators to easily operate.

#### 1/ vCloudStack Admin Site <a href="#vcloudstack-admin-site" id="vcloudstack-admin-site"></a>

System administrators are usually senior staff (admin) whose administrative role requires them to grasp all the information that the network system is operating, especially information about physical infrastructure and virtualization information, as well as managing personnel accessing and operating the virtual machine system. Therefore, vCloudstack provides businesses with a comprehensive administration interface for users who are system-level administrators, which is vCloudstack Admin Site, this interface provides the following main features:

* **Dashboard:** Physical resource management;
* **User Management:** Manage, authorize and limit usage for operating personnel;
* **Infrastructure:** Monitor virtualization resource information (compute/storage/network/backup);
* **User Resource:** Monitors the operations staff's management of virtualized resources (Server/Volume).

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fs1bZgekkiP1yAIGZ6sVp%252Fimage.png%3Falt%3Dmedia%26token%3D11ecfcd2-a096-4545-b9d5-32c738ccc6e3&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=dd277bf&#x26;sv=1" alt=""><figcaption><p>Admin Site Management Interface</p></figcaption></figure>

#### 2/ vCloudStack User Site <a href="#vcloudstack-user-site" id="vcloudstack-user-site"></a>

To operate the hybrid network system, vCloudStack provides a server virtualization management interface called vCloudStack User Site. This interface allows performing server virtualization functions such as:

* **Server:** Server virtualization and server operations;
* **Blockstore** : Create storage, backup, snapshot for virtual server;
* **Network:** Manage the network part for the server and distribute traffic with LoadBalancer;

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FzQ85D88QigqSjKKc38NN%252Fimage.png%3Falt%3Dmedia%26token%3De617442b-a5a3-4378-a4a1-93081c704331&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6c2b9043&#x26;sv=1" alt=""><figcaption><p>User Site Operating Interface</p></figcaption></figure>
