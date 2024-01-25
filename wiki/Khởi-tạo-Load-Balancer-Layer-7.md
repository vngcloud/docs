 VNG Cloud cung cấp một dashboard để dễ dàng tạo Load Balancer.



| <ul><li>[Khởi tạo Load Balancer](https://docs.vinadata.vn/pages/viewpage.action?pageId=2719874#KhởitạoLoadBalancer-KhởitạoLoadBalancer)</li><li>[Thêm server member vào Load Balancer](https://docs.vinadata.vn/pages/viewpage.action?pageId=2719874#KhởitạoLoadBalancer-ThêmservermembervàoLoadBalancer)</li><li>[Kiểm tra sức khoẻ của server member](https://docs.vinadata.vn/pages/viewpage.action?pageId=2719874#KhởitạoLoadBalancer-Kiểmtrasứckhoẻcủaservermember)</li></ul> | 
|  --- | 



 **Trước khi bắt đầu ** Để tạo Load balancer bạn cần phải có network, nếu chưa tạo bạn có thể xem hướng dẫn [[Tạo network|Tạo-network]]

 **Khởi tạo Load Balancer** Chọn **Load balancer**  và chọn create  **load balancer**  layer 7 - HTTP/HTTPS



![](images/storage/image2019-5-8_11-1-4.png)




##  **Bước 1:**  Thiết lập cấu hình của Load balancer 
![](images/storage/image2019-5-8_14-8-25.png)

 **Global Setting: ** 


*  **Name** : tên gợi nhớ cho Load balancer, yêu cầu tối thiểu 6 ký tự (a-z, 0-9)
*  **Scheme:** 
    * Internet facing: Cho tất cả truy cập từ internet
    * Internal: Cho mạng truy cập nội bộ

    

 **Listener setting** 


*  **Listener name** : tên listener, yêu cầu tối thiểu 6 ký tự (a-z, 0-9)
*  **Protocol: ** HTTP hoặc HTTPS. Khi chọn HTTPS bạn sẽ cần upload certificate. 

    

    ![](images/storage/image2019-5-12_16-51-6.png)
*  **Port: ** Sẽ thay đổi tùy theo lựa chọn HTTP (80) hay HTTPS ( 443). Bạn cũng có thể tùy chỉnh theo nhu cầu

 **Network setting** 


*  **Network** : Chọn 1 trong những network bạn đã tạo, nếu chưa có bạn có thể xem hướng dẫn [[Tạo network|Tạo-network]]

    

    


##  **Bước 2** : Thiết lập cấu hình của Pool 
![](images/storage/image2019-5-12_16-59-25.png)

 **Pool setting**  


*  **Name** :  tên gợi nhớ cho pool, yêu cầu tối thiểu 6 ký tự (a-z, 0-9)
*  **Algorithm:**  Gồm 3 option
    * Round robin: Các connection sẽ được phân phối đều đến instance trong pool. 
    * Least connection: Dựa trên số lượng kết nối để thực hiện cân bằng tải, instance với lượng kết nối nhỏ nhất sẽ được đưa lên nhận connection. 
    * Source IP 

    
*  **Enable Sticky Sessions** 
*  **Protocol** 

 **Heath Setting ** 


* Path: dẫn đến nơi bạn cần health check  
* Protocol

Các  **setting advance**  sẽ mặc định được cấu hình như bên dưới, bạn có thể điều chỉnh theo nhu cầu 





![](images/storage/image2019-5-12_17-10-16.png)


##  **Bước 3** : Thêm instance vào pool Loadbalancer 
Chọn các instance có sẵn và attach vào pool, nếu chưa có instance nào bạn có thể bỏ qua bước này và bổ sung sau 

![](images/storage/image2019-5-12_17-21-13.png)


##  **Bước 4:**  Summary 
Xem lại các thiết lập cho Load balancer bạn đã thực hiện bao gồm cả package Load balancer bạn sẽ cần thanh toán. 

Hiện tại, VNG Cloud load balancer cung cấp 2 loại package là Mini và Medium. Ở các thiết lập mặc định bạn chỉ có thể tạo và thanh toán package Mini, nếu có nhu cầu sử dụng package lớn hơn hãy liên hệ 1900-1549 để được hỗ trợ. 

![](images/storage/image2019-5-12_17-22-36.png)

Chọn create load balancer để thực hiện bước thanh toán 

![](images/storage/image2019-5-12_17-29-39.png)



Chọn pay và kết hoàn tất việc tạo. Load balancer của bạn sẽ hiện ra tại giao diện quản lý chung load balancer như bên dưới 

![](images/storage/image2019-5-12_17-30-14.png)




## Các chủ đề liên quan
falseONVINAfalsetitlepagelabel = "balancer" and type = "page" and space = "ONVINA"documentation-space-sample



*****

[[category.storage-team]] 
[[category.confluence]] 
