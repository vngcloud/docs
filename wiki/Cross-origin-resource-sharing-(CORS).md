 **Giới thiệu:**  Cross-origin resource sharing (viết tắt là CORS) là một tiêu chuẩn để truy cập tài nguyên web trên các tên miền khác nhau. CORS cho phép các web scripts tương tác cởi mở hơn với nội dung bên ngoài tên miền gốc, dẫn đến sự tích hợp tốt hơn giữa các dịch vụ web.

Bạn thực hiện cấu hình CORS như sau 

 **Bước 1:**  Lực chọn domain CDN cần thiết lập CORS

![Chọn CDN cần cấu hình](images/storage/NANGCAO_CORS_1.jpg)

 **Bước 2:** Tại tab Access Protection

![Thực hiện cấu hình](images/storage/NANGCAO_CORS_2.jpg)


1.  **Lựa chọn CORS** 


1.  **Enable CORS:** 


    * Enabled: bật các thiết lập bên dưới (mục 3 và 4)


    * Disable: tắt các thiết lập bên dưới (mục 3 và 4)



    
1.  **Header Name** : phần đầu của HTTP trong mỗi yêu cầu mà client gửi tới server cũng như phản hồi của server gửi về cho client.


    *  **vCDN hỗ trợ các Header sau** :

    Access-Control-Allow-Origin

    Access-Control-Allow-Credentials

    Access-Control-Expose-Headers

    Access-Control-Max-Age

    Access-Control-Allow-Methods

    Access-Control-Allow-Headers

    Timing-Allow-Origin

    Accept-Range



    
1.  **Header Value:**  các giá trị theo sau của Header Name.



 **Bước 3:**  Lực chọn OK để kết thúc quy trình thiết lập CORS

Sau khi hoàn thành thiết lập CORS bạn sẽ nhận được thông báo như hình sau:

![Kết quả](images/storage/NANGCAO_CORS_3.jpg)





Theo bạn thì bài hướng dẫn này có giúp ích cho bạn không? Nếu bạn có thắc mắc, vui lòng liên hệ hotline 1900 54 55 69 hoặc email [support@vngcloud.vn](mailto:support@vngcloud.vn) của vCDN để được hỗ trợ nhé.



*****

[[category.storage-team]] 
[[category.confluence]] 
