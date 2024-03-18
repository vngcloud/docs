# Configure Health Monitor

Health Monitor is one of the very important features of the Load Balancer service, which helps us detect Server down and remove that Server from its Pool.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802716/image2020-5-12_17-19-56.png?version=1&#x26;modificationDate=1685080826000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Information is as follows:

* **Protocol:** Monitor protocol
  * TCP: merely checks the server port, used for Layer 4 and Layer 7 Load Balancers.
  * HTTP: allows users to check the status code of HTTP, allowing users to check for errors at the application level (eg database errors), this is an advanced feature only available in Load Balancer layer 7.
* **Path:** HTTP status code check path, default is set to "/"
* **HTTP method:** Calling method of request like GET, PUT, POST. This information is only available on the Load Balancer layer 7.
* **Healthy threshold:** The number of successful health checks for the Load Balancer to decide to change the member status from ONLINE to ERROR.
* **Unhealthy threshold:** The number of times the health check failed for the Load Balancer to decide to change the member status from ERROR to ONLINE.
* **Timeout:** The time the Load Balancer waits for the member to return the signal.
* **Interval:** How often does the Load Balancer send out a health check.
* **Success code:** User-defined code for Load Balancer to recognize whether a member is ONLINE or ERROR, usually "200". This information is only available on the Load Balancer layer 7.

### **Error message from Health Monitor** <a href="#configurehealthmonitor-errormessagefromhealthmonitor" id="configurehealthmonitor-errormessagefromhealthmonitor"></a>

Some users often wonder when they see the  **ERROR**  status in the  **OPERTATING STATE** column. In this case, it is usually because the Load Balancer health check detects that a member has an error in the Load Balancer's Pool, now we should check the server on the user side to find the cause.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802716/error.jpg?version=1&#x26;modificationDate=1685080826000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
