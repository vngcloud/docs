# Create a File Storage

To initialize a File Storage on the File Storage system, you can follow these steps:

## Initialize File Storage <a href="#khoi-tao-file-storage" id="khoi-tao-file-storage"></a>

**Step 1:** Go to [https://efs.console.vngcloud.vn/overview](https://efs.console.vngcloud.vn/overview)

**Step 2:** Select **File Storage** then select **Create a File storage.**

<figure><img src="../../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

**Step 3:** At the File Storage initialization screen, you need to enter/select:

* **File Storage name:** the descriptive name of the storage file. The file name must be between 5 and 50 characters long and can include the characters a-z, AZ, 0-9, '-', '\_'
* **Description** : enter a description for the storage file.
* **File storage type:** select the type of drive you want to use. Currently we only provide **Standard HDD drive type.**
* **Protocol:** select the protocol you want. We currently support:
  * **NFS** : v4.0, 4.1
  * **SMB** : v2.0+ (coming soon)
* **Tag:** you can add tags to mark file storage as needed.

<figure><img src="../../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

* **File Storage Max quota:** in the file storage initialization step, you need to set a maximum quota limit for that file storage. This quota means the limit of storage capacity that the file storage can use, helping to manage resources effectively. <mark style="color:red;">**The minimum quota you need to choose is 1 TB and the maximum quota we provide is 50 TB**</mark>**.** If you need to use more than 50 TB for a file storage, please contact us.
* **Network type** : select the network type you want. Currently, we support:
  * **Public** : all access is public, you can use this storage file for VMs, K8S on-premise, on VNG Cloud or resources from other sources.
  * **Private: coming soon.**
* **Permission:** configure IP-based access permissions
  * **No one:** No IP is allowed to access.
  * **All:** Allow all IPs to have RO (Read-Only) or RW (Read-Write) access.
  * **Restricted:** Only allow specific IPs to access with RO or RW permissions.

<figure><img src="../../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

For example, in the picture, I only allow IP 192.168.1.100 to have RO rights and IP 192.168.1.101 to have RW rights

**Step 5:** Select **Create File Storage.**

***

## Get mount guide information <a href="#lay-thong-tin-mount-guide" id="lay-thong-tin-mount-guide"></a>

After the system has finished initializing your File Storage, to get the mount guide, please select **Action** then select **Mount Guide**

<figure><img src="../../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>
