# Backup

vBackup là dịch vụ sao lưu toàn phần của VNG Cloud giúp bảo vệ dữ liệu của bạn, cho phép tự động hoá sao lưu ổ đĩa trên máy chủ ảo và lưu trữ chúng trên môi trường điện toán đám mây. Khi sử dụng vBackup, bạn có thể định cấu hình tập trung các chính sách sao lưu và giám sát hoạt động sao lưu cho tài nguyên VNG Cloud bao gồm việc tạo các bản sao lưu tự động hàng ngày, hàng tuần và hàng tháng. Mỗi bản sao lưu là một ảnh chụp nhanh dựa trên tệp đầy đủ về ổ đĩa của bạn được thực hiện trong khung thời gian đã lên lịch ưa thích dựa trên các chính sách của bạn trong khi máy chủ ảo vẫn đang chạy. Điều này có nghĩa là dịch vụ Sao lưu không gây gián đoạn và cung cấp cho bạn một số tùy chọn khôi phục hoàn chỉnh. vBackup tự động hóa và hợp nhất các tác vụ sao lưu từng dịch vụ đã thực hiện trước đó, loại bỏ nhu cầu tạo tập lệnh tùy chỉnh và quy trình thủ công tốn nhiều thời gian, cho phép bạn đáp ứng các yêu cầu tuân thủ về sao lưu theo quy định và kinh doanh của mình.

### **Chức năng chính** <a href="#backup-chucnangchinh" id="backup-chucnangchinh"></a>

Dịch vụ vBackup cung cấp cho bạn các chức năng chính bao gồm:

* **Backup:** Tạo bản sao lưu cho các ổ đĩa trên máy chủ ảo của bạn
* **Restore:** Thực hiện khôi phục từ file backup của máy chủ ảo lên một máy chủ mới tại thời điểm tạo file backup

### **Phân bố thành phần** <a href="#backup-phanbothanhphan" id="backup-phanbothanhphan"></a>

<figure><img src="https://docs.vngcloud.vn/download/attachments/49649794/image2023-3-16_17-9-40.png?version=1&#x26;modificationDate=1678961454000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### **Diễn giải các thành phần:** <a href="#backup-diengiaicacthanhphan" id="backup-diengiaicacthanhphan"></a>

* Portal: nơi tiếp nhận, quản lý thời điểm cần thực thi backup/restore cùng như vòng đời của các bản sao lưu theo quy ước mà người dùng cung cấp trong đó đi theo logic sau
* Đối tượng khai báo sao lưu là instance vServer (đơn lẻ) nhưng có thể có hoặc không bao gồm toàn bộ Volumes đang attach trên instance. Lượng volumes backup tại một thời điểm có thể lớn hơn 1 cần đảm bảo snapshot gần như đồng thời
* vBackup service: là service backend chịu trách nhiệm tiếp nhận hai hành động chính là backup hoặc restore từ Portal song song đó trách nhiệm quản lý tối ưu không gian lưu trữ của vòng đời một instance cùng volumes đi kèm. Xa hơn sẽ trách nhiệm thực thi các task tích hợp gần nhất là ra vStorage như một “Backup Location” hỗ trợ khởi điểm
* vSnapshot service: là service với ý tưởng quản lý các bản snapshot nhằm tập trung vai trò này tại một điểm, xa hơn các thao tác trên snapshot sẽ có thể cover toàn bộ snapshot mà hệ thống tạo ra cho đa mục đích (Ex vSnapshot có thể rollback snapshot do vbackup sinh ra nhưng vẫn được vSnapshot quản lý)
* Message Queue: dùng rabbitmq như channel trao đổi message không quá nhiều giải thích đặc thù tại thành phần này, nhưng thành phần chủ yếu phục vụ message giao tiếp giữa các api nếu có, không dùng cho mô hình distributed backup jobs.
* Backup Worker: là các Edge service của vBackup được phân bố ở các Region chịu trách nhiệm thực thi các lệnh Export/Import từ Storage ra một Cephfs cùng các tác vụ thao tác dữ liệu khác trong tương lai (Ex. compress, encrypt, zip, generate download archive, migrate amazon…)
* vStorage: backup location sẽ support trong giai đoạn đầu sau đó có thể là các options on-cloud hoặc on-premise location khác.

***

#### Chủ đề <a href="#backup-chude" id="backup-chude"></a>

* [Tạo bản sao lưu cho máy chủ ảo theo bộ lịch Policy](tao-ban-sao-luu-cho-may-chu-ao-theo-bo-lich-policy.md)
* [Tạo bản sao lưu ngay lập tức (Backup Now) cho bản Backup Server](tao-ban-sao-luu-ngay-lap-tuc-backup-now.md)
* [Thay đổi chính sách sao lưu](thay-doi-chinh-sach-sao-luu.md)
* [Khôi phục bản sao lưu](khoi-phuc-ban-sao-luu.md)
* [Xóa bản sao lưu](xoa-ban-sao-luu.md)
* [Chính sách sao lưu](chinh-sach-sao-luu/)

\
