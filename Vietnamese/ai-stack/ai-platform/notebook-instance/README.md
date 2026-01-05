# Notebook Instance

Notebook là môi trường phát triển tương tác (interactive environment) tích hợp sẵn trên AI Platform, cho phép bạn dễ dàng chạy các Jupyter notebook, huấn luyện mô hình, phân tích dữ liệu và trực quan hoá kết quả ngay trên nền tảng cloud – mà không cần cài đặt môi trường cục bộ.

**Tổng quan Notebook trên AI Platform**

* Hỗ trợ nhiều framework như **PyTorch, TensorFlow, HuggingFace, scikit-learn...**
* Chạy trên GPU, CPU tuỳ nhu cầu.
* Có thể gắn **Network Volume** để truy cập dữ liệu hoặc model.

***

## **Truy cập giao diện AI Platform**

1. Đăng nhập vào [GreenNode AI Platform](https://aiplatform.console.vngcloud.vn/overview).
2. Chọn mục **Notebook instance** từ menu bên trái.

## **Khởi tạo một Notebook mới**

Nhấn nút **“Create Notebook”** và điền các thông tin sau:

### **Basic configuration:**

* **Notebook instance name:** Đặt tên hợp lệ theo quy tắc sau : Chỉ cho phép các chữ cái (a-z, A-Z, 0-9, '\_', '-', '.'). Dữ liệu đầu vào phải nằm trong khoảng từ 1 đến 50 ký tự.
* **Region:** Khu vực triển khai, hiện tại hỗ trợ `HCM`

### **Resource configuration:**

Chọn loại instance hợp nhất với khối lượng công việc và yêu cầu hiệu suất của bạn. Các loại instance này sẽ xác định cấu hình CPU, RAM và GPU cho notebook instance của bạn.

1. Tìm kiếm theo tên của loại instance bạn cần&#x20;
2. **Chọn một nhóm (họ tài nguyên)** phù hợp với nhu cầu của bạn. Ví dụ :
   * CPU-CODE-S: Các phiên bản chỉ có CPU, phù hợp cho các tác vụ không cần GPU.
   * GPU-CODE-RTX2080TI: Các phiên bản có GPU NVIDIA RTX 2080 Ti.
   * GPU-CODE-RTX4090: Các phiên bản có GPU NVIDIA RTX 4090.
   * GPU-CODE-A40: Các phiên bản có GPU NVIDIA A40.
3. **Chọn một loại instance**
   * sau khi chọn một nhóm (họ tài nguyên) , bạn sẽ thấy các loại phiên bản cụ thể trong họ đó, kèm theo thông số chi tiết về GPU, CPU và RAM.

### **Image**

Chọn một framework cho notebook instance. (hiện tại chỉ hỗ trợ Pytorch 2.5.1 CUDA 12.4)

### [**Data mount**](../network-volume.md#buoc-3-mount-network-volume-vao-notebook)**:**

#### Nhấn nút "Create Instance" để khởi tạo

***

## **Cơ chế đồng bộ dữ liệu giữa Network Volume và Notebook**

AI Platform hỗ trợ **tự động đồng bộ hai chiều dữ liệu** giữa **Network Volume** và **block storage của Notebook**, giúp đảm bảo người dùng làm việc trên bản sao dữ liệu mới nhất và có thể lưu lại kết quả dễ dàng.

### **Khi Notebook được khởi động (Start):**

* Dữ liệu trong Network Volume (được mount trước đó) sẽ **được đồng bộ toàn bộ một chiều** vào thư mục chỉ định trong block storage của Notebook (ví dụ: `/workspace/notebook-data`).
* Quá trình này giúp người dùng thao tác trên dữ liệu “cục bộ” để đảm bảo hiệu năng cao và tốc độ truy cập nhanh.

> ✅ **Note:** Dữ liệu trên Notebook là bản sao tạm thời — các thay đổi tại đây chưa ảnh hưởng đến dữ liệu gốc trên Network Volume.

### **Khi Notebook được dừng lại (Stop):**

* Hệ thống sẽ **tự động đồng bộ ngược trở lại** từ thư mục block storage của Notebook về Network Volume.
* Dữ liệu được ghi đè lên Network Volume, tức là **mọi chỉnh sửa, file mới, hoặc xoá file trong quá trình làm việc sẽ được phản ánh ngược lại** vào Network Volume.

> ⚠️ **Lưu ý:** Việc ghi đè sẽ thay thế nội dung cũ trên Network Volume bằng nội dung trong thư mục notebook. Hãy chắc chắn bạn không làm mất dữ liệu quan trọng.

{% hint style="info" %}
**Chú ý:**

* Notebook instance không cung cấp Public IP để access vào container.&#x20;
{% endhint %}
