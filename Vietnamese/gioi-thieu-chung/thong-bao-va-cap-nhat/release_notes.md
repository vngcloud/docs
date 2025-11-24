={% tabs %}
{% tab title="Nâng cấp mới" %}

**Tháng 11, 2024**

#### **VKS – Auto-scaling Enhancement**

VNG Cloud đã triển khai cải tiến đáng kể cho cơ chế auto-scaling của các VKS cluster, mang lại hiệu suất và độ tin cậy cao hơn cho các ứng dụng containerized. Hệ thống giờ đây có khả năng tự động điều chỉnh số lượng node trong cluster dựa trên các chỉ số CPU và Memory với độ chính xác được nâng cao, đảm bảo tài nguyên luôn được tối ưu theo nhu cầu thực tế của workload.

Với bản nâng cấp này, thời gian phản hồi của cơ chế auto-scaling đã được rút ngắn đáng kể, chỉ còn 30 giây, giúp ứng dụng của bạn duy trì hiệu suất ổn định ngay cả trong các tình huống tải tăng đột biến. Sự tích hợp chặt chẽ với vMonitor cho phép giám sát real-time các chỉ số tài nguyên, cung cấp cái nhìn toàn diện và chính xác để đưa ra quyết định scaling tối ưu. Điều này không chỉ giúp tối ưu chi phí vận hành mà còn nâng cao trải nghiệm người dùng cuối.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vks/autoscaling)

{% endtab %}

{% tab title="Tính năng mới" %}

**Tháng 11, 2024**

#### **vServer – Live Migration**

VNG Cloud tự hào giới thiệu tính năng Live Migration cho dịch vụ vServer, mang đến khả năng di chuyển liền mạch các máy chủ ảo giữa các máy chủ vật lý mà không gây ra bất kỳ gián đoạn nào cho hoạt động của bạn. Tính năng đột phá này cho phép các quản trị viên hệ thống thực hiện bảo trì hạ tầng, nâng cấp phần cứng hoặc cân bằng tải một cách linh hoạt mà không cần phải tắt máy chủ hay chịu bất kỳ downtime nào.

Với Live Migration, VNG Cloud cam kết đảm bảo mức độ khả dụng dịch vụ (uptime) lên đến 99.9%, giúp doanh nghiệp duy trì hoạt động liên tục và tối ưu hóa hiệu suất. Điều này đặc biệt quan trọng đối với các ứng dụng và dịch vụ yêu cầu tính sẵn sàng cao, nơi mỗi phút downtime đều có thể gây ra thiệt hại đáng kể.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/live-migration)

#### **vServer – Snapshot Scheduling**

VNG Cloud xin trân trọng giới thiệu tính năng Snapshot Scheduling cho dịch vụ vServer, mang đến khả năng tự động hóa việc quản lý backup dữ liệu một cách mạnh mẽ và linh hoạt. Với tính năng này, người dùng có thể dễ dàng thiết lập lịch trình tạo snapshot định kỳ cho các vServer của mình theo các chu kỳ Daily, Weekly hoặc Monthly, đảm bảo dữ liệu luôn được bảo vệ mà không cần can thiệp thủ công.

Bên cạnh đó, Snapshot Scheduling còn cho phép người dùng cấu hình chính sách lưu giữ (retention policy) một cách chi tiết. Điều này giúp tối ưu hóa chi phí lưu trữ bằng cách tự động xóa các snapshot cũ không còn cần thiết, đồng thời vẫn duy trì các điểm khôi phục quan trọng theo quy định. Tính năng này đặc biệt hữu ích cho các môi trường yêu cầu tuân thủ quy định về sao lưu dữ liệu hoặc cần quản lý tài nguyên hiệu quả.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/snapshot-schedule)

#### vDB-Kafka – Multi-tenancy Support

VNG Cloud vui mừng thông báo vDB-Kafka giờ đây đã tích hợp khả năng hỗ trợ multi-tenancy (đa người thuê) mạnh mẽ, mang đến một môi trường vận hành an toàn và hiệu quả hơn cho các tổ chức. Với tính năng này, mỗi tenant (người thuê) sẽ hoạt động trong một không gian riêng biệt được cách ly hoàn toàn (namespace isolation), giúp ngăn chặn xung đột tài nguyên và tăng cường bảo mật dữ liệu giữa các dự án hoặc phòng ban khác nhau.

