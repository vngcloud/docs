# Working with bucket

## Overview <a href="#tong-quan" id="tong-quan"></a>

To store your data in a project, you need to create a bucket and upload objects to that bucket. In a project, you can create one or more buckets that act as a directory to store data. However, a bucket is different from a directory in that a bucket is a hierarchy that allows users or service providers to provide features and execute them from this hierarchy down. For example, we provide bucket policy, bucket ACLs, bucket lifecycle, etc. for each bucket in a project.

In terms of deployment, projects, buckets, objects are resources of vStorage and we also provide API for you to manage them. For example, you can create a project, bucket and upload objects using API. You can also use the admin interface we provide or 3rd party softwares to perform these operations.

***

## Bucket limit range <a href="#pham-vi-gioi-han-bucket" id="pham-vi-gioi-han-bucket"></a>

### **Bucket naming rules**

The following rules apply to bucket naming in vStorage:

* Bucket name must be between 3 (minimum) and 235 (maximum) characters long.
* Bucket names can only contain uppercase letters, lowercase letters (a-z, A-Z), numbers (0-9), periods (.), spaces ( ), underscores (\_), hyphens (-), and the @ character.
* Bucket names should not contain sensitive information (e.g. IP address, account name, login password, etc.). We recommend that you name your buckets with lowercase letters, numbers, and no specific characters like #, @, $, %, ?, /, \`, \~ ... If you really need to name your buckets with uppercase characters, please note that you may encounter some problems when working with 3rd party softwares supported by other vendors.
* Bucket names must be unique within a region until that bucket is deleted.

### **Example**

* The following example bucket names are valid and follow the recommended naming guidelines:
  * bucketexample1
  * bucket-data-2022
  * ...
* The following example bucket names are valid but we do not recommend using them:
  * [docexamplewebsite.com](http://docexamplewebsite.com/)
  * [www.docexamplewebsite.com](http://www.docexamplewebsite.com/)
  * ...
* The following example bucket names are invalid:
  * Bucket data is 80% efficient (contains %)
  * con\_1/2022 (contains / character)
  * ...
