# Chỉnh sửa File Storage

Trên mỗi file storage, bạn có thể thực hiện chỉnh sửa một số thông số, cụ thể:

* **Đối với file storage NFS**: Cho phép chỉnh sửa quyền truy cập (ACL) trực tiếp trên file hoặc thư mục. Tuy nhiên, việc chỉnh sửa ACL có thể gây gián đoạn cho File storage này lên đến **10 giây**. Thực hiện hành động này thường xuyên sẽ gây gián đoạn cho File storage của bạn.

<figure><img src="../../../.gitbook/assets/image (910).png" alt=""><figcaption></figcaption></figure>

* **Đối với file storage SMB sử dụng Basic Authentication**: Có thể thực hiện các thao tác như thêm mới tài khoản, vô hiệu hóa, thay đổi mật khẩu, hoặc xóa các tài khoản authentication đã tạo.

<figure><img src="../../../.gitbook/assets/image (911).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (912).png" alt=""><figcaption></figcaption></figure>

* **Đối với file storage SMB sử dụng AD Authentication**: Không cho phép thay đổi thông tin của Active Directory; nếu cần thay đổi, nên tạo một file storage mới để đảm bảo tính ổn định của hệ thống.
