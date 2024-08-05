# Pfsense as a NAT Gateway

Use the instructions below to work with Private Node groups through Pfsense

### Prerequisites <a href="#dieu-kien-can" id="dieu-kien-can"></a>

To be able to use Pfsense as NAT Gateway for Cluster on VKS system, you need:

* A **Pfsense server (VM)** is initialized on the **vMarketPlace** system according to the instructions below with the following configuration:

| Item                | Configuration |
| ------------------- | ------------- |
| Flavor              | 2x4           |
| Volume              | 80 GB         |
| VPC                 | 10.3.0.0/16   |
| Network Interface 1 | 10.3.0.3      |

***

### Initialize Pfsense <a href="#khoi-tao-pfsense" id="khoi-tao-pfsense"></a>

**Step 1:** Visit [https://marketplace.console.vngcloud.vn/](https://marketplace.console.vngcloud.vn/)

**Step 2:** At the main screen, search for **Pfsense , at Pfsense** service , select **Launch** .

**Step 3:** Now, you need to configure **Pfsense.** Specifically, you can select the desired **Volume, IOPS, Network, Security Group . You need to choose the same VPC and Subnet as the VPC and Subnet you choose to use for your Cluster.** In addition, you also need to select an existing Server Group or select **Dedicated SOFT ANTI AFFINITY group** so we can automatically create a new server group.

**Step 4:** Proceed to pay like normal resources on VNG Cloud.

***

### Configure parameters for Pfsense <a href="#toc165621058" id="toc165621058"></a>

**Step 1:** After initializing Pfsense from vMarketPlace according to the instructions above, you can access the vServer interface here [to](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) check whether the server running Pfsense has been initialized.

**Step 2: After the server running Pfsense is successfully initialized** . To access the Pfsense GUI, you need to use the IP address of the External Interface to log in with the default Username and password **admin/pfsense.**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2Fp1.png\&width=768\&dpr=4\&quality=100\&sign=445b98d\&sv=1)

* To get this IP information, go to **the Network Interface** section of **Pfsense** to view the information

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-29da2d3106656e3bc2cbe21bca05696379cb309c%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=f6396195\&sv=1)

**Step 3** : Conduct **General Setup** , please do as below

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-6150904a1d7485347d9045989cbb5ebd51e0be6b%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=cf9635b\&sv=1)![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-d678f47c3c75a99f562786b2237ddd2dd5f0a73c%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=db5b9aba\&sv=1)![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-84723c07c391c9402e1366000a49b2a7d243c56a%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=125d2166\&sv=1)![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-b094e72b1f3b9d0b47c8139ba925669706dcc937%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=13e35f32\&sv=1)

* Configure **WAN Interface**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-3cd0c6f853cc345aadd6946305687f7546457555%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=947d1b0d\&sv=1)

* Change **password** in **GUI**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-7df721d64edd2afa45b556b7efd4f59965f271a4%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=b88507a7\&sv=1)

* Proceed **to reload**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-4aa595195ac176ee2401b974d3cebbdc4312ea9c%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=1c4968d4\&sv=1)

* **General Setup** completed

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-4e21c606d00e58607a553685328289b76d07f787%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=90b8d868\&sv=1)

**Step 4** : Open **the rule** on **the firewall**

* Proceed to **Add rule**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-1c4bb2f050c45904dc4e24d8e72c2eda4c4c9295%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=f37d8a05\&sv=1)

* You can open the rule as below to access the GUI using **External Interface** .

**Attention:**

* You should limit the IP Range allowed to connect to the Pfsense GUI to limit users allowed to access the Pfsense GUI.

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-968dd383c10ed5723b1e0c3f57be4e11ba8f4354%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=d488fa6b\&sv=1)

* Select **Save**
* Then select **Apply changes**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-8e8c5a936d2548ec3670b48253ea7c2b22129475%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=e12a2214\&sv=1)

**Step 5:** Configure **LAN Interface**

* Go to **Interfaces** -> **Assignments** to add **a LAN Interface**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-b06ac0a5cb3914c441d707b04fb90f50db07c2b8%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=8fe2d409\&sv=1)

* Click **Add**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-12f7637538fa4a8535dd89cc080c9f866dce9147%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=8b4f7782\&sv=1)

* Then click **Save**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-330f786543b637eb865dc9c416be570033ce3eae%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=5bf8a981\&sv=1)

* Go to **Interfaces** -> **Assignments** to **enable LAN Interface**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-bb54f52531789c7ebde4cd35cc8efc8498740bdd%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=28d95a95\&sv=1)

