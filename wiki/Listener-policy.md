Bạn có thể thêm policy cho 1 listener bằng cách : Chọn **load balance** r →  **Chọn listerne** r → Chọn  **Add policy ** 

![](images/storage/image2019-5-12_20-51-14.png)

 **Add policy ** 



![](images/storage/image2019-5-12_20-50-0.png)

 **Policy name:**  Đặt tên gợi nhớ giúp bạn quản lý policy . Tên policy cần tối thiểu 6 ký tự , A-Z, 0-9

 **Condition:**  Một condition bao gồm 


*  **Mệnh đề if**  : Host hoặc Path 
*  **Rule:**  
    * Contains chứa điều kiện thỏa
    * Match: chính xác điều kiện

    
*  **Điều kiện** : Input điều kiện bạn muốn kiểm tra. 

 **Action** : Khi thỏa condition bên trên, action bạn setting sẽ được thực hiện. Action gồm


*  **Forward to pool:**  Khi thỏa điều kiện, connection sẽ được đẩy vào pool trong danh sách bạn chọn
*  **Redirect to:**  Nhập URL bạn muốn chuyển connection đến khi thỏa điều kiện





*****

[[category.storage-team]] 
[[category.confluence]] 
