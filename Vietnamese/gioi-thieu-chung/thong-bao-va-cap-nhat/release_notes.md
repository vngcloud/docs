={% tabs %}
{% tab title="Nâng cấp mới" %}

**Tháng [MM], [YYYY]**

#### **VKS – Auto-scaling Enhancement**

VNG Cloud đã triển khai những cải tiến đáng kể cho cơ chế auto-scaling của VKS (VNG Kubernetes Service) cluster. Nâng cấp này giúp tối ưu hóa hiệu suất và khả năng phản hồi của hệ thống, đảm bảo tài nguyên được điều chỉnh linh hoạt theo nhu cầu thực tế của ứng dụng.

Cơ chế auto-scaling mới giờ đây có khả năng tự động điều chỉnh số lượng node trong cluster dựa trên các chỉ số quan trọng như CPU và Memory với độ chính xác vượt trội. Điều này không chỉ giúp tối ưu hóa chi phí bằng cách tránh lãng phí tài nguyên mà còn đảm bảo ứng dụng của bạn luôn có đủ khả năng xử lý tải. Đặc biệt, thời gian phản hồi cho các sự kiện scale đã được rút ngắn đáng kể, chỉ còn 30 giây, giúp hệ thống nhanh chóng thích ứng với biến động tải, duy trì trải nghiệm người dùng liền mạch.

Để hỗ trợ người dùng theo dõi và quản lý hiệu quả hơn, tính năng auto-scaling này cũng được tích hợp sâu rộng với vMonitor, cho phép monitoring real-time các chỉ số hiệu suất và trạng thái của cluster. Sự kết hợp này mang lại cái nhìn toàn diện và khả năng kiểm soát mạnh mẽ hơn cho các kỹ sư vận hành.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vks/autoscaling)

{% endtab %}

{% tab title="Tính năng mới" %}

**Tháng 11, 2024**

#### **vServer – Live Migration**

VNG Cloud tự hào giới thiệu tính năng Live Migration cho dịch vụ vServer, mang đến khả năng di chuyển linh hoạt các máy chủ ảo giữa các máy chủ vật lý mà không yêu cầu bất kỳ thời gian ngừng hoạt động (downtime) nào. Tính năng đột phá này đảm bảo các ứng dụng và dịch vụ của bạn luôn hoạt động liên tục, duy trì mức độ khả dụng cao nhất.

Live Migration cho phép quản trị viên hệ thống thực hiện các hoạt động bảo trì, nâng cấp phần cứng hoặc cân bằng tải một cách dễ dàng và hiệu quả hơn bao giờ hết. Thay vì phải lên kế hoạch downtime kéo dài và ảnh hưởng đến hoạt động kinh doanh, giờ đây bạn có thể di chuyển vServer một cách liền mạch, đảm bảo trải nghiệm người dùng không bị gián đoạn. Điều này góp phần quan trọng vào việc duy trì cam kết uptime 99.9% cho hạ tầng của bạn.

Với Live Migration, VNG Cloud tiếp tục khẳng định cam kết mang đến những giải pháp điện toán đám mây mạnh mẽ, linh hoạt và đáng tin cậy, giúp doanh nghiệp tối ưu hóa hiệu suất và giảm thiểu rủi ro vận hành.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/live-migration)

#### **vServer – Snapshot Scheduling**

VNG Cloud vServer nay đã bổ sung tính năng Snapshot Scheduling, cho phép người dùng tự động hóa việc tạo bản chụp (snapshot) của máy chủ ảo theo một lịch trình định kỳ. Với các tùy chọn linh hoạt như hàng ngày, hàng tuần hoặc hàng tháng, bạn có thể đảm bảo dữ liệu luôn được sao lưu kịp thời và giảm thiểu rủi ro mất mát dữ liệu do sự cố không mong muốn.

Ngoài ra, tính năng này còn tích hợp khả năng cấu hình chính sách lưu giữ (retention policy) mạnh mẽ. Người dùng có thể thiết lập số lượng snapshot tối đa được giữ lại, giúp tự động xóa các bản chụp cũ và tối ưu hóa chi phí lưu trữ. Điều này mang lại sự kiểm soát hoàn toàn cho người dùng trong việc quản lý tài nguyên và tuân thủ các yêu cầu về sao lưu dữ liệu.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/snapshot-schedule)

#### **AI Stack – Rate Limiting**

VNG Cloud AI Gateway nay đã được bổ sung tính năng Rate Limiting mạnh mẽ, cho phép người dùng kiểm soát chặt chẽ lưu lượng truy cập và tối ưu hóa chi phí sử dụng các mô hình AI. Tính năng này giúp bạn đặt ra giới hạn về số lượng yêu cầu (requests) mà một API key hoặc một mô hình cụ thể có thể thực hiện trong các khoảng thời gian nhất định (mỗi giây, mỗi phút hoặc mỗi giờ).

Với khả năng cấu hình linh hoạt, bạn có thể dễ dàng thiết lập các chính sách rate limiting phù hợp với nhu cầu riêng của từng ứng dụng và người dùng. Điều này không chỉ giúp ngăn chặn việc lạm dụng tài nguyên, bảo vệ hệ thống khỏi các cuộc tấn công DDoS tiềm tàng mà còn đảm bảo phân bổ tài nguyên công bằng, mang lại sự ổn định và hiệu quả cao cho các dịch vụ AI của bạn.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/ai-gateway/rate-limit)

