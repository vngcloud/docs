# Using Rclone

#### Common usecase <a href="#usingrclone-commonusecase" id="usingrclone-commonusecase"></a>

**List all of containers**

> $ rclone lsd \<remote\_name>:

**Create a container**

> $ rclone mkdir \<remote\_name>:mybucket

**List all of objects in a container**

> $ rclone ls \<remote\_name>:mybucket

**Download `file.txt` from a container**

> $ rclone copy \<remote\_name>:mybucket/file.txt fichier.txt

***

#### Advances usecase <a href="#usingrclone-advancesusecase" id="usingrclone-advancesusecase"></a>

**Sync all of object in directory `/home/user/documents` to a container**

> $ rclone sync /home/user/documents \<remote\_name>:mybucket

**Copy file from directory `/home/user/file.txt` into a bucket**

> $ rclone copy /home/user/file.txt \<remote\_name>:mybucket

{% hint style="info" %}
**Note:**

* Do not use an Rclone version that is too old or too new on operating systems with extremely outdated or very new versions, as it may lead to errors.
* It is not recommended to use rclone sync because it will copy the **source** to the **destination** and delete the differences in the **destination**, making the **destination** a copy of the **source**. This can cause accidental data deletion if the **source** or **destination** information is incorrect. It is advised to use rclone copy.
*   There are several issues when using rclone mount to mount vStorage containers (buckets) into a local directory for use:

    1. Unable to copy, rename, move.
    2. Unable to list quickly.
    3. No permissions like on traditional filesystems: rwx, uid, gid, etc.

    Rclone supports cleaning up incomplete segments when uploading large objects (multipart upload). When using Rclone to upload large files, the file is divided into multiple segments for uploading to the vStorage system. During the file upload process, some segments may be uploaded successfully, while others may not be uploaded due to errors such as network issues, vStorage system overload, Rclone being stopped or hanging, etc. The file is considered to have been unsuccessfully uploaded, and the uploaded segments are considered incomplete or garbage segments, occupying your storage space. It is recommended to delete these garbage segments to optimize costs and storage space. You can do this by:

    1. Listing all incomplete multipart uploads with the following command:

    > rclone backend list-multipart-uploads [vng:/my-bucket](http://vng/my-bucket)

    * Deleting incomplete segments (garbage segments) using the following command to delete all garbage segments from the last 24 hours

    > rclone cleanup [vng:/my-bucket](http://vng/my-bucket)

    * Exercise caution when using the max-age option in the cleanup command, as setting max-age too low (e.g., 1 second) may delete segments of multipart uploads in progress rather than actual garbage segments. It is recommended to use max-age > 3 days to ensure safety when deleting data.

    > rclone backend cleanup [vng:/my-web](http://vng/my-web) -o max-age=3d

    For more details, please refer to \[rclone cleanup documentation]\([https://rclone.org/s3/#cleanup](https://rclone.org/s3/#cleanup)).
{% endhint %}
