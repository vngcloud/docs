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

For all traffic to be audited and protected by **VNG Cloud’s WAF**, all domains in applications **must have their DNS A record pointed to the service’s public IP address `103.7.174.2`**.

WAF protection will not become effective until this DNS configuration is completed.

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

Enter one or more domains to be protected by the WAF.

* Multiple domains can be added by pressing **Enter** or separating them with spaces
* Wildcard domains such as `*.example.com` are supported

**System notice:**

All domains must have their DNS A record pointed to `103.7.174.2` before WAF protection becomes effective.

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
