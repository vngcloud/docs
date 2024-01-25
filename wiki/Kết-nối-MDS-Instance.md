Để kết nối với DB Instance có  **Database Engine**  là Redis, bạn có thể sử dụng redis-cli, hay các thư viện redis client của các ngôn ngữ lập trình như jedis, redis-py,...

Nếu muốn truy cập bằng giao diện, bạn có thể tham khảo tool AnotherRedisDesktopManager tải tại link sau:

[https://www.electronjs.org/apps/anotherredisdesktopmanager](https://www.electronjs.org/apps/anotherredisdesktopmanager)

sau đó thực hiện theo video hướng dẫn (bắt đầu ở 1:00):



6001200https://www.youtube.com/embed/1kvJi3Hg4wM?start=89INLINE

Nếu sử dụng tool cli, bạn có thể làm theo bài viết sau sử dụng  **redis-cli** .

Để sử dụng redis-cli, trên Linux bạn có thể tải source và build như sau:


```
wget http://download.redis.io/redis-stable.tar.gz
tar xvzf redis-stable.tar.gz
cd redis-stable
make distclean // Ubuntu systems only
make
sudo make install
```




Bước 1. Xác định thông tin Endpoint & Port để truy cập:Tại giao diện quản lý Database, bạn chọn vào MemoryCache Database instance vừa tạo, chọn đến tab  **Connectivity & Security** , xem tại mục  **Endpoint & Port** . Vì lí do bảo mật, các MDS Instance chỉ có một Endpoint Private. Bạn chỉ có thể kết nối tới từ một vServer chung Network hoặc từ các Network có mở ACL tới.

Ngoài ra, bạn cũng có thể thiết lập một SSH Tunnel trên một vServer chung Network với MDS Instance này và kết nối từ xa thông qua Internet. 

VD: như hình duới, MemoryStore Instance này có Endpoint là 10.4.113.3/32: 

![](images/storage/Screenshot from 2020-02-21 10-40-50.png)





Bước 2: Tùy chỉnh Security Group Rules để bảo vệ DB Instance (tùy chọn)Mục  **Security Group Rules ** cho phép bạn ** ** giới hạn những  **Remote IP**  nào được phép truy cập vào DB Instance của bạn. Để tiện lợi cho việc sử dụng, khi vừa khởi tạo, VNG Cloud cho phép bạn truy cập không hạn chế từ mọi nơi (0.0.0.0/0) vào DB Instance. Tuy nhiên, VNG Cloud khuyến nghị bạn tùy chỉnh lại mục này sao cho chỉ những  **Remote IP ** tin cậy được truy cập vào.

Để thay đổi, bạn chọn vào  **EDIT ** và điền IP (theo chuẩn CIDR) thích hợp. Bên cạnh đó bạn cũng có thể nhấn  **ADD RULE**  để thêm những RULE mới.

![](images/storage/Screenshot from 2020-02-21 10-41-26.png)



Sau khi hiệu chỉnh, nhấn  **Save ** và chờ một lát để thay đổi được lưu lại.

![](images/storage/Screenshot from 2020-02-21 10-41-55.png)



Để chắc chắn kết nối được thông suốt, bạn có thể dùng các công cụ kiểm tra như telnet.

Khi kết nối đã thông suốt, bạn có thể tiến hành kết nối tới DB Instance.



Bước 3. Kết nối bằng redis-cliSau khi có thông tin endpoint, bạn có thể kết nối tới thông qua IP & Port.

VD: DB Instance có IP: 10.4.113.3, port: 6379, bạn kết nối bằng redis-cli như sau:



| $ redis-cli -h 10.4.113.3 -p 637910.4.113.3:6379> | 



Chúc mừng bạn đã truy cập thành công.









*****

[[category.storage-team]] 
[[category.confluence]] 
