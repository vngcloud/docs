# Phân quyền truy cập ACLs container

Phân quyền truy cập ACLs là một tính năng của vStorage cho phép hệ thống thiết lập quyền truy cập (Đọc, Ghi, Đọc và Ghi) đến một container và các object thuộc container đó cho một hay nhiều tài khoản người dùng Root thuộc hệ thống vStorage.

Bạn có thể cấp quyền Đọc, Ghi hoặc Đọc và Ghi cho một hoặc tất cả tài khoản người dùng Root khác (Tài khoản người dùng Root được cấp quyền truy cập qua ACLs phải là tài khoản được hợp lệ trên hệ thống VNG Cloud của chúng tôi).

* Đối với quyền Đọc: bạn có thể tải xuống các object từ container được cấp quyền.
* Đối với quyền Ghi: bạn có thể tải lên, tải xuống object từ container được cấp quyền.

<figure><img src="https://www.vngcloud.vn/documents/20126/1455799/vng-cloud-product-vstorage-acl-vi-01-slideshow.jpg" alt=""><figcaption></figcaption></figure>

Để thiết lập phân quyền truy cập ACLs, bạn có thể thực hiện theo hướng dẫn bên dưới:&#x20;

&#x20;Sử dụng vStorage Portal

1\. Đăng nhập vào [https://vstorage.console.vngcloud.vn](https://vstorage.console.vngcloud.vn/storage/list).

2\. Chọn **project** và chọn **container** bạn muốn phân quyền truy cập ACLs.

3\. Chọn ![](https://docs.vngcloud.vn/download/thumbnails/49648513/image2023-3-6\_10-26-12.png?version=1\&modificationDate=1678073173000\&api=v2) hoặc chọn biểu tượng ![](https://docs.vngcloud.vn/download/thumbnails/49648513/image2023-2-6\_10-20-54.png?version=1\&modificationDate=1675654311000\&api=v2)tại **container** bạn muốn thực hiện sử dụng tính năng phân quyền truy cập ACls và chọn ![](https://docs.vngcloud.vn/download/thumbnails/49648513/image2023-3-6\_10-26-49.png?version=1\&modificationDate=1678073210000\&api=v2)

4\. Màn hình **Thiết lập ACLs** được hiển thị. Trong mục **Truy cập cho những tài khoản khác**, bạn nhập địa chỉ email hoặc số điện thoại của Root user account muốn thực hiện thêm quyền. Email hoặc số điện thoại mà bạn nhập phải là email, số điện thoại đã được đăng ký tài khoản VNG Cloud. Nếu email, số điện thoại chưa được đăng ký thì sẽ không được thêm quyền truy cập ACLs cho container này.

5\. Chọn quyền truy cập tương ứng cho Root user account vừa nhập, các quyền truy cập chúng tôi đang cung cấp cho bạn bao gồm: ContainerAdmin, ContainerViewer, ContainerReader, ContainerEditor. Chọn **Cập nhật.**

6\. Nếu bạn muốn tất cả người dùng có thể truy cập tới container với 1 quyền giống nhau, hãy chọn tương tự các bước trên trong mục **Truy cập công khai**.

Sau khi bạn hoàn thành 7 bước được mô tả bên trên, bạn đã phân quyền truy cập ACLs container cho một vài tập người dùng mà bạn chọn. Nếu có việc truy cập không được phép, bạn có thể điều chỉnh thông tin truy cập của các Root user account này sang các quyền truy cập thấp hơn.
