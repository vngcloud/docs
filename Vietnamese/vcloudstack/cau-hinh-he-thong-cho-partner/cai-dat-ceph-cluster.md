# Cài đặt Ceph Cluster

Bước 1: Cần cái Cài đặt các chương trình tiên quyết:

* Python 3
* Systemd
* Podman or Docker for running containers
* Time synchronization (such as Chrony or the legacy ntpd)
* LVM2 for provisioning storage devices

Step2: Install Cephadm

· In Ubuntu:

_apt install -y cephadm_\
<br>

· In CentOS Stream:

_dnf search release-ceph_\
\&#xNAN;_dnf install --assumeyes centos-release-ceph-quincy_\
\&#xNAN;_dnf install --assumeyes cephadm_

Step3: Create cephadmin user, pull ceph component images

useradd -m cephadmin

ssh-keygen -t rsa -b 4096 -C "cephadm@yourhostname"

docker pull quay.io/ceph/ceph:v17

docker pull quay.io/prometheus/node-exporter:v1.5.0

Step4: Running the bootstrap Command (running on admin node)

cephadm --image quay.io/ceph/ceph:v17 bootstrap \\\
\--cluster-network 10.237.123.0/24 \\\
\--mon-ip 10.237.123.11 \\\
\--ssh-user cephadmin \\\
\--ssh-private-key /home/cephadmin/.ssh/id\_rsa \\\
\--ssh-public-key /home/cephadmin/.ssh/authorized\_keys \\\
\--initial-dashboard-user admin \\\
\--initial-dashboard-password "admin@storage" --skip-pull

Step5: Enable CEPH CLI

apt install ceph-common

Confirm that the ceph command is accessible with:

_ceph -v_\
<br>

Confirm that the ceph command can connect to the cluster and also its status with:

_ceph status_

Step6: Adding host

ceph orch host add lab-vcloudstack-cehp012 10.237.123.12 mon mgr osd\
ceph orch host add lab-vcloudstack-cehp013 10.237.123.13 mon mgr osd

Step7: Adding OSD

· Print a list of devices discovered by cephadm, run command:

ceph orch device ls

· Check hardware support libstoragemgmt:

cephadm shell lsmcli ldl

![](file:///C:/Users/LAP14997-local/AppData/Local/Packages/oice_16_974fa576_32c1d314_195d/AC/Temp/msohtmlclip1/01/clip_image002.png)

· Check disk rotation (SSD: rotate =0, HDD: rotate =1)\
&#xNAN;_&#x6C;sblk -o name,rota_

![](file:///C:/Users/LAP14997-local/AppData/Local/Packages/oice_16_974fa576_32c1d314_195d/AC/Temp/msohtmlclip1/01/clip_image004.png)

· Apply osd spec

_ceph orch apply -i osd\_spec.yaml_

![](file:///C:/Users/LAP14997-local/AppData/Local/Packages/oice_16_974fa576_32c1d314_195d/AC/Temp/msohtmlclip1/01/clip_image005.png)

· Add available device to cluster:

_ceph orch apply osd --all-available-devices_

Step8: Create and Configure Crush RULE

· Create crush rule

_ceph osd crush add-bucket ssd-01 root_

_ceph osd crush add-bucket ssd-02 root_

_ceph osd crush move lab-vcloudstack-cehp013 root=ssd-01_

_ceph osd crush move lab-vcloudstack-cehp012 root=ssd-01_
