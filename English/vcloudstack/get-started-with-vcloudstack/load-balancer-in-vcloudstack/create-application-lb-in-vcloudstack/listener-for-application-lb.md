# Listener for Application LB

### Add new HTTP Listener <a href="#them-moi-http-listener" id="them-moi-http-listener"></a>

1/ Access the Load Balancers section;

2/ At Load Balancers, click to select the Load Balancer that needs to add a new Listener.

3/ In the Load Balancer details section, select the Listener tab.

4/ Click the "Add new Listener" button, an interface window appears allowing you to configure Listener information.

5/ In the new window, configure information such as:

* **Listener Name:** Note that the Listener name cannot be changed after initialization.
* **Select HTTP Protocol and Port** (default shows Port 80 and increments if smaller Ports are already in use)
* **Configure request Header** in advanced configuration section: Default is filled with X-Forwarded-For, X-Forwarded-Proto, X-Forwarded-Port, you can uncheck Header if not needed.
* **Default Pool Configuration and Action:** In case requests to Listener are outside the configured Policies list, these requests will be redirected to the default Pool for processing.
* **Advanced Configuration:** Refer to the advanced configuration instructions by feature below.
  * [Config timeout](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/listener/config-timeout)
  * [Config IP whitelist to load balancer](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/listener/config-ip-whitelist-to-load-balancer)

***

### Add new HTTPS Listener <a href="#them-moi-https-listener" id="them-moi-https-listener"></a>

1/ Access the Load Balancers section;

2/ At Load Balancers, click to select the Load Balancer that needs to add a new Listener.

3/ In the Load Balancer details section, select the Listener tab.

4/ Click the "Add new Listener" button, an interface window appears allowing you to configure Listener information.

5/ In the new window, configure information such as:

* **Listener Name:** Note that the Listener name cannot be changed after initialization.
* **Select HTTPS Protocol and Port** (default shows Port 443 and increments if smaller Ports are already in use)
* **Select Default Certificate**
* **Select the list of Certificates to use as SNI:** Note that you cannot remove/change the Certificates used for SNI feature once the HTTPS Listener initialization is complete.
* **Configure request Header** in advanced configuration section: Default is filled with X-Forwarded-For, X-Forwarded-Proto, X-Forwarded-Port, you can uncheck Header if not needed.
* **Enable Client Certificate Authentication:** Client CA is an advanced security feature of Load Balancer that authenticates clients using Certificates. Learn more about [Client Certificate Authentication](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/listener/client-certificate-authentication)
* **Default Pool Configuration and Action:** In case requests to Listener are outside the configured Policies list, these requests will be redirected to the default Pool for processing.
* **Advanced Configuration:** Refer to the advanced configuration instructions by feature below.
  * [Config timeout](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/listener/config-timeout)
  * [Config IP whitelist to load balancer](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vn/vserver/compute-hcm03-1a/vlb-load-balancer-new-version/application-load-balancer/listener/config-ip-whitelist-to-load-balancer)

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

### Listener Policies <a href="#listener-policies" id="listener-policies"></a>

In general, Policies decide how the Load Balancer, specifically the Listener, will handle requests, such as routing to backend servers, performing redirects, and many other features.

#### 1. Add Policy <a href="#listenerpolicies-1.thempolicy" id="listenerpolicies-1.thempolicy"></a>

To add a Policy to the Listener, follow the instructions below.

1/ Access the Load Balancers section;

2/ At Load Balancers, click to select the Load Balancer to configure.

3/ In the Load Balancer details section, select the Listener tab.

4/ Click to select the Listener that needs to add Policy.

5/ In the corresponding Listener details section on the left, scroll to the Policy Information section.

6/ Click the "Add Policy" button in the upper right corner of the Policy Information section.

7/ A pop-up interface window allows you to configure the Policy with information such as

* **Policy Name**
* **If Condition (IF):**
  * Check incoming request based on **HOST/PATH**
  * How to check incoming requests based on HOST/PATH: **CONTAINS** (contains a specific value) / **EQUAL** (contains exactly a specific value)
  * Enter the HOST/PATH value to check
