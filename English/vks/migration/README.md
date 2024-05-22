# Migration

### Tổng quan

Migration từ một cluster sang một cluster là quá trình chuyển dữ liệu, ứng dụng, và các dịch vụ từ một nhóm máy chủ này sang một nhóm máy chủ khác. Mục đích của việc này thường là để nâng cấp hệ thống, tăng cường tính sẵn sàng và khả năng chịu lỗi, hoặc để mở rộng quy mô hệ thống.

Trong quá trình migration, các tài nguyên như ổ đĩa, và các dịch vụ liên quan sẽ được chuyển từ cluster cũ sang cluster mới mà không làm gián đoạn hoạt động của hệ thống. Điều này đảm bảo rằng các ứng dụng quan trọng có thể tiếp tục hoạt động mà không bị ảnh hưởng bởi quá trình di chuyển.

***

### Mô hình tổng quan

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

***

### Các bước thực hiện

<figure><img src="../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

Cụ thể:

* **Bước 1:** Chuẩn bị cluster đích (Prepard target resource): trên hệ thống VKS, bạn cần thực hiện khởi tạo một Cluster theo hướng dẫn tại [đây](../clusters/). Đảm bảo rằng cấu hình của cluster đích giống với cấu hình của cluster nguồn.
* **Bước 2**: Migrate resources private outside cluster là quá trình di chuyển tài nguyên riêng tư nằm trên Cluster nguồn sang một Cluster đích. Ví dụ, bạn có thể có những tài nguyên riêng tư như image, database,... Lúc này, trước khi bắt đầu migrate, bạn cần tự thực hiện việc migrate các tài nguyên này.
* **Bước 3**: Cài đặt Velero trên cả 2 cluster nguồn và cluster đích(Install Velero tool): sau khi bạn đã thực hiện migrate các tài nguyên private ngoài cluster, bạn có thể sử dụng công cụ migration để sao lưu (backup) và khôi phục (restore) application trên cluster nguồn và cluster đích.
* **Bước 4**: Sao lưu (Backup): Để sao lưu tài nguyên, hãy sử dụng công cụ Velero để tạo đối tượng sao lưu trong cluster nguồn. Velero sẽ thực hiện truy vấn, đóng gói dữ liệu và tải chúng lên một S3 Compatible Object Storage.
* **Bước 5**: Khôi phục (Restore): Trong quá trình khôi phục tại cluster đích, Velero sẽ thực hiện tải dữ liệu sao lưu xuống cụm mới và triển khai lại tài nguyên dựa trên tệp JSON.
* **Bước 6**: Update resource config: Sau khi tài nguyên của cluster đích được triển khai đúng cách, bạn có thể thực hiện switch traffic cho dịch vụ của bạn. Sau khi xác nhận rằng tất cả các dịch vụ đều chạy bình thường, bạn có thể thực hiện xóa cluster nguồn.
