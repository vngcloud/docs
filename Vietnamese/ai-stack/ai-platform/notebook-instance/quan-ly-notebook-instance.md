---
description: >-
  Sau khi tạo notebook instance, có thể thực hiện các chức năng sau để quản lý
  chúng:
---

# Quản Lý Notebook Instance

## **Truy cập Notebook instance**

1. Đăng nhập vào [VNG Cloud AI Platform](https://aiplatform.console.vngcloud.vn/overview).
2. Chọn mục **Notebook instance** từ menu bên trái.

## &#x20;**1. Kết nối với các instance đang chạy**

Khi trạng thái chuyển sang **Active**, bạn có thể nhấn **“Connect”** để mở giao diện Notebook Jupyter nơi bạn có thể bắt đầu làm việc cho các dự án của mình.

* Cách 1: Truy cập vào đường dẫn qua tên instance

<figure><img src="../../../.gitbook/assets/image (1106).png" alt=""><figcaption></figcaption></figure>

* Cách 2: Kết nôi qua cột Action (Hành Động)

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

## **2. Chạy và Dừng Instance**

### **Chạy Instance**

Sau khi notebook instance được tạo, nó sẽ tự động chạy. Nếu một notebook hiện đang dừng, hãy tìm instance của bạn trong bảng và nhấp vào nút "Start" (Chạy).

* Cách 1: Truy cập vào đường dẫn qua tên instance

<figure><img src="../../../.gitbook/assets/image (1108).png" alt=""><figcaption></figcaption></figure>

* Cách 2: Chạy qua cột Action (Hành Động)

<figure><img src="../../../.gitbook/assets/image (1110).png" alt=""><figcaption></figcaption></figure>

### **Dừng Instance**

Nếu bạn cần tạm dừng công việc hoặc tiết kiệm tài nguyên, bạn có thể dừng phiên bản notebook của mình. Chỉ cần chọn phiên bản bạn muốn dừng và nhấp vào nút "Stop" (Dừng). Thao tác này sẽ tạm dừng phiên bản cho đến khi bạn khởi động lại.

* Cách 1: Truy cập vào đường dẫn qua tên instance

<figure><img src="../../../.gitbook/assets/image (1107).png" alt=""><figcaption></figcaption></figure>

* Cách 2: Dừng qua cột Action (Hành Động)

<figure><img src="../../../.gitbook/assets/image (1105).png" alt=""><figcaption></figcaption></figure>

## **3. Xoá Instance**

Khi một phiên bản notebook không còn cần thiết, bạn có thể xóa nó để giải phóng tài nguyên và quản lý chi phí. Xin lưu ý rằng một khi phiên bản notebook bị xóa, nó không thể được khôi phục.

* Cách 1: Truy cập vào đường dẫn qua tên instance

<figure><img src="../../../.gitbook/assets/image (1112).png" alt=""><figcaption></figcaption></figure>

* Cách 2: Dừng qua cột Action (Hành Động)

<figure><img src="../../../.gitbook/assets/image (1111).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1113).png" alt=""><figcaption><p>Một hộp thoại xác nhận sẽ xuất hiện để đảm bảo bạn không vô tình xóa nhầm phiên bản</p></figcaption></figure>

## 4. Tăng dung lượng block storage

Chọn "Resize" khi muốn tăng dung lượng block storage để có thể lưu trữ thêm data.&#x20;

Chỉ được nhập size lớn hơn hoặc bằng storage size hiện tại

* Truy cập vào đường dẫn qua tên instance

<figure><img src="../../../.gitbook/assets/image (1115).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1116).png" alt=""><figcaption></figcaption></figure>

## Những lưu ý quan trọng:

* **Tính phí:** Các Notebook instance sẽ phát sinh chi phí khi chúng đang chạy. Hãy đảm bảo dừng các instance khi bạn không sử dụng chúng để tránh các chi phí không cần thiết.
* **Tính bền vững của dữ liệu:** Dữ liệu được lưu trữ trên bộ nhớ cục bộ của phiên bản sẽ không còn khi phiên bản bị dừng. Do đó, hãy nhớ lưu trữ dữ liệu của bạn ở nơi khác để sao lưu (ví dụ: S3 bucket) trước khi dừng phiên bản.