* **Then Action (THEN):** When the above conditions are met, you need to configure additional actions to perform request coordination, currently supporting the following coordination actions
  * **Forward to pool:** When the condition is met, the incoming request will be pushed to the selected pool, so it is necessary **to select a Pool from the list of Pools in the Load Balancer** displayed to direct the incoming request.
  * **Redirect to Url:** Enter the URL you want to redirect the request to when the condition is met.

8/ Click the "Add" button to complete the new addition

#### 2. Update Policy <a href="#listenerpolicies-2.capnhatpolicy" id="listenerpolicies-2.capnhatpolicy"></a>

To update the conditions & actions of a Policy, follow the instructions below.

1/ Access the Load Balancer section;

2/ On the Load Balancer homepage, click to select the Load Balancer that needs to be configured.

3/ In the Load Balancer details section, select the Listener tab.

4/ Click to select the Listener that needs to update Policy.

5/ In the corresponding Listener details section on the left, scroll to the Policy Information section.

6/ In the Policy list, click on the Edit icon on the Policy that needs to be updated.

7/ A pop-up interface window allows you to edit the Policy with information about the If (IF) Condition & Then (THEN) Action

8/ Click the "Add" button to complete the new addition

#### 3. Policy Arrangement <a href="#listenerpolicies-3.sapxeppolicy" id="listenerpolicies-3.sapxeppolicy"></a>

The ordering of Policies on a Listener in a Load Balancer is important because it directly affects how rules and behaviors are applied to traffic. Policies are applied in a top-down order on a Listener. This means that Policies higher up will have priority over Policies lower down. Ordering can allow you to prioritize the application of more important rules first.

To arrange the Policies in the desired order, follow the instructions below.

1/ Access the Load Balancer section;

2/ At Load Balancers, click to select the Load Balancer to configure.

3/ In the Load Balancer details section, select the Listener tab.

4/ Click to select the Listener that needs to add Policy.

5/ In the corresponding Listener details section on the left, scroll to the Policy Information section.

6/ Click the "Reorder" button in the upper right corner of the Policy Information section, next to the Add Policy button.

7/ Here, you can drag/drop Policies according to the desired priority

8/ Click the "Save" button to complete the Policy arrangement at the original "Reorder" button position.

***

### Client Certificate Authentication <a href="#client-certificate-authentication" id="client-certificate-authentication"></a>

**The " Client Certificate Authentication** " feature is an important part of network and application security. It allows you to ensure that only clients or devices with valid authentication certificates can access your application or service. **How it works**

* When a client or device accesses your application, the system asks them to provide a separate digital authentication certificate.
* This certificate is usually created and managed by a certificate authority or PKI (Public Key Infrastructure).
* The system then checks this certificate to ensure that it is valid and can identify the client or device.
* If the certificate is valid, the client or device is authorized to access the application or service.

**Benefit**

* **Increased Security** : Certificate authentication creates a strong layer of security by ensuring that only identified users or devices have access.
* **Detailed Access Management** : You can manage access for each client or device based on individual certificates.
* **Security Compliance** : It helps you comply with strict security rules and standards.

**How to enable/disable Client Certificate Authentication**

For HTTPS Listener, users can proactively enable/disable the Client Certificate feature at any time. **Instructions for enabling/disabling Client Certificate Authentication**

1/ Access the Load Balancer section;

2/ At Load Balancer, click to select the Load Balancer that needs to be edited.

3/ In the Load Balancer details section, select the Listener tab.

4/ Click the Edit icon at HTTPS Listener to enable/disable the Client CA feature.

5/ An interface window will appear, in the Listener information section, find Advanced Settings.

6/ In the Advanced Settings section, check/uncheck the Enable Client CA check box. In case of Enable Client CA, the user needs to select a Certificate from the list of Certificates on the system.

7/ Click the "Save" button in the lower right corner of the window to complete the update.

***

