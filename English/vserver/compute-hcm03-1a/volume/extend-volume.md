# Extend volume

The volume (removable) of vServer can be easily expanded, without interrupting vServer.

Note: Volume Status must be AVAILABLE to expand the size. Volume cannot be reduced in size, it can only increase in size.

***

### **Extend Volume on Portal with Linux operating system** <a href="#extendvolume-extendvolumeonportalwithlinuxoperatingsystem" id="extendvolume-extendvolumeonportalwithlinuxoperatingsystem"></a>

Use the following guide to resize the Volume on the panel:

1. Open the vServer console at: [https://hcm-3.console.vngcloud.vn/vserver/block-store/volumes](https://hcm-3.console.vngcloud.vn/vserver/block-store/volumes)
2. On the VPC/Volumes tab, select a Volume and click **Actions**
3. Then select **Expand**
4. Choose a new size and IOPS for the Volume, note the size of the Volume must be 20 GB or more and the largest size is 10000 GB, you can check the additional cost in the right column
5. Click **Expand** to finish
6. Go to VPS and execute the command **growpart /dev/vda 1 resize2fs /dev/vda1**

### **Extend Volume on Portal with Windows operating system** <a href="#extendvolume-extendvolumeonportalwithwindowsoperatingsystem" id="extendvolume-extendvolumeonportalwithwindowsoperatingsystem"></a>

Use the following guide to resize the Volume on the panel:

1. Open the vServer console at: [https://hcm-3.console.vngcloud.vn/vserver/block-store/volumes](https://hcm-3.console.vngcloud.vn/vserver/block-store/volumes)
2. On the VPC/Volumes tab, select a Volume and click Actions
3. Then select **Expand**
4. Choose a new size and IOPS for the Volume, note the size of the Volume must be 20 GB or more and the largest size is 10000 GB, you can check the additional cost in the right column
5. Click **Expand** to finish
6. Then go to Disk Management->Rescan disk->Select disk to extend
