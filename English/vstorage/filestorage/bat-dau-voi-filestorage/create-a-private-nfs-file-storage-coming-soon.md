# Create a Private NFS File Storage

To create a Private NFS (Network File System) on the File Storage system, you can follow these steps:

## Create a File Storage <a href="#khoi-tao-file-storage" id="khoi-tao-file-storage"></a>

**Step 1:** Go to [https://efs.console.vngcloud.vn/overview](https://efs.console.vngcloud.vn/overview)

**Step 2:** Select **File Storage** then select **Create a File storage.**

<figure><img src="../../../.gitbook/assets/image (5) (3).png" alt=""><figcaption></figcaption></figure>

**Step 3:** At the File Storage initialization screen, you need to enter/select:

* **File Storage name:** the descriptive name of the storage file. The file name must be between 5 and 50 characters long and can include the characters a-z, AZ, 0-9, '-', '\_'
* **Description** : enter a description for the storage file.
* **File storage type:** select the type of drive you want to use. Currently we only provide **Standard HDD drive type.**
* **Protocol:** select NFS and the NFS version you want
* **Tag:** you can add tags to mark file storage as needed.

<figure><img src="../../../.gitbook/assets/image (6) (3).png" alt=""><figcaption></figcaption></figure>

* **File Storage Max quota:** in the file storage initialization step, you need to set a maximum quota limit for that file storage. This quota means the limit of storage capacity that the file storage can use, helping to manage resources effectively. <mark style="color:red;">**The minimum quota you need to choose is 1 TB and the maximum quota we provide is 50 TB**</mark>**.** If you need to use more than 50 TB for a file storage, please contact us.
* **Network type** : select the network type you want. In this example, you can choose Private. Now, you need to select **the VPC** , **Subnet** that you have created from vServer Portal.
* **Permission:** configure IP-based access permissions
  * **No one:** No IP is allowed to access.
  * **All:** Allow all IPs to have RO (Read-Only) or RW (Read-Write) access.
  * **Restricted:** Only allow specific IPs to access with RO or RW permissions.

<figure><img src="../../../.gitbook/assets/image (7) (3).png" alt=""><figcaption></figcaption></figure>

**Step 5:** Select **Create File Storage.**

***

## Get mount guide information <a href="#lay-thong-tin-mount-guide" id="lay-thong-tin-mount-guide"></a>

After the system has finished initializing your File Storage, to get the mount guide, please select **Action** then select **Mount Guide**

<figure><img src="../../../.gitbook/assets/image (8) (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (9) (3).png" alt=""><figcaption></figcaption></figure>

***

## Mount File Storage to the server <a href="#mount-file-storage-toi-server" id="mount-file-storage-toi-server"></a>

Steps to mount FileStorage to a server via **NFS protocol:**

**Step 1:** Update package list and install NFS client:

* **For Debian/Ubuntu:**

```bash
sudo apt-get -y update && sudo apt-get install nfs-common
```

* **For Red Hat Enterprise Linux/CentOS:**

```bash
sudo yum update && sudo yum install nfs-utils
```

**Step 2:** Create mount directory:

* For example command below I created directory /mnt/demo

```bash
sudo mkdir -p /mnt/demo
```

**Step 3:** Mount FileStorage volume:

* For example, the command below I mount FileStorage with name = demo\_test with mount directory = /mnt/demo

```bash
sudo mount -t nfs -o vers=4.1,hard,timeo=600,retrans=3,rsize=1048576,wsize=1048576,resvport,async hcm04.efs.vngcloud.vn:/demo_test /mnt/demo/
```

**Step 4** : Check mount:

```bash
df -h
```

These steps will help you mount a FileStorage file share to your server.
