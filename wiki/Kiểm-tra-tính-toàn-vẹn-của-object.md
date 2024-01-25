vStorage cung cấp tính năng checksum để bạn có thể kiểm tra tính toàn vẹn của object được upload lên. 

Thực hiện kiểm tra checksum theo các bước sau 


* Chọn object bạn muốn checksum 
* Down script checksum của object
* Tạo checksum

 **For big file (>100MB)** 

1. Open terminal at folder which includes vStorage_checksum.sh file

2. Run below cmd:

./vStorage_checksum.sh filepath/filename 100000000



 **For small file (<100MB)** 

1. Open terminal at folder which includes vStorage_checksum.sh file

2. Run below cmd:

md5sum filepath/filename 


* Copy đoạn checksum vào so sánh, nếu hiện tick xanh là đã ok

![](images/storage/image2020-4-13_10-45-36.png)



*****

[[category.storage-team]] 
[[category.confluence]] 