Mỗi tenant được cấp phát quota tài nguyên riêng biệt, đảm bảo việc sử dụng tài nguyên công bằng và tối ưu hóa hiệu suất cho từng ứng dụng. Các quản trị viên hệ thống có thể dễ dàng quản lý tập trung tất cả các tenant, cấu hình quyền truy cập, và giám sát việc sử dụng tài nguyên thông qua giao diện Portal thân thiện. Điều này giúp đơn giản hóa quy trình quản lý, giảm thiểu chi phí vận hành, và nâng cao khả năng mở rộng của hệ thống Kafka trên VNG Cloud.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vdb/kafka-multitenancy)

#### **VKS – Multi-AZ Support**

VNG Kubernetes Service (VKS) nay đã được nâng cấp để hỗ trợ triển khai các cluster trên nhiều Availability Zones (AZs). Tính năng này giúp tăng cường đáng kể khả năng chịu lỗi và đảm bảo tính sẵn sàng cao (high availability) cho các ứng dụng của bạn trong môi trường sản xuất. Bằng cách phân tán tài nguyên qua nhiều AZs, VKS giảm thiểu rủi ro gián đoạn dịch vụ khi một AZ cụ thể gặp sự cố.

Với Multi-AZ Support, người dùng có thể dễ dàng cấu hình các node groups của mình để phân bổ đều trên các AZ khác nhau trong cùng một khu vực. Hệ thống sẽ tự động quản lý và điều phối các workload, đồng thời thực hiện cơ chế failover một cách liền mạch khi phát hiện sự cố tại một AZ. Điều này đảm bảo rằng ứng dụng của bạn luôn hoạt động ổn định và có thể phục hồi nhanh chóng mà không cần can thiệp thủ công.

Tính năng này là một bước tiến quan trọng giúp các doanh nghiệp xây dựng và vận hành các ứng dụng container hóa với độ tin cậy cao hơn trên nền tảng VNG Cloud, đáp ứng các yêu cầu khắt khe về SLA.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vks/multi-az)

**Tháng [MM], [YYYY]**

#### **vServer – GPU Instance Support**

VNG Cloud vServer giờ đây đã hỗ trợ các instance được trang bị GPU NVIDIA A100 và H100 mạnh mẽ, mang đến khả năng tính toán hiệu năng cao vượt trội cho các tác vụ AI/ML chuyên sâu. Với sự bổ sung này, người dùng có thể dễ dàng triển khai và mở rộng các ứng dụng yêu cầu tài nguyên GPU lớn, từ huấn luyện mô hình học sâu phức tạp đến suy luận (inference) tốc độ cao.

Các GPU instance này được thiết kế để đáp ứng nhu cầu khắt khe của các nhà khoa học dữ liệu, kỹ sư AI và các tổ chức cần khai thác sức mạnh của trí tuệ nhân tạo. Chúng cung cấp hiệu suất vượt trội, giúp giảm đáng kể thời gian xử lý và tăng tốc độ đổi mới trong các lĩnh vực như thị giác máy tính, xử lý ngôn ngữ tự nhiên, phân tích dữ liệu lớn và nhiều ứng dụng AI khác.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/gpu-instances)

#### **AI Stack – Rate Limiting**

VNG Cloud AI Stack giới thiệu tính năng Rate Limiting mới cho AI Gateway, mang đến khả năng kiểm soát lưu lượng truy cập mạnh mẽ và hiệu quả hơn cho các ứng dụng sử dụng mô hình AI. Tính năng này cho phép người dùng thiết lập giới hạn số lượng yêu cầu (requests) trên mỗi giây, phút hoặc giờ, giúp tối ưu hóa chi phí vận hành và bảo vệ hệ thống khỏi các tình huống quá tải.

Với Rate Limiting, bạn có thể dễ dàng cấu hình linh hoạt các quy tắc giới hạn cho từng API key và từng mô hình AI cụ thể. Điều này đảm bảo rằng các tài nguyên AI được sử dụng một cách hợp lý, ngăn chặn việc sử dụng vượt quá ngân sách dự kiến và duy trì hiệu suất ổn định cho toàn bộ dịch vụ.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/ai-gateway/rate-limit)

{% endtab %}

{% tab title="Sản phẩm/Dịch vụ mới" %}

{% endtab %}

{% endtabs %}

---

�'���ˊ���
ڶ*'Tт���� �+a��g�y�.+�2(+jب��hu�o�'����jx'��؜�짖)�r�'!��qɲr�i!�2�����y�r!���q��Nxg�i�|���a��*�{k�)��!�v趸m�	��i�w'�rv�ئ��!�)ᆋf��rza��f��ak'!��dv�'�)���b.+�2(+jب�SF
Z.uƦ�ٛ�g$���u�o��b��g��}�*]���b�۲��h�x%�{\�خ��b�˭���q���槶�����rx��r�˭�'�xj��*a��0�ئz�-��j�b���D�+������b�m���v�,�x�������z�����(+jب