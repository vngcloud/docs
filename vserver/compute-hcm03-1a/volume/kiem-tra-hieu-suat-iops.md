---
description: >-
  Chủ đề này mô tả cách kiểm tra hiệu suất IOPS của SSD . Thông số kỹ thuật của
  đĩa và điều kiện kiểm tra ảnh hưởng đến kết quả kiểm tra. Nếu bạn định cấu
  hình các điều kiện kiểm tra như được mô tả tron
---

# Kiểm tra hiệu suất IOPS

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-10_15-38-26.png?version=1&#x26;modificationDate=1691656708000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### **Điều kiện thử nghiệm** <a href="#kiemtrahieusuatiops-dieukienthunghiem" id="kiemtrahieusuatiops-dieukienthunghiem"></a>

* Thao tác mẫu: ghi ngẫu nhiên (random read & random write).
* Image: Chúng tôi khuyên bạn nên sử dụng phiên bản mới hơn của hình ảnh công khai Linux do VNG Cloud cung cấp, chẳng hạn như Almalinux9.0 x 64, AmalinuxOS-8.5 x 64
* Công cụ: Chúng tôi khuyên bạn nên sử dụng [FIO](https://linux.die.net/man/1/fio?spm=a2c63.p38356.0.0.5dd851c3Me9qMH).

### **Ghi chú hoạt động** <a href="#kiemtrahieusuatiops-ghichuhoatdong" id="kiemtrahieusuatiops-ghichuhoatdong"></a>

Cảnh báo

* Bạn có thể thu được kết quả kiểm tra chính xác bằng cách kiểm tra phân vùng đĩa. Tuy nhiên, bạn có thể phá hủy cấu trúc hệ thống tệp trong phân vùng đĩa nếu bạn trực tiếp kiểm tra phân vùng đó. Trước khi bạn kiểm tra đĩa, chúng tôi khuyên bạn nên sao lưu dữ liệu của mình bằng cách chụp nhanh đĩa. Để biết thêm thông tin, hãy xem Tạo ảnh chụp nhanh của đĩa .
* Chúng tôi khuyên bạn không nên kiểm tra đĩa chứa hệ điều hành hoặc đĩa lưu trữ dữ liệu quan trọng. Để tránh mất dữ liệu, chúng tôi khuyên bạn nên sử dụng ổ đĩa mới không chứa dữ liệu cho thử nghiệm.

### **Kiểm tra hiệu suất đồng thời random read & random write** <a href="#kiemtrahieusuatiops-kiemtrahieusuatdongthoirandomread-and-randomwrite" id="kiemtrahieusuatiops-kiemtrahieusuatdongthoirandomread-and-randomwrite"></a>

1. Tạo một Server với ổ đĩa Volume có loại NVME với IOPS 1000 tại trang chủ vServer
2. Kết nối vào Server của bạn. Để biết thêm thông tin hãy xem hướng dẫn [Kết nối vào máy chủ ảo](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49650318).
3.  Chạy lệnh sau để cài đặt FIO:

    | `sudo yum install -y epel-release && yum install -y fio \|\| ( apt-get update && apt-get install -y fio )` |
    | ---------------------------------------------------------------------------------------------------------- |
4.  Sử dụng câu lệnh sau để thực hiện đo lường hiệu suất SSD:\
    Tạo 1 file 4GB, thực hiện việc đọc/ghi đồng thời với blocksize 4KB theo tỉ lệ 75% – 25% (tức 3 đọc/1 ghi) và thực hiện đồng thời 64 tác vụ một lúc. Tỉ lệ 3:1 rất phổ biến và xấp xỉ với các dạng database hiện nay.

    | `sudo fio --randrepeat=1` `--ioengine=libaio --direct=1` `--gtod_reduce=1` `--name=TGS --filename=TGS --bs=4k --iodepth=64` `--size=4G --readwrite=randrw --rwmixread=75` `--numjobs=8` |
    | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
5.  Đây là kết quả sau khi chạy hoàn tất với **numjob = 1**:\
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-23_14-31-37.png?version=1&#x26;modificationDate=1692775898000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Có thể thấy, VPS test có thể thực hiện đồng thời **IOPS =** 7**500** tác vụ đọc và**. IOPS = 2506** tác vụ ghi mỗi giây.

Kết quả với **numjob = 8**:

<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-23_16-22-5.png?version=1&#x26;modificationDate=1692782525000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-23_16-22-25.png?version=1&#x26;modificationDate=1692782546000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Có thể thấy, VPS test có thể chạy 8 job với  mỗi job có **IOPS =** **938** tác vụ đọc và **IOPS = 313** tác vụ ghi mỗi giây.

**Kiểm tra hiệu suất random read**

1.  Sử dụng câu lệnh sau để thực hiện đo lường hiệu suất SSD:\
    Tạo 1 file 4GB, thực hiện việc đọc với tất cả hiệu năng của ổ cứng với blocksize 4KB và thực hiện đồng thời 64 tác vụ một lúc.&#x20;

    | `sudo fio --randrepeat=1` `--ioengine=libaio --direct=1` `--gtod_reduce=1` `--name=TGS --filename=TGS --bs=4k --iodepth=64` `--size=4G --readwrite=randread --numjobs=8` |
    | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
2.  Đây là kết quả sau khi chạy hoàn tất với **numjob = 1**:



    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-23_16-30-23.png?version=1&#x26;modificationDate=1692783024000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



    Có thể thấy, VPS test có thể thực hiện **IOPS = 10.0K (10000)** tác vụ đọc mỗi giây.\
    \
    Kết quả với **numjob = 8**:\


    <figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-29_13-32-25.png?version=1&#x26;modificationDate=1693290746000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Có thể thấy, VPS test có thể chạy 8 job với  mỗi job có **IOPS =** 1254 tác vụ đọc mỗi giây.

### **Kiểm tra hiệu suất random write** <a href="#kiemtrahieusuatiops-kiemtrahieusuatrandomwrite" id="kiemtrahieusuatiops-kiemtrahieusuatrandomwrite"></a>

1.  Sử dụng câu lệnh sau để thực hiện đo lường hiệu suất SSD:\
    Tạo 1 file 4GB, thực hiện việc ghi với tất cả hiệu năng của ổ cứng với blocksize 4KB và thực hiện đồng thời 64 tác vụ một lúc.&#x20;

    | `sudo fio --randrepeat=1` `--ioengine=libaio --direct=1` `--gtod_reduce=1` `--name=TGS --filename=TGS --bs=4k --iodepth=64` `--size=4G --readwrite=randwrite --numjobs=8` |
    | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
2.  Đây là kết quả sau khi chạy hoàn tất với **numjob = 1**:\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-23_16-34-58.png?version=1&#x26;modificationDate=1692783299000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
3.  Có thể thấy, VPS test có thể thực hiện. **IOPS =** **10.0K (10000)** tác vụ ghi mỗi giây.\
    \
    Kết quả với **numjob = 8**:\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-30_14-53-48.png?version=1&#x26;modificationDate=1693382029000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



### **Giám sát hiệu suất ổ đĩa bằng vMonitor** <a href="#kiemtrahieusuatiops-giamsathieusuatodiabangvmonitor" id="kiemtrahieusuatiops-giamsathieusuatodiabangvmonitor"></a>

*   Bạn có thể truy cập vào trang chủ vMonitor tại: [https://hcm-3.console.vngcloud.vn/vmonitor/dashboard](https://hcm-3.console.vngcloud.vn/vmonitor/dashboard) để theo dõi tốc độ ghi và đọc của ổ đĩa SSD:\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-14_15-19-19.png?version=1&#x26;modificationDate=1692001160000&#x26;api=v2" alt=""><figcaption></figcaption></figure>





### **Kết quả thử nghiệm kiểm tra hiệu suất ổ đĩa VNG Cloud** <a href="#kiemtrahieusuatiops-ketquathunghiemkiemtrahieusuatodiavngcloud" id="kiemtrahieusuatiops-ketquathunghiemkiemtrahieusuatodiavngcloud"></a>



<figure><img src="https://docs.vngcloud.vn/download/attachments/63766877/image2023-8-29_9-54-22.png?version=1&#x26;modificationDate=1693277663000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
