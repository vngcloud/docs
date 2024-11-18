# Install Sigma Media Server

Use the instructions below to install Sigma Media Server:

## Initialize Sigma Media Server on vMarketplace <a href="#khoi-tao-sigma-media-server-tren-vmarketplace" id="khoi-tao-sigma-media-server-tren-vmarketplace"></a>

**Step 1:** Go to [https://marketplace.console.vngcloud.vn/](https://marketplace.console.vngcloud.vn/)

**Step 2:** On the main screen, search for **Sigma , at the Sigma Stream** service , select **Launch** .

**Step 3:** Now, you need to configure **Sigma.** Specifically, you need to choose:

* **Instance Type (CPU, RAM, GPU).**
* **Volume Type and Size, IOPS**
* **Network:**
  * **VPC**
  * **Security Group**

that you want to use for your server. You also need to select an existing Server Group or select **Dedicated SOFT ANTI AFFINITY group** so that we can automatically create a new server group.

**Step 4:** Proceed **to payment** as normal resources on VNG Cloud.

<figure><img src="../../../.gitbook/assets/image (308).png" alt=""><figcaption></figcaption></figure>

**At this point, the vServer** system will initialize a Server corresponding to the configuration you selected. Please wait until the server creation is complete and continue with the following steps.

{% include "../../../.gitbook/includes/untitled (1).md" %}

***

## Configure parameters for Sigma Media Server <a href="#cau-hinh-thong-so-cho-sigma-media-server" id="cau-hinh-thong-so-cho-sigma-media-server"></a>

**Step 1:** After initializing Sigma from **vMarketPlace** according to the instructions above, you can access the vServer interface [here ](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server)**to** check if the server running Sigma has been initialized. <mark style="color:red;">**Next, you need to open the following on the Security Group for the newly created Sigma server.**</mark>

* 4000 (TCP): Portal
* 8080 (TCP): HTTP origin (nginx)
* 1935 (TCP): RTMP
* 10080 (UDP): optional for SRT protocol

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FlytKYGRvfmp19ZNor1Ww%252Fimage.png%3Falt%3Dmedia%26token%3D2a0206fc-b228-4d88-84f9-4c87938524b5&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=49524cf2&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 2:** After the Sigma server is successfully initialized. To access the Sigma GUI, you need to use the External Interface IP address and access the link: _**http://VM\_External\_IP:4000**_

**Step 3:** At Sigma's GUI, select the **Register Server** button

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FfPhvc5h9OCIvfn8uhZYj%252Fimage.png%3Falt%3Dmedia%26token%3D358a4780-6a07-468e-8022-a7c02f056b15&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=48f56f1b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 4:** Enter **Email/ Password** if you have one or choose **Quick Login** with **Github** or **Google** . Here, I choose to log in with my Google account.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FUHJXVxlIjobdsCJcb6Ge%252Fimage.png%3Falt%3Dmedia%26token%3Db3d93d1e-d897-4118-a321-e6d378383a85&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=89980f0d&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 5** : After the system successfully performs **authentication** , you need to enter basic information for Sigma including:

* **Name**
* **Phone Number**
* **Role**
* **Company**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FsVFs2cOt2W4mnmviIbna%252Fimage.png%3Falt%3Dmedia%26token%3D991a317e-2fad-46bd-9ae4-7639c5508567&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d3d5fa82&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 6:** Enter **the server name** . You can get this server name from the VNGCloud portal. In the example below, I use the Demo\_Sigma server created earlier.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F0M8ZMPrOMBLt7GIOz5MT%252Fimage.png%3Falt%3Dmedia%26token%3D4bf2afc8-8bc0-4c86-9f5b-2d130f3a827c&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=748ffbc4&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 7** : You can adjust on/off configurations including:

* Turn On/Off using **Ingest App** by selecting ON, OFF icon
* Turn on/off using **Origin App** by selecting the ON, OFF icon
* Install **Data Dir** by selecting the Pick button
* Select **Submit** .

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FGQ1nMkuhbM1gelDIS7hR%252Fimage.png%3Falt%3Dmedia%26token%3Db1a566c3-ee04-4f87-9bf6-5b07b5ba7d51&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=900579bb&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 8** : At the server deployment warning screen, select **Yes**

**Step 9:** Continue to select **Done** , the screen will display as follows, continue to select **App Editor.**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FlviHVFWVe5po6a9WI00m%252Fimage.png%3Falt%3Dmedia%26token%3D0379f3b6-89b2-4a4a-880d-63d5e2e1cb09&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=e82bb5a&#x26;sv=1" alt=""><figcaption></figcaption></figure>

After accessing **the Sigma Media Portal** , you will see the previously created server information from **vMarketplace** and the corresponding **License** information .

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FZISwHElEpHiUtQqTXffx%252Fimage.png%3Falt%3Dmedia%26token%3D1cc02598-ac9b-4195-ab85-403acc8429df&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=74863fdd&#x26;sv=1" alt=""><figcaption></figcaption></figure>
