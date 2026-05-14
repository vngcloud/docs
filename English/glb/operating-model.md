# Operating Model

GLB is a critical solution for ensuring the performance and availability of web applications on a global scale. By distributing traffic to the most appropriate servers, GLB helps minimize latency, improve resiliency, and enhance user experience. Below is an example of how GLB operates.

<figure><img src="../.gitbook/assets/image (441).png" alt=""><figcaption></figcaption></figure>

1. Geographic Distributio&#x6E;**:** You deploy your application servers across multiple geographic regions (for example: HCM-03, HAN-01).
2. GLB Configuratio&#x6E;**:** You configure a GLB to manage traffic distribution across these servers. The GLB continuously monitors server health and network conditions.
3. User Acces&#x73;**:** When a user enters your website address, the request is first sent to the GLB.
4. Location Identificatio&#x6E;**:** The GLB determines the user’s geographic location based on their IP address.
5. Server Selectio&#x6E;**:** Based on the user’s location and other factors (such as server load and server health status), the GLB selects the nearest and most suitable server to handle the request.
6. Request Routin&#x67;**:** The GLB then routes the user’s request to the selected server.

**Key Components in GLB Operations:**

* **Geolocation:** The ability to identify the geographic location of users is a core component of GLB.
* **Load Balancing Algorithms:** GLB uses load balancing algorithms to distribute traffic efficiently, ensuring that no server becomes overloaded.
* **Health check:** GLB continuously performs health checks on servers to detect failures and automatically remove unhealthy servers from traffic distribution.
* **DNS:** GLB typically works closely with the DNS system to route requests to the appropriate server IP addresses.
