# Create a SMB File Storage without AD

To create an SMB (Server Message Block) without Active Directory on the File Storage system, you can follow these steps:

## Create a Windows server on vServer <a href="#khoi-tao-windows-server-on-vserver" id="khoi-tao-windows-server-on-vserver"></a>

Below is a basic guide for initializing Windows server on vServer, if you already have a server, skip this step.

<details>

<summary>Instructions for creating Windows server</summary>

Before you can perform Windows server initialization, make sure you initialize VPC, Subnet on the vServer system. Next, follow the steps below to initialize Windows server:

1. Log in to vServer at [https://hcm-03.console.vngcloud.tech/vserver](https://hcm-03.console.vngcloud.tech/vserver/v-server/create-server) .
2. Continue to select **Servers** .
3. Select **Create a Server.**
4. In the **Basic Configuration** section , enter **the Server name** to describe the name for your Server. The Server name can consist of letters (az, AZ, 0-9, '\_', '-'). The input data length is between 5 and 50. It cannot contain leading or trailing spaces and the Server name must be different from the Username.
5. Select **the Zone** where you want to create the server.
6. **Enter Tag** information including **Key** / **Value** for the server and click **Add** to add this tag if you need.
7. Select **OS Images: Windows,** continue to select **Window version** depending on your usage needs.
8. Under **Instance type,** there is a list of Flavor configurations, you can choose the desired Flavor configuration for your Server according to. **iot.v1.small1x1** is recommended by us as a default basic configuration to initialize the Server
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

<figure><img src="../../../../.gitbook/assets/image (15) (2).png" alt=""><figcaption></figcaption></figure>

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

* **File Storage Max quota:** in the file storage initialization step, you need to set a maximum quota limit for that file storage. This quota means the limit of storage capacity that the file storage can use, helping to manage resources effectively. <mark style="color:red;">**The minimum quota you need to choose is 1 TB and the maximum quota we provide is 50 TB**</mark>**.** If you need to use more than 50 TB for a file storage, please contact us.
* **Network type** : for SMB file type, network type must be Private. At this point, you need to select **VPC** , **Subnet** that you have created from vServer Portal.

<figure><img src="../../../../.gitbook/assets/image (17) (2).png" alt=""><figcaption></figcaption></figure>

* **Window Authentication:** configure access rights via **Basic Authentication**
  * **Basic Authentication:** If your Windows server does not have Active Directory or you want to manage access simply through username and password, you can use Basic authentication, we support you to create up to 10 username/password accounts to access file storage.

<figure><img src="../../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

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

```bash
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

3. Press **Enter**.

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
