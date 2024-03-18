# Configure HTTPS Redirect for Load Balancer

In our case our Load balancer (LB) is running HTTPS and wants all HTTP traffic to the LB to switch to HTTPS. We have to create a listener that runs HTTP to catch all traffic from HTTP, then create a policy that uses the Redirect to URL action to forward traffic to the listener running HTTPS. The steps are as follows:

**1. Create a Listener that runs the HTTP protocol**

_If you already have a listener running the HTTP protocol, then skip this step and do step 2 (add policy redirect)._

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802700/http_https1.jpg?version=1&#x26;modificationDate=1685076377000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 1:** Select the Load Balancers (LB) tab.

**Step 2:** Select the LB name to configure.

**Step 3:** Select the **LISTENER** tab.

**Step 4:** Select **ADD LISTENER.**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802700/image2020-5-12_10-44-26.png?version=1&#x26;modificationDate=1685076377000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Add the following information:

* Friendly name: give the listener a name.
* Protocol: select the HTTP protocol.
* Port: select port 80 (or desired port).
* Action: leave default (no effect for redirect purposes).

**2. Add Policy redirect for Listener running HTTP protocol**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802700/http_https.jpg?version=1&#x26;modificationDate=1685076378000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 1:** Select the **Load Balancers** (LB) tab.

**Step 2:** Select the LB name to configure.

**Step 3:** Select the **LISTENER** tab and select the Listener name to be configured.

**Step 4:** Select **ADD POLICY.**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802700/https.jpg?version=1&#x26;modificationDate=1685076378000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Add the following information:

* Information: give the name for **Policy name**
* If clause chooses HOST, the other clause chooses contains.
  * **Text box** to enter the domain name to redirect.
* Action: select **Redirect to URL**.
  * **URL to direct** enter the path to redirect.
  * _**HTTP Response code**_ select 301.
  * _**Keep query string** selects the tick mark._

Once done select **ADD POLICY.**

\
