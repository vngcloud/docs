 **Giới thiệu:**  Bạn sử dụng Pre Cache khi bạn cần Cache trước Resource (vd: Video có dung lượng lớn) từ Origin của bạn lên CDN (Web Download, VOD) để phục vụ lượng lớn User (CDN có sẵn Resource để phục vụ User một cách nhanh nhất)

 **_Lưu ý:_** chức năng Pre Cache được áp dụng với Web Download, VOD

Để Pre Cache, bạn thực hiện các bước sau.



 **Bước 1:**  Lựa chọn CDN cần Pre Cache (Web Download hoặc VOD)

![Chọn CDN cần Pre Cache](images/storage/PurgeCache_CDN.jpg)

 **Bước 2:**  Click chọn "Pre Cache" trong menu bên trái -> màn hình Pre Cache sẽ xuất hiện

![Chọn Pre Cache ở menu bến trái](images/storage/PreCache_CDN.jpg)![Màn hình Pre Cache xuất hiện](images/storage/PreCache_CDN_2.jpg)

Tại đây, bạn nhập URI của các Resource bạn cần Cache lên CDN vào ô  **(Resource path (Split by ";")**  như hình, mỗi URI cách nhau bơi dấu ";"

 **Bước 3:**  Click nút "Preload" để thực hiện Pre Cache

Nếu Pre Cache thành công sẽ có thông báo

![Thông báo Pre Cache thành công](images/storage/PreCache_CDN_3.jpg)

 **_Lưu ý:_** trường hợp bạn nhập URI không tồn tại trên Origin của bạn, vẫn sẽ có thông báo thành công xuất hiện, nên hãy chắc chắn bạn nhập đúng URI mình muốn Cache lên CDN.



Theo bạn thì bài hướng dẫn này có giúp ích cho bạn không? Nếu bạn có thắc mắc, vui lòng liên hệ hotline 1900 54 55 69 hoặc email [support@vngcloud.vn](mailto:support@vngcloud.vn) của vCDN để được hỗ trợ nhé.



*****

[[category.storage-team]] 
[[category.confluence]] 