### Config IP whitelist to load balancer <a href="#config-ip-whitelist-to-load-balancer" id="config-ip-whitelist-to-load-balancer"></a>

**The Load Balancer IP Source Whitelist** feature is an important part of network security, allowing you to define specific source IP addresses that the Load Balancer will accept traffic from. IP addresses that are not in the allowed IP range will be denied access. **How it works**

* When a request reaches the Load Balancer, the system checks the source IP address of the request.
* If the source IP address is within the allowed CIDRs range, the request will be accepted and continue to the backend server.
* If the source IP address is not in the allowed CIDRs range, the request will be rejected and not forwarded.

**Why do we need to configure IP Whitelist to Load Balancer?**

* **Enhanced Security** : This feature enhances security by tightly controlling access from unknown source IP addresses.
* **Attack Prevention** : It helps prevent attacks from suspicious or unwanted IP addresses.
* **Access Management** : Whitelist IP Source allows you to manage access to the Load Balancer in a granular and efficient manner.

**Configuration Guide**

1/ Access the Load Balancers section;

2/ At Load Balancers, click to select the Load Balancer to configure.

3/ In the Load Balancer details section, select the Listener tab.

4/ Click the Edit icon at the Listener that needs to be configured.

5/ An interface window will appear, find the Advanced Configuration section at the bottom of the window.

6/ In the Allowed CIDRs section, users can configure the IP range allowed to access.

* For example, if the user enters "192.168.0.0/24, 172.16.0.0/24", it means that only IP addresses in these 2 IP Ranges have access.

7/ Click the "Save" button in the lower right corner of the window to complete the update.

***

### Config timeout <a href="#config-timeout" id="config-timeout"></a>

**The Load Balancer timeout configuration** feature allows you to specify the maximum time a connection or request can exist before being closed. This is important for resource management and ensuring stable system performance.

**How it works**

* When a connection or request is sent to the Load Balancer, the system begins calculating the time allowed for that connection to exist.
* If the connection is not completed or the request is not responded to within this time period, it will be closed.
* Configuring Timeout helps avoid connection or request hangs and resource consumption.

**Why do we need to configure Timeout for Load Balancer?**

* **Resource Management** : Configurable timeouts help efficiently manage system resources by ensuring that unnecessary connections or requests do not consume resources.
* **Performance Guarantee** : This helps ensure that the Load Balancer is always performing efficiently and does not get stuck on unresponsive connections or requests.

**Instructions for configuring timeout for Load Balancer**

1/ Access the Load Balancer homepage

2/ On the Load Balancer homepage, click to select the Load Balancer that needs to be configured.

3/ In the Load Balancer details section, select the Listener tab.

4/ Click the Edit icon at the Listener that needs Timeout configuration.

5/ An interface window will appear, find the Advanced Configuration section at the bottom of the window.

6/ In the Idle Timeout section, users can configure Timeout based on the following properties

* **Client Timeout:**
  * **Explanation** : Client Timeout is the maximum time that the Load Balancer allows a client to maintain a connection to it without making any requests. If there is no activity from the client during this time, the connection will be closed.
  * **Benefits** : This frees up backend server and Load Balancer resources, ensuring that there are no unnecessary connections consuming resources.
* **Member Timeout (Member Timeout):**
  * **Explanation** : Member Timeout is the maximum time that the Load Balancer allows a member server in the backend server group to maintain an open connection without receiving data from it. If the member server does not send data within this time, the connection is closed.
  * **Benefit** : This helps ensure that the member server does not consume resources by maintaining inactive connections.
* **Connection Timeout:**
  * **Explanation** : Connection Timeout is the maximum amount of time that the Load Balancer allows a network connection between itself and a backend server to exist before it is closed. This time starts when the connection is established. If there is no activity on the connection (including data transfer) during this time, the connection will be closed.
  * **Benefits** : This helps ensure that unnecessary connections are closed, freeing up resources and ensuring stable network performance.

7/ Click the "Save" button in the lower right corner of the window to complete the update.
