# Import Model Registry với custom container

## Bước 1: Truy cập Model Registry

* Đăng nhập với VNG Cloud account của bạn và truy cập tới Model Registry Dashboard.
* Tìm và nhấn vào nút "Import a model registry" (Nhập một model registry).

## Bước 2: Import Model Registry

* **Region & Model registry name**: Chọn region và tên cụ thể cho model của bạn.
* Chọn **“Custom container”** trong Container Section.
  * **Custom image URI**:
    * Cung cấp URL của custom container image của bạn, được lưu trữ trong container registry.\
      AI Platform sẽ sử dụng URL này để tải image trong quá trình trainning.
  * **Cung cấp Credentials**:
    * Nếu container image của bạn yêu cầu xác thực để truy cập, hãy cung cấp các thông tin cần thiết như (**username và password hoặc access token**).
    * Đảm bảo các credential được lưu trữ một cách bảo mật và cung cấp đúng định dạng yêu cầu.
  * **Cấu hình Ports và Health Checks**:
    * Định nghĩa port truy cập mà các predictions requests sẽ được gửi đến
    * Cấu hình port metric để theo dõi các metric hiệu suất của model.
    * Chỉ định port và path để theo dõi health status của prediction service.
