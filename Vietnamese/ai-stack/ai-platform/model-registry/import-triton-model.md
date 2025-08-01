# Import Triton Model

## Chuẩn bị Model

* Vì AI Platform chỉ truy cập các mô hình từ Network Volume, bạn cần tạo một Network Volume trước. Sau đó, sao chép mô hình từ hệ thống tệp cục bộ hoặc bộ lưu trữ đám mây (như AWS S3, Azure Blob hoặc Google Cloud Storage - GCS) vào Network Volume đó.
* Đảm bảo Model tương thích với Triton Format bao gồm:&#x20;
  * **ONNX** (`.onnx`)
  * **TensorFlow** (dạng **SavedModel** hoặc tệp `.pb`)
  * **PyTorch TorchScript** (`.pt`)
  * **TensorRT** (`.engine`)
  * **OpenVINO** (`.xml` và `.bin`)
  * **Ensemble Model** (kết hợp nhiều mô hình lại với nhau) [<mark style="color:$primary;">Tham khảo</mark>](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/user_guide/ensemble_models.html)

## Bước 1: Truy cập Model Registry

* Đăng nhập với VNG Cloud account của bạn và truy cập tới <mark style="color:$primary;">Model Registry Dashboard</mark><mark style="color:$info;">.</mark>
* Tìm và nhấn vào nút "Import a model registry" (Nhập một model registry).

## Bước 2: Truy cập Model Registry

* **Region & Model registry name**: Chọn region và tên cụ thể cho model của bạn.
* **Container**: Chọn option Pre-built container để sử dụng các framework được hỗ trợ.
* **Framework**: Chọn framework để triển khai model và version phù hợp. Trong hướng dẫn này, ta chọn Triton 24.12.
* **Model Source**: Chọn Network Volume chứa mô hình Triton của bạn. Với Triton, bạn cần đảm bảo model repository có format sau:
  * **Model Repository**: Chọn Network Volume chứa model Triton của bạn, bạn cần chuẩn bị [**model repository**](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/tutorials/Conceptual_Guide/Part_1-model_deployment/README.html#setting-up-the-model-repository) có cấu trúc như sau:
  * ```
    network-volume
    +-- model_repository
        |
        +-- resnet
            |
            +-- config.pbtxt
            +-- 1
                |
                +-- model.onnx
    ```
  * Hãy kiểm tra [Triton documentation for compatibility guidelines](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/user_guide/model_repository.html) để đảm bảo model của bạn tương thích và thực hiện các điều chỉnh cấu hình cần thiết nếu có.
* Nhấn nút **"Import"** để hoàn thành quá trình.
