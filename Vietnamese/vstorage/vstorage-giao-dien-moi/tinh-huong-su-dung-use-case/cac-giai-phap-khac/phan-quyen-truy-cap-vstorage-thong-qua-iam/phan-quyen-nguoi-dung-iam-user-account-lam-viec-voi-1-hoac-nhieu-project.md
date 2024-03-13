# Phân quyền người dùng IAM User Account làm việc với 1 hoặc nhiều project

#### Kịch bản <a href="#phanquyennguoidungiamuseraccountlamviecvoi1hoacnhieuproject-kichban" id="phanquyennguoidungiamuseraccountlamviecvoi1hoacnhieuproject-kichban"></a>

* Giả sử bạn là người dùng **Root User Account** và bạn đã khởi tạo và tải lên tệp tin vào 2 project: **Project01** và **Project02**.
* Hiện tại, bạn muốn tạo 2 một người dùng mới, trong đó
  * Người dùng Leo có thể **đăng nhập vào vStorage Portal** và có quyền đọc tất cả dữ liệu bao gồm các container, directory, object trên **Project01**.
  * Người dùng Anne có thể **đăng nhập vào vStorage Portal** và có quyền đọc và ghi trên tất cả các container, directory, object trên **Project01** và **Project02**.

Minh họa cấu trúc lưu trữ dữ liệu của bạn trên vStorage:

```
Project01 - HAN01            
Container01                                          
    └── Directory01                                            
           ├── object01.txt                                
           ├── object02.jpg
    └── object03.png
    └── object04.txt
Container03
    └── object10.png
Container04
-------------------------------
Project02 - HCM01          
Container02
    └── Directory02                                            
           ├── object05.txt                                
           ├── object06.jpg
    └── object07.png
    └── object08.txt
Container05
```

#### Để giải quyết bài toán phân quyền này, hãy làm theo các bước bên dưới: <a href="#phanquyennguoidungiamuseraccountlamviecvoi1hoacnhieuproject-degiaiquyetbaitoanphanquyennay-haylamthe" id="phanquyennguoidungiamuseraccountlamviecvoi1hoacnhieuproject-degiaiquyetbaitoanphanquyennay-haylamthe"></a>

**Bước 1: Khởi tạo tài khoản IAM User Account**

Thực hiện khởi tạo 2 tài khoản IAM User Account theo hướng dẫn tại [Khởi tạo tài khoản IAM User Account](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59804814). Giả sử 2 tài khoản IAM User Account được khởi tạo là:

* **IAM\_User\_Leo**
* **IAM\_User\_Anne**

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/64554004/image2023-9-19_10-59-55.png?version=1&#x26;modificationDate=1695095996000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


**Bước 2: Khởi tạo policy cho 2 IAM User Account( IAM\_User\_Leo và IAM\_User\_Anne)**

Thực hiện khởi tạo policy cho 2 IAM User Account theo hướng dẫn tại [Khởi tạo policy cho IAM User Account](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59804816). Cụ thể:

<table><thead><tr><th width="149">Thành phần</th><th width="260">Policy cho IAM_User_Leo</th><th width="215">Policy cho IAM_User_Anne</th><th></th></tr></thead><tbody><tr><td>Product</td><td>vstorage</td><td>vstorage</td><td></td></tr><tr><td>Action</td><td><ul><li><strong>List</strong></li><li><strong>Read</strong></li></ul><p>(Bao gồm tất cả các actions trong mỗi nhóm)</p></td><td><ul><li><strong>All vstorage actions</strong>. (List, Read, Write)</li></ul><p>(Bao gồm tất cả các actions trong mỗi nhóm)).</p></td><td></td></tr><tr><td>Resource</td><td>Region</td><td><ul><li><strong>HAN01</strong></li></ul></td><td><ul><li><strong>HAN01</strong></li><li><strong>HCM01</strong></li></ul></td></tr><tr><td>Project_ID</td><td><ul><li><strong>Project_ID</strong> của <strong>Project01</strong></li></ul></td><td><ul><li><strong>Project_ID</strong> của <strong>Project01</strong></li><li><strong>Project_ID</strong> của <strong>Project02</strong></li></ul></td><td></td></tr><tr><td>Container name</td><td><ul><li>Any</li></ul></td><td><ul><li>Any</li></ul></td><td></td></tr><tr><td>Object name</td><td><ul><li>Any</li></ul></td><td><ul><li>Any</li></ul></td><td></td></tr></tbody></table>

<figure><img src="https://docs.vngcloud.vn/download/attachments/64554004/image2023-10-9_10-24-26.png?version=1&#x26;modificationDate=1696821867000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



<figure><img src="https://docs.vngcloud.vn/download/attachments/64554004/image2023-10-9_10-24-48.png?version=1&#x26;modificationDate=1696821890000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



<figure><img src="https://docs.vngcloud.vn/download/attachments/64554004/image2023-10-9_10-28-46.png?version=1&#x26;modificationDate=1696822127000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



**Bước 3: Liên kết (Gán quyền) tài khoản IAM User Account với policy tương ứng.**

Thực hiện liên kết (gán quyền) 2 tài khoản IAM User Account với policy đã tạo ở bước 2 theo hướng dẫn tại [Liên kết tài khoản IAM User Account với policy tương ứng](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59804818).&#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/64554004/image2023-10-9_10-34-15.png?version=1&#x26;modificationDate=1696822457000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



<figure><img src="https://docs.vngcloud.vn/download/attachments/64554004/image2023-10-9_10-34-34.png?version=1&#x26;modificationDate=1696822475000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



**Bước 4: Truy cập vStorage Portal sử dụng IAM User Account**

Thực hiện truy cập vStorage Portal sử dụng tài khoản IAM User Account theo hướng dẫn tại [Truy cập tài nguyên sử dụng tài khoản người dùng IAM](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648948).

<figure><img src="https://docs.vngcloud.vn/download/attachments/64554004/image2023-10-9_10-35-43.png?version=1&#x26;modificationDate=1696822544000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

