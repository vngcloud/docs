# Create Network LB in vCloudStack

In this article, we will learn how to use and manage a Network Load Balancer (ALB) with the vCloudStack service.

### **Prerequisites:** <a href="#dieu-kien-tieu-quyet" id="dieu-kien-tieu-quyet"></a>

* A Network is required to do this, refer to the Network configuration article;
* Have an account to access VNG Cloud with the enterprise's Region CloudStack;
* Have at least one TLS/SSL certificate.

### **How to do:** <a href="#cach-thuc-hien" id="cach-thuc-hien"></a>

**Step 1:** On the Load Balancer homepage, click **"Create a Load Balancer".**

**Step 2:** Configure Load Balancer

* _**Load Balancer Name**_**&#x20;:** If the user does not actively fill in the Load Balancer name, the system will automatically generate the Load Balancer name.
* _**Layer**_**&#x20;:** Select **"Network - TCP/UDP"**
* **Tags:** Fill in the Tags and values ​​to mark the Load Balancer to create
* _**Load Balancer Package**_ : Choose the initialization package that suits your needs and purposes, note that this package is the main factor used to initialize and operate your Load Balancer.
* _**Network Settings**_**&#x20;: Select an** available Network (VPC) from your network list. If you have not initialized a VPC, refer to the Network Configuration guide .

{% hint style="info" %}
vCloudStack service only applies **the Internal Scheme mechanism** , which only allows access to the internal network, so the default system configuration is with the Internal mechanism.
{% endhint %}

**Step 3** : Configure Listener

* **Listener Name:** If the user does not actively fill in the Listener name, the system will automatically generate the Listener name.
* **Protocol & Port**
  * In case of selecting Protocol = **TCP** : User needs to **select Port** (default pre-filled Port **80)** .
  * In case of selecting Protocol = **UDP** : User needs to **select Port** (default pre-filled Port **53** ).

**Step 4:** Configure Default Pool

* **Pool Name** : If the user does not actively fill in the Pool name, the system will automatically generate a Pool name.
* **Protocol TCP/Proxy** (for TCP Listener) or **UDP** (for UDP Listener)
* **Algorithm:** Choose the appropriate load balancing algorithm
* **Health Check Settings** : Protocol: **TCP / HTTP / HTTPS** (for TCP/Proxy Pool) or **PING-UDP** (for UDP Pool)

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

Above are the basic instructions for initializing Network Load Balancer in the fastest way. In addition, there are advanced configurations for each different Load Balancer usage needs. Let's learn in detail how a Network Load Balancer works as well as the advanced features through the following series of articles.
