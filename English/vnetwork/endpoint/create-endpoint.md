# Create Endpoint



{% hint style="danger" %}
**Important**

_<mark style="color:blue;">In the same region, corresponding to one VPC, users are only allowed to create one Endpoint connecting to a specified VNG Cloud service (e.g., vStorage)</mark>_
{% endhint %}

* Users log in to the link [https://hcm-3-vnetwork.console.vngcloud.vn/endpoint/list](https://hcm-3-vnetwork.console.vngcloud.vn/nat/list), region = HCM
* Select the "**Endpoint**" menu from the left-hand menu bar.
* Select the "**Create an Endpoint**" function
* Enter the Endpoint information as required, including:

&#x20;  \- **Endpoint Name**: Name of Endpoint        &#x20;

&#x20;  \- **Service Package**: The Endpoint service package provides a default configuration of Standard package, users do not need to choose a service package

&#x20;  \- **Service Selection**: The services of VNG Cloud to which the endpoint connects, choose a value from the list consisting vServer, vStorage, vMonitor, vCR, IAM

* Select the VPC and subnet you want to connect with VNG Cloud services through the service endpoint.
* Check the service price information in the "**Summary**" section
* Click on “**CREATE ENDPOINT**”

Users will wait for the system to create the Endpoint until it is completed. When the Endpoint is successfully created, users will see the Endpoint appears on the Endpoint list screen.

