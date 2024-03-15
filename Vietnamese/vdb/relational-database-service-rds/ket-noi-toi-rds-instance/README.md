# Kết nối tới RDS Instance

Để kết nối với RDS Instance có **Database Engine** là **MySQL** hay **Mariadb**, bạn có thể sử dụng bất kì công cụ MySQL Client nào như mysql-client (CLI Client của MySQL phát triển), MySQL Workbench (GUI client của MySQL phát triển), Heidi,…&#x20;

Tương tự, đối với **Postgresql**, bạn có thể dùng các client như: psql (ClI Client do PostgreSQL phát triển), pgAdmin (GUI Client phổ biến),...

Bạn có thể tham khảo video sau:

{% embed url="https://youtu.be/1kvJi3Hg4wM" %}

Hoặc tham khảo bài viết hướng dẫn dưới đây. Bài viết này VNG Cloud sử dụng mysql-client, MySQL Workbench và psql.

\


* [Bước 0. Cài đặt client tool để kết nối:](https://docs.vngcloud.vn/pages/viewpage.action?pageId=2723017#K%E1%BA%BFtn%E1%BB%91it%E1%BB%9BiRDSInstance-B%C6%B0%E1%BB%9Bc0.C%C3%A0i%C4%91%E1%BA%B7tclienttool%C4%91%E1%BB%83k%E1%BA%BFtn%E1%BB%91i:)
* [Bước 1. Xác định thông tin Endpoint & Port để truy cập:](https://docs.vngcloud.vn/pages/viewpage.action?pageId=2723017#K%E1%BA%BFtn%E1%BB%91it%E1%BB%9BiRDSInstance-B%C6%B0%E1%BB%9Bc1.X%C3%A1c%C4%91%E1%BB%8Bnhth%C3%B4ngtinEndpoint\&Port%C4%91%E1%BB%83truyc%E1%BA%ADp:)
* [Bước 2: Tùy chỉnh Security Group Rules để bảo vệ DB Instance (tùy chọn)](https://docs.vngcloud.vn/pages/viewpage.action?pageId=2723017#K%E1%BA%BFtn%E1%BB%91it%E1%BB%9BiRDSInstance-B%C6%B0%E1%BB%9Bc2:T%C3%B9ych%E1%BB%89nhSecurityGroupRules%C4%91%E1%BB%83b%E1%BA%A3ov%E1%BB%87DBInstance\(t%C3%B9ych%E1%BB%8Dn\))
* [Bước 3. Kết nối bằng các client tools:](https://docs.vngcloud.vn/pages/viewpage.action?pageId=2723017#K%E1%BA%BFtn%E1%BB%91it%E1%BB%9BiRDSInstance-B%C6%B0%E1%BB%9Bc3.K%E1%BA%BFtn%E1%BB%91ib%E1%BA%B1ngc%C3%A1cclienttools:)

### Bước 0. Cài đặt client tool để kết nối: <a href="#ketnoitoirdsinstance-buoc0.caidatclienttooldeketnoi" id="ketnoitoirdsinstance-buoc0.caidatclienttooldeketnoi"></a>

Để cài đặt MySQL Workbench (Windows/Linux), bạn có thể download theo hướng dẫn của MySQL:

[https://dev.mysql.com/downloads/workbench/](https://dev.mysql.com/downloads/workbench/)

\


Để cài đặt MySQL-Client (Linux), bạn có thể cài đặt nhanh bằng:

Ubuntu:

| `sudo apt-get install mysql-client` |
| ----------------------------------- |

CentOS:

| `sudo yum install mysql` |
| ------------------------ |

\


Để cài đặt Psql (Linux/MacOS), bạn cài đặt như sau:

Ubuntu:

| `sudo apt-get install postgresql-client` |
| ---------------------------------------- |

CentOS:

| `sudo yum install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-redhat10-10-2.noarch.rpm` `sudo yum install postgresql10` |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ |

MacOS:

| `brew install libpq` |
| -------------------- |

\


### Bước 1. Xác định thông tin Endpoint & Port để truy cập: <a href="#ketnoitoirdsinstance-buoc1.xacdinhthongtinendpoint-and-portdetruycap" id="ketnoitoirdsinstance-buoc1.xacdinhthongtinendpoint-and-portdetruycap"></a>

Tại giao diện quản lý Database, bạn chọn vào RDS Instance vừa tạo, chọn đến tab **Connectivity & Security**, xem tại mục **Endpoint & Port**.

VD: như hình duới, RDS Instance này có 2 endpoint: private (trong nội bộ VPC) & public (có thể kết nối tới thông qua Internet). Tùy vào usecase, bạn lựa chọn endpoint thích hợp.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723017/image2019-6-24_13-58-33.png?version=1&#x26;modificationDate=1561359513000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


**Lưu ý**: Để phân biệt **Public Endpoint** & **Private Endpoint**, bạn xem mục **Networking** để xác định **Private Network** **Subnet** của RDS Instance này.

VD: DB Instance trên có **Private Network Subnet** là 10.0.116.0/24 nên 10.0.116.3 sẽ là **Private Endpoint**.

### Bước 2: Tùy chỉnh Security Group Rules để bảo vệ DB Instance (tùy chọn) <a href="#ketnoitoirdsinstance-buoc2-tuychinhsecuritygrouprulesdebaovedbinstance-tuychon" id="ketnoitoirdsinstance-buoc2-tuychinhsecuritygrouprulesdebaovedbinstance-tuychon"></a>

Mục **Security Group Rules** cho phép bạn giới hạn những **Remote IP** nào được phép truy cập vào RDS Instance của bạn. Để tiện lợi cho việc sử dụng, khi vừa khởi tạo, VNG Cloud cho phép bạn truy cập không hạn chế từ mọi nơi (0.0.0.0/0) vào RDS Instance. Tuy nhiên, VNG Cloud khuyến nghị bạn tùy chỉnh lại mục này sao cho chỉ những **Remote IP** tin cậy được truy cập vào.

Để thay đổi, bạn chọn vào **EDIT** và điền IP (theo chuẩn CIDR) thích hợp.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723017/image2019-6-24_13-58-57.png?version=1&#x26;modificationDate=1561359538000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Sau khi hiệu chỉnh, nhấn **Save** và chờ một lát để thay đổi được lưu lại.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723017/image2019-6-24_13-59-12.png?version=1&#x26;modificationDate=1561359553000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Để chắc chắn kết nối được thông suốt, bạn có thể dùng các công cụ kiểm tra như telnet.

Khi kết nối đã thông suốt, bạn có thể tiến hành kết nối tới RDS Instance.

### Bước 3. Kết nối bằng các client tools: <a href="#ketnoitoirdsinstance-buoc3.ketnoibangcacclienttools" id="ketnoitoirdsinstance-buoc3.ketnoibangcacclienttools"></a>

Sau khi có thông tin endpoint, bạn sử dụng **Master User** vừa tạo để kết nối.

Lưu ý: Master user chỉ được tạo một lần duy nhất, nếu quên password, bạn có thể chọn **Action** > **Edit Database** để tự thay đổi password. Nếu quên thông tin Master User, bạn có thể liên hệ **VNG Cloud Support** để được hỗ trợ.

VD: RDS Instance vừa tạo có master user là: dba, endpoint truy cập là public endpoint: 61.28.224.201, port: 3306, bạn kết nối như sau:

Trên **Linux** (**Ubuntu**, **CentOS**), bạn có thể dùng ngay luôn **mysqlclient** (thường được cài đặt sẵn trong hệ điều hành):

| `$ mysql -h 61.28.224.201` `-P 3306` `-u dba –p` `Password` `mysql>` |
| -------------------------------------------------------------------- |

\


Trên **Windows/Linux/MacOS** bạn có thể tải **MySQL Workbench** tại: [https://dev.mysql.com/downloads/workbench/](https://dev.mysql.com/downloads/workbench/)

Workbench là client tool của chính MySQL phát triển, có giao diện đồ họa trực quan, dễ sử dụng. Trên các máy Linux (Ubuntu, Centos) bạn cũng có thể sử dụng Workbench.

Sau khi tải & cài đặt Workbench, bạn thiết lập các thông tin kết nối như sau:

Tại giao diện khởi động, bạn chọn **Database** > **Connect to Database.**

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723017/connect-win-0.PNG?version=1&#x26;modificationDate=1609664818000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Bạn điền các thông tin:

* Connection Name: đặt một tên dễ nhớ cho kết nối này để bạn dễ phân biệt.
* Hostname: IP Endpoint của vDB, ở đây là **61.28.244.201**
* Port: giữ nguyên mặc định 3306.
* Username: Master User của bạn, ở đây là **dba**

sau khi chắc chắn các thông tin đã chính xác, bạn nhấn **Test Connection**

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723017/connect-win-1.PNG?version=1&#x26;modificationDate=1609664819000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Một hộp thoại hiện ra để yêu cầu bạn nhập mật khẩu truy cập, bạn có thể tick chọn **Save Password in vault** để Workbench lưu lại password cho phiên kết nối sau.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723017/connect-win-4.PNG?version=1&#x26;modificationDate=1609664820000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Lưu ý, nếu bạn sử dụng Workbench kết nối đến MariaDB hoặc MySQL version cũ, sẽ có cảnh báo không hoàn toàn tương thích như sau, bạn có thể bỏ qua và chọn **Continue Anyway**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723017/connect-win-2.PNG?version=1&#x26;modificationDate=1609664819000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Nếu không có trở ngại gì, bạn sẽ nhận được thông báo thành công như sau:

<figure><img src="https://docs.vngcloud.vn/download/attachments/2723017/connect-win-3.PNG?version=1&#x26;modificationDate=1609664819000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Đối với Postgresql, bạn dùng psql với cú pháp sau và nhập password đã đăng kí lúc khởi tạo vDB:

| `psql -h<Endpoint_vDB> -U<master_user> -W -d<Database_Name>` `Password:` |
| ------------------------------------------------------------------------ |

trong đó:

* Endpoint\_vDB: là endpoint kết nối tới vDB.
* Master\_user: là master user bạn đăng kí lúc khởi tạo.
* Database\_Name: là Database Name bạn điền vào ở phần DB Options. (khác với DB Instance Name ở mục DB Settting lúc khởi tạo và hiển thị ở mục Database trên Portal). Nếu quên, bạn có thể liên hệ VNG Cloud Support để lấy lại thông tin này.&#x20;

\


Nếu có vấn đề gì cần hỗ trợ, bạn có thể liên hệ **VNG Cloud Support Team** ngay. Cảm ơn bạn đã xem hết bài hướng dẫn.
