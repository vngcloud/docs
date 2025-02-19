# \[Rclone] Mount vStorage as Local Drive on Linux

To Mount vStorage to Local Drive on Linux using Rclone, follow these instructions:

**1:** Download & install **rclone** according to the following instructions:

With CentOS 7:

`curl https://`[`rclone.org/install.sh`](http://rclone.org/install.sh) `| sudo bash` `sudo yum install fuse -y`

For other OS: you can refer to the download link at: [https://downloads.rclone.org/v1.55.1/](https://downloads.rclone.org/v1.55.1/)

**Note:** If your rclone is using **an old version < 1.50** (To check the version, use the command **rclone version** ), you should upgrade to **the new rclone version** as follows:

* If you install by script: curl [https://rclone.org/install.sh](https://rclone.org/install.sh) | sudo bash.

`sudo rm /usr/bin/rclone` `sudo rm /usr/local/share/man/man1/rclone.1`

* If you install from OS repo, you can:

`yum remove rclone`

Then, you download and install **the new version** as instructed above.

**2:** Create a certificate file rclone.conf according to the following template:

`[vstorage]`

`type = swift`

`env_auth = false`

`auth_version = 3`

`user = ******`

`key = ******`

`auth =` [`https://hcm.auth.vstorage.vngcloud.vn/v3`](https://hcm.auth.vstorage.vngcloud.vn/v3tenant_id)

[`tenant_id`](https://hcm.auth.vstorage.vngcloud.vn/v3tenant_id) `= 410ded5c02674846b534ff7b4a894c2e`

`endpoint_type = public`

`tenant_domain = default`

`domain = default`

`location_constraint = HCM01`

`region = HCM01`

You can get the above information according to the instructions at [Integrating Rclone tool with vStorage](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vstorage/vstorage-hcm03/3rd-party-softwares/rclone/tich-hop-cong-cu-rclone-voi-vstorage) . In which:

* User/ Key: Swift user information you created from IAM.
* Auth: see [what is Farm?](https://docs.vngcloud.vn/vng-cloud-document/v/vn/vstorage/vstorage-hcm03/vstorage-la-gi/farm-la-gi)
* Tenant\_id: project id information, you can get it at vStorage Portal.

Before mounting, you check the connection to vStorage using rclone's lsd command with the syntax:

`rclone --config=rclone.conf lsd vstorage:`

If you have used vStorage before, you will see containers containing the files you have uploaded.

**3** : To mount, use the command with the following syntax:

`rclone mount --config=rclone.conf vstorage:<container_name> <mount_point> --vfs-cache-mode full --allow-non-empty --allow-other --drive-chunk-size 128M --max-read-ahead 200M --dir-cache-time 30m --daemon`

In there:

* **container\_name** : the name of the container you will backup files to on vStorage. (if not, rclone will automatically generate it). Note, you should set a different name from the existing containers.
* **mount\_point** : the area to mount on your local.

For example: you want to mount a container named **backup** at the path **/backup** on your local machine:

`rclone mount --config=/root/.config/rclone/rclone.conf vstorage:backup /backup --vfs-cache-mode full --allow-non-empty --allow-other --drive-chunk-size 128M --max-read-ahead 200M --dir-cache-time 30m --daemon`

The mounting process will take a while to complete. (About 3 minutes).

To test whether the mount process is complete or not, you can create a file in the mount area above:

Example: touch /backup/abc

Wait a moment for the data sync process to take place (depending on the size of your file, this process will be fast or slow).

To check if the sync process was successful, use rclone's **ls** command to check:

`rclone --config=rclone.conf ls vstorage:<container_name>`

For example:

`rclone --config=rclone.conf ls vstorage:backup`

To unmount, use the following command:

`fusermount -uz <mount_point>`
