# Check the IOPS performance

This topic describes how to check the IOPS performance of an SSD. The disk specifications and testing conditions affect the test results. If you configure the testing conditions as described in the following example to fully utilize the performance of a multi-core system with high concurrency, you can achieve very high IOPS values when performing a stress test on the SSD.

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-10_15-38-26.png?version=1&#x26;modificationDate=1691656708000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### Test Conditions <a href="#kiemtrahieusuatiops-dieukienthunghiem" id="kiemtrahieusuatiops-dieukienthunghiem"></a>

* Sample Operation: Random read and random write.
* Image: We recommend using the latest version of the public Linux image provided by VNG Cloud, such as Almalinux9.0 x64, AlmalinuxOS-8.5 x64.&#x20;
* Tool: We recommend using [FIO](https://linux.die.net/man/1/fio).

### Operational Notes <a href="#kiemtrahieusuatiops-ghichuhoatdong" id="kiemtrahieusuatiops-ghichuhoatdong"></a>

**Warning:**&#x20;

* You can obtain accurate test results by testing the disk partition. However, you may destroy the file system structure within the disk partition if you test the partition directly. Before testing the disk, we recommend backing up your data by taking a snapshot of the disk. For more information, see Creating a Snapshot of the Disk.
* We advise against testing disks that contain the operating system or store important data. To avoid data loss, we recommend using a new drive with no data for testing.

### Performance Testing for Concurrent Random Read and Random Write <a href="#kiemtrahieusuatiops-kiemtrahieusuatdongthoirandomread-and-randomwrite" id="kiemtrahieusuatiops-kiemtrahieusuatdongthoirandomread-and-randomwrite"></a>

1. Create a Server: Create a server with an NVMe Volume drive with 1000 IOPS on the vServer homepage.
2. Connect to Your Server: For more information, see the Guide to [Connecting to a Virtual Server](../instance/connect-to-virtual-server/).
3. Run the following command to install FIO:

```
sudo yum install -y epel-release && yum install -y fio || ( apt-get update && apt-get install -y fio )
```

4. Use the following command to measure SSD performance:\
   This command creates a 4GB file and performs simultaneous read/write operations with a 4KB block size at a 75% read and 25% write ratio (i.e., 3 reads for every 1 write), executing 64 tasks simultaneously. The 3:1 ratio is common and approximates current database formats.

```
sudo fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=TGS --filename=TGS --bs=4k --iodepth=64 --size=4G --readwrite=randrw --rwmixread=75 --numjobs=8
```

5. The following are the results after completing the test with `numjobs=1`:

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-23_14-31-37.png?version=1&#x26;modificationDate=1692775898000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

It can be seen that the test VPS can simultaneously perform **IOPS = 7500** read operations and **IOPS = 2506** write operations per second.

Results with **numjobs = 8**:

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-23_16-22-5.png?version=1&#x26;modificationDate=1692782525000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-23_16-22-25.png?version=1&#x26;modificationDate=1692782546000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

It can be seen that the test VPS can run 8 jobs with each job having **IOPS = 938** read operations and **IOPS = 313** write operations per second.

**Performance Testing for Random Read**

1. Use the following command to measure SSD performance: Create a 4GB file, perform reads with full disk performance using a 4KB block size, and execute 64 tasks simultaneously.

```
sudo fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=TGS --filename=TGS --bs=4k --iodepth=64 --size=4G --readwrite=randread --numjobs=8
```

2. Here are the results after completing the test with **numjobs = 1**:

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-23_16-30-23.png?version=1&#x26;modificationDate=1692783024000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

It can be seen that the test VPS can perform **IOPS = 10.0K (10000)** read operations per second.\
\
Results with **numjobs = 8**:

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-29_13-32-25.png?version=1&#x26;modificationDate=1693290746000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

It can be seen that the test VPS can run 8 jobs with each job having **IOPS = 1254** read operations per second.

### Performance Testing for Random Write <a href="#kiemtrahieusuatiops-kiemtrahieusuatrandomwrite" id="kiemtrahieusuatiops-kiemtrahieusuatrandomwrite"></a>

1. Use the following command to measure SSD performance: Create a 4GB file, perform writes with full disk performance using a 4KB block size, and execute 64 tasks simultaneously.

```
sudo fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=TGS --filename=TGS --bs=4k --iodepth=64 --size=4G --readwrite=randwrite --numjobs=8
```

2. Here are the results after completing the test with **numjobs = 1**:

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-23_16-34-58.png?version=1&#x26;modificationDate=1692783299000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

3. It can be seen that the test VPS can perform **IOPS = 10.0K (10000)** write operations per second.\
   \
   Results with **numjobs = 8**:

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-30_14-53-48.png?version=1&#x26;modificationDate=1693382029000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### Monitor Disk Performance with vMonitor <a href="#kiemtrahieusuatiops-giamsathieusuatodiabangvmonitor" id="kiemtrahieusuatiops-giamsathieusuatodiabangvmonitor"></a>

*   You can access the vMonitor homepage at: [https://hcm-3.console.vngcloud.vn/vmonitor/dashboard](https://hcm-3.console.vngcloud.vn/vmonitor/dashboard) to track the read and write speeds of the SSD:\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-14_15-19-19.png?version=1&#x26;modificationDate=1692001160000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### VNG Cloud Disk Performance Test Results <a href="#kiemtrahieusuatiops-ketquathunghiemkiemtrahieusuatodiavngcloud" id="kiemtrahieusuatiops-ketquathunghiemkiemtrahieusuatodiavngcloud"></a>

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-29_9-54-22.png?version=1&#x26;modificationDate=1693277663000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

