# Create Application LB in vCloudStack

In this article, we will learn how to use and manage an Application Load Balancer (ALB) with the vCloudStack service.

### **Prerequisites:** <a href="#dieu-kien-tieu-quyet" id="dieu-kien-tieu-quyet"></a>

* A Network is required to do this, refer to the Network configuration article;
* Have an account to access GreenNode with the enterprise's Region CloudStack;
* Have at least one TLS/SSL certificate.

### **How to do:** <a href="#cach-thuc-hien" id="cach-thuc-hien"></a>

**Step 1:** On the Load Balancers homepage, click **"Create a Load Balancer".**

**Step 2:** Configure Load Balancer

* _**Load Balancer Name**_**&#x20;:** If the user does not actively fill in the Load Balancer name, the system will automatically generate the Load Balancer name.
* _**Layer**_**&#x20;:** Select **"Application - HTTP/HTTPS"**
* **Tags:** Fill in the Tags and values ​​to mark the Load Balancer to create
* _**Load Balancer Package**_ : Choose the initialization package that suits your needs and purposes, note that this package is the main factor used to initialize and operate your Load Balancer.
* _**Network Settings**_**&#x20;: Select an** available Network (VPC) from your network list. If you have not initialized a VPC, refer to the Network Configuration guide .

{% hint style="info" %}
vCloudStack service only applies **the Internal Scheme mechanism** , which only allows access to the internal network, so the default system configuration is with the Internal mechanism.
{% endhint %}

**Step 3** : Configure Listener

* **Listener Name:** If the user does not actively fill in the Listener name, the system will automatically generate the Listener name.
* **Protocol & Port**
  * In case of selecting Protocol = **HTTP** : User needs to **select Port** (default pre-filled Port **80** ) and **Header** (default pre-filled X-Fowarded-For, X-Forwarded-Proto, X-Fowarded-Port, can uncheck Header if not needed).
  * In case of selecting Protocol = **HTTPS** : User needs to **select Port** (default pre-filled Port **443** ) and **Certificate** (refer to instructions [Upload a certificate](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/certificate/upload-a-certificate) if no Certificate is available).

**Step 4:** Configure Default Pool

* **Pool Name** : If the user does not actively fill in the Pool name, the system will automatically generate a Pool name.
* **Default HTTP protocol**
* **Algorithm:** Choose the appropriate load balancing algorithm
* **Health Check Settings** : Protocol: TCP / HTTP (enter default path in case of selecting HTTP Protocol)

**Step 5:** Select Pool Member: Add backend servers to the Pool

* **Select Pool Member** from a list of available backend servers belonging to the Load Balancer Network (same subnet as LB)
* **Click the "Attach" button** to add a member server.

**Step 6:** Check initialization information: Users can check configuration information before completing initialization, this information will be displayed on the right side of the input screen.

* **"Summary" tab** : Check the configuration information of Load Balancer, Listener, Pool and Pool Member in turn.
* **"List / Item list" tab:** Check Load Balancer Package information

**Step 7:** Complete initialization: After completing the configuration and checking the information, click the "Create Load Balancer" button to complete the initialization.

**Step 8:** Observe and check ALB

* After successful initialization, the system will redirect the user to the Load Balancer list page, where the user can monitor the Load Balancer initialization status from **Creating** to **Active.**
* After successful initialization, users can access the Load Balancer detail page to observe and check the correctness of the Load Balancer.

Above are the basic instructions for initializing Application Load Balancer in the fastest way. In addition, there are advanced configurations for each different Load Balancer usage needs. Let's learn in detail how an Application Load Balancer works as well as the advanced features of an Application Load Balancer through the Advanced Features article series.
