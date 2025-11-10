# Làm việc với bucket

## Tổng quan <a href="#tong-quan" id="tong-quan"></a>

Để lưu trữ dữ liệu trong một dự án, bạn cần tạo một bucket và tải các object lên bucket đó. Trong một project, bạn có thể tạo một hoặc nhiều bucket hoạt động như một thư mục để lưu trữ dữ liệu. Tuy nhiên, bucket khác với thư mục ở chỗ bucket là một hệ thống phân cấp cho phép người dùng hoặc nhà cung cấp dịch vụ cung cấp các tính năng và thực thi chúng từ hệ thống phân cấp này trở xuống. Ví dụ: chúng tôi cung cấp bucket policy, ACL bucket, bucket lifecycle, v.v. cho mỗi bucket trong một dự án.

Về mặt triển khai, project, bucket, object là tài nguyên của vStorage và chúng tôi cũng cung cấp API để bạn quản lý chúng. Ví dụ: bạn có thể tạo project, bucket và tải các object lên bằng API. Bạn cũng có thể sử dụng giao diện quản trị mà chúng tôi cung cấp hoặc phần mềm của bên thứ ba để thực hiện các thao tác này.

***

## Phạm vi giới hạn bucket <a href="#pham-vi-gioi-han-bucket" id="pham-vi-gioi-han-bucket"></a>

### **Quy tắc đặt tên bucket**

Các quy tắc sau đây được áp dụng cho việc đặt tên bucket trong vStorage:

* Tên bucket phải có độ dài từ 3 (tối thiểu) đến 235 (tối đa) ký tự.
* Tên bucket chỉ có thể chứa chữ cái viết hoa, chữ cái viết thường (a-z, A-Z), số (0-9), dấu chấm (.), khoảng trắng (), dấu gạch dưới (\_), dấu gạch nối (-) và ký tự @.
* Tên bucket không được chứa thông tin nhạy cảm (ví dụ: địa chỉ IP, tên tài khoản, mật khẩu đăng nhập, v.v.). Chúng tôi khuyên bạn nên đặt tên bucket bằng chữ cái viết thường, số và không sử dụng các ký tự cụ thể như #, @, $, %, ?, /, \`, \~ ... Nếu bạn thực sự cần đặt tên bucket bằng ký tự viết hoa, xin lưu ý rằng bạn có thể gặp một số vấn đề khi làm việc với các phần mềm của bên thứ ba được các nhà cung cấp khác hỗ trợ.
* Tên bucket phải là duy nhất trong một region cho đến khi bucket đó bị xóa.

### Ví dụ

* Các tên bucket ví dụ sau đây là hợp lệ và tuân theo hướng dẫn đặt tên được khuyến nghị:
  * bucketexample1
  * bucket-data-2022
  * ...
* Các tên bucket ví dụ sau đây là hợp lệ nhưng chúng tôi không khuyến nghị sử dụng:
  * [docexamplewebsite.com](http://docexamplewebsite.com/)
  * [www.docexamplewebsite.com](http://www.docexamplewebsite.com/)
  * ...
* Các tên bucket ví dụ sau đây là không hợp lệ:
  * Dữ liệu bucket có hiệu suất 80% (chứa %)
  * con\_1/2022 (chứa / ký tự)
  * ...
