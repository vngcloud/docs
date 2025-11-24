=## VSERVER - LIVE MIGRATION

Chúng tôi hân hạnh giới thiệu tính năng Live Migration cho vServer, một cải tiến quan trọng cho phép bạn di chuyển các máy chủ ảo (vServer) giữa các host vật lý mà không cần bất kỳ thời gian ngừng hoạt động (downtime) nào. Điều này đảm bảo các ứng dụng và dịch vụ của bạn luôn khả dụng và hoạt động liên tục, mang lại trải nghiệm liền mạch cho người dùng cuối.

Với Live Migration, việc quản lý và bảo trì hạ tầng của bạn trở nên linh hoạt hơn bao giờ hết. Các quản trị viên hệ thống có thể thực hiện các tác vụ như nâng cấp phần cứng, vá lỗi bảo mật hoặc tối ưu hóa tài nguyên giữa các host mà không làm gián đoạn dịch vụ. Tính năng này giúp nâng cao đáng kể hiệu quả vận hành và giảm thiểu rủi ro liên quan đến các hoạt động bảo trì, đồng thời củng cố cam kết của VNG Cloud về mức uptime 99.9% cho vServer.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/live-migration)

---

## VKS - AUTO-SCALING ENHANCEMENT

VNG Cloud trân trọng thông báo về những cải tiến đáng kể trong cơ chế Auto-scaling dành cho các cluster VKS (VNG Kubernetes Service). Nâng cấp này được thiết kế để tối ưu hóa việc quản lý tài nguyên và đảm bảo hiệu suất ổn định cho các ứng dụng của bạn, đặc biệt trong môi trường có tải trọng biến động. Giờ đây, các cluster VKS có thể tự động điều chỉnh tài nguyên một cách thông minh và hiệu quả hơn bao giờ hết.

Với cơ chế auto-scaling được cải thiện, hệ thống VKS sẽ tự động mở rộng hoặc thu hẹp số lượng node dựa trên các chỉ số CPU và Memory với độ chính xác cao hơn đáng kể. Điều này giúp ngăn chặn tình trạng thiếu hụt tài nguyên trong giờ cao điểm và tránh lãng phí khi tải thấp, đảm bảo ứng dụng của bạn luôn có đủ tài nguyên cần thiết. Đặc biệt, thời gian phản hồi của cơ chế auto-scaling đã được rút ngắn ấn tượng xuống chỉ còn 30 giây, giúp các ứng dụng nhanh chóng thích nghi với sự thay đổi của lưu lượng truy cập và duy trì trải nghiệm người dùng liền mạch.

Để tăng cường khả năng giám sát và quản lý, tính năng auto-scaling mới cũng được tích hợp sâu rộng với vMonitor. Sự kết hợp này mang lại khả năng theo dõi hiệu suất cluster theo thời gian thực, cung cấp cho bạn cái nhìn toàn diện về hoạt động của hệ thống và đưa ra các quyết định điều chỉnh tối ưu. Những cải tiến này không chỉ giúp giảm chi phí vận hành mà còn nâng cao độ tin cậy và khả năng mở rộng của các ứng dụng chạy trên VKS.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vks/autoscaling)

---

undefined

---

## VKS - MULTI-AZ SUPPORT

VKS (VNG Kubernetes Service) tự hào ra mắt tính năng Multi-AZ Support, mang đến khả năng triển khai các cụm Kubernetes với độ sẵn sàng cao và khả năng chịu lỗi vượt trội. Với tính năng này, người dùng giờ đây có thể phân bổ các thành phần của cụm VKS trên nhiều Availability Zones (AZs) khác nhau trong cùng một khu vực, giảm thiểu rủi ro gián đoạn dịch vụ do sự cố cục bộ tại một AZ.

