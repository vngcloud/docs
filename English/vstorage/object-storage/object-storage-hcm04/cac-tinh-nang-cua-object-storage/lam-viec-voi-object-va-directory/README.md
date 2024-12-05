# Working with objects and directories

## Overview <a href="#tong-quan" id="tong-quan"></a>

To store an object in vStorage, you create a bucket using 3rd party software and upload a file to that bucket. The newly uploaded file is stored inside the bucket as an object. Once the object is in the bucket, you can upload the same file to the bucket to overwrite the object (update the object), download, copy, move, or change the tag and metadata settings for that object. When you no longer need an object or a group of objects, you can delete them to clean up your vStorage resources.

## Object scope <a href="#pham-vi-gioi-han-object" id="pham-vi-gioi-han-object"></a>

### **Object renaming rules**

The following rules apply to renaming objects in vStorage:

* Object names must be between 1 (minimum) and 255 (maximum) characters long.
* Object names can contain uppercase letters, lowercase letters (a-z, A-Z), numbers (0-9), all special characters, and spaces if present.
* To limit errors when working with objects using client tools or on vStorage, we recommend that object names should not use special characters such as $, #, %, &, ^, etc. and that the Latin script should be used to name objects and directories.

### **Regulations on maximum file size when uploading**

* No limit on the number of files in one upload or download.
* The maximum total size of files in a single upload through vStorage Portal is 20GB.
* The maximum total size of files in a single upload via 3rd party software or vStorage API is 5TB.
