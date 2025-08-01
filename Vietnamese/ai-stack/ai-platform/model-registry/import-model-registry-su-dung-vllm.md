# Import Model Registry sử dụng vLLM

## Bước 1: Truy cập Model Registry

* Đăng nhập với VNG Cloud account của bạn và truy cập tới [Model Registry Dashboard](https://aiplatform.console.vngcloud.vn/registry)<mark style="color:$info;">.</mark>
* Tìm và nhấn vào nút "Import a model registry" (Nhập một model registry).

## Bước 2: Truy cập Model Registry

* **Region & Model registry name**: Chọn region và tên cụ thể cho model của bạn.
* **Container**: Chọn option Pre-built container để sử dụng các framework được hỗ trợ.
* **Framework**: Chọn framework để triển khai model và version phù hợp. Trong hướng dẫn này, ta chọn vLLM 0.7.2
* **Model Source**: Truy cập model được lưu trữ: từ network volume của bạn, AI Platform catalog, hoặc trực tiếp từ Hugging Face.
* **Model Repository**: Chọn Network Volume chứa model Triton của bạn, bạn cần chuẩn bị [**model repository**](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/tutorials/Conceptual_Guide/Part_1-model_deployment/README.html#setting-up-the-model-repository) có cấu trúc như sau:
* **Cấu hình vLLM (vLLM Settings):**
  * **Served model name:** Tên model được sử dụng trong API.\
    &#xNAN;_&#x4C;ưu ý:_ tên này cũng sẽ được dùng trong tag `model_name`
  * **Max number of sequences:** Số lượng sequence tối đa mỗi iteration. Mặc định: **256**.
  * **Max Context Length:** Chiều dài context tối đa của model. Nếu không chỉ định, hệ thống sẽ tự động lấy từ model config.
  * **Nếu bật hỗ trợ Tool Call:**
    * Chọn loại tool call parser bạn cần: hermes, mistral...
* Nhấn nút **"Import"** để hoàn thành quá trình.
