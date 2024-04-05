# Initialize Load Balancer Layer 7

![(tick)](https://docs.vngcloud.vn/s/en\_US/8100/e533a30abc9e1cf90ba3519e12647de186f0ee76/\_/images/icons/emoticons/check.svg) VNG Cloud data provides a dashboard to easily create  Load Balancer.

***

### Before start <a href="#initializeloadbalancerlayer7-beforestart" id="initializeloadbalancerlayer7-beforestart"></a>

To create a Load balancer you need to have a network, if you haven't created one you can see the tutorial [Work with VPC - Create a network](../vpc/virtual-private-cloud-vpc.md)

### Initialize Load Balancer <a href="#initializeloadbalancerlayer7-initializeloadbalancer" id="initializeloadbalancerlayer7-initializeloadbalancer"></a>

Select **Load balancer** and select create **load balancer** layer 7 - HTTP/HTTPS



<figure><img src="https://docs.vngcloud.vn/download/attachments/59802658/image2019-5-8_11-1-4.png?version=1&#x26;modificationDate=1685071049000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### **Step 1**: Configuration of Load balancer <a href="#initializeloadbalancerlayer7-step1-configurationofloadbalancer" id="initializeloadbalancerlayer7-step1-configurationofloadbalancer"></a>

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802658/image2019-5-8_14-8-25.png?version=1&#x26;modificationDate=1685071049000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Global Setting:**&#x20;

* **Name**: Reminiscent name for Load balancer, minimum 6 characters required (a-z, 0-9)
* **Scheme:**
  * Internet facing: For all access from the internet
  * Internal: For internal network access

**Listener setting**

* **Listener name**: listener name, minimum 6 characters required (a-z, 0-9)
*   **Protocol:** HTTP or HTTPS. When you choose HTTPS you will need to upload the certificate.\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802658/image2019-5-12_16-51-6.png?version=1&#x26;modificationDate=1685071050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
* **Port:** Will vary depending on HTTP (80) or HTTPS (443) selection. You can also customize it according to your needs

**Network setting**

* **Network**: Select one of the networks you have created, if you don't have one, you can see the instructions [Create a network](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648036)

#### **Step 2**: Configure Pool <a href="#initializeloadbalancerlayer7-step2-configurepool" id="initializeloadbalancerlayer7-step2-configurepool"></a>

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802658/image2019-5-12_16-59-25.png?version=1&#x26;modificationDate=1685071050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Pool setting**&#x20;

* **Name**: reminder name for pool, minimum 6 characters required (a-z, 0-9)
* **Algorithm:** Includes 3 options
  * Round robin: Connections will be distributed evenly to the instance in the pool.
  * Least connection: Based on the number of connections to perform load balancing, the instance with the smallest number of connections will be brought up to receive the connection.
  * Source IP&#x20;
* **Enable Sticky Sessions**
* **Protocol**

**Heath Setting**&#x20;

* Path: leads to where you need health check
* Protocol

&#x20;The **advanced settings** will default to be configured as below, you can adjust according to your needs\
\
\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59802658/image2019-5-12_17-10-16.png?version=1&#x26;modificationDate=1685071050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### **Step 3**: Add the instance to the Loadbalancer pool <a href="#initializeloadbalancerlayer7-step3-addtheinstancetotheloadbalancerpool" id="initializeloadbalancerlayer7-step3-addtheinstancetotheloadbalancerpool"></a>

Select the available instances and attach to the pool, if you don't have any instance you can skip this step and add it later:

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802658/image2019-5-12_17-21-13.png?version=1&#x26;modificationDate=1685071050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### **Step 4:** Summary  <a href="#initializeloadbalancerlayer7-step4-summary" id="initializeloadbalancerlayer7-step4-summary"></a>

Review the Load balancer settings you've made including the Load balancer package you'll need to pay for.

Currently, VNG Cloud data load balancer provides 2 types of packages, Mini and Medium. At the default settings you can only create and pay for Mini packages, if you have a need to use a larger package, please contact 1900-1549 for support.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802658/image2019-5-12_17-22-36.png?version=1&#x26;modificationDate=1685071050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Select create load balancer to make the payment step&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802658/image2019-5-12_17-29-39.png?version=1&#x26;modificationDate=1685071050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Select pay and finish creating. Your load balancer will appear at the load balancer general management interface as below

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802658/image2019-5-12_17-30-14.png?version=1&#x26;modificationDate=1685071050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
