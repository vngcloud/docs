# Ứng dụng gateway thay thế Fileserver

Một trong những ứng dụng phổ biến của storage gateway là sử dụng làm nơi lưu trữ quản lý file, thay thế cho giải pháp Fileserver truyền thống. Theo đó gateway được dựng tại 1 server tại vngcloud hoặc on-premise của bạn nhằm đảm nhiệm vai trò trung gian quản lý phân quyền, chia sẻ dữ liệu theo các cơ chế có sẵn như SMB/NFS. Dữ liệu do user upload sẽ được cache tại gateway và đồng thời ghi vào vStorage để lưu trữ lâu dài, nhờ tận dụng cache nên việc latency khi truy cập dữ liệu có thể xem là tương đồng với 1 fileserver truyền thống.

Các dữ liệu của bạn sẽ được mã hóa AES-256 và lưu chủ yếu tại vStorage, nhờ vậy dữ liệu được bảo vệ an toàn theo các cơ chế bảo mật của vStorage như Replication 3 bản trên 3 server vật lý khác nhau, Tính năng lưu phiên bản bảo vệ dữ liệu bị mất do các lỗi upload đè do trùng tên hoặc xóa nhầm. Đặc biệt khi dữ liệu của bạn đủ lớn, việc sử dụng gateway và vStorage sẽ tiết kiệm chi phí lưu trữ đáng kể nhờ chi phí thấp của vStorage so với việc lưu trên một ổ đĩa SSD thông thưởng.

**Mô hình**

<figure><img src="../../../../../.gitbook/assets/image (566).png" alt=""><figcaption></figcaption></figure>

**Tính năng**

* Hỗ trợ NFS, SMB.
* Phân quyền truy cập read/write trên từng folder theo cơ chế SMB/NFS.
* Hỗ trợ encryption AES-256 tại gateway trước khi truyền tải dữ liệu sang vStorage
* Số lượng user cấp quyền không giới hạn.
* Hỗ trợ cơ chế HA gateway theo cơ chế Active-standby.

***

**Lợi ích:**

* Sử dụng cache của gateway giúp truy cập dữ liệu nhanh chóng.
* Quá trình đồng bộ dữ liệu từ gateway sang storage hoàn toàn tự động.
* Việc đồng bộ thực hiện trong mạng nội bộ VNG, không gây ảnh hưởng đến internet chung của KH.
* Dữ liệu lưu trữ trên object storage giúp giảm chi phí đáng kể.
* Khi nhu cầu tăng đột biến, bạn có thể scale dung lượng lưu trữ của vStorage trên portal trong 5phút và hoàn toàn không có downtime dịch vụ.
* Có thể triển khai on-premise.

***

**Tips:**

* Nên đặt gateway tại on-premise để tối ưu về chi phí, tốc độ truy cập, và trải nghiệm tốt nhất.
* Cấu hình tối thiểu cho gateway nên từ 4 CPU x 8 G Ram x 100 SSD.
* SSD được dùng để cache dữ liệu khi người dùng upload. Tối thiểu SSD phải đủ để chứa dữ liệu của 1 lần upload từ người dùng.
* Tùy theo lượng user truy cập (CCU) cùng lúc mà lượng CPU nên được cấu hình phù hợp , 1 CPU có thể đảm nhiệm từ 3-5 CCU.
* Để trải nghiệm tốt nhất BW gateway nên thiết lập ở ngưỡng 1Gbps.
* Tối đa 1 gateway chỉ nên đảm nhiệm 250 CCU (upload / download đồng thời) để có trải nghiệm tốt nhất.
* Gateway trên cloud chỉ nên phục vụ nhu cầu CCU <20.
* Ngoài ra bạn có thể tăng trải nghiệm người dùng bằng cách thiết lập thêm SSD để gateway có thể cache nhiều hơn.

Để khởi tạo gateway và dùng thử gateway bạn có thể xem chi tiết tại đây: [Storage gateway](./).
