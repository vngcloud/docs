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

**Step 4:** Proceed to pay like normal resources on GreenNode.

***

### Configure parameters for Pfsense <a href="#toc165621058" id="toc165621058"></a>

**Step 1:** After initializing Pfsense from vMarketPlace according to the instructions above, you can access the vServer interface here [to](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server) check whether the server running Pfsense has been initialized. **Next, open the Any rule on the Security Group for the Pfsense server you just created. Opening the Any rule on the Security Group will allow all traffic to the Pfsense server.**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F5Bumdpr1FTWdMPFOmgGG%252Fimage.png%3Falt%3Dmedia%26token%3Df6e965e0-5207-43f8-9c66-b35bf9048d36&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7630a1ac&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 2: After the server running Pfsense is successfully initialized** . To access the Pfsense GUI, you need to use the IP address of the External Interface to log in with the default Username and password **admin/pfsense.**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FbbVNJkzv3hhZ6C9034WR%252Fp1.png%3Falt%3Dmedia%26token%3Dd667ab22-d617-46d4-a99f-cbc85ff3dd69&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=e52dfa60&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* To get this IP information, go to **the Network Interface** section of **Pfsense** to view the information

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F08SZD6D4qktk1o5eiyr5%252Fimage.png%3Falt%3Dmedia%26token%3Da825d000-47e9-4b54-8459-023da603f294&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=bd60085d&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 3** : Open **the rule** on **the firewall**

* Proceed to **Add rule**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FCntDihHTlHJilLIJAJK6%252Fimage.png%3Falt%3Dmedia%26token%3D906ef5b8-5e6d-4ba3-b32f-43ff133d9899&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=e56c45f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* You can open the rule as below to access the GUI using **External Interface** .

**Attention:**

* You should limit the IP Range allowed to connect to the Pfsense GUI to limit users allowed to access the Pfsense GUI.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F1Zeen4sOULEmrHjwrcrQ%252Fimage.png%3Falt%3Dmedia%26token%3Dbb00138f-ac91-47ae-ac27-67142b1b9145&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7512263b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Select **Save**
* Then select **Apply changes**

**Step 4** : Proceed with **General Setup** , please do as below

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FsaXi7UMyCgCl4j8d797O%252Fimage.png%3Falt%3Dmedia%26token%3D1c37e049-40f5-4242-8098-e147eebb3945&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=200cf9f6&#x26;sv=1" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FMBP0zsOGXfCRysPZpQ59%252Fimage.png%3Falt%3Dmedia%26token%3D639d2870-32b3-4d14-88fc-c35641f8c6e3&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=2c24b48a&#x26;sv=1" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (244).png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F0gDLcWa36cpUJo2iSnyG%252Fimage.png%3Falt%3Dmedia%26token%3D5eadf23d-e50a-4b63-8465-fa0edd6b11e6&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=e8488882&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Configure **WAN Interface**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FhZ0X19fth88XDhHUJ56A%252Fimage.png%3Falt%3Dmedia%26token%3Dbf32c3c6-38c3-452f-8623-97be9b77f0b0&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=94d592d2&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Change **password** in **GUI**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FaUrrBKufnvXEyJhoWiOV%252Fimage.png%3Falt%3Dmedia%26token%3D268706ad-69f9-40bb-a9aa-338c698fb3eb&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c535caf8&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Proceed **to reload**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FvTTcLpMz1cNYT31EBezk%252Fimage.png%3Falt%3Dmedia%26token%3Df0e49146-14b8-41fc-aa7a-2bf9813182b8&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=5c2c82e6&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* **General Setup** completed

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FszmG5h1aYsKtVP9fpje2%252Fimage.png%3Falt%3Dmedia%26token%3D8d133fed-5d7d-4849-8cba-52baa20242c6&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6965b822&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 5:** Configure **LAN Interface**

