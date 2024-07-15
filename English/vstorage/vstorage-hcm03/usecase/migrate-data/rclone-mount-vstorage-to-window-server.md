# \[Rclone] Mount vStorage to Window server

Rclone is a tool designed to synchronize data and directories across various cloud storage services, including AWS S3, Google Cloud, Dropbox, Google Drive, vStorage, and more. For additional information about Rclone, please visit: [https://rclone.org/](https://rclone.org/).

To perform an upload to vStorage using Rclone on the Windows operating system, refer to: [https://vstorage.console.vngcloud.vn/integration/integration](https://vstorage.console.vngcloud.vn/integration/integration).

**Note:**

* If you encounter a missing winfsp package error, as shown below, you can download the package from this link: [https://github.com/billziss-gh/winfsp/releases/tag/v1.4.19049](https://github.com/billziss-gh/winfsp/releases/tag/v1.4.19049).
* You don't need to create the local\_path directory on the local machine before mounting.
* Rclone does not support background mode, so you should not close the command prompt while using it.
