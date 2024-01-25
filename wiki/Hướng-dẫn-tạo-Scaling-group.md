Tại giao diện Scaling Group Management chọn group configure  

![](images/storage/image2019-5-23_23-57-46.png)

Tại scaling group configuration, nhập các thông tin cần thiết  


* Group name (Bắt buộc): Đặt tên giúp bạn gợi nhớ và quản lý khi có nhiều group. Tên group cho phép đặt các ký tự (a-z, A-Z, 0-9, '_'), bắt đầu với chữ và giới hạn từ 6-20 ký tự  


* Profile (Bắt buộc): Mỗi scaling group bắt buộc phải được gắn với 1 profile. Click drop down list để xem danh sách các profile đã tạo và chọn 1 profile mong muốn. Nếu như không có option nào thì bạn cần quay lại giao diện profile management và tạo 1 profile trước.  


* Desire Capacity: Nhập số lượng instance bạn mong muốn, scaling group sẽ scale số instance lên tương ứng. Số desire không được nhỏ hơn Min Capacity hoặc lớn hơn Max.  


* Min capcity: Số lượng instance nhỏ nhất mà bạn mong muốn group này có 




* Max capcity: Số lượng instance tối đa. Khi sử dụng receiver để scale tự động thì chỉ số Min / Max sẽ đảm bảo instance không vượt ra khỏi con số bạn mong muốn.  


* Timeout: Đơn vị là giây (s), nếu thời gian tạo group vượt quá Timeout, group này sẽ bị lỗi, bình thường bạn không cần điều chỉnh thông số này.  



![](images/storage/image2019-5-23_23-57-55.png)

Nếu bạn đã có policy tạo sẵn và muốn gắn vào , có thể nhấn Advance và chọn trong danh sách policy. Bạn có thể bỏ qua phần này và bổ sung sau.  

Lưu ý: nếu bạn đã tạo policy mà không thấy trong danh sách Policy, thì có thể xem lại và thay đổi lựa chọn phần Type policy. Danh sách policy chỉ hiển thị những policy phù hợp với type policy đã chọn 

![](images/storage/image2019-5-23_23-58-0.png)

Nhấn next để đến giao diện Summary, tại đây hãy kiểm tra lại các thông tin bạn đã nhập lại một lần nữa. Lưu ý bạn không thể thay đổi profile & group name sau khi tạo group thành công  

![](images/storage/image2019-5-23_23-58-7.png)

Chọn configure group để tạo, sau khi tạo thành công bạn sẽ thấy group xuất hiện ở giao diện quản lý Auto-scaling group với Status là CREATING.  

![](images/storage/image2019-5-23_23-58-13.png)

Sau một khoảng thời gian, bạn sẽ thấy group có Status là ACTIVE (nhấn Refresh trong Action hoặc F5) 

![](images/storage/image2019-5-23_23-58-20.png)

Nếu muốn xem thông tin chi tiết của Group,  nhấp vào ô vuông tickbox ngay tại màn hình Scaling Group Management để xem 





*****

[[category.storage-team]] 
[[category.confluence]] 
