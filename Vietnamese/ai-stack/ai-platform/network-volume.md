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

Dữ liệu có thể được đồng bộ từ S3 vào Network Volume theo hai phương thức: **tự động (auto-sync)** hoặc **thủ công (manual sync)**.

#### 2.1 Manual Sync Dữ liệu khi Notebook vẫn đang chạy

Nếu bạn không muốn tắt notebook nhưng vẫn muốn cập nhật dữ liệu thủ công, có thể sử dụng các API sync nội bộ từ terminal của notebook:

```bash
#kéo dữ liệu từ S3 về Notebook
curl -X POST localhot:8080/pull

#đẩy data từ Notebook lên S3 (ghi đè dữ liệu cũ)
curl -X POST localhot:8080/finalize
```

> Lưu ý: Cần thực hiện lệnh này từ **bên trong notebook**, nơi đang mount Network Volume.

#### 2.2 Sử dụng S3 Key với công cụ CLI

Mỗi Network Volume tương ứng với một S3 bucket nội bộ. Có thể sử dụng s3 key của network volume để sử dụng với các công cụ command line [3rd party softwares | VNG Cloud docs](https://docs.vngcloud.vn/vng-cloud-document/vn/vstorage/object-storage/vstorage-hcm03/3rd-party-softwares). Bạn có thể sử dụng các công cụ dòng lệnh (CLI) như **s3cmd** để thao tác trực tiếp với dữ liệu trong volume. Ở tài liệu này sẽ hướng dẫn trên s3cmd.

**Chuẩn bị:**

* Cài đặt `s3cmd` trên máy
* Tạo file cấu hình `s3cnf` như sau:

```bash
[default]
access_key = <access_key>
secret_key = <secret_key>
host_base = <hostname>
bucket_location = HCM03
list_md5 = False
host_bucket = %(bucket)s.<hostname>
```

> Bạn có thể lấy các thông tin `<access_key>`, `<secret_key>`, `<hostname>` từ trang chi tiết của Network Volume trong AI Platform.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

**Sử dung s3cmd với file s3cnf đã tạo có thể sử dung các action put, ls ... với bucket**

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

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
