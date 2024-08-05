# Palo Alto as a NAT Gateway

Use the instructions below to work with a Private Node group through Palo Alto.

### Prerequisites <a href="#dieu-kien-can" id="dieu-kien-can"></a>

To be able to use Palo Alto as NAT Gateway for Cluster on VKS system, you need:

* A **Windows server (VM)** has been initialized on the **vServer** system with the following configuration:

| Item                | Configuration |
| ------------------- | ------------- |
| Flavor              | 2x4           |
| Volume              | 20GB          |
| VPC                 | 10.76.0.0/16  |
| Subnet              | 10.76.0.4/24  |
| Network Interface 1 | 10.76.0.3     |

* A **Palo Alto server (VM)** is initialized on the **vMarketPlace** system according to the instructions below with the following configuration:

| Item                | Configuration |
| ------------------- | ------------- |
| Flavor              | 2x8           |
| Volume              | 60GB          |
| VPC                 | 10.76.0.0/16  |
| Network Interface 1 | 10.76.255.4   |
| Network Interface 2 | 10.76.0.4     |

### Initialize Palo Alto <a href="#toc165621057" id="toc165621057"></a>

**Step 1:** Visit [https://marketplace.console.vngcloud.vn/](https://marketplace.console.vngcloud.vn/)

**Step 2:** At the main screen, search for **Palo Alto , at Palo Alto** services , select **Launch** .

**Step 3:** Now, you need to configure **Palo Alto.** Specifically, you can select the desired **Volume, IOPS, Network, Security Group . You need to choose the same VPC and Subnet as the VPC and Subnet you choose to use for your Cluster.** In addition, you also need to select an existing Server Group or select **Dedicated SOFT ANTI AFFINITY group** so we can automatically create a new server group.

**Step 4:** Proceed to pay like normal resources on VNG Cloud.

***

### Configure parameters for Palo Alto <a href="#toc165621058" id="toc165621058"></a>

**Step 1:** After initializing Palo Alto from vMarketPlace according to the instructions above, you can access the vServer interface here [to](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) check if the server running Palo Alto has been initialized.

**Step 2: After the server running Palo Alto is successfully initialized** . To access the Palo Alto GUI you need a vServer running Windows. Then you access it using IP Internal Interface with the default login name and password: **admin/admin**

Note: Go to the Network section of vServer Windows to access the Palo Alto GUI. You need to create the same VPC and use a different subnet than the subnet with priority 1 when initializing Palo Alto

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F3%2520%281%29.png\&width=768\&dpr=4\&quality=100\&sign=22583bd2\&sv=1)

**Step 3** : After logging in, you need to change your password for the first time. Please enter a new password according to your wishes.

**Step 4:** You need to create 1 Zone Inside and 1 Zone Outside according to the instructions below:

* Select **Add pen**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F4%2520%281%29.png\&width=768\&dpr=4\&quality=100\&sign=54f22251\&sv=1)

* Name **the Zone** : **Inside** then select **OK**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F5%2520%281%29.png\&width=768\&dpr=4\&quality=100\&sign=7a4cb488\&sv=1)

* Do the same for **Zone Outside**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F6%2520%281%29.png\&width=768\&dpr=4\&quality=100\&sign=38d93427\&sv=1)

**Step 5** : Configure **External Interface**

* Interface Type: **Layer 3**
* Virtual Router: **default**
* Security Zone: **Outside**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F7%2520%281%29.png\&width=768\&dpr=4\&quality=100\&sign=5920afc6\&sv=1)

* Switch to **IPv4 Tab** and select **Add** to enter **Static IP** for **External Interface**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F8.png\&width=768\&dpr=4\&quality=100\&sign=1a486112\&sv=1)

* To get this IP information, go to **Palo Alto** 's **Network Interface** section to view the information

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F9.png\&width=768\&dpr=4\&quality=100\&sign=545a180b\&sv=1)

* Switch to the **Advanced** tab , in the **MTU** section you need to set it to **1400**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F10.png\&width=768\&dpr=4\&quality=100\&sign=246ea00f\&sv=1)

**Step 6:** Perform similar configuration for **Internal Interfaces**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F11.png\&width=768\&dpr=4\&quality=100\&sign=f8152556\&sv=1)

* At the **IPv4 tab:** you proceed to set up **Static IP**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F12.png\&width=768\&dpr=4\&quality=100\&sign=52419b31\&sv=1)

* Switch to the **Advanced** tab , in the **MTU** section , set it to 1400

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F13.png\&width=768\&dpr=4\&quality=100\&sign=fa9cf8f8\&sv=1)

**Step 7:** Create **static route**

