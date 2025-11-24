={% tabs %}
{% tab title="Nâng cấp mới" %}

**Tháng MM, YYYY**

**Tháng MM, YYYY**

#### **VKS – Auto-scaling Enhancement**

Chúng tôi tự hào thông báo về những cải tiến đáng kể trong cơ chế auto-scaling của VKS (VNG Kubernetes Service). Bản nâng cấp này tập trung vào việc tối ưu hóa khả năng tự động điều chỉnh tài nguyên cho các VKS cluster, đảm bảo hiệu suất ổn định và khả năng phản hồi nhanh chóng trước mọi biến động về tải.

Với cơ chế auto-scaling mới, hệ thống VKS giờ đây có thể tự động mở rộng hoặc thu hẹp số lượng node trong cluster một cách thông minh hơn, dựa trên các chỉ số CPU và Memory được thu thập với độ chính xác cao hơn. Điều này giúp tối ưu hóa việc sử dụng tài nguyên, tránh tình trạng thừa hoặc thiếu hụt, đồng thời giảm thiểu chi phí vận hành. Đặc biệt, thời gian phản hồi của hệ thống khi thực hiện các tác vụ auto-scaling đã được rút ngắn đáng kể, chỉ còn 30 giây, đảm bảo ứng dụng của bạn luôn sẵn sàng phục vụ người dùng mà không bị gián đoạn.

Để hỗ trợ việc giám sát và quản lý hiệu quả hơn, cơ chế auto-scaling mới đã được tích hợp sâu rộng với vMonitor, cho phép người dùng theo dõi các metrics liên quan đến auto-scaling theo thời gian thực. Sự cải tiến này mang lại một giải pháp quản lý tài nguyên mạnh mẽ và linh hoạt hơn cho các ứng dụng container hóa trên VKS.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vks/autoscaling)

{% endtab %}

{% tab title="Tính năng mới" %}

**Tháng 11, 2024**

**Tháng 11, 2024**

#### **vServer – Live Migration**

VNG Cloud tự hào giới thiệu tính năng Live Migration cho dịch vụ vServer, mang đến khả năng di chuyển liền mạch các máy chủ ảo giữa các host vật lý mà không gây ra bất kỳ gián đoạn nào. Tính năng đột phá này đảm bảo vServer của bạn luôn hoạt động liên tục, ngay cả khi chúng tôi thực hiện các công việc bảo trì hạ tầng cần thiết.

Live Migration giúp các quản trị viên hệ thống dễ dàng thực hiện bảo trì, nâng cấp hoặc cân bằng tải trên các host vật lý mà không ảnh hưởng đến dịch vụ đang chạy của bạn. Điều này không chỉ tối ưu hóa hiệu suất và độ ổn định của hạ tầng VNG Cloud mà còn góp phần nâng cao cam kết uptime 99.9% cho các ứng dụng và dịch vụ quan trọng của khách hàng.

Với Live Migration, bạn có thể hoàn toàn yên tâm về tính sẵn sàng và hiệu suất của vServer, giảm thiểu rủi ro downtime và tối đa hóa trải nghiệm người dùng cuối.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/live-migration)

**Tháng 11, 2024**

#### **vDB-Kafka – Multi-tenancy Support**

VNG Cloud tự hào giới thiệu tính năng hỗ trợ đa người thuê (multi-tenancy) cho dịch vụ vDB-Kafka, mang đến khả năng cách ly tài nguyên mạnh mẽ và quản lý hiệu quả hơn. Với tính năng này, mỗi tenant (người thuê) sẽ được cấp phát một namespace riêng biệt, đảm bảo sự cô lập hoàn toàn về dữ liệu và tài nguyên, từ đó nâng cao tính bảo mật và ổn định cho từng môi trường làm việc.

Hệ thống multi-tenancy mới cho phép quản trị viên thiết lập và quản lý quota tài nguyên cụ thể cho mỗi tenant, bao gồm giới hạn về số lượng topic, dung lượng lưu trữ, và băng thông. Điều này giúp đảm bảo việc sử dụng tài nguyên công bằng (fair usage) giữa các người dùng, đồng thời ngăn chặn các sự cố do một tenant chiếm dụng quá nhiều tài nguyên.

Tính năng này cũng tích hợp khả năng quản lý tập trung thông qua VNG Cloud Portal, giúp các admin dễ dàng giám sát, cấu hình và điều chỉnh các thiết lập cho từng tenant một cách hiệu quả, tối ưu hóa vận hành và giảm thiểu chi phí quản lý.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vdb/kafka-multitenancy)

**Tháng 11, 2024**

#### **VKS – Multi-AZ Support**

VNG Kubernetes Service (VKS) nay đã được nâng cấp với khả năng hỗ trợ triển khai cluster trên nhiều Availability Zones (AZs). Tính năng này là một bước tiến quan trọng nhằm tăng cường khả năng chịu lỗi và đảm bảo tính sẵn sàng cao (high availability) cho các ứng dụng của bạn trên VNG Cloud. Với Multi-AZ Support, các thành phần của cluster VKS có thể được phân tán trên các vùng sẵn sàng khác nhau, giảm thiểu rủi ro khi một AZ gặp sự cố, từ đó nâng cao độ bền vững của hệ thống.

