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

* [Tổng quan container](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648674)
* [Phạm vi giới hạn container](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648678\&src=contextnavpagetreemode)
* [Khởi tạo container](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648505\&src=contextnavpagetreemode)
* [Xem thông tin container](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648507\&src=contextnavpagetreemode)
* [Sử dụng tính năng container versioning](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648511\&src=contextnavpagetreemode)
* [Chuyển chế độ công khai container](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648685\&src=contextnavpagetreemode)
* [Chuyển chế độ riêng tư container](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648509\&src=contextnavpagetreemode)
* [Phân quyền truy cập ACLs container](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648513\&src=contextnavpagetreemode)
* [Chia sẻ tài nguyên CORS container](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648515\&src=contextnavpagetreemode)
* [Sử dụng tính năng container lifecycle](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648517\&src=contextnavpagetreemode)
* [Xóa container](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648522\&src=contextnavpagetreemode)
* [Sử dụng tính năng IP range ACLs container](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59802032\&src=contextnavpagetreemode)

**Làm việc với directory và object**

* [Tổng quan object](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648696\&src=contextnavpagetreemode)
* [Phạm vi giới hạn object](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648698\&src=contextnavpagetreemode)
* [Tải lên tệp tin](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648524\&src=contextnavpagetreemode)
* [Chia sẻ object](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648532\&src=contextnavpagetreemode)
* [Di chuyển object](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648528\&src=contextnavpagetreemode)
* [Sao chép object](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648526\&src=contextnavpagetreemode)
* [Thay đổi tên object](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648530\&src=contextnavpagetreemode)
* [Thiết lập tag object](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648536\&src=contextnavpagetreemode)
* [Thiết lập metadata object](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648701\&src=contextnavpagetreemode)
* [Tải xuống object](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648540\&src=contextnavpagetreemode)
* [Xóa object](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648534\&src=contextnavpagetreemode)
* [Làm việc với directory](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648478\&src=contextnavpagetreemode)

**Làm việc với báo cáo**

* [Xem báo cáo tóm tắt trên toàn bộ các region](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648621)
* [Xem báo cáo tóm tắt trên một region cụ thể](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648617)
* [Xem báo cáo tóm tắt trên một project cụ thể](https://docs.vngcloud.vn/pages/viewpage.action?pageId=49648619)

\
