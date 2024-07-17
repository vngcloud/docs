# Transcoding

**Transcoding**, hay còn gọi là **chuyển mã**, là quá trình chuyển đổi một tệp tin media từ định dạng này sang định dạng khác. Trong CDN, transcoding được sử dụng để tối ưu hóa nội dung video cho nhiều thiết bị và điều kiện mạng khác nhau.

Quá trình transcoding có thể bao gồm:

* **Chuyển đổi định dạng video:** Ví dụ: từ H.264 sang H.265, MP4 sang WebM, v.v.
* **Chuyển đổi độ phân giải:** Ví dụ: từ 1080p sang 720p, 480p, v.v.
* **Chuyển đổi tỷ lệ khung hình:** Ví dụ: từ 16:9 sang 4:3, v.v.
* **Điều chỉnh bitrate:** Ví dụ: giảm bitrate để tiết kiệm băng thông cho người dùng có kết nối mạng chậm.
* **Thêm phụ đề:** Thêm phụ đề cho người khiếm thính hoặc người học ngôn ngữ mới.

Do đó, transcoding là một tính năng quan trọng của CDN giúp cải thiện trải nghiệm người dùng, giảm tải cho server gốc, tiết kiệm băng thông và mở rộng phạm vi tiếp cận cho nội dung video.

***

### Các usecase cơ bản:

* **Truyền phát video theo yêu cầu (VoD):** Khi người dùng yêu cầu xem một video VoD, CDN sẽ chọn phiên bản video phù hợp nhất với thiết bị và mạng của họ.
* **Truyền phát video trực tiếp:** Transcoding được sử dụng để chuyển đổi video trực tiếp thành nhiều định dạng khác nhau để có thể truyền phát đến nhiều người dùng cùng lúc.
* **Phát sóng OTT:** Transcoding được sử dụng để cung cấp nội dung video cho các dịch vụ OTT (Over-the-top) như Netflix, Hulu và Amazon Prime Video.
* **Livestreaming trên mạng xã hội:** Transcoding được sử dụng để chuyển đổi video livestreaming thành nhiều định dạng khác nhau để có thể phát trên các mạng xã hội như Facebook, YouTube,....