Người dùng giờ đây có thể dễ dàng cấu hình các node groups của mình để phân bổ đều trên nhiều AZ khác nhau. Điều này không chỉ giúp bảo vệ ứng dụng khỏi các sự cố cục bộ trong một AZ mà còn đảm bảo rằng các workload của bạn luôn có thể truy cập được và hoạt động liên tục. Khi một AZ gặp vấn đề, VKS sẽ tự động xử lý việc chuyển đổi sang các AZ khỏe mạnh khác, giúp duy trì hoạt động ổn định cho hệ thống mà không yêu cầu can thiệp thủ công, mang lại sự an tâm tuyệt đối cho các ứng dụng quan trọng.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vks/multi-az)

**Tháng [MM], [YYYY]**

**Tháng [MM], [YYYY]**

#### **vServer – Snapshot Scheduling**

VNG Cloud vui mừng thông báo ra mắt tính năng Snapshot Scheduling cho vServer, cho phép người dùng tự động hóa việc tạo các bản sao lưu (snapshot) của máy chủ ảo theo lịch trình định kỳ. Tính năng này được thiết kế để đơn giản hóa quy trình bảo vệ dữ liệu, đảm bảo rằng dữ liệu quan trọng của bạn luôn được sao lưu một cách nhất quán mà không cần can thiệp thủ công.

Với Snapshot Scheduling, bạn có thể dễ dàng thiết lập các lịch trình tạo snapshot hàng ngày, hàng tuần hoặc hàng tháng, phù hợp với nhu cầu vận hành và yêu cầu tuân thủ của doanh nghiệp. Ngoài ra, tính năng này còn cung cấp khả năng cấu hình chính sách lưu giữ (retention policy) linh hoạt. Người dùng có thể quy định số lượng snapshot tối đa được giữ lại, giúp tối ưu hóa chi phí lưu trữ và quản lý tài nguyên hiệu quả hơn.

Việc tự động hóa snapshot và quản lý vòng đời của chúng không chỉ nâng cao mức độ an toàn dữ liệu mà còn giảm thiểu rủi ro mất mát dữ liệu do lỗi hệ thống hoặc sự cố không mong muốn. Điều này giúp các quản trị viên hệ thống tập trung vào các tác vụ quan trọng khác, đồng thời duy trì khả năng phục hồi dữ liệu mạnh mẽ cho các ứng dụng và dịch vụ trên vServer.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/snapshot-schedule)

**Tháng [MM], [YYYY]**

#### **AI Stack – Rate Limiting**

VNG Cloud vui mừng thông báo về việc bổ sung tính năng Rate Limiting cho AI Gateway, một cải tiến quan trọng nhằm mang lại khả năng kiểm soát chi phí và quản lý tài nguyên hiệu quả hơn cho người dùng. Với tính năng này, quý khách có thể dễ dàng thiết lập giới hạn về số lượng yêu cầu (requests) được gửi đến các mô hình AI thông qua AI Gateway trong một khoảng thời gian cụ thể, như mỗi giây, mỗi phút hoặc mỗi giờ. Điều này giúp ngăn chặn việc sử dụng quá mức, bảo vệ hệ thống khỏi các hành vi lạm dụng và tối ưu hóa ngân sách vận hành.

Tính năng Rate Limiting được thiết kế với sự linh hoạt cao, cho phép người dùng cấu hình các quy tắc giới hạn riêng biệt và chi tiết. Quý khách có thể áp dụng các chính sách Rate Limiting khác nhau cho từng API key cụ thể hoặc thậm chí cho từng mô hình AI riêng lẻ mà bạn đang sử dụng. Khả năng tùy chỉnh này đảm bảo rằng bạn có thể điều chỉnh chính sách giới hạn tốc độ một cách chính xác để phù hợp với nhu cầu và mô hình tiêu thụ của từng ứng dụng, đảm bảo hiệu suất ổn định và phân bổ tài nguyên hợp lý.

Việc tích hợp Rate Limiting vào AI Gateway không chỉ giúp kiểm soát chi phí mà còn nâng cao độ ổn định và bảo mật cho các ứng dụng AI của bạn. Nó cung cấp một lớp bảo vệ bổ sung, đảm bảo rằng hệ thống không bị quá tải do lưu lượng truy cập đột biến và duy trì trải nghiệm người dùng mượt mà.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/ai-gateway/rate-limit)

**Tháng MM, YYYY**

**Tháng MM, YYYY**

#### **vServer – Hỗ trợ GPU Instance**

VNG Cloud hân hạnh thông báo vServer hiện đã hỗ trợ các instance với GPU NVIDIA A100 và H100 mạnh mẽ. Tính năng mới này được thiết kế đặc biệt để đáp ứng nhu cầu tính toán hiệu năng cao cho các tác vụ AI/ML chuyên sâu, từ huấn luyện mô hình phức tạp đến suy luận (inference) ở quy mô lớn.

Với sự tích hợp của các dòng GPU hàng đầu từ NVIDIA, người dùng có thể tận dụng sức mạnh xử lý song song vượt trội để tăng tốc đáng kể thời gian phát triển và triển khai các ứng dụng trí tuệ nhân tạo. Điều này mở ra khả năng xử lý các bộ dữ liệu khổng lồ và thực hiện các thuật toán học sâu phức tạp một cách hiệu quả hơn bao giờ hết, giúp các nhà khoa học dữ liệu và kỹ sư AI tối ưu hóa quy trình làm việc của mình.

Việc cung cấp các tùy chọn GPU Instance cao cấp này khẳng định cam kết của VNG Cloud trong việc mang đến hạ tầng điện toán đám mây tiên tiến, hỗ trợ khách hàng đạt được những đột phá trong lĩnh vực AI và Machine Learning.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/gpu-instances)

{% endtab %}

{% tab title="Sản phẩm/Dịch vụ mới" %}

{% endtab %}

{% endtabs %}