---
description: >-
  VNG Cloud Endpoint is the private connection point between VPC and VNG Cloud
  services
---

# Create Endpoint

How to create

{% hint style="danger" %}
**Important**

_<mark style="color:blue;">In the same region, corresponding to one VPC, users are only allowed to create one Endpoint connecting to a specified VNG Cloud service (e.g., vStorage)</mark>_
{% endhint %}

* Users log in to the link [https://hcm-3-vnetwork.console.vngcloud.vn/endpoint/list](https://hcm-3-vnetwork.console.vngcloud.vn/nat/list), region = HCM
* Select the "**Endpoint**" menu from the left-hand menu bar.
* Select the "**Create an Endpoint**" function
* Enter the Endpoint information as required, including:

&#x20;  \- **Endpoint Name**: Name of Endpoint        &#x20;

&#x20;  \- **Service Package**: The Endpoint service package provides a default configuration of the Standard package, users do not need to choose a service package

&#x20;  \- **Service Selection**: The services of VNG Cloud to which the endpoint connects, choose a value from the list consisting of vServer, vStorage, vMonitor, vCR, IAM

* Select the VPC and subnet you want to connect with VNG Cloud services through the service endpoint.
* Check the service price information in the "**Summary**" section
* Click on “**CREATE ENDPOINT**”

Users will wait for the system to create the Endpoint until it is completed. When the Endpoint is successfully created, users will see the Endpoint appear on the Endpoint list screen.



## How to use

After creating Endpoint, users still cannot access Endpoint Service, do some steps below to config your Servers' access Eto ndpoint Service privately

#### Access the Endpoint List and Select your Endpoint

At detail, page will provide two main information

* Endpoint Url: This is the Public URL of the Endpoint Service
* Endpoint IP: Use this IP to add a host in the Servers that need to go with private

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Endpoint List</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Endpoint Detail</p></figcaption></figure>



#### Add host and Try to access Endpoint Url

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Add host</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

