# \[Rclone] Mount vStorage as Local Drive on Linux

To Mount vStorage to Local Drive on Linux using Rclone, follow these instructions:

## 1. Download and Install R**clone**  <a href="#id-1.-tai-va-cai-dat-rclone-theo-huong-dan-sau" id="id-1.-tai-va-cai-dat-rclone-theo-huong-dan-sau"></a>

* With CentOS 7:

```bash
curl https://rclone.org/install.sh
sudo bash
sudo yum install fuse -y
```

For other OS: you can refer to the download link at: [https://downloads.rclone.org/v1.55.1/](https://downloads.rclone.org/v1.55.1/)

**Note:** If your rclone is using **an old version < 1.50** (To check the version, use the command **rclone version** ), you should download **the new rclone version** in the following way:

* If you install by script:

```bash
curl https://rclone.org/install.sh
sudo bash
sudo rm /usr/bin/rclone
sudo rm /usr/local/share/man/man1/rclone.
```

* If you install from OS repo, you can:

```bash
yum remove rclone
```

Then, you download and install **the new version** as instructed above.

## 2. Create a certificate file rclone.conf <a href="#id-2.-tao-file-chung-thuc-rclone.conf-theo-mau-sau" id="id-2.-tao-file-chung-thuc-rclone.conf-theo-mau-sau"></a>

* Create the rclone.conf file according to the template below, you can get the access\_key\_id and secret\_access\_key information at vStorage Portal:

```bash
[vstorage]
type = s3
provider = Other
access_key_id = <<Lấy thông tin từ vStorage Portal>>
secret_access_key = <<Lấy thông tin từ vStorage Portal>>
endpoint = https://hcm04.vstorage.vngcloud.vn
```

* Before mounting, you check the connection to vStorage using rclone's lsd command with the syntax:

```bash
rclone --config=rclone.conf lsd vstorage:
```

If you have used vStorage before, you will see buckets containing the files you have uploaded.

## 3. Perform mount <a href="#id-3.-thuc-hien-mount" id="id-3.-thuc-hien-mount"></a>

To mount, use the command with the following syntax:

```bash
rclone mount --config=rclone.conf vstorage:<bucket_name> <mount_point> --vfs-cache-mode full --allow-non-empty --allow-other --drive-chunk-size 128M --max-read-ahead 200M --dir-cache-time 30m --daemon
```

In there:

* **bucket\_name** : the name of the bucket you will backup files to on vStorage. (If it doesn't exist, rclone will automatically generate it). Note, you should set a different name from the existing buckets.
* **mount\_point** : the area to mount on your local.

For example: you want to mount a bucket named **backup** at the path **/backup** on your local machine:

```bash
rclone mount --config=/root/.config/rclone/rclone.conf vstorage:backup /backup --vfs-cache-mode full --allow-non-empty --allow-other --drive-chunk-size 128M --max-read-ahead 200M --dir-cache-time 30m --daemon
```

The mounting process will take a while to complete. (About 3 minutes).

To test whether the mount process is complete or not, you can create a file in the mount area above:

Example: touch /backup/abc

Wait a moment for the data sync process to take place (depending on the size of your file, this process will be fast or slow).

* To check if the sync process was successful, use rclone's **ls** command to check:

```bash
 rclone --config=rclone.conf ls vstorage:<bucket_name>
```

For example:

```bash
rclone --config=rclone.conf ls vstorage:backup
```

* To unmount, use the following command:

```bash
fusermount -uz <mount_point>
```
