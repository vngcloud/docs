# Mount FileStorage to the server

Steps to mount FileStorage to a server via **NFS protocol:**

**Step 1:** Update package list and install NFS client:

* **For Debian/Ubuntu:**

```
sudo apt-get -y update && sudo apt-get install nfs-common
```

* **For Red Hat Enterprise Linux/CentOS:**

```
sudo yum update && sudo yum install nfs-utils
```

**Step 2:** Create mount directory:

* For the command example below I have created the directory /mnt/nfs

```
sudo mkdir -p /mnt/nfs
```

**Step 3:** Mount FileStorage volume:

* For example, the command below I mount FileStorage with name = demo\_test with mount directory = /mnt/nfs

```
sudo mount -t nfs -o vers=4,hard,timeo=600,retrans=3,rsize=1048576,wsize=1048576,resvport,async hcm04.efs.vngcloud.vn:/demo_test /mnt/nfs/
```

**Step 4** : Check mount:

```
df -h
```

These steps will help you mount a FileStorage file share on your server.
