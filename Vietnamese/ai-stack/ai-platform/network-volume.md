# Network volume

## **Giới thiệu tổng quan**

**Network Volume** là một loại lưu trữ dùng chung (shared storage) trong AI Platform, cho phép người dùng lưu trữ dữ liệu như model, dataset, và kết quả huấn luyện, đồng thời truy cập từ nhiều service khác nhau như Notebook, Model Registry và Inference.

**Lợi ích chính**

* Chia sẻ dữ liệu giữa các service dễ dàng
* Dữ liệu bền vững, không bị mất khi notebook tắt
* Giảm thời gian truyền dữ liệu giữa các bước trong pipeline AI

**Cách hoạt động**

* Network Volume được gắn (mount) vào các môi trường compute như Notebook, Inference container.
* Dữ liệu trong Network Volume có thể được đồng bộ từ nguồn bên ngoài (ví dụ S3).
* Khi sử dụng trong Notebook, dữ liệu sẽ được **sync từ Network Volume → block storage** của Notebook khi bắt đầu, và **sync ngược lại** khi tắt notebook (đảm bảo dữ liệu luôn được cập nhật).
* Với Inference, Network Volume sẽ được mount trực tiếp vào pod khi model được triển khai.

## **Hướng dẫn sử dụng Network volume**

### Bước 1: Khởi tạo Network Volume

1. Truy cập vào tab **Network Volume** trong AI Platform theo đường dẫn: [https://aiplatform.console.vngcloud.vn/volume](https://aiplatform.console.vngcloud.vn/volume)
2. Click **Create Network Volume**.
3. Nhập thông tin:
   * **Tên Volume**: Ví dụ `ai-storage`
   * **Kích thước (GB)**: Chọn đủ lớn để chứa dataset hoặc model
   * **Region**: Ví dụ `HCM`
4. Click **Tạo Volume**

> Sau khi tạo xong, volume sẽ sẵn sàng để gắn vào Notebook hoặc dùng cho Model Registry / Inference.

### Bước 2: Sync dữ liệu từ S3 vào Network Volume

### Bước 3: Mount Network Volume vào Notebook

Khi khởi tạo Notebook:

* Chọn phần **Data Mount**
* Chỉ định:
  * Network volume: `ai-storage`
  * Mount folder name (Folder Sync): Tên thư mục trên notebook (VD: `/workspace/notebook-data`)
  * Block storage size: Dung lượng đủ lớn để chứa toàn bộ dữ liệu từ network volume

<figure><img src="../../.gitbook/assets/image (1079).png" alt="" width="337"><figcaption></figcaption></figure>

* **Khi start notebook:**
  * Dữ liệu từ Network Volume sẽ **tự động copy vào thư mục** mount trên Notebook
* **Khi stop notebook:**
  * Dữ liệu thay đổi sẽ được **sync ngược lại vào Network Volume**

### Bước 4: Dùng Network Volume trong Inference

#### **A. Import vào Model Registry**

1. Tạo Model Registry mới
2. Chọn:
   * **Loại lưu trữ (Model source)**: Network Volume
   * **Model repository:** Đường dẫn tới file model (VD: `/models/llama3/`)
   * **Network volume**: Chỉ định Network Volume **chứa model AI** để hệ thống có thể truy cập khi chạy inference. Lưu ý model phải được lưu đúng với đường dẫn nhập tại Model repository `ai-storage`&#x20;

<figure><img src="../../.gitbook/assets/image (1080).png" alt="" width="375"><figcaption></figcaption></figure>

> Sau khi import, model sẽ sẵn sàng để deploy.

#### **B. Khởi tạo Inference với Network Volume**

Khi tạo Endpoint:

1. Chọn Model Registry đã import ở bước trước
2. AI Platform sẽ tự động:
   * **Mount network volume vào Pod**
   * **Deploy model lưu trữ tại đường dẫn** để phục vụ inference

> Quá trình này giúp giảm thời gian khởi tạo vì không cần upload lại model mỗi lần. Nếu model repository nhập không chính xác, quá trình deploy inference sẽ xảy ra lỗi.