* Go to **Interfaces** -> **Assignments** to add **a LAN Interface**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FYLVRkwlX48bQdWV62Gvy%252Fimage.png%3Falt%3Dmedia%26token%3Ded8aa676-be31-41ca-9461-09f67e9068cf&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=aa8680fa&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Click **Add**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FR59LdFDHFMWepP3ngkNV%252Fimage.png%3Falt%3Dmedia%26token%3D08a8c52d-6b10-4efa-a635-8797ce2908dd&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=21062159&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Then click **Save**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FD5NYmMS03fnTrthP2XVq%252Fimage.png%3Falt%3Dmedia%26token%3D75e3890c-8af9-4ca4-af18-bc4999975a97&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=db11583b&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Go to **Interfaces** -> **Assignments** to **enable LAN Interface**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FpRJKN10OrBMO411xPBEI%252Fimage.png%3Falt%3Dmedia%26token%3D4fa1f5e8-78e7-4dea-80fb-6f3ec9fd3b5e&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7ce824e1&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* You make the configuration as below

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FN5ZWCkDRUFv5jOkhEP9j%252Fimage.png%3Falt%3Dmedia%26token%3D654937a0-bf5b-4ed2-9c2a-c64c8655f5cf&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=177f854c&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Configure **IP** for **LAN**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F94s15OONsfcvojKMUlX9%252Fimage.png%3Falt%3Dmedia%26token%3Ddbbbdc7d-b0f3-4441-aefa-4337f3a1befe&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=e000c2f6&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Then proceed to **Add a new gateway:** enter **Gateway for LAN Interface**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FVjKTmeyShyeMWcXsTGbf%252Fimage.png%3Falt%3Dmedia%26token%3D061efbf8-6e92-435f-b922-b8cc6f4f040c&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=dcc21120&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* To get this IP information, go to the **Network Interface** section of the Pfsense server to view the information:

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F9bSiYvyqsnc2IOcSmeLT%252Fimage.png%3Falt%3Dmedia%26token%3Da21daec1-61a8-47e3-9044-c6b988848d12&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7fa76509&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Proceed to **Save** again

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F6PB2z5gv559YWtNQ3KvI%252Fimage.png%3Falt%3Dmedia%26token%3Dc6f9ddf0-b3de-4a0e-b522-ce35334f682c&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=bbfb2cdb&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 6** : Review configuration information

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fz3pi4Ek7jgPlfUjitqCW%252Fimage.png%3Falt%3Dmedia%26token%3D4fffa2b4-ee5b-4a7b-aaaa-b183d2b8215b&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=b5c11f17&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 7 : Open the Internet** outbound rule for **the LAN interface**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FmbtufOcDh1nLJHVc52QM%252Fimage.png%3Falt%3Dmedia%26token%3D083b87c2-9c71-425a-b5c6-b8fb9a5f9195&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=88012efb&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* At source, select the **IP** range that is allowed to go out to **the Internet**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FuL4w0EAYoLRN2PqZKuy4%252Fimage.png%3Falt%3Dmedia%26token%3D78cb6cee-099d-4558-a267-8acf9d9a4b07&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c6ab9915&#x26;sv=1" alt=""><figcaption></figcaption></figure>

**Step 8:** Configure **NAT** so that **vServers** can go out to **the Internet**

* Go to **Firewall** -> **NAT**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FK4bMcpQ0AVn326TwaeWZ%252Fimage.png%3Falt%3Dmedia%26token%3D42265735-5805-492d-a0ec-df7bb395103b&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=5c8d656&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Select **NAT** mode then proceed to configure **NAT**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fpl6UBUNx7LhQ2s14CxgM%252Fimage.png%3Falt%3Dmedia%26token%3D521208a2-eee2-41a4-9cf4-62dd34903bc1&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d9329e3e&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Click **Add** to add **the rule**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FH0suT2MbGSjBtb2sPrzk%252Fimage.png%3Falt%3Dmedia%26token%3Deeab42e3-cdcd-4fbb-ab37-e031847be2ec&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=60803f4c&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Select **source** , **destination NAT**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FLi2mKDVOQ0kcqf0HBFh8%252Fimage.png%3Falt%3Dmedia%26token%3D8ed841eb-e1c5-439c-a0d1-30932ccbfe77&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=839046aa&#x26;sv=1" alt=""><figcaption></figcaption></figure>

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

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FnRgpIREHbUa7KDoh5jyu%252F6.png%3Falt%3Dmedia%26token%3D6510abe7-2809-4eb2-89c1-eeb987082d1d&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c1ba042f&#x26;sv=1" alt=""><figcaption></figcaption></figure>

***

### **Checking connection** <a href="#kiem-tra-ket-noi" id="kiem-tra-ket-noi"></a>

Proceed to ping google.com or 8.8.8.8 to check

* Before **Enable NAT** the server could not access the internet

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252Fz64tUO9hdPhoJyFGCp1Q%252Fimage.png%3Falt%3Dmedia%26token%3Db3c240e6-b46a-4f2c-a27a-a401cce52aa0&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=eb6bf7e5&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* After **configuring NAT,** ping 8.8.8.8 to check

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FqYJBLX69Fu0jdwJPoQX7%252Fimage.png%3Falt%3Dmedia%26token%3De082cc4a-e9ac-40ee-8707-e64dceb7c706&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=97985a84&#x26;sv=1" alt=""><figcaption></figcaption></figure>
