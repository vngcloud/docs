# Application Management

### Overview

The **Applications** section allows users to manage all applications (websites or services) protected by the WAF.

From this page, users can:

* View protection status and operating mode
* Check domain configuration and service ports
* Review enabled security features
* See application activation time
* Perform application management actions

This page provides a centralized view of all WAF-protected applications.

#### Application List Information

Each application in the list displays the following information:

* Application name
* Protection mode
* Operational status
* Domain pointing to the WAF
* Service ports
* Enabled protection modules
* Activation time

#### DNS Requirement

The WAF only takes effect once DNS configuration is complete. Every domain in the application must be pointed to the vWAF system using **one of the two methods** below:

* **CNAME** _(recommended)_ — point your service domain's CNAME record to the dedicated DNS domain issued by GreenNode (in the form `<routing-code>.waf.greennode.vn`). With this method, GreenNode can steer traffic to the appropriate vWAF zone without requiring any DNS change on your side.
* **A Record** — point your service domain's A record directly to the public IP address `103.7.174.2`. Works for Root Domains (Apex) and for DNS providers that do not support CNAME at the Root Domain.

Your account's CNAME routing domain is shown in the notice box above the application list on the **Applications** screen.

***

### Add Application

The **Add Application** page allows users to register a new website or service to be protected by the WAF.

Before activating WAF protection, users must configure:

* Application information
* Domain settings
* Service ports
* SSL certificate
* Access method
* Upstream servers

***

### Application Information

#### Application Name

Enter a descriptive name for the application.

This name is used only for identification within the WAF dashboard and does not affect traffic handling.

***

#### Domain

Enter the root domain to be protected by the WAF, without http/https or a wildcard (\*) — e.g. `example.com`.

* Check the box below if you also want to protect the `www` subdomain (e.g. `www.example.com`).

***

#### Ports

Specify the service ports used by your application.

Common ports include:

* **80** for HTTP
* **443** for HTTPS

Each port can be configured as either HTTP or HTTPS.\
Ports can be added or removed as needed.

***

#### SSL Certificate

Select the SSL certificate to be used for HTTPS connections.

Available options include:

* Certificates uploaded by the user
* Free certificates issued by the system
* Certificates previously associated with the account

This field is required if any configured port uses HTTPS.

***

#### Access Method

**Reverse Proxy**

Reverse Proxy is the default and recommended access method.

In Reverse Proxy mode, the WAF sits in front of the origin server and inspects all incoming traffic before forwarding it to the backend.

This mode enables full security capabilities, including:

* Attack detection and blocking
* HTTP flood mitigation
* IP and geo-based access control
* Rate limiting
* Bot detection and mitigation

***

#### Upstream Servers

Configure upstream servers where the WAF forwards clean, filtered traffic.

* Each upstream must be an IP address or domain name
* URL paths are not supported

**Valid examples:**

* `http://192.168.1.10:8080`
* `http://backend.example.com:8080`

Multiple upstream servers can be added for redundancy or load balancing.
