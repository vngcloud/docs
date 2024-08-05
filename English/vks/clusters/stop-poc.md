# Stop POC

Before learning how to Stop POC for your resources on VKS, you should clearly understand the concepts and actions you can take on POC resources. For more details, refer [here](https://docs.vngcloud.vn/vng-cloud-document/v/vn/quan-ly-hoa-don-chi-phi-and-tai-nguyen-tren-vng-cloud/trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/quan-ly-vong-doi-tai-nguyen/tai-nguyen-poc) .

**Before your POC wallet for Cluster expires, you have two main options:**

* Delete this POC Cluster and recreate another normal Cluster.
* Perform Stop POC to renew the POC Cluster into a normal Cluster.

**To continue using the resource that just stopped POC as a normal resource (for the purpose of keeping the configuration intact), the user can do:**

**Step 1:** Access [VKS Portal](https://vks.console.vngcloud.vn/k8s-cluster) , select the Cluster where you want to Stop POC.

**Step 2:** Select the **Stop POC** button on the top right corner of the screen.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FpfruVD7gRlq4Wh1Y6Gtk%252Fimage.png%3Falt%3Dmedia%26token%3Dcededf5a-1c49-4dd8-8d6f-ec11c7c767c8&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c04f0731&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 3:** At this time, the screen displays a list of all Servers and Volumes in the Cluster ( **including the Boot Volume and PVC that you attached to the node in your Cluster)** that have POC status. You can check the information then select **Stop POC**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fw16qab1QEjCdG5g6eec0%252Fimage.png%3Falt%3Dmedia%26token%3D70a44312-fb8f-4849-8b3b-2d1ca50e74ce&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=94da8eda&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 4** : Proceed to pay for resources with real money, you can select **the desired usage cycle, turn on and off Auto-renew, enter Coupon** if available and select **Continue** to make Resource Payment

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FThz0n36JDLF67s09vEDh%252Fimage.png%3Falt%3Dmedia%26token%3De7710865-a83f-4c24-8446-2a21b0041625&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=65a25c33&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 5** : Make payment using credit balance or other forms of payment if available.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FqoEayKltx0kYxI6gz7HJ%252Fimage.png%3Falt%3Dmedia%26token%3Dadef3c84-9734-426c-b62d-9697da8c9896&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ba64fd8a&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**To ensure VKS works correctly, Stop POC implementation needs to be performed on VKS Portal instead of doing it individually on each resource server or volume on vServer Portal.** If you have previously performed an individual POC stop for each resource on vServer Portal, you still **need to perform a POC Stop** for the Cluster at VKS Portal. At this time, the screen will display as follows. Please press **Stop** to turn off the POC option for your Cluster.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FjXKXT8x32vWWcPdnDXJ1%252Fimage.png%3Falt%3Dmedia%26token%3D7a469b1a-438c-4d23-a58e-ff48ba51f6ab&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=bb9fa80d&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Attention:**

* After stopping POC on VKS, the "Stop POC" button will continue to display if there are still resources that have not been Stop POC after doing so on VKS Portal. You can continue to select and execute Stop POC until all resources are converted to real resources.
* Currently, VKS only applies payment by POC for Server and Volume and has not yet applied payment for Load Balancer and Snapshot by POC. Therefore, you do not need to perform Stop POC for these two resource types Load Balancer and Snapshot.
