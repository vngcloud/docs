# Replace SSL Certificate for vLB Layer 7

When there is a need to replace the SSL Certificate (expiry, change domain name, ...) you need to upload a new certificate and proceed to delete and recreate the Listener with a new Certificate.

**Step 1**: Go to the management tab Certificateand use the option Upload Certificate  to update new certificates

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802758/image2021-10-27_12-27-11.png?version=1&#x26;modificationDate=1685085893000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

You can refer to the instructions for [Uploading certificates here](https://docs.vngcloud.vn/display/VSERVERENG/Upload+Certificates)

For example, in this tutorial, the writer uploads 2 new certificates, [cert\_www.server1.com](http://cert\_www.server1.com/) and  [cert\_www.server2.com](http://cert\_www.server2.com/).

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802758/image2021-10-27_12-27-33.png?version=1&#x26;modificationDate=1685085893000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 2:**  From the Load Balancer management tab, you remember the current Default Pool (if there are many pools) and then  delete the Listener with the **Delete** option at the Listener tab of the respective Load Balancer. Here the current Default Pool is: **demo\_https\_pool**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802758/image2021-10-27_12-27-53.png?version=1&#x26;modificationDate=1685085893000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 3**: Also at the Listener Tab, we select the option **Add Listener** to add a new Listener

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802758/image2021-10-27_12-28-14.png?version=1&#x26;modificationDate=1685085893000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


**Step 4**: Enter the necessary information to create a Listener

\+ Friendly name: Enter the name of the Listener

\+ Protocol & Port: Here we choose the HTTPS protocol and can replace the default HTTPS port of 443 if needed.

\+ **SSL CERTIFICATE**: here we select the new SSL Certificates that have been updated at **Step 1**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802758/image2021-10-27_12-28-32.png?version=1&#x26;modificationDate=1685085893000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


\+ The  **DEFAULT ACTION** ta section selects the pool corresponding to the old Listener just deleted in **Step 2**.

\+ Finally, we can change more advanced configurations at the **ADVANCED CONFIGURATION** section (see more [Advanced configuration options here](configure-timeout-for-load-balancer.md))

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802758/image2021-10-27_12-28-48.png?version=1&#x26;modificationDate=1685085894000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


**Bước 5**: After entering the information, select **Add Listener** to create a new one

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802758/image2021-10-27_12-29-10.png?version=1&#x26;modificationDate=1685085894000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

You wait a while for the system to update the new configuration.

**Result**: After the creation is complete, you will see the Listener appear with the updated certificate information

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802758/image2021-10-27_12-29-27.png?version=1&#x26;modificationDate=1685085894000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
