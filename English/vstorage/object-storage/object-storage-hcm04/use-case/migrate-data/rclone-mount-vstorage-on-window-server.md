# \[Rclone] Mount vStorage on Window server

To Mount vStorage to Local Drive on Windows using Rclone, follow these instructions:

## 1. Download and Install Rclone <a href="#id-1.-tai-va-cai-dat-rclone-theo-huong-dan-sau" id="id-1.-tai-va-cai-dat-rclone-theo-huong-dan-sau"></a>

* You download Rclone via the link: [https://rclone.org/downloads/](https://rclone.org/downloads/) .

## 2. Create a certificate file rclone.conf  <a href="#id-2.-tao-file-chung-thuc-rclone.conf-theo-mau-sau" id="id-2.-tao-file-chung-thuc-rclone.conf-theo-mau-sau"></a>

* After downloading and installing Rclone, create a file rclone.conf in the directory `C:\Users\username\.config\rclone`with the content

```bash
[vstorage]
type = s3
provider = Other
access_key_id = <<Lấy thông tin từ vStorage Portal>>
secret_access_key = <<Lấy thông tin từ vStorage Portal>>
endpoint = https://hcm04.vstorage.vngcloud.vn
```

## 3. Perform mount <a href="#id-3.-thuc-hien-mount" id="id-3.-thuc-hien-mount"></a>

* Next, you can use Rclone with CMD or PowerShell
  *   To list the objects in a bucket, use the command:

      ```bash
      C:\Users\stackops\Downloads\rclone.exe ls vstorage:[bucket_name]
      ```
  *   To upload an object to a bucket, use the command:

      ```bash
      C:\Users\stackops\Downloads\rclone.exe copy [local_path] vstorage:[bucket_name]
      ```
  *   To mount a bucket on vStorage to local\_path, run the command:

      ```bash
      C:\Users\stackops\Downloads\rclone.exe mount vstorage:[bucket_name] [local_path] --vfs-cache-mode off --allow-non-empty --allow-other --drive-chunk-size 128M  --max-read-ahead 200M --dir-cache-time 30m
      ```

**Note:**

* If you encounter an error about missing winfsp package as shown below, you can download additional packages at this link [https://github.com/billziss-gh/winfsp/releases/tag/v1.4.19049](https://github.com/billziss-gh/winfsp/releases/tag/v1.4.19049)

<figure><img src="../../../../../.gitbook/assets/image (347).png" alt=""><figcaption></figcaption></figure>

* You do not need to create the local\_path on the local machine when mounting.
* Rclone does not support background mode so you must not close cmd during use.
