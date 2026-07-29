# Edit a File Storage

On each storage file, you can edit some parameters, specifically:

* **For NFS file storage** : Allow editing access rights (ACL) directly on the file by selecting **Edit** on the storage file you want to edit. However, editing ACL can cause disruption to this storage File for up to **10 seconds** . <mark style="color:red;">**Performing this action frequently will cause disruption to your storage File.**</mark>

<figure><img src="../../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

* **For SMB file storage using Basic Authentication** : Allows operations such as adding new accounts, disabling, changing passwords, or deleting created authentication accounts.

<figure><img src="../../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

* **For SMB storage files using AD Authentication** : Do not allow changes to Active Directory information; if changes are needed, <mark style="color:red;">**a new storage file should be created to ensure system stability.**</mark>