* Go to **Network** -> **Virtual Routers** -> Select **default** -> Switch to **Static Routes**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F14.png\&width=768\&dpr=4\&quality=100\&sign=82b0bfc3\&sv=1)

* Create a **route** as shown below

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F15.png\&width=768\&dpr=4\&quality=100\&sign=463fabaa\&sv=1)

**Step 8:** Create **Security Policy Rule**

* Go to **Policies** -> **Security** -> **Add**
* On the **General** tab , you need to name the rule

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F16.png\&width=768\&dpr=4\&quality=100\&sign=57cbbb25\&sv=1)

* At the **Source** tab , set information such as **Source Zone** , **Source Address** , **Source User, Source Device**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F17.png\&width=768\&dpr=4\&quality=100\&sign=c887edbc\&sv=1)

* At the **Destination** tab , set information such as **Destination Zone, Destination Address, Destination Device**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F18.png\&width=768\&dpr=4\&quality=100\&sign=dfafb617\&sv=1)

* At the **Application** tab , set information such as **Application, Depend On**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F19.png\&width=768\&dpr=4\&quality=100\&sign=d8384a1e\&sv=1)

* At the **Service/URL Category** tab , set information such as **Service, URL Category**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F20.png\&width=768\&dpr=4\&quality=100\&sign=c64de03a\&sv=1)

* At the **Actions** tab , set information such as **Action, Log, Profile, Other Settings**

**Step 9** : Create **a NAT rule** so that VMs can go out to the Internet

* Go to **Policies** -> **NAT** -> **Add**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-d34e711b6b3fa0d758cc77f0c470d2c8c5465b0b%252F1.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=c7f2da58\&sv=1)

* On the **General** tab , name **the NAT rule**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-62814b880ed26021a79b49040b9e4833b6dd1b64%252F2.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=324a9aec\&sv=1)

* At the **Original Packet** tab, select **Source Zone, Destination Zone, Destination Interface, Service, Source Address, Destination Address**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F3.png\&width=768\&dpr=4\&quality=100\&sign=9cc73b65\&sv=1)

* Create the **Translated Packet** tab and perform configuration as shown below

Note: Need to change **the IP Address to the Static IP** address that you configured in step 6

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F4.png\&width=768\&dpr=4\&quality=100\&sign=9bd19b96\&sv=1)

**Step 10** : Proceed **to Commit**

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fgithub.com%2Fvngcloud%2Fdocs%2Fblob%2Fmain%2FEnglish%2F.gitbook%2Fassets%2F5.png\&width=768\&dpr=4\&quality=100\&sign=5058084f\&sv=1)

***

### Initialize Route Table <a href="#khoitaomotpublicclustervoiprivatenodegroup-khoitaoroutetable" id="khoitaomotpublicclustervoiprivatenodegroup-khoitaoroutetable"></a>

After Palo Alto is successfully initialized and configured, you need to create a Route table to connect to different networks. Specifically, follow these steps to create a Route table:

**Step 1:** Visit [https://hcm-3.console.vngcloud.vn/vserver/network/route-table](https://hcm-3.console.vngcloud.vn/vserver/network/route-table)

**Step 2:** In the navigation menu bar, select **Network Tab/ Route table.**

**Step 3:** Select **Create Route table.**

**Step 4:** Enter a descriptive name for the Route table. Route table names can include letters (az, AZ, 0-9, '\_', '-'). The input data length is between 5 and 50. It must not include leading or trailing spaces.

**Step 5:** Select **VPC** for your Route table. If you do not have a VPC, you need to create a new VPC according to the instructions on [the VPC Page](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648039) . **The VPC used to set up the Route table must be the VPC selected for your Palo Alto and Cluster.**

**Step 6** : Select **Create** to create a new Route table.

**Step 7:** Select ![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762068%2Fimage2024-4-16\_15-40-3.png%3Fversion%3D1%26modificationDate%3D1713256805000%26api%3Dv2\&width=40\&dpr=4\&quality=100\&sign=7bf6e57b\&sv=1)the newly created Route table then select **Edit Routes.**

**Step 8:** In the add new **Route** section , enter the following information:

* For Destination, enter **Destination CIDR as 0.0.0.0/0**
* For Target, enter **Target CIDR as the Palo Alto Network Interface 2 IP address.**

For example:

![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fgit-blob-f2ce363bb830cb7e3607f230606d1987bc481d93%252Fimage.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=2d80b393\&sv=1)

***

### **Checking connection** <a href="#kiem-tra-ket-noi" id="kiem-tra-ket-noi"></a>

* Proceed to ping 8.8.8.8 or google.com
