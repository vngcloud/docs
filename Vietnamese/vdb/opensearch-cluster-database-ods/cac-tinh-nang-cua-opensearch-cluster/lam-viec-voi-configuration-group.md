# Làm việc với Configuration Group

Trong **vDB OpenSearch** của **VNG Cloud**, chúng tôi hỗ trợ cấu hình thông số hoạt động DB của bạn **thông qua Configuration Group**, giúp bạn dễ dàng quản lý và tối ưu hiệu suất cho OpenSearch Cluster.

## **Configuration Group Mặc Định**

* Khi bạn tạo một **OpenSearch Cluster**, hệ thống sẽ tự động gán **Configuration Group mặc định** theo phiên bản OpenSearch mà bạn chọn.
* Hiện tại, chúng tôi cung cấp **2 Configuration Group mặc định** tương ứng với:
  * **OpenSearch v2.15**
  * **OpenSearch v2.17**
* Bạn **không thể chỉnh sửa hoặc xóa** các **Configuration Group** mặc định này.

## **Tạo Mới & Gắn Configuration Group Tùy Chỉnh**

Nếu bạn muốn tùy chỉnh thông số cấu hình, hãy tạo **một Configuration Group mới** và gắn vào OpenSearch Cluster.

### **Khởi tạo một Configuration Group**

**Bước 1:** Truy cập vào [https://vdb.console.vngcloud.vn/](https://vdb.console.vngcloud.vn/)

**Bước 2:** Chọn mục **Configuration group** trên mục **OpenSearch.**

**Bước 3:** Chọn **Create a Configuration group".** Màn hình tạo mới configuration group hiển thị, tại đây bạn cần:&#x20;

Nhập các thông tin cần thiết:

* **Configuration Name**:
  * Chỉ cho phép các ký tự: `a-z`, `A-Z`, `0-9`, `_`, `-`, `.`, `@` và dấu cách.
  * Phải bắt đầu bằng một chữ cái.
  * Độ dài từ **5 đến 50 ký tự**.
* **Description** (Mô tả ngắn gọn về Configuration Group).
* **OpenSearch Version**: Chọn phiên bản tương thích với OpenSearch Cluster của bạn.

**Bước 4:** Chọn **Create** để hoàn tất việc tạo Configuration Group.

### Chỉnh sửa tham số trong một Configuration Group

Sau khi một Configuration Group được tạo, bạn có thể chỉnh sửa các tham số trong Configuration Group này bằng cách:

**Bước 1:** Chọn vào **Configuration group** mà bạn đã khởi tạo

**Bước 2:** Chọn **Edit parameters**

**Bước 3:** Chọn/Nhập giá trị tham số theo **Allowed Values** và **Data Type** quy định.

**Bước 4:** Chọn **Preview and Save** sau đó kiểm tra lại thay đổi bạn đã update

**Bước 5:** Chọn đồng ý việc **Edit parameter** có thể gây ảnh hưởng tới DB của bạn

**Bước 6**: Chọn **Apply**

### **Gắn Configuration Group vào OpenSearch Cluster**

**Bước 1: Chọn** biểu tượng <img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt="" data-size="line">tại cluster bạn muốn thay đổi configuration group

**Bước 2:** Chọn **Edit Configuration group**

**Bước 3:** Chọn một **Configuration Group** mà bạn muốn áp dụng.

**Bước 4: Chọn Save** để hoàn tất.

{% hint style="info" %}
**Chú ý:**

* Mỗi OpenSearch Cluster luôn phải có ít nhất một Configuration Group.
* Một Configuration Group có thể được gắn vào nhiều OpenSearch Cluster cùng lúc.
* Bạn có thể tạo nhiều Configuration Group tùy chỉnh để phù hợp với từng mục đích sử dụng
{% endhint %}
