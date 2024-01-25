Tại giao diện profile management chọn create profile  

![](images/storage/image2019-5-14_0-26-43.png)

 **Bước 1: ** Tạo template cho instance. Tại đây bạn sẽ define các giá trị cấu hình của 1 instance mà mình muốn auto-scaling group sẽ tạo thêm / giảm bớt khi thực hiện scaling.  

Tạo template sẽ gồm các thông tin là: Profile / instance name, Image, Flavor, Volume, Network 

Các bước dưới đây sẽ mô tả cách nhập thông tin cho template 


* Profile & Instance name:  



Tại Profile information, click chọn và đặt tên cho profile &  instance, lưu ý chỉ đặt các ký tự A->Z hoặc số. Tên profile và instance giới hạn từ 6-20 ký tự 

![](images/storage/image2019-5-14_0-29-34.png)


*  **IMAGE**  **: ** Chọn trong danh sách OS có sẵn   

![](images/storage/image2019-5-14_0-30-4.png)

Bạn cũng có thể chọn danh sách Image bạn đã upload (hướng dẫn bạn xem tại [đây](https://docs.vinadata.vn/pages/viewpage.action?pageId=2723140)) 

![](images/storage/image2019-5-14_0-31-51.png)


*  **FLAVOR ** 

![](images/storage/image2019-5-14_0-32-14.png)


*  **VOLUME ** 

![](images/storage/image2019-5-14_0-35-18.png)


*  **NETWORK** 

![](images/storage/image2019-5-14_0-35-40.png)



Tương ứng với các thông số bạn chọn cho template, bạn có thể xem giá tham khảo ở góc trái với các thông tin như hình dưới  

Lưu ý đây chỉ là giá tham khảo cho profile, VNDT sẽ không lấy bất kỳ phí gì khi bạn tạo profile (template). Phí phải trả khi sử dụng auto-scaling sẽ tính dựa vào thực tế sử dụng của bạn (tổng số phút instance scale) và thanh toán vào cuối tháng. (Xem thêm tại phần phí auto-scaling)  

![](images/storage/image2019-5-14_0-36-31.png)



Sau khi đã nhập đầy đủ các thông tin cho template, chọn vào Next để qua bước 2 profile information  



 **Bước**  ** 2: Profile information (Optional)**  ** ** 

Các thông tin ở bước 2 không bắt buộc, bạn có thể bỏ qua nếu không có nhu cầu sử dụng.  

![](images/storage/image2019-5-14_0-41-33.png)

 **Bước 3: Summary  ** 

Xem lại các thông tin đã tạo, nếu không có vấn đề gì chọn create profile. Lưu ý: bạn sẽ không bị charge bất kỳ phí gì khi tạo profile. 

![](images/storage/image2019-5-14_0-46-43.png)

Sau khi tạo thành công, bạn sẽ thấy profile mới tạo hiển thị ở giao diện profile managment  

![](images/storage/image2019-5-14_0-47-6.png)

Nếu bạn muốn xem thông tin chi tiết của profile, nhấp vào ô vuông tickbox bên trái tên profile 

![](images/storage/image2019-5-14_0-47-35.png)











*****

[[category.storage-team]] 
[[category.confluence]] 