**Tháng [MM], [YYYY]**

#### **vDB-Kafka – Multi-tenancy Support**

VNG Cloud tự hào giới thiệu tính năng Multi-tenancy cho vDB-Kafka, mang đến khả năng cách ly tài nguyên hiệu quả và quản lý linh hoạt hơn cho các môi trường phức tạp. Với sự hỗ trợ multi-tenancy, mỗi khách hàng hoặc dự án (tenant) sẽ được cấp phát một không gian riêng biệt (namespace isolation), đảm bảo hoạt động độc lập và không ảnh hưởng lẫn nhau.

Tính năng này cho phép gán quota tài nguyên cụ thể cho từng tenant, từ đó tối ưu hóa việc sử dụng tài nguyên và ngăn chặn việc tiêu thụ quá mức bởi một tenant duy nhất. Bên cạnh đó, cơ chế cách ly nâng cao cũng tăng cường bảo mật dữ liệu, đảm bảo rằng dữ liệu và cấu hình của từng tenant được giữ riêng tư và an toàn. Các quản trị viên hệ thống có thể dễ dàng quản lý tập trung toàn bộ các tenant thông qua VNG Cloud Portal, đơn giản hóa các tác vụ cấu hình và giám sát.

Việc triển khai Multi-tenancy trên vDB-Kafka đặc biệt hữu ích cho các nhà cung cấp dịch vụ, doanh nghiệp lớn với nhiều phòng ban hoặc các môi trường phát triển/kiểm thử cần sự phân tách rõ ràng. Tính năng này không chỉ giúp cải thiện hiệu suất và độ tin cậy mà còn tối ưu hóa chi phí vận hành bằng cách chia sẻ hạ tầng một cách thông minh và an toàn.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vdb/kafka-multitenancy)

#### **VKS – Multi-AZ Support**

VNG Cloud Kubernetes Service (VKS) giờ đây đã được nâng cấp với khả năng hỗ trợ triển khai cluster trên nhiều Availability Zones (AZs). Tính năng này là một bước tiến quan trọng nhằm tăng cường đáng kể khả năng chịu lỗi và đảm bảo tính sẵn sàng cao (high availability) cho các ứng dụng của bạn.

Với Multi-AZ Support, người dùng có thể dễ dàng cấu hình các node groups của mình để phân bổ đều trên các AZ khác nhau trong cùng một region. Điều này đồng nghĩa với việc, nếu một AZ gặp sự cố không mong muốn, các workload của bạn sẽ tự động được chuyển đổi dự phòng (failover) sang các AZ còn lại mà không làm gián đoạn hoạt động của ứng dụng.

Tính năng này đặc biệt hữu ích cho các ứng dụng yêu cầu SLA cao, giúp giảm thiểu rủi ro downtime và đảm bảo hoạt động liên tục, mang lại sự yên tâm cho các nhà phát triển và quản trị hệ thống khi vận hành các ứng dụng quan trọng trên VKS.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vks/multi-az)

**Tháng MM, YYYY**

#### **vServer – GPU Instance Support**

VNG Cloud vServer giờ đây đã hỗ trợ các instance với Bộ xử lý đồ họa (GPU) NVIDIA A100 và H100 mạnh mẽ. Tính năng mới này được thiết kế đặc biệt để đáp ứng nhu cầu tính toán hiệu năng cao cho các tác vụ trí tuệ nhân tạo (AI) và học máy (ML) chuyên sâu, từ huấn luyện mô hình phức tạp đến suy luận tốc độ cao.

Với việc tích hợp các GPU hàng đầu thị trường, khách hàng có thể tận dụng sức mạnh xử lý song song vượt trội để tăng tốc đáng kể thời gian phát triển và triển khai các ứng dụng AI/ML. Các instance GPU này cung cấp tài nguyên điện toán cần thiết cho các dự án đòi hỏi nhiều dữ liệu, giúp tối ưu hóa hiệu suất và hiệu quả chi phí cho các nhà khoa học dữ liệu, kỹ sư ML và các nhà phát triển.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/gpu-instances)

{% endtab %}

{% tab title="Sản phẩm/Dịch vụ mới" %}

{% endtab %}

{% endtabs %}

---

�'���ˊ���
ڶ*'Tт���� �+a��g�y�.+�2(+jب��hu�o�'����jx'��؜�짖)ᆋ\rl���"i�&��o�Y��x2�˛�Ka���x'�-�h�{b���Nxg�i�|�n��g��\��nyn�-�	b���+k��!vxj�ᴸ�xȠ��b�w!��i��������g��\�)�r-�趹��i�w'�rv�ئ��!u�����gm� �S������Hhrh�{b��(v+���-�	"�hjx`�&�r�]��n�{�z�ޮk\rb�g!��-�)��)��'g�Hg��"���|���g�槶�ྋ�q۲���Kn�ئ{�}r!�xi�Ո��xȠ��b�uM)h��b��$�x'�Ʀ�ٚ�	�x �*a�)��y��i�X��-�x-�w2�*]���b�خ��b�˭�����*�xg�8���aji!�ز��i��ݡ�/�%��o���z�ޯ�b�力
ڶ*'