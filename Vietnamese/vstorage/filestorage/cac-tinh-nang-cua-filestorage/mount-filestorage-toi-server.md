# Mount FileStorage tới server

Các bước thực hiện mount FileStorage tới một server qua giao thức **NFS:**

**Bước 1:** Cập nhật danh sách gói và cài đặt NFS client:&#x20;

* **Đối với Debian/Ubuntu:**

```
sudo apt-get -y update && sudo apt-get install nfs-common
```

* **Đối với Red Hat Enterprise Linux/CentOS:**

```
sudo yum update && sudo yum install nfs-utils
```

**Bước 2:** Tạo thư mục mount:

* Ví dụ lệnh bên dưới tôi đã tạo thư mục /mnt/nfs

```
sudo mkdir -p /mnt/nfs
```

**Bước 3:** Mount FileStorage volume:&#x20;

* Ví dụ lệnh bên dưới tôi mount FileStorage có name = demo\_test với thư mục mount = /mnt/nfs

<pre><code><strong>sudo mount -t nfs -o vers=4,hard,timeo=600,retrans=3,rsize=1048576,wsize=1048576,resvport,async hcm04.efs.vngcloud.vn:/demo_test /mnt/nfs/
</strong></code></pre>

**Bước 4**: Kiểm tra mount:

```
df -h
```

Các bước này sẽ giúp bạn mount một file share của FileStorage lên server của mình.