* You make the configuration as below

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-56e4c42fb67eaa77371c9bdb7e1cbc0cace3c18e%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=244cd97c\&sv=1)

* Configure **IP** for **LAN**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-a0cf787263845d07da87f2d4513c30190c2f6544%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=a3964fcb\&sv=1)

* Then proceed to **Add a new gateway:** enter **Gateway for LAN Interface**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-ee5867db038457d0db9d285371828b2d7cb63e24%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=772fb571\&sv=1)

* To get this IP information, go to the **Network Interface** section of the Pfsense server to view the information:

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-b146a16ff7e3d01afd4898c5a6c0dd6cf1fb82da%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=20ba6f41\&sv=1)

* Proceed to **Save** again

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-909ec2c151b19e60be8016ddafcead580a4b778f%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=690d081a\&sv=1)

**Step 6** : Review configuration information

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-4277c1efb0a6a99803f9c61958e64f4e026e6020%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=6733407b\&sv=1)

**Step 7 : Open the Internet** outbound rule for **the LAN interface**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-61af0d80a6d427378bd20f4a47deed08ffee8c01%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=b23a7677\&sv=1)

* At source, select the **IP** range that is allowed to go out to **the Internet**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-c1f7ab3ba6fb9ab9d87aee74f8f1a63e7ff65131%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=d715e3fc\&sv=1)

**Step 8:** Configure **NAT** so that **vServers** can go out to **the Internet**

* Go to **Firewall** -> **NAT**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-687d2c0c66a9436e0652b48c9fdb764ae8cc3e2a%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=3859b6f\&sv=1)

* Select **NAT** mode then proceed to configure **NAT**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-6a8c22399f25c71304c410936b9c540f0229e8b4%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=7100a3aa\&sv=1)

* Click **Add** to add **the rule**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-124e13530d47be72afc53879895befeb032dd57e%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=2c98b60a\&sv=1)

* Select **source** , **destination NAT**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-63a024d5a90836fd480e3178b1fa49fb0ce81f75%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=3a2f3dcf\&sv=1)

***

### Initialize Route Table <a href="#khoitaomotpublicclustervoiprivatenodegroup-khoitaoroutetable" id="khoitaomotpublicclustervoiprivatenodegroup-khoitaoroutetable"></a>

After Pfsense is successfully initialized and configured, you need to create a Route table to connect to different networks. Specifically, follow these steps to create a Route table:

**Step 1:** Visit [https://hcm-3.console.vngcloud.vn/vserver/network/route-table](https://hcm-3.console.vngcloud.vn/vserver/network/route-table)

**Step 2:** In the navigation menu bar, select **Network Tab/ Route table.**

**Step 3:** Select **Create Route table.**

**Step 4:** Enter a descriptive name for the Route table. Route table names can include letters (az, AZ, 0-9, '\_', '-'). The input data length is between 5 and 50. It must not include leading or trailing spaces.

**Step 5:** Select **VPC** for your Route table. If you do not have a VPC, you need to create a new VPC according to the instructions on [the VPC Page](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648039) . **The VPC used to set up the Route table must be the VPC selected for your Pfsense and Cluster.**

**Step 6** : Select **Create** to create a new Route table.

**Step 7:** Select ![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762068%2Fimage2024-4-16\_15-40-3.png%3Fversion%3D1%26modificationDate%3D1713256805000%26api%3Dv2\&width=40\&dpr=4\&quality=100\&sign=7bf6e57b\&sv=1)the newly created Route table then select **Edit Routes.**

**Step 8:** In the add new **Route** section , enter the following information:

* For Destination, enter **Destination CIDR as 0.0.0.0/0**
* For Target, enter **Target CIDR as the Pfsense Network Interface 2 IP address.**

For example:

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F6.png\&width=768\&dpr=4\&quality=100\&sign=3f987938\&sv=1)

***

### **Checking connection** <a href="#kiem-tra-ket-noi" id="kiem-tra-ket-noi"></a>

Proceed to ping google.com or 8.8.8.8 to check

* Before **Enable NAT** the server could not access the internet

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-ee5f07fff7f17c9c726bb3504e78b890ef290179%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=26ddf106\&sv=1)

* After **configuring NAT,** ping 8.8.8.8 to check

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-ccd84a9b2a47d3f7cb27d0e50c269406de363362%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=b701924f\&sv=1)[\
](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/vks/bat-dau-voi-vks/khoi-tao-mot-public-cluster-voi-private-node-group/palo-alto-as-a-nat-gateway)
