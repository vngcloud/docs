# Làm việc với object và directory

## Tổng quan

Để lưu trữ một object trong vStorage, bạn tạo một bucket thông qua 3rd party software rồi tải một tệp tin lên bucket đó. Tệp tin mới được tải lên này được lưu trữ bên trong bucket như một object. Khi object đó ở trong bucket, bạn có thể tải cùng một tệp tin lên bucket để ghi đè object (cập nhật object), tải xuống, sao chép, di chuyển hoặc thay đổi thiết thiết lập tag, metadata cho object đó. Khi bạn không còn cần một object hoặc một nhóm object, bạn có thể xóa để dọn sạch tài nguyên của mình trên vStorage.

## Phạm vi giới hạn object

**Quy tắc đổi tên object**

Các quy tắc sau áp dụng cho việc đổi tên object trong vStorage:

* Tên object phải dài từ 1 (tối thiểu) đến 255(tối đa) ký tự.
* Tên object có thể bao gồm các chữ cái viết hoa, viết thường (a-z, A-Z), số (0-9), tất cả các ký tự đặc biệt và khoảng trắng nếu có.
* Để hạn chế lỗi trong quá trình làm việc với các object sử dụng công cụ phía người dùng (client tool) hoặc trên vStorage, chúng tôi khuyến khích việc đặt tên object không nên sử dụng các ký tự đặc biệt như $, #, %, &, ^, v.v. và nên sử dụng hệ chữ viết Latin để đặt tên cho object, directory.

**Quy định về dung lượng tối đa của tệp tin khi tải lên**

* Không giới hạn số lượng tệp tin trong một lần tải lên hoặc tải xuống.
* Tổng dung lượng tối đa của các tệp tin trong một lần tải lên thông qua vStorage Portal là 20GB.
* Tổng dung lượng tối đa của các tệp tin trong một lần tải lên thông qua 3rd party software hoặc vStorage API là 5TB.

## Upload/ Download object

Để Upload/download object, bạn hãy chọn 2 biểu tượng tương ứng như hình sau.

<figure><img src="../../../../.gitbook/assets/image (612).png" alt=""><figcaption></figcaption></figure>

## Tìm kiếm object/ folder

Để tìm kiếm object/ folder, bạn hãy chọn biểu tượng tương ứng như hình sau.

<figure><img src="../../../../.gitbook/assets/image (613).png" alt=""><figcaption></figcaption></figure>

## Di chuyển object

Để di chuyển object, bạn hãy nhấn chuột phải vào object cần di chuyển và chọn **Move to** tương ứng như hình sau.

<figure><img src="../../../../.gitbook/assets/image (614).png" alt=""><figcaption></figcaption></figure>

## Sao chép object

Để di chuyển object, bạn hãy nhấn chuột phải vào object cần di chuyển và chọn **Copy to** tương ứng như hình sau.

<figure><img src="../../../../.gitbook/assets/image (615).png" alt=""><figcaption></figcaption></figure>

## Đổi tên object

Để đổi tên object, bạn hãy nhấn chuột phải vào object cần di chuyển và chọn **Rename** tương ứng như hình sau.

<figure><img src="../../../../.gitbook/assets/image (616).png" alt=""><figcaption></figcaption></figure>

## Thiết lập tag object

Để thiết lập tag cho object, bạn hãy nhấn chuột phải vào object cần di chuyển và chọn **Edit Object Tags** tương ứng như hình sau.

<figure><img src="../../../../.gitbook/assets/image (617).png" alt=""><figcaption></figcaption></figure>

## Thiết lập metadata object

Để thiết lập metadata cho object, bạn hãy nhấn chuột phải vào object cần di chuyển và chọn **Edit HTTP Header** tương ứng như hình sau.

<figure><img src="../../../../.gitbook/assets/image (619).png" alt=""><figcaption></figcaption></figure>

## Xóa object

Để xóa object, bạn hãy nhấn chuột phải vào object cần di chuyển và chọn **Delete** tương ứng như hình sau.

<figure><img src="../../../../.gitbook/assets/image (618).png" alt=""><figcaption></figcaption></figure>

Chi tiết các tính năng, vui lòng tham khảo thêm tại [https://s3browser.com/](https://s3browser.com/).
