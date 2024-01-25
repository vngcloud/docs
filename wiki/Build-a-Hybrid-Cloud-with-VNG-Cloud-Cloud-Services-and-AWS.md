 **Tổng Quan ** 

Mô hình kết nối Hybrid Cloud giữa VNG Cloud và AWS 



                                                                                                                ![](images/storage/image2019-5-23_22-50-20.png)



 **THỰC HIỆN ** 

 **Bước 1  : Kiếm tra VPC với các subnet đã được tạo ra ở AWS ** 



 **    Ở đây sẽ lấy subnet default là 172.31.16.0/20 để gán Server Database .** 

 **Bước 2 : Kiểm tra thông tin server đã được gán vào đúng subnet 172.31.16.0/20 ở AWS ** 



 **           Như vậy đã tao được server với IP : 172.31.12.216 làm server Database ** 

 **Bước 3 : Kiếm tra VPC với các subnet đã được tạo ra ở VNG Cloud ** 



 **Như vậy ở VNG CLOUD sẽ có 03 server : 10.0.10.6, 10.0.10.4, 10.0.10.3 đã được tạo trong subnet 10.0.10.0/24** 

 **Bước 4 : Kiểm tra Firewall vSRX tạo ra để sử dụng cho kết nối với AWS ** 



 **ở bước này đã tạo được Firewall : VPN_vSRX_AWS dùng để kết nối lên cloud của AWS ** 



 **Bước 5 : Tiến hành tạo VPN profile để kết nôi cho VNG Cloud ** 


1.  **Tạo Customer Gateway trên AWS Console ** 
1.  **Tao Virtual Private Gateway ** 
1.  **Tạo Site to Site VPN Connection ** 
1.  **Download profile VPN ** ![](images/storage/image2019-5-23_22-52-28.png)
1. Minh sẽ thấy 02 IP public được dùng để kết nối VPN ở AWS gồm :  **52.74.242.162**  và  **52.220.93.195** 

    và đầu VNG Cloud là ** 61.28.224.68** 

 **Bước 6 : Insert configuration vào Firewall vSRX đã được tạo ra trên VNG Cloud ** 

![](images/storage/image2019-5-23_22-52-37.png)

lưu ý ở bước cấu hình IKE Gateway gắn với external-interface, bạn chọn là ge-0/0/1.0 (thay vì ge-0/0/0.0 như trong ví dụ của AWS).

VD: trong config mẫu

set security ike gateway gw-vpn-0fb64c1-1 external-interface  **ge-0/0/0.0** 

bạn đổi lại thành

set security ike gateway gw-vpn-0fb64c1-1 external-interface  **ge-0/0/1.0** 



 **Bước 7 : Kiểm tra các kết nối từ AWS và VNG Cloud ** 


1.  **Kiểm tra kết nối Ipsec ** ![](images/storage/image2019-5-23_22-52-46.png)
1.   Minh sẽ thấy state " **UP** " với 02 IP của AWS gồm :  **52.74.242.162**  và  **52.220.93.195** 

    
1.  **Kiểm tra kết nối BGP (AWS ---VNG sư dụng internal BGP )** 

    

    BGP internal với đầu AWS qua 2 hướng khác nhau  ** ** 
1.  **Kiểm tra routing nhận quảng bá từ AWS ** 

    Phần routing cho subnet từ AWS đã được quảng bá qua 2 hướng 

 **Bước 8 : Kiểm tra đầu AWS ** 





Mình sẽ thấy đã xuất hiện phần routing  **10.0.10.0/24**  do VNG cloud services quảng bá thông qua BGP 

Bước 9 : Đứng từ đầu 2 server tại AWS và VNG Cloud Services để kiểm tra 


1. Server tại đầu VNG Cloud :

    ![](images/storage/image2019-5-23_22-53-47.png)
1. Server tại đầu AWS : 

    ![](images/storage/image2019-5-23_22-54-10.png)



 **Như vậy hoàn thành việc kết nối toàn bộ VPC của AWS với VPC của VNG  !!!!! (LATENCY THẤP HƠN DIRECT CONNECT KHÁ NHIỀU)** Link reference : [http://bluechiptek.com/blog/aws-vpn-with-juniper-srx](http://bluechiptek.com/blog/aws-vpn-with-juniper-srx)



*****

[[category.storage-team]] 
[[category.confluence]] 