Cụ thể, Multi-AZ Support cho phép bạn cấu hình các node group và các tài nguyên khác của cụm VKS để trải đều trên các AZ đã chọn. Trong trường hợp một AZ gặp sự cố, hệ thống sẽ tự động chuyển đổi sang các AZ còn lại, đảm bảo ứng dụng của bạn vẫn hoạt động liên tục mà không bị ảnh hưởng. Điều này giúp tăng cường đáng kể độ bền vững và khả năng phục hồi của hạ tầng Kubernetes, đáp ứng các yêu cầu khắt khe nhất về uptime cho các ứng dụng mission-critical.

Việc triển khai Multi-AZ trên VKS rất đơn giản, cho phép các nhà phát triển và quản trị viên hệ thống dễ dàng thiết kế kiến trúc có khả năng chịu lỗi cao ngay từ đầu. Hãy khám phá Multi-AZ Support để tối ưu hóa độ tin cậy và hiệu suất cho các ứng dụng container hóa của bạn trên VKS.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vks/multi-az)

---

---

## VSERVER - GPU INSTANCE SUPPORT

VNG Cloud tự hào ra mắt tính năng hỗ trợ GPU Instance trên dịch vụ vServer, mang đến sức mạnh xử lý vượt trội cho các tác vụ AI/ML chuyên sâu. Với sự tích hợp các dòng GPU NVIDIA A100 và H100 hàng đầu thị trường, khách hàng giờ đây có thể triển khai các ứng dụng yêu cầu hiệu năng cao một cách dễ dàng và hiệu quả.

Tính năng này được thiết kế đặc biệt để đáp ứng nhu cầu khắt khe của các quy trình huấn luyện mô hình (training) và suy luận (inference) trong lĩnh vực trí tuệ nhân tạo và học máy. Các GPU mạnh mẽ giúp tăng tốc đáng kể thời gian xử lý dữ liệu lớn, phức tạp, từ đó rút ngắn chu kỳ phát triển và triển khai các giải pháp AI tiên tiến.

Việc cung cấp GPU Instance trên vServer không chỉ tối ưu hóa hiệu suất mà còn giúp các nhà phát triển và nhà khoa học dữ liệu tập trung hơn vào việc sáng tạo và đổi mới, mà không cần lo lắng về hạ tầng phần cứng. Đây là bước tiến quan trọng, khẳng định cam kết của VNG Cloud trong việc hỗ trợ cộng đồng AI/ML tại Việt Nam.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/gpu-instances)

---

undefined

---

## VSERVER - SNAPSHOT SCHEDULING

VNG Cloud vui mừng thông báo ra mắt tính năng Snapshot Scheduling cho vServer, mang đến khả năng tự động hóa việc tạo snapshot cho các máy chủ ảo của bạn. Tính năng này cho phép người dùng thiết lập lịch trình chụp nhanh định kỳ theo ngày, tuần hoặc tháng, đảm bảo dữ liệu luôn được sao lưu một cách nhất quán mà không cần can thiệp thủ công.

Với Snapshot Scheduling, bạn không chỉ có thể lên lịch tạo snapshot mà còn có toàn quyền kiểm soát chính sách lưu giữ (retention policy). Điều này cho phép bạn định cấu hình số lượng snapshot tối đa muốn giữ lại và thời gian lưu trữ, giúp tối ưu hóa chi phí lưu trữ một cách hiệu quả. Các snapshot cũ hơn sẽ tự động bị xóa theo quy tắc đã định, giải phóng không gian và giảm gánh nặng quản lý.

Tính năng này được thiết kế để đơn giản hóa quy trình bảo vệ dữ liệu, giảm thiểu rủi ro mất mát dữ liệu do lỗi người dùng hoặc sự cố hệ thống, đồng thời giải phóng thời gian cho đội ngũ vận hành để tập trung vào các tác vụ quan trọng hơn. Nâng cao độ tin cậy và khả năng phục hồi cho hạ tầng vServer của bạn.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/snapshot-schedule)

---

