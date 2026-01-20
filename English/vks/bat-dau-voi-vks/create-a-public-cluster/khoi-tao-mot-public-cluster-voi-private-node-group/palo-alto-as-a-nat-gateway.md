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

**Step 4:** Proceed to pay like normal resources on GreenNode.

***

### Configure parameters for Palo Alto <a href="#toc165621058" id="toc165621058"></a>

**Step 1:** After initializing Palo Alto from vMarketPlace according to the instructions above, you can access the vServer interface here [to](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) check if the server running Palo Alto has been initialized. **Next, open the Any rule on the Security Group for the Palo Alto server you just created. Opening the Any rule on the Security Group will allow all traffic to the Palo Alto server.**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FMo5Y0pu0O6CEU5CvUNE0%252Fimage.png%3Falt%3Dmedia%26token%3Dd9fc371d-1c8b-4d6a-9922-a1d179a182de&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=46b79f8b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 2: After the server running Palo Alto is successfully initialized** . To access the Palo Alto GUI you need a vServer running Windows. Then you access it using IP Internal Interface with the default login name and password: **admin/admin**

Note: Go to the Network section of vServer Windows to access the Palo Alto GUI. You need to create the same VPC and use a different subnet than the subnet with priority 1 when initializing Palo Alto

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FfTVtgpMAHJkTjDwWbvcS%252F3.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=92961540&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 3** : After logging in, you need to change your password for the first time. Please enter a new password according to your wishes.

**Step 4:** You need to create 1 Zone Inside and 1 Zone Outside according to the instructions below:

* Select **Add pen**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fsxq4KiD45CiFnLvgvT97%252F4.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=969d833&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Name **the Zone** : **Inside** then select **OK**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fij66Mg6hfFyQgW8NUYMz%252F5.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1a7196e&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Do the same for **Zone Outside**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FmT4jxTevbstzFMq2cSH4%252F6.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7e4a6d68&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 5** : Configure **External Interface**

* Interface Type: **Layer 3**
* Virtual Router: **default**
* Security Zone: **Outside**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fl5BvtPhJ4aj6rKsqXgav%252F7.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=18b67d6b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Switch to **IPv4 Tab** and select **Add** to enter **Static IP** for **External Interface**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FmwD1RHw4lPsQaEmYKnVU%252F8.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=cf3bab43&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* To get this IP information, go to **Palo Alto** 's **Network Interface** section to view the information

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FJlcTU3IM66mh4dJwBjah%252F9.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d6b3e068&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Switch to the **Advanced** tab , in the **MTU** section you need to set it to **1400**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F0gt8OgqCeBCYCiWAm8AZ%252F10.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=cc092e02&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 6:** Perform similar configuration for **Internal Interfaces**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fd7wHzLfZrljuSwLYpnpd%252F11.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=82dfc359&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* At the **IPv4 tab:** you proceed to set up **Static IP**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FpfcMwq9l6fvqTA2lUDg4%252F12.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7073aa9f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Switch to the **Advanced** tab , in the **MTU** section , set it to 1400

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FXAw0reWRA2mDWUp9WZ9a%252F13.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=95c732cd&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 7:** Create **static route**

* Go to **Network** -> **Virtual Routers** -> Select **default** -> Switch to **Static Routes**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FA2aQgd5pd9pZ3JWhJNwP%252F14.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7342857f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Create a **route** as shown below

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FvsC8tROTQ0mky8obky6b%252F15.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d174dfe1&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 8:** Create **Security Policy Rule**

* Go to **Policies** -> **Security** -> **Add**
* On the **General** tab , you need to name the rule

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FpP5eixJyZZX8E3Yuy27v%252F16.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=96e75460&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* At the **Source** tab , set information such as **Source Zone** , **Source Address** , **Source User, Source Device**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F3lYCwAmMy1TITH5QHtes%252F17.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1663e1d&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* At the **Destination** tab , set information such as **Destination Zone, Destination Address, Destination Device**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fp97uUTeexfwVJTpg5fVf%252F18.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b59c89f3&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* At the **Application** tab , set information such as **Application, Depend On**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FVgqawaODEexO0NIST1Jo%252F19.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=27c690c6&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* At the **Service/URL Category** tab , set information such as **Service, URL Category**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FjbBinxnlUQBJi1CXOnGI%252F20.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ace2fee&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* At the **Actions** tab , set information such as **Action, Log, Profile, Other Settings**

**Step 9** : Create **a NAT rule** so that VMs can go out to the Internet

* Go to **Policies** -> **NAT** -> **Add**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FTHEB8RlsXB5l68dXBjeb%252F1.png%3Falt%3Dmedia%26token%3D8b48e79d-32ba-4020-94ca-759a10058400&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=3aebed9e&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* On the **General** tab , name **the NAT rule**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F7l4Ou8TlDHWIGRvSdXiY%252F2.png%3Falt%3Dmedia%26token%3D2cdc3921-6586-47c4-ba77-7d8f44dee23c&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ce1152e6&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* At the **Original Packet** tab, select **Source Zone, Destination Zone, Destination Interface, Service, Source Address, Destination Address**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FjRLcya4QZ1uIpMlp6ct6%252F3.png%3Falt%3Dmedia%26token%3Db7676618-4884-48b5-9543-9d8e50200cc1&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=dcfbd716&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Create the **Translated Packet** tab and perform configuration as shown below

Note: Need to change **the IP Address to the Static IP** address that you configured in step 6

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F6HxruDAG2Dl9ewMJyH7I%252F4.png%3Falt%3Dmedia%26token%3D4505b24f-84d4-4a05-85d8-87a429251401&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=67371524&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 10** : Proceed **to Commit**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FfnOw3psNPa0oobJ7jCqo%252F5.png%3Falt%3Dmedia%26token%3Da2137701-c8d7-4049-a548-23ce1acad88f&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=5a58522f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

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

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FZc60y0UEzBvPiuxzVD7R%252Fimage.png%3Falt%3Dmedia%26token%3D69bc0216-92aa-44a6-b572-11374f16e0d7&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7788e4b1&#x26;sv=1" alt=""><figcaption></figcaption></figure>

***

### **Checking connection** <a href="#kiem-tra-ket-noi" id="kiem-tra-ket-noi"></a>

* Proceed to ping 8.8.8.8 or google.com

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F1L08GGz5kd3i8A4h6VK7%252F7.png%3Falt%3Dmedia%26token%3Dd1959dff-38d1-49a8-a30b-718a1ec6ae77&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=fbc0270&#x26;sv=1" alt=""><figcaption></figcaption></figure>
