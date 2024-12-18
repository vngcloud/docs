# Using Rclone

## Some common use cases <a href="#sudungcongcurclone-motsousecasethongthuong" id="sudungcongcurclone-motsousecasethongthuong"></a>

**Get list of all buckets**

> $ rclone lsd \<remote\_name>:

**Create a new bucket**

> $ rclone mkdir \<remote\_name>:mybucket

**Get a list of all objects in a bucket**

> $ rclone ls \<remote\_name>:mybucket

**Download files `file.txt`from a bucket**

> $ rclone copy \<remote\_name>:mybucket/file.txt fichier.txt

***

## Some advanced use cases <a href="#sudungcongcurclone-motsousecasenangcao" id="sudungcongcurclone-motsousecasenangcao"></a>

**Synchronize a folder `/home/user/documents`with a bucket**

> $ rclone sync /home/user/documents \<remote\_name>:mybucket

**Copy a file in a folder `/home/user/file.txt`into a bucket**

> $ rclone copy /home/user/file.txt \<remote\_name>:mybucket

{% hint style="info" %}
**Attention:**

1. Do not use Rclone version that is too old/too new on operating systems with too old/too new version because it may cause errors.
2. It is not recommended to use rclone sync because when syncing, it will copy **the source** to **the destination** and delete the difference in **the destination** (making **the destination** a copy of **the source ), which can easily cause the problem of deleting data by mistake if the source** and **destination** information are transmitted incorrectly . It is recommended to use rclone copy.
3. There are some problems when using rclone mount to mount vStorage buckets (buckets) into local directories for use: + Cannot copy, rename, move + Cannot list quickly + No permissions like on traditional filesystems: rwx, uid, gid,...
4. Rclone supports incomplete segment cleaning when uploading large objects (multipart upload). When you use Rclone to upload large files (multipart upload), the file is divided into multiple segments to upload to the vStorage system. During the file upload process, some segments may be uploaded, some segments may not be uploaded due to errors such as network problems, vStorage system is overloaded, your Rclone is stopped, hangs, etc. The file is then considered as an unsuccessful upload, the uploaded segments are considered incomplete segments or junk segments and are taking up your storage space. We recommend that you delete these junk segments to optimize costs and storage space by:
5. List the uncompleted multipart uploads using the following command:

> rclone backend list-multipart-uploads [vng:/my-bucket](http://vng/my-bucket)

* Delete incomplete segments (garbage segments) use the following command to delete all garbage segments from 24 hours ago:

> rclone cleanup [vng:/my-bucket](http://vng/my-bucket)

Be careful when using the max-age option in the cleanup command as below because if the max-age value is too small (e.g. 1 second), you may delete segments of the multipart upload in progress that are not actually garbage segments. We recommend using max-age > 3 days to be safe when deleting data.

> rclone backend cleanup [vng:/my-web](http://vng/my-web) -o max-age=3d

For more details, please refer to [https://rclone.org/s3/#cleanup](https://rclone.org/s3/#cleanup) .
{% endhint %}
