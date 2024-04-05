# Các tính năng của vStorage

#### Tổng quan <a href="#cactinhnangcuavstorage-tongquan" id="cactinhnangcuavstorage-tongquan"></a>

vStorage là dịch vụ lưu trữ objects trong containers. Một object là một tập tin và bất kỳ metadata nào mô tả tập tin đó. Một container là một thùng chứa cho các objects. Để lưu trữ dữ liệu của bạn trong vStorage, trước tiên bạn tạo một project và chỉ định tên project, gói lưu trữ cũng như region muốn lưu dữ liệu. Sau đó bạn tạo một container bên trong project vừa tạo, chỉ định tên container. Lúc này, bạn tải object của mình lên container đó dưới dạng object trong vStorage. Mô hình tổ chức lưu trữ của vStorage được chúng tôi mô tả bên dưới.

<figure><img src="https://docs.vngcloud.vn/download/attachments/49648407/image2022-12-30_9-45-20.png?version=1&#x26;modificationDate=1672368322000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

#### Chủ đề <a href="#cactinhnangcuavstorage-chude" id="cactinhnangcuavstorage-chude"></a>

Từ mô hình lưu trữ này, chúng tôi cung cấp các tính năng mà bạn có thể sử dụng để lưu trữ dữ liệu bao gồm:

**Làm việc với project**

* [Tổng quan project](lam-viec-voi-project/tong-quan-project.md)
* [Phạm vi giới hạn project](lam-viec-voi-project/pham-vi-gioi-han-project.md)
* [Khởi tạo project](lam-viec-voi-project/khoi-tao-project.md)
* [Làm việc với trial project](lam-viec-voi-trial-project.md)
* [Xem thông tin project](lam-viec-voi-project/xem-thong-tin-project.md)
* [Tăng giảm hạn mức project](lam-viec-voi-project/tang-giam-han-muc-project.md)
* [Gia hạn project](lam-viec-voi-project/gia-han-project.md)
* [Gia hạn tự động project](lam-viec-voi-project/gia-han-tu-dong-project.md)
* [Xóa project](lam-viec-voi-project/xoa-project.md)
* [Khôi phục project](lam-viec-voi-project/khoi-phuc-project.md)
* [Làm việc với POC project](lam-viec-voi-poc-project.md)
* [Sử dụng tính năng IP range ACLs project](lam-viec-voi-project/su-dung-tinh-nang-ip-range-acls-project.md)
* [Làm việc với vBackup project](lam-viec-voi-vbackup-project.md)
* [Làm việc với Archive clas](lam-viec-voi-archive-project.md)s

**Làm việc với container**

* [Tổng quan container](lam-viec-voi-container/tong-quan-container.md)
* [Phạm vi giới hạn container](lam-viec-voi-container/pham-vi-gioi-han-container.md)
* [Khởi tạo container](lam-viec-voi-container/khoi-tao-container.md)
* [Xem thông tin container](lam-viec-voi-container/xem-thong-tin-container.md)
* [Sử dụng tính năng container versioning](lam-viec-voi-container/su-dung-tinh-nang-container-versioning.md)
* [Chuyển chế độ công khai container](lam-viec-voi-container/chuyen-che-do-cong-khai-container.md)
* [Chuyển chế độ riêng tư container](lam-viec-voi-container/chuyen-che-do-rieng-tu-container.md)
* [Phân quyền truy cập ACLs container](lam-viec-voi-container/phan-quyen-truy-cap-acls-container.md)
* [Chia sẻ tài nguyên CORS container](lam-viec-voi-container/chia-se-tai-nguyen-cors-container.md)
* [Sử dụng tính năng container lifecycle](lam-viec-voi-container/su-dung-tinh-nang-container-lifecycle.md)
* [Xóa container](lam-viec-voi-container/xoa-container.md)
* [Sử dụng tính năng IP range ACLs container](lam-viec-voi-container/su-dung-tinh-nang-ip-range-acls-container.md)

**Làm việc với directory và object**

* [Tổng quan object](lam-viec-voi-directory-va-object/tong-quan-object.md)
* [Phạm vi giới hạn object](lam-viec-voi-directory-va-object/pham-vi-gioi-han-object.md)
* [Tải lên tệp tin](lam-viec-voi-directory-va-object/tai-len-tep-tin.md)
* [Chia sẻ object](lam-viec-voi-directory-va-object/chia-se-object.md)
* [Di chuyển object](lam-viec-voi-directory-va-object/di-chuyen-object.md)
* [Sao chép object](lam-viec-voi-directory-va-object/sao-chep-object.md)
* [Thay đổi tên object](lam-viec-voi-directory-va-object/thay-doi-ten-object.md)
* [Thiết lập tag object](lam-viec-voi-directory-va-object/thiet-lap-tag-object.md)
* [Thiết lập metadata object](lam-viec-voi-directory-va-object/thiet-lap-metadata-object.md)
* [Tải xuống object](lam-viec-voi-directory-va-object/tai-xuong-object.md)
* [Xóa object](lam-viec-voi-directory-va-object/xoa-object.md)
* [Làm việc với directory](lam-viec-voi-directory-va-object/lam-viec-voi-directory.md)

**Làm việc với báo cáo**

* [Xem báo cáo tóm tắt trên toàn bộ các region](lam-viec-voi-bao-cao/xem-bao-cao-tom-tat-tren-toan-bo-cac-region.md)
* [Xem báo cáo tóm tắt trên một region cụ thể](lam-viec-voi-bao-cao/xem-bao-cao-tom-tat-tren-mot-region-cu-the.md)
* [Xem báo cáo tóm tắt trên một project cụ thể](lam-viec-voi-bao-cao/xem-bao-cao-tom-tat-tren-mot-project-cu-the.md)

\
