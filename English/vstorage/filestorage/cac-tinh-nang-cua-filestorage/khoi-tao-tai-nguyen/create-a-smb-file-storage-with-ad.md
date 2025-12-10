# Create a SMB File Storage with AD

To create an SMB (Server Message Block) with Active Directory on the File Storage system, you can follow these steps:

## Create a Windows server on vServer <a href="#khoi-tao-windows-server-on-vserver" id="khoi-tao-windows-server-on-vserver"></a>

Below is a basic guide for initializing Windows server on vServer, if you already have a server, skip this step.

<details>

<summary>Instructions for creating Windows server</summary>

Before you can perform Windows server initialization, make sure you create a VPC, Subnet on the vServer system. Next, follow the steps below to create a Windows server:

1. Log in to vServer at [https://hcm-03.console.vngcloud.tech/vserver](https://hcm-03.console.vngcloud.tech/vserver/v-server/create-server) .
2. Continue to select **Servers** .
3. Select **Create a Server.**
4. In the **Basic Configuration** section , enter **the Server name** to describe the name for your Server. The Server name can consist of letters (az, AZ, 0-9, '\_', '-'). The input data length is between 5 and 50. It cannot contain leading or trailing spaces and the Server name must be different from the Username.
5. Select **the Zone** where you want to create the server.
6. **Enter Tag** information including **Key** / **Value** for the server and click **Add** to add this tag if you need.
7. Select **OS Images: Windows,** continue to select **Window version** depending on your usage needs.
8. Under **Instance type,** there is a list of Flavor configurations, you can choose the desired Flavor configuration for your Server according to. **iot.v1.small1x1** is recommended by us as a default basic configuration to create the Server
9. In **Volume Settings** , enter the configuration for Boot OS Volume (Root) including **Size GB** , **Volume Type SSD** and **IOPS** , then select **Next.**
10. In addition, you can add **Data Volume** to the Server during the initialization process by selecting **Add Data volume,** then **enter** the configuration for the Data Volume including **Volume name** , **Size GB** , **Volume Type SSD** and **IOPS** , select **Next.**
11. **Next, select the Network settings** parameter : Here you can select **VPC** to assign Private IP to Server and **Subnet** from the list you created earlier, or you can click [**here**](https://hcm-3.console.vngcloud.vn/vserver/network/vpc) to create a new VPC and Subnet. Note that after creating VPC and Subnet, it will be displayed on the list page for you to choose during Server initialization:
    1. Check the Floating IP box to assign Public IP to the Server (Click [**here**](https://docs.vngcloud.vn/vng-cloud-document/vn/vserver/compute-hcm03-1a/network/floating-ip) to see instructions for attaching/ detach Floating IP)
    2. **Security group** to manage ACL - Access Control List for Server. (Click [**here**](https://docs.vngcloud.vn/vng-cloud-document/vn/vserver/compute-hcm03-1a/security/security-groups) to see instructions for creating and managing Security group)
12. **Enter Authentication** information : Empty: the system will automatically generate and attach a password or the user can manually adjust and enable or disable skipping the first password change.
13. In **Other Settings** , you can choose Server Group or not according to your needs. You can assign Server to previously created Groups (With properties such as same Compute Host or different Compute Host)
14. Select **Launch Server** and follow the payment steps to complete the server initialization.

![](<../../../../.gitbook/assets/image (22) (2).png>)

</details>

{% hint style="info" %}
**Attention:**

Security Groups on Windows server need to open the following ports to share data:

* With NFS File Storage: open additional port **2049**
* With SMB File Storage with Basic Authentication: open additional port **445**
* With SMB File Storage with Active Directory Authentication: open additional port list to be able to connect from File Storage to AD.
{% endhint %}

***

## Connect to the Windows server <a href="#ket-noi-toi-windows-server-vua-khoi-tao" id="ket-noi-toi-windows-server-vua-khoi-tao"></a>

Below is a basic guide for connecting to Windows server on vServer, if you have used Console directly on vServer Portal, please skip this step.

<details>

<summary>Connect to Windows server</summary>

**To be able to connect to a Windows server, you first need to install RDP:** By default, Windows includes an RDP Client. To verify, type **mstsc** at the Command Prompt window. If your computer does not recognize this command, check the Windows home page and search for a download for the [Microsoft Remote Desktop](https://www.microsoft.com/vi-vn/windows) application .

1. Access the Server management page in our driver at: [https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server)
2. Select **the Server** you want to connect to, then select **Action, then select Connect.**
3. On the **Connect to Server** page , select **the RDP (Window) tab**

![](<../../../../.gitbook/assets/image (23) (2).png>)

4. Select **Download RDP File** . Your browser will prompt you to open or save the RDP file. When you've finished downloading the file, select **Done** to return to the server page:
5. Open the downloaded file to remote to Windows server. Select **Connect** to continue connecting to your server.

![](<../../../../.gitbook/assets/image (24) (2).png>)

6. The administrator account is selected by default. You need to copy and paste the password you saved earlier into the login pop-up (This information is taken from the email), in which enter the information **InstanceLogin** into **Username** , **InstancePassword** into **Password.**
7. Select **OK.** Due to the nature of self-signed certificates, you may receive a warning that the security certificate cannot be validated. Use the following steps to verify the identity of the remote computer, or simply select **Yes** (Windows) or **Continue** (Mac OS X) if you trust the certificate.

![](<../../../../.gitbook/assets/image (13) (2).png>)

8. The screen will show that the connection to the **Windows** server is successful.

![](<../../../../.gitbook/assets/image (14) (2).png>)

</details>

After you have connected to Windows server, you need to make sure your Windows server has a static IP address, you can check and configure static IP according to the following instructions:

* **Check the VM's network configuration by:**
  * Go to **Control Panel > Network & Internet > Network Connections** .
  * Select **the Ethernet adapter** , right-click and select **Properties** .
* **Set up a static IP address:**
  * **In the Properties** screen , select **Internet Protocol Version 4 (TCP/IPv4)** and then click the **Properties** button .
  * Select **Use the following IP address** to set up a static IP address.
  * Provide address information:
    * **IP Address:** static IP address of the VM.
    * **Subnet Mask:** Corresponding subnet, for example: 255.0.0.0
    * **Preferred DNS server:** IP address of DNS Domain (usually also the static IP address of VM) (you can add it after initializing DNS domain according to the instructions below)

<figure><img src="../../../../.gitbook/assets/image (15) (2).png" alt=""><figcaption></figcaption></figure>

***

## Create an Active Directory on Windows Server <a href="#khoi-tao-active-directory-tren-windows-server" id="khoi-tao-active-directory-tren-windows-server"></a>

To create an Active Directory on Windows Server, you need to do the following:

* **Install and configure DNS Server**
* **Create a Forward Lookup Zone**
* **Create a Reverse Lookup Zone**
* **Check DNS Name**
* **Install and configure Active Directory**

Specifically, please follow the steps below:

### Install and configure DNS Server <a href="#cai-dat-va-cau-hinh-dns-server" id="cai-dat-va-cau-hinh-dns-server"></a>

To install and configure DNS Server on Windows Server, you can follow these steps:

1. **From the Desktop** screen , open **the Start** menu and select **Server Manager.**
2. Select **All Servers,** right click then select **Add roles and Features**

<figure><img src="../../../../.gitbook/assets/image (29) (1).png" alt="" width="563"><figcaption></figcaption></figure>

3. On the **Before you begin page,** click **Next**

<figure><img src="../../../../.gitbook/assets/image (30) (2).png" alt="" width="563"><figcaption></figcaption></figure>

4. On the **Installation Type** page : Select **Role-based or feature-based installation** then select **Next**

<figure><img src="../../../../.gitbook/assets/image (31) (2).png" alt="" width="563"><figcaption></figcaption></figure>

5. In **Server Selection** : select **Select a server from the server pool** and **select the current server** then select **Next**

<figure><img src="../../../../.gitbook/assets/image (32) (1).png" alt="" width="563"><figcaption></figcaption></figure>

6. In **Server Roles** : Tick **DNS Server** then click **Next** and **Install** to install.

<figure><img src="../../../../.gitbook/assets/image (33) (2).png" alt="" width="563"><figcaption></figcaption></figure>

7. At this point, you will be prompted to add the necessary features for the DNS Server, select **Add Features** if you agree with the defaults.

<figure><img src="../../../../.gitbook/assets/image (34) (2).png" alt="" width="563"><figcaption></figcaption></figure>

8. On the **Confirmation** page , review your selections and click Install to begin installing the DNS Server.

<figure><img src="../../../../.gitbook/assets/image (35) (2).png" alt="" width="563"><figcaption></figcaption></figure>

9. Once the installation is complete, click **Close** .

<figure><img src="../../../../.gitbook/assets/image (36) (2).png" alt="" width="563"><figcaption></figcaption></figure>

### Create a Forward Lookup Zone <a href="#tao-mot-forward-lookup-zone" id="tao-mot-forward-lookup-zone"></a>

Next, you will need to create a Forward Lookup Zone to convert the domain to an IP address. Here are the steps:

1. Open **DNS Manager** by selecting **Tools** , then selecting **DNS**

<figure><img src="../../../../.gitbook/assets/image (37) (2).png" alt="" width="336"><figcaption></figcaption></figure>

2. In DNS Manager, select the existing DNS and continue to right-click on **Forward Lookup Zones** and select **New Zone**

<figure><img src="../../../../.gitbook/assets/image (38) (1).png" alt="" width="563"><figcaption></figcaption></figure>

3. The Create new zone screen appears, continue to select **Next**

<figure><img src="../../../../.gitbook/assets/image (39) (1).png" alt="" width="514"><figcaption></figcaption></figure>

4. **At the Zone Type** screen : select **Primary zone,** then select **Next**

<figure><img src="../../../../.gitbook/assets/image (40) (1).png" alt="" width="509"><figcaption></figcaption></figure>

5. **At the Zone Name** screen : enter your domain name and select **Next** . For example: `example.local`. <mark style="color:red;">**Remember this domain because this is the DNS domain you need to use to create AD and enter information when creating File Storage on the File Storage Portal system.**</mark>

<figure><img src="../../../../.gitbook/assets/image (41) (2).png" alt="" width="509"><figcaption></figcaption></figure>

6. **At the Zone File** screen , select **Next**

<figure><img src="../../../../.gitbook/assets/image (42) (2).png" alt=""><figcaption></figcaption></figure>

7. **At the Dynamic Update** screen : Select **Do not allow dynamic updates** , then select **Next**

<figure><img src="../../../../.gitbook/assets/image (43) (2).png" alt="" width="509"><figcaption></figcaption></figure>

8. Select **Finish** to complete creating the New Zone.

<figure><img src="../../../../.gitbook/assets/image (44) (2).png" alt="" width="508"><figcaption></figcaption></figure>

9. After selecting **Finish** , you will see the forwarding lookup zone on the main screen as shown.

<figure><img src="../../../../.gitbook/assets/image (45) (2).png" alt="" width="563"><figcaption></figcaption></figure>

10. After creating the zone, you need to add a record for **the Domain Controller** by selecting the newly created **Zone** , right-clicking and selecting **New Host (A or AAAA)**

<figure><img src="../../../../.gitbook/assets/image (46) (2).png" alt="" width="563"><figcaption></figcaption></figure>

11. **On the New Host** screen , you need to:

* **Name** : Enter your Windows server name (eg: `demo-smb`).
* **IP Address** : Enter the static IP address of the Domain Controller (eg: `10.50.3.9`).
* Click **Add Host** .

12. If you choose **Create associated pointer (PTR) record** , you need to create a **Reverse Loopup Zone** , the initialization steps are similar to creating **a Forward Lookup Zone** .

<figure><img src="../../../../.gitbook/assets/image (47) (2).png" alt="" width="278"><figcaption></figcaption></figure>

### Create a Reverse Lookup Zone <a href="#tao-mot-reverse-lookup-zone" id="tao-mot-reverse-lookup-zone"></a>

Next, you will need to create a Reverse Lookup Zone to convert the IP to a domain. Specifically, the steps are as follows:

1. Open **DNS Manager** by selecting **Tools** , then selecting **DNS**

<figure><img src="../../../../.gitbook/assets/image (37) (2).png" alt="" width="336"><figcaption></figcaption></figure>

2. In DNS Manager, select the existing DNS and continue to right-click on **Reverse Lookup Zones** and select **New Zone**

<figure><img src="../../../../.gitbook/assets/image (49) (2).png" alt="" width="407"><figcaption></figcaption></figure>

3. **At the Zone Type** screen : select **Primary zone,** then select **Next**

<figure><img src="../../../../.gitbook/assets/image (50) (2).png" alt="" width="407"><figcaption></figcaption></figure>

4. The Create new zone screen appears, select **IPv4 Reverse Lookup Zone** and continue to select **Next.**

<figure><img src="../../../../.gitbook/assets/image (51) (2).png" alt="" width="406"><figcaption></figcaption></figure>

5. **At the Reverse Lookup Zone Name** screen : enter Network ID, the Network ID here is the subnet of the IP that you need to perform reverse lookup and select **Next** . For example: `10.50.3`.

<figure><img src="../../../../.gitbook/assets/image (52) (2).png" alt="" width="407"><figcaption></figcaption></figure>

6. **At the Zone File** screen , you can create a new Zone File or select an existing Zone File, then select **Next.**

<figure><img src="../../../../.gitbook/assets/image (53) (2).png" alt="" width="407"><figcaption></figcaption></figure>

7. **At the Dynamic Update** screen : Select **Do not allow dynamic updates** , then select **Next**

<figure><img src="../../../../.gitbook/assets/image (54) (2).png" alt="" width="407"><figcaption></figcaption></figure>

8. Select **Finish** to complete creating the New Zone.

<figure><img src="../../../../.gitbook/assets/image (55) (2).png" alt="" width="407"><figcaption></figcaption></figure>

8. After selecting **Finish** , you will see Reverse lookup zone on the main screen as shown

<figure><img src="../../../../.gitbook/assets/image (56) (2).png" alt="" width="563"><figcaption></figcaption></figure>

10. After creating **a reverse lookup zone** , you need to create **a Pointer (PTR)** by selecting the newly created **Zone** , right-clicking and selecting **New Pointer (PTR)**

<figure><img src="../../../../.gitbook/assets/image (57) (2).png" alt="" width="563"><figcaption></figcaption></figure>

11. **On the New Resource Record** screen , you need to:
    1. **Host IP Address** : Enter the static IP address of the Domain Controller (eg: `10.50.3.9`).
    2. **Host Name:** Enter your Windows server name (eg: `demo-smb`).
    3. Click **OK** .

<figure><img src="../../../../.gitbook/assets/image (58) (2).png" alt="" width="327"><figcaption></figcaption></figure>

### Check DNS name <a href="#kiem-tra-dns-name" id="kiem-tra-dns-name"></a>

On your Windows server, open Command Prompt and run:

```bash
nslookup <DNS Domain>
or
nslookup <IP Address>
```

For example:

```bash
nslookup example.local
hoặc
nslookup 10.50.3.9
```

The result displays an example as follows:

```bash
nslookup example.local
---
Server: demo-smb
Address: 10.50.3.9
Name: example.local

nslookup 10.50.3.9
---
Server: demo-smb
Address: 10.50.3.9
```

### Install and configure Active Directory Domain Services <a href="#cai-dat-va-cau-hinh-active-directory-domain-services" id="cai-dat-va-cau-hinh-active-directory-domain-services"></a>

To install and configure Active Directory Domain Service on Windows Server, you can follow these steps:

1. **From the Desktop** screen , open **the Start** menu and select **Server Manager**
2. Select **All Servers,** right click then select **Add roles and Features**

<figure><img src="../../../../.gitbook/assets/image (59) (2).png" alt="" width="563"><figcaption></figcaption></figure>

3. In the **Before You Begin** section , select **Next**

<figure><img src="../../../../.gitbook/assets/image (60) (2).png" alt="" width="563"><figcaption></figcaption></figure>

4. In **Installation Type** : Select **Role-based or feature-based installation** then select **Next**

<figure><img src="../../../../.gitbook/assets/image (61) (2).png" alt="" width="563"><figcaption></figcaption></figure>

5. In **Server Selection** : select **Select a server from the server pool** and **select the current server** then select **Next**

<figure><img src="../../../../.gitbook/assets/image (32) (1).png" alt="" width="563"><figcaption></figcaption></figure>

6. In the **Server Roles** section : Tick **Active Directory Domain Services.**

<figure><img src="../../../../.gitbook/assets/image (63) (3).png" alt="" width="563"><figcaption></figcaption></figure>

7. At this point, you will be prompted to add the required features to Active Directory, select **Add Features** if you agree with the defaults, then select **Next**

<figure><img src="../../../../.gitbook/assets/image (64) (2).png" alt="" width="563"><figcaption></figcaption></figure>

8. On the **Feature** page , keep the default parameters and select **Next**

<figure><img src="../../../../.gitbook/assets/image (65) (2).png" alt="" width="563"><figcaption></figcaption></figure>

9. On the AD DS page, select **Next**

<figure><img src="../../../../.gitbook/assets/image (66) (3).png" alt="" width="563"><figcaption></figcaption></figure>

10. On the **Confirmation** page , review your selections and click **Install** to begin installing AD DS.

<figure><img src="../../../../.gitbook/assets/image (67) (3).png" alt="" width="563"><figcaption></figcaption></figure>

11. After selecting **Install** . The system will start installing, you do not need to restart the server immediately after installation.
12. When the installation is complete, you continue to select **Promote this server to a domain controller**

<figure><img src="../../../../.gitbook/assets/image (68) (3).png" alt="" width="563"><figcaption></figcaption></figure>

13. **At the Deployment Configuration** screen , select **Add a new forest** then enter **the DNS domain name** created (<mark style="color:red;">**which is the Zone name created in the Create a Forward Lookup Zone step**</mark>) then select **Next**

<figure><img src="../../../../.gitbook/assets/image (69) (3).png" alt="" width="563"><figcaption></figcaption></figure>

14. **At the Domain Controller Options** screen , enter **the Password** and **Confirm Password** for your DSRM.

<figure><img src="../../../../.gitbook/assets/image (70).png" alt="" width="563"><figcaption></figcaption></figure>

15. In the DNS Option section, you skip it and just click **Next.**

<figure><img src="../../../../.gitbook/assets/image (71).png" alt="" width="563"><figcaption></figcaption></figure>

16. In the **Additional Options** section , check **the NetBIOS name** again and change it if necessary, then select **Next. The NetBIOS domain name** is a shortened domain of the Root domain name,

<figure><img src="../../../../.gitbook/assets/image (72).png" alt="" width="563"><figcaption></figcaption></figure>

17. **At the Paths** screen , you can change the paths to **the Database folder, Log file folder, Sysvol** or keep them as the system default, then select Next.

<figure><img src="../../../../.gitbook/assets/image (73).png" alt="" width="563"><figcaption></figcaption></figure>

18. **At the Review Options** screen , review the parameters and select **Next** if the information is correct.

<figure><img src="../../../../.gitbook/assets/image (74).png" alt="" width="563"><figcaption></figcaption></figure>

19. **At the Prerequisites Check** screen , you will see the test results, continue to select **Install** for the system to install AD.

<figure><img src="../../../../.gitbook/assets/image (75).png" alt="" width="563"><figcaption></figcaption></figure>

20. After the installation process is complete, the system will automatically restart your server, you need to log back into the server with the **Administrator account.**

{% hint style="info" %}
**Attention:**

* You can grant permissions to AD accounts or groups through Group Policy or ACL access permissions. For more details, see [here](https://learn.microsoft.com/en-us/troubleshoot/windows-server/active-directory/active-directory-overview) .
{% endhint %}

***

## Create a File Storage <a href="#khoi-tao-file-storage" id="khoi-tao-file-storage"></a>

**Step 1:** Go to [https://efs.console.vngcloud.vn/overview](https://efs.console.vngcloud.vn/overview)

**Step 2:** Select **File Storage** then select **Create a File storage.**

**Step 3:** At the File Storage initialization screen, you need to enter/select:

* **File Storage name:** the descriptive name of the storage file. The file name must be between 5 and 50 characters long and can include the characters a-z, AZ, 0-9, '-', '\_'
* **Description** : enter a description for the storage file.
* **File storage type:** select the type of drive you want to use. Currently we only provide **Standard HDD drive type.**
* **Protocol:** select NFS and the NFS version you want
* **Tag:** you can add tags to mark file storage as needed.

<figure><img src="../../../../.gitbook/assets/image (16) (2).png" alt=""><figcaption></figcaption></figure>

* **File Storage Max quota:** in the file storage initialization step, you need to set a maximum quota limit for that file storage. This quota means the limit of storage capacity that the file storage can use, helping to manage resources effectively. **The minimum quota you need to choose is 1 TB and the maximum quota we provide is 50 TB.** If you need to use more than 50 TB for a file storage, please contact us.
* **Network type** : for SMB file type, network type must be Private. At this point, you need to select **VPC** , **Subnet** that you have created from vServer Portal.

<figure><img src="../../../../.gitbook/assets/image (17) (2).png" alt=""><figcaption></figcaption></figure>

* **Window Authentication:** Configure access rights via **Active Directory Authentication**
  * **Active Directory Authentication:** If your Windows server uses Active Directory to manage users and access, AD Authentication is easy to integrate and centrally manage. You can authenticate via Active Directory domain name, DNS server IP addresses, Username, Password on your Active Directory. For example, for the Active Directory created above, I would enter:
    * **Active Directory domain name** : This is **the Root domain name** you created in the step of **Installing and configuring Active Directory Domain Services** . For example:`example.local`
    * **DNS server IP Address** : DNS Server IP address, usually also the static IP address of the VM, for example: `10.50.3.9.` If you have 2 DNS IPs, you can enter according to the form `10.50.3.3,10.50.3.9`
    * **Username:** Admin account name, for example`Administrator`
    * **Password** : The password you created in the **Install and configure Active Directory Domain Services** step , for example:`123456789aA@`
    * **Confirm Password:** Confirm password, for example:`123456789aA@`

<figure><img src="../../../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

**Step 5:** Select **Create File Storage.**

**Step 6:** After the system has completed initializing the SMB File Storage, you can get the **File Storage IP Address** information in the File Storage details section and continue to perform the steps below.

<figure><img src="../../../../.gitbook/assets/image (19) (2).png" alt=""><figcaption></figcaption></figure>

***

## Map the File Storage to Windows server <a href="#map-file-storage-vua-khoi-tao-toi-windows-server" id="map-file-storage-vua-khoi-tao-toi-windows-server"></a>

On Windows Server, you can map SMB file storage through the interface or command line.

### **Through the interface** <a href="#qua-giao-dien" id="qua-giao-dien"></a>

1. **Open File Explorer.**
2. Right click on **This PC** and select **Map network drive** .
3. **In the Map Network Drive** window :
   1. **Drive letter** : Select a drive letter (eg: `Z:`).
   2. **Folder** : Enter the SMB share path, for example: `\\<File Storage IP Address>\<File Storage Name>`. For example `\\10.50.3.8\demo-smb`.
   3. Select **Finish** , once done, you can check in **File Explorer** to see the mapped drive.

<figure><img src="../../../../.gitbook/assets/image (20) (2).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (21) (1).png" alt="" width="501"><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* To automatically map the SMB storage file each time Windows Server starts, you can save the information when mapping through the interface by checking **the Reconnect at sign-in** box before clicking **Finish** .
{% endhint %}

### **Through command line** <a href="#qua-dong-lenh" id="qua-dong-lenh"></a>

Use the following command in **Command Prompt** or **PowerShell** :

```
net use Z: \\<File Storage IP Address>\<File Storage Name> 
```

* **Z:** : Is the drive letter you want to mount.
* **\\\\\<File Storage IP Address>\\\<File Storage Name>** : File Storage SMB path.

For example:

```
net use Z: \\10.50.3.8\demo-smb
```

### Through File Explorer <a href="#qua-truc-tiep-file-explorer" id="qua-truc-tiep-file-explorer"></a>

More simply, you can also directly access the SMB File Storage via File Explorer through the following steps:

1. Open **File Explorer** : Press **Windows key + E** or click the File Explorer icon.
2. Enter **UNC Path** : In the address bar, enter the UNC path to the file share. For example:

```
\\10.50.3.8\demo-smb
```

3. Press **Enter** .

***

## Write data to File Storage <a href="#write-data-toi-file-storage" id="write-data-toi-file-storage"></a>

After you have successfully **mapped the SMB File Storage** to Windows Server, you can write data to the File Storage as follows:

1. **Open a text editor (Notepad):**
   * On Windows Server, open **Notepad** by:
     * Click **Start** and type **Notepad** , then press **Enter** .
   * Or, press Windows key **+ R** , type `notepad`and press **Enter** .
2. **Write content to file:**
   *   In Notepad, type something simple, for example:

       Copy

       ```
       Đây là file test ghi vào SMB share.
       ```
   * Or enter whatever content you want.
3. **Save file to SMB file storage:**
   * Click **File > Save As...** .
   * **In the Save As** dialog box , navigate to the drive that you mapped the SMB share to (eg: `Z:`).
   * Name the file (eg: `testfile.txt`).
   * Click **Save** to save the file.
4. **Check files in SMB share:**
   * Open **File Explorer** (shortcut: **Windows + E** ).
   * Navigate to the SMB drive (eg. `Z:`).
   * Find and open the file `testfile.txt`you just saved to verify the contents.
