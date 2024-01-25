 **Giới thiệu:**  Rule có thể thiết lập trong lúc khởi tạo (như các hướng dẫn khởi tạo ở trên) hoặc tại edit setting.


* Các rule CDN cho phép thiết lập gồm:

![Các Rule của vCDN](images/storage/image2019-5-23_23-12-11.png)


* Một vài lưu ý về thứ tự & cách hoạt động

![Lưu ý về cách hoạt động](images/storage/image2019-5-23_23-12-20.png)


* 
    * Group 1: 2 condition HTTP METHOD & CLIENT IP xảy ra đồng thời thì mới thực hiện SET TTL 
    * Group 1 & group 2 & 3: 3 rules chạy độc lập. Theo thứ tự từ trên xuống 
    * Với Group 2 & 3: Condition & Action value của group 2 sẽ được thực hiện trước, sau đó đến group 3. Nếu Action của group 3 trùng với group 2 (như ví dụ bên trên) thì action group 3 (Set TTL = 50) sẽ đè lên group 2 (Set TTL = 100). 

    

Theo bạn thì bài hướng dẫn này có giúp ích cho bạn không? Nếu bạn có thắc mắc, vui lòng liên hệ hotline 1900 54 55 69 hoặc email [support@vngcloud.vn](mailto:support@vngcloud.vn) của vCDN để được hỗ trợ nhé.



*****

[[category.storage-team]] 
[[category.confluence]] 
