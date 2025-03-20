# Working with objects and directories via vStorage Portal

Below are the basic features when you work with objects.

## Upload/Download object <a href="#upload-download-object" id="upload-download-object"></a>

To upload an object to a bucket, please follow the steps below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) . Select **the project** and **bucket** you want to upload objects to.
2. Select **Upload** .
3. Select **Choose files to upload** or drag the files from your personal device you want to upload into this area.
4. After dragging or selecting one or more files into this area. Select **Upload.**

<figure><img src="../../../../../.gitbook/assets/image (80) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Attention:**

* When using vStorage Portal, you can only upload objects up to 20GB in size.
{% endhint %}

***

To download one or more objects, please follow the steps below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) . Select **the project** and **bucket** you want to download the object from.
2. Select the **objects** you want to download.
3. Select the action icon, then select the **Download button**

<figure><img src="../../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Search object/folder <a href="#tim-kiem-object-folder" id="tim-kiem-object-folder"></a>

To search for an object/ folder, please follow the steps below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) . Select **the project** and **bucket** you want to search for object/folder
2. In the **Find objects by prefix** box , you can search for objects/folders by prefix by entering the character string that is the prefix you want to search for.
3. Press **Enter or select the Search** icon

<figure><img src="../../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Move object <a href="#di-chuyen-object" id="di-chuyen-object"></a>

To move an object, please follow the steps below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) . Select **the project** and **bucket** containing the object you want to move.
2. **Select the Action** icon and select **Move**

<figure><img src="../../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

3. Select **the bucket** and **directory** (if any) that you want to move the object to. We also support you to create a new directory if the directory you want to move to does not exist.

You can move objects across buckets within a project. We currently do not support moving objects across projects.

## Copy object <a href="#sao-chep-object" id="sao-chep-object"></a>

To copy an object, please follow the steps below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) . Select **the project** and **bucket** containing the object you want to copy.
2. **Select the Action** icon and select **Copy.**

<figure><img src="../../../../../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

3. Select **the bucket** and **directory** (if any) that you want to copy the object to. We also support you to create a new directory if the directory you want to copy to does not exist.

You can copy objects across buckets within a project. Currently we do not support copying objects across different projects.

## Rename object <a href="#doi-ten-object" id="doi-ten-object"></a>

To rename an object, please follow the steps below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) . Select **the project** and **bucket** containing the object you want to rename.
2. **Select the Action** icon and select **Rename.**

<figure><img src="../../../../../.gitbook/assets/image (5) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

3. Enter the name of the object you want to change, the object name must comply with our description.

When renaming an object, you should not change the file type (e.g. abc.pdf, .pdf is the file type) in the object name. Changing this extension of the object name may change the content type of the object, which may cause errors when you download the object to your personal device.

## Share object <a href="#chia-se-object" id="chia-se-object"></a>

To share an object in a bucket, you can follow the steps below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .
2. Select **project, bucket** then select one or more objects **you** want to share.
3. **Select the Action** icon then select **Share**
4. Enter **the Expiration time** you want to share the object: the time the access link to the object is valid. You can limit the number of **days** , **hours** , and **minutes** that the access link to the object exists.
5. Select **Generate**

<figure><img src="../../../../../.gitbook/assets/image (6) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Set up metadata object <a href="#thiet-lap-metadata-object" id="thiet-lap-metadata-object"></a>

To set metadata for an object, please follow the steps below:

1. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) . Select **the project** and **bucket** containing the object you want to set metadata for.
2. **Select the Action** icon and select **Metadata.**

<figure><img src="../../../../../.gitbook/assets/image (7) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

3. **The Metadata Setup** screen is displayed.
4. We provide you with two methods of setting metadata including:

* **Default key** : select a key from the list of available keys we provide.
* **Custom key** : create your own custom key according to your needs with the prefix **X-Object-Meta-Vng-** .

5. Enter the Value **corresponding** to the selected or created **Key . Select Add** then select **Update.**

After performing the above 5 steps, metadata has been successfully set for your object.

We currently support 8 default metadata key types including: **Cache-Control, Content-Encoding, Expires, Content-Language, Content-Type.**

## Delete object <a href="#xoa-object" id="xoa-object"></a>

To delete one or more objects, you can:

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .

2\. Select **project, bucket** then select the **objects** you want to delete **.**

**2. Select the Action** icon then select **Delete**

<figure><img src="../../../../../.gitbook/assets/image (8) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

After selecting Delete, the system will automatically switch to the main screen. If you see the object you just performed disappears from the list, you have successfully deleted it. The object has now been permanently deleted from the system. Once an object has been deleted from the vStorage system, you cannot restore that object.

## Create directory <a href="#khoi-tao-directory" id="khoi-tao-directory"></a>

To initialize a directory, you can:

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .

2\. Select **the project, bucket** you want to create a directory

3\. Select **Create a directory**

4\. Enter **Directory name** , enter a name that complies with our regulations for your directory.

<figure><img src="../../../../../.gitbook/assets/image (9) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

4\. Select **Create**

Once a directory is created, you cannot change its name. We recommend that the directory name should contain lowercase letters, digits and no specific special characters like #, @, $, %, ?, /, \`, \~ ... If you really need to name it with uppercase letters, please note that it may cause some problems when working with supported 3rd party softwares from other vendors.

## Delete directory <a href="#xoa-directory" id="xoa-directory"></a>

To delete a directory, you can:

1\. Log in to [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list) .

2\. Select **the project, bucket** containing the directory you want to delete

**3. Select the Action** icon and select **Delete**

<figure><img src="../../../../../.gitbook/assets/image (10) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
