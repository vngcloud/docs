# Listener for Network LB

### Add **new TCP Listener** <a href="#them-moi-tcp-listener" id="them-moi-tcp-listener"></a>

1/ Access the Load Balancers section;

2/ At Load Balancers, click to select the Load Balancer that needs to add a new Listener.

3/ In the Load Balancer details section, select the Listener tab.

4/ Click the "Add new Listener" button, an interface window appears allowing you to configure Listener information.

5/ In the new window, configure information such as:

* **Listener Name:** Note that the Listener name cannot be changed after initialization.
* **Select TCP Protocol and Port** (default shows Port 80 and increments if smaller Ports are already in use)
* **Default Pool Configuration and Action:** In case requests come to the Load Balancer that do not match any specific pool, NLB will redirect that traffic to the default pool.
* **Advanced Configuration:** Refer to the advanced configuration instructions by feature below.
  * [Config timeout](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/listener/config-timeout)
  * [Config IP whitelist to load balancer](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/listener/config-ip-whitelist-to-load-balancer)

***

### **Add new UDP Listener** <a href="#them-moi-udp-listener" id="them-moi-udp-listener"></a>

1/ Access the Load Balancers section

2/ On the Load Balancers homepage, click on the Load Balancer that needs to add a new Listener.

3/ In the Load Balancer details section, select the Listener tab.

4/ Click the "Add new Listener" button, an interface window appears allowing you to configure Listener information.

5/ In the new window, configure information such as:

* **Listener Name:** Note that the Listener name cannot be changed after initialization.
* **Select UDP Protocol and Port** (default shows Port 53 and increments if smaller Ports are already in use)
* **Default Pool Configuration and Action:** In case requests come to the Load Balancer that do not match any specific pool, NLB will redirect that traffic to the default pool.
* **Advanced Configuration:** Refer to the advanced configuration instructions by feature below.
  * [Config timeout](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/listener/config-timeout)
  * [Config IP whitelist to load balancer](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/listener/config-ip-whitelist-to-load-balancer)

**Note:** Note that you can only select Pool with UDP protocol to specify as default Pool for UDP Listener

***

### Change Listener information <a href="#update-and-deletelistener-nlb-thaydoithongtinlistener" id="update-and-deletelistener-nlb-thaydoithongtinlistener"></a>

1/ Access the Load Balancers section

2/ On the Load Balancers homepage, click on the Load Balancer that needs to edit the Listener.

3/ In the Load Balancer details section, select the Listener tab.

4/ In the Listener list, hover your mouse over the Listener you want to edit, an "Edit" icon will appear, click on that icon to start editing the Listener.

5/ An editing interface window appears, users can edit the following information:

* **Change Default Pool:** In case requests come to the Load Balancer that do not fit into any specific pool, NLB will redirect that traffic to the default pool.
* **Change advanced configuration:** Refer to the advanced configuration instructions by feature below.
  * [Config timeout](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/listener/config-timeout)
  * [Config IP whitelist to load balancer](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/listener/config-ip-whitelist-to-load-balancer)

6/ Click the "Save" button to complete editing

***

### Delete Listener <a href="#update-and-deletelistener-nlb-xoalistener" id="update-and-deletelistener-nlb-xoalistener"></a>

1/ Access the Load Balancer section

2/ At Load Balancers, click to select the Load Balancer that needs to delete the Listener.

3/ In the Load Balancer details section, select the Listener tab.

4/ In the Listener list, click the "Delete" icon in the Listener row to be deleted.

5/ An interface window will appear to confirm deletion, click the "Delete" button to complete.

***

### Configure IP Whitelist to Load Balancer (NLB) <a href="#cau-hinh-ip-whitelist-to-load-balancer-nlb" id="cau-hinh-ip-whitelist-to-load-balancer-nlb"></a>

**The Load Balancer IP Source Whitelist** feature is an important part of network security, allowing you to define specific source IP addresses that the Load Balancer will accept traffic from. IP addresses that are not in the allowed IP range will be denied access. **How it works**

* When a request reaches the Load Balancer, the system checks the source IP address of the request.
* If the source IP address is within the allowed CIDRs range, the request will be accepted and continue to the backend server.
* If the source IP address is not in the allowed CIDRs range, the request will be rejected and not forwarded.

**Why do we need to configure IP Whitelist to Load Balancer?**

* **Enhanced Security** : This feature enhances security by tightly controlling access from unknown source IP addresses.
* **Attack Prevention** : It helps prevent attacks from suspicious or unwanted IP addresses.
* **Access Management** : Whitelist IP Source allows you to manage access to the Load Balancer in a granular and efficient manner.

**Configuration Guide**

* Visit the Load Balancers homepage.​
* At Load Balancers, click to select the Load Balancer to configure.
* In the Load Balancer details section, select the Listener tab.
* Click the Edit icon at the Listener that needs to be configured.
* An interface window will appear, look for the Advanced Configuration section at the bottom of the window.
* In the Allowed CIDRs section, users can configure the IP range allowed for access.
  * For example, if the user enters "192.168.0.0/24, 172.16.0.0/24", it means that only IP addresses in these 2 IP Ranges have access.
* Click the "Save" button in the lower right corner of the window to complete the update.

***

### Configure timeout (NLB) <a href="#cau-hinh-timeout-nlb" id="cau-hinh-timeout-nlb"></a>

**The Load Balancer timeout configuration** feature allows you to specify the maximum time a connection or request can exist before being closed. This is important for resource management and ensuring stable system performance. **How it works**

* When a connection or request is sent to the Load Balancer, the system begins calculating the time allowed for that connection to exist.
* If the connection is not completed or the request is not responded to within this time period, it will be closed.
* Configuring Timeout helps avoid connection or request hangs and resource consumption.

**Why do we need to configure Timeout for Load Balancer?**

* **Resource Management** : Configurable timeouts help efficiently manage system resources by ensuring that unnecessary connections or requests do not consume resources.
* **Performance Guarantee** : This helps ensure that the Load Balancer is always performing efficiently and does not get stuck on unresponsive connections or requests.

**Instructions for configuring timeout for Load Balancer**

* **Go** to Load Balancer.
* On the Load Balancer homepage, click on the Load Balancer that needs to be configured.
* In the Load Balancer details section, select the Listener tab.
* Click the Edit icon at the Listener that needs Timeout configuration.
* An interface window will appear, look for the Advanced Configuration section at the bottom of the window.
* In the Idle Timeout section, users can configure Timeout based on the following properties
  * Client Timeout:
    * Explanation: Client Timeout is the maximum time that the Load Balancer allows a client to stay connected to it without making any requests. If there is no activity from the client during this time, the connection will be closed.
    * Benefits: This frees up backend server and Load Balancer resources, ensuring that there are no unnecessary connections consuming resources.
  * Member Timeout (Member Timeout):
    * **Explanation** : Member Timeout is the maximum time that the Load Balancer allows a member server in the backend server group to maintain an open connection without receiving data from it. If the member server does not send data within this time, the connection is closed.
    * **Benefit** : This helps ensure that the member server does not consume resources by maintaining inactive connections.
    * **Connection Timeout:**
      * **Explanation** : Connection Timeout is the maximum amount of time that the Load Balancer allows a network connection between itself and a backend server to exist before it is closed. This time starts when the connection is established. If there is no activity on the connection (including data transfer) during this time, the connection will be closed.
      * **Benefits** : This helps ensure that unnecessary connections are closed, freeing up resources and ensuring stable network performance.
* Click the "Save" button in the lower right corner of the window to complete the update.
