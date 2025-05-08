# Notebook instance

Notebook là môi trường phát triển tương tác (interactive environment) tích hợp sẵn trên AI Platform, cho phép bạn viết code, huấn luyện mô hình, phân tích dữ liệu và trực quan hoá kết quả ngay trên nền tảng cloud – mà không cần cài đặt môi trường cục bộ.

**Tổng quan Notebook trên AI Platform**

* Hỗ trợ nhiều framework như **PyTorch, TensorFlow, HuggingFace, scikit-learn...**
* Chạy trên GPU hoặc CPU tuỳ nhu cầu.
* Có thể gắn **Network Volume** để truy cập dữ liệu hoặc model.

***

## **Các bước sử dụng Notebook**

#### **Bước 1: Truy cập giao diện AI Platform**

1. Đăng nhập vào [VNG Cloud AI Platform](https://aiplatform.console.vngcloud.vn/overview).
2. Chọn mục **Notebook instance** từ menu bên trái.

#### **Bước 2: Khởi tạo một Notebook mới**

Nhấn nút **“Create Notebook”** và điền các thông tin sau:

<table><thead><tr><th width="208">Field</th><th>Mô tả</th></tr></thead><tbody><tr><td><strong>Notebook Name</strong></td><td>Đặt tên dễ nhớ, ví dụ <code>image-classification-notebook</code></td></tr><tr><td><strong>Region</strong></td><td>Khu vực triển khai, hiện tại hỗ trợ <code>HCM</code></td></tr><tr><td><strong>Framework/Container</strong></td><td>Chọn môi trường phù hợp: e.g. <code>PyTorch</code>, <code>TensorFlow</code></td></tr><tr><td><strong>Instance Type</strong></td><td>Chọn tài nguyên phù hợp: <code>CPU</code>, <code>GPU</code></td></tr><tr><td><strong>Attach Network Volume (tuỳ chọn)</strong></td><td><em>Chọn Network Volume đã được tạo sẵn</em> (ví dụ: <code>ai-storage</code>) để lấy dữ liệu đầu vào hoặc model</td></tr><tr><td><strong>Folder Name on Notebook</strong></td><td><em>Chỉ định thư mục đích trong notebook để đồng bộ dữ liệu từ Network Volume</em>. Ví dụ: <code>/workspace/notebook-data</code></td></tr><tr><td><strong>Storage Size (Block Storage)</strong></td><td><em>Chọn dung lượng lưu trữ tạm (ephemeral block storage) để chứa bản sao dữ liệu đồng bộ từ Network Volume</em>. Nên chọn kích thước đủ lớn so với dữ liệu cần dùng (ví dụ: 20 GB, 50 GB...)</td></tr></tbody></table>

#### **Bước 3: Mở và sử dụng Notebook**

1.  Khi trạng thái chuyển sang **Active**, bạn có thể nhấn **“Connect”** để mở giao diện.&#x20;

    <figure><img src="../../.gitbook/assets/image.png" alt="" width="206"><figcaption></figcaption></figure>
2. Viết code Python, import thư viện, truy cập dữ liệu từ blockstorage.

#### **Bước 4: Lưu, chia sẻ và ngắt kết nối**

* **Notebook sẽ tự động lưu định kỳ**.
* Khi không dùng, bạn nên nhấn **“Stop”** để tiết kiệm tài nguyên.
* Có thể **xuất Notebook (.ipynb)** để chia sẻ hoặc tái sử dụng.

***

## **Cơ chế đồng bộ dữ liệu giữa Network Volume và Notebook**

AI Platform hỗ trợ **tự động đồng bộ hai chiều dữ liệu** giữa **Network Volume** và **block storage của Notebook**, giúp đảm bảo người dùng làm việc trên bản sao dữ liệu mới nhất và có thể lưu lại kết quả dễ dàng.

#### **Khi Notebook được khởi động (Start):**

* Dữ liệu trong Network Volume (được mount trước đó) sẽ **được đồng bộ toàn bộ một chiều** vào thư mục chỉ định trong block storage của Notebook (ví dụ: `/workspace/notebook-data`).
* Quá trình này giúp người dùng thao tác trên dữ liệu “cục bộ” để đảm bảo hiệu năng cao và tốc độ truy cập nhanh.

> ✅ **Note:** Dữ liệu trên Notebook là bản sao tạm thời — các thay đổi tại đây chưa ảnh hưởng đến dữ liệu gốc trên Network Volume.

#### **Khi Notebook được dừng lại (Stop):**

* Hệ thống sẽ **tự động đồng bộ ngược trở lại** từ thư mục block storage của Notebook về Network Volume.
* Dữ liệu được ghi đè lên Network Volume, tức là **mọi chỉnh sửa, file mới, hoặc xoá file trong quá trình làm việc sẽ được phản ánh ngược lại** vào Network Volume.

> ⚠️ **Lưu ý:** Việc ghi đè sẽ thay thế nội dung cũ trên Network Volume bằng nội dung trong thư mục notebook. Hãy chắc chắn bạn không làm mất dữ liệu quan trọng.
