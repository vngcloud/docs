# 2025

{% tabs %}
{% tab title="Nâng cấp mới" %}
**Tháng 11, 2025**

#### **vDB – Redis version 7.2.11**

Cập nhật Redis lên version 7.2.11 nhằm cải thiện hiệu năng và tính tương thích.

#### **vLB – Access Log tại AZ 1B, 1C HCM**

Bổ sung access log cho HCM, giúp theo dõi và phân tích lưu lượng chi tiết theo vùng.



**Tháng 9, 2025**

#### **VKS (VNG Cloud Kubernetes Service) - Tự động xóa cluster không có node active sau 30 ngày (Cải tiến hệ thống):**&#x20;

Hệ thống sẽ tự động quét và xóa các cluster không có node nào active trong vòng 30 ngày. Trong thời hạn quét và trước khi xóa, email cảnh báo sẽ được gửi đến Khách hàng để đảm bảo Khách hàng có thể chủ động xử lý nếu cần giữ lại cluster – đảm bảo an toàn và minh bạch trong quá trình quản lý.. Việc nâng cấp này giúp Quý Khách Hàng tiết kiệm chi phí vận hành và tránh lãng phí tài nguyên do các cluster không còn hoạt động.



**Tháng 7, 2025**

#### vStorage - FileStorage tích hợp thêm 1 region HAN

* Dịch vụ File storage cải tiến với 2 region HCM và HAN. Cung cấp khả năng lưu trữ file theo cách thức phân tán, dễ dàng mở rộng, và có khả năng truy cập từ nhiều instance cùng lúc

Tài liệu tham khảo [tại đây](../../vstorage/filestorage/bat-dau-voi-filestorage.md)



**Tháng 6, 2025**

#### **vDB – Multi-AZ cho Relational & MemoryStore**

* vDB – Multi-AZ cho Relational & MemoryStore (06/2025)
* Hỗ trợ triển khai Multi-AZ tại HCM.
* Nâng cao độ bền và tính sẵn sàng của dịch vụ.



**Tháng 1, 2025**

#### **vDB – Hỗ trợ PostgreSQL version 14 & pgvector**

* vDB – PostgreSQL 14 & pgvector (01/2025)
* Bổ sung PostgreSQL 14 và extension pgvector cho các phiên bản 14, 15.
* Tăng khả năng hỗ trợ ứng dụng AI/ML.
{% endtab %}

{% tab title="Tính năng mới" %}
**Tháng 9, 2025**

#### **VKS - HỖ TRỢ MULTI-AZ NODE GROUP**

Multi-AZ Node Group cho phép người dùng triển khai worker nodes – nơi chạy các ứng dụng và workloads – trên nhiều Availability Zone (AZ) khác nhau. Cách triển khai này giúp hệ thống Kubernetes đạt được tính sẵn sàng cao và khả năng chịu lỗi mạnh mẽ, phù hợp cho các ứng dụng quan trọng của doanh nghiệp.

#### **AI Gateway**

Bản cập nhật mới của AI Gateway mang đến hai tính năng quan trọng giúp Quý Khách Hàng vận hành hiệu quả hơn, giảm chi phí và quản lý tốt hơn việc gọi mô hình AI (LLM):

* Caching (Exact/Semantic Caching): Hệ thống tự động lưu lại kết quả của các yêu cầu (prompt) trùng lặp hoặc có ngữ nghĩa tương đồng. Nhờ đó, Quý Khách Hàng có thể giảm đáng kể số lần gọi mô hình LLM, tối ưu chi phí sử dụng, đồng thời rút ngắn thời gian phản hồi cho người dùng cuối.
* Rate Limit: Cho phép Quý Khách Hàng thiết lập giới hạn tần suất sử dụng mô hình AI, giúp kiểm soát hiệu quả lưu lượng truy cập và chi phí, đồng thời đảm bảo hiệu năng ổn định cho các ứng dụng đang khai thác AI Gateway.

_Như vậy, đến nay, AI Gateway đã hỗ trợ các tính năng bao gồm: Hỗ trợ đa mô hình AI (Multi-LLM Support); Giám sát toàn diện thông qua metrics và logs, giúp người dùng dễ dàng theo dõi/ phân tích và tối ưu hóa quá trình vận hành; một số tính năng đảm bảo an toàn cho các thông tin nhạy cảm của khách hàng như authentication token và API key; và mới nhất là tính năng Caching và Rate Limit._

#### **vNetwork - tích hợp vDNS cho dịch vụ Endpoint**

vDNS là dịch vụ DNS (Domain Name System), được thiết kế đặc biệt cho môi trường Private Cloud trên VNG Cloud, cung cấp khả năng quản lý và phân giải tên miền một cách an toàn, linh hoạt và hiệu quả trong mạng riêng ảo (VPC). vDNS được tích hợp chặt chẽ với các dịch vụ khác của VNG Cloud, tạo thành một hệ sinh thái hoàn chỉnh và mạnh mẽ cho hạ tầng trực tuyến của khách hàng. Trước đây, vDNS đã hỗ trợ tích hợp với các dịch vụ gồm vLB (Load Balancing) ,VKS. Với bản cập nhật lần này, việc tích hợp thêm dịch vụ Endpoint, sẽ giúp kết nối giữa VPC với các dịch vụ VNG Cloud gồm HCM-03 (vStorage, vMonitor, vServer, vCR, IAM) và HCM-04 (vStorage).

#### **vStorage – Sử dụng tính năng Lifecycle**

* Tích hợp tính năng Lifecycle transition object trên region HCM04/HAN02 để phục vụ chuyển đổi các object giữa các tier trong cùng bucket nhằm mục đích tiết kiệm chi phí lưu trữ.

Tài liệu tham khảo [tại đây](../../vstorage/object-storage/object-storage-han02/cac-tinh-nang-cua-object-storage/lam-viec-voi-bucket/lam-viec-voi-bucket-thong-qua-vstorage-portal/su-dung-tinh-nang-lifecycle.md)



**Tháng 8, 2025**

#### **VKS - Hỗ trợ Placement Group cho từng Node Group**

Việc hỗ trợ này cho phép kiểm soát vị trí triển khai node một cách hiệu quả hơn nhằm tối ưu hiệu năng và đảm bảo độ sẵn sàng cao, đặc biệt hữu ích cho các workload yêu cầu phân tán vật lý (anti-affinity) hoặc đồng vị trí (affinity) để giảm độ trễ và tăng tốc độ phản hồi hệ thống.

**vNetwork -  Hỗ trợ Multi-AZ zone cho các dịch vụ Endpoint, NAT, VPN**&#x20;

Tính năng hỗ trợ Multi-AZ này giúp Quý Khách Hàng chủ động hơn trong việc thiết kế hệ thống HA, giúp hệ thống duy trì hoạt động ổn định ngay cả khi một AZ gặp sự cố.



**Tháng 7, 2025**

#### **vStorage – Object storage (HCM04)**

* Tích hợp nhiều tier trên region HCM04 tương ứng với các cấp độ lưu trữ và chi phí phù hợp với nhiều nhu cầu lưu trữ khác nhau của khách hàng.
* Gói công khai: Instant Archive, Gold.

Tài liệu tham khảo [tại đây](../../vstorage/object-storage/object-storage-han02/bat-dau-voi-object-storage/buoc-1-khoi-tao-project.md)

#### **vLB – ALB hỗ trợ CORS Header, ALPN, SSL Policy**

* vLB/ALB – CORS Response Header, ALPN, SSL Policy (07/2025)
* Cập nhật ALB hỗ trợ CORS response header và tùy chỉnh ALPN, SSL Policy giúp tăng cường bảo mật và tương thích tốt hơn.



**Tháng 6, 2025**

#### **vDB-Kafka - Hỗ trợ metric/logs**

Tính năng hỗ trợ Metric/Logs mới giúp Quý Khách Hàng có thể theo dõi toàn bộ trạng thái hoạt động của cụm Kafka trực tiếp ngay trên trang quản lý. Việc tích hợp này sẽ giúp Khách hàng đơn giản hóa việc giám sát, nâng cao khả năng chủ động trong quản trị hệ thống, và giảm thiểu rủi ro downtime cho các ứng dụng sử dụng Kafka.



**Tháng 4, 2025**

#### **vStorage – Object storage (HAN02)**

* Tích hợp region mới HAN02 trên portal vStorage cung cấp khả năng lưu trữ mạnh mẽ và linh hoạt hơn nhằm thay thế region HAN01 hiện có.
* Chuyển đổi tất cả các khách hàng trên region HAN01 sang HAN02 và đóng region HAN01.

Tài liệu tham khảo [tại đây](../../vstorage/object-storage/object-storage-han02/)



**Tháng 3, 2025**

#### **vLB – Ra mắt vLB Autoscale region HAN**

* vLB – Autoscale tại Region HAN (03/2025)
* Kích hoạt tính năng Autoscale tại khu vực Hà Nội, tự động mở rộng năng lực xử lý theo tải thực tế.
{% endtab %}

{% tab title="Sản phẩm/Dịch vụ mới" %}


**Tháng 5, 2025**

**AI STACK**

VNGCloud cung cấp một nền tảng AI toàn diện giúp doanh nghiệp triển khai, tích hợp và vận hành các ứng dụng Generative AI một cách dễ dàng, bảo mật và hiệu quả. AI Stack của VNGCloud được thiết kế theo hướng modular, linh hoạt và tối ưu cho cả đội ngũ kỹ thuật và nhà quản lý.

Hệ sinh thái các dịch vụ chính của AI stack bao gồm:

* **VKS (VNGCloud Kubernetes Service):** là dịch vụ Kubernetes được quản lý toàn diện.Tích hợp GPU, khả năng autoscaling, giám sát tài nguyên và bảo mật. Giúp tối ưu cho AI workloads cần GPU, nhưng cũng phù hợp để triển khai ứng dụng web, microservices và backend quy mô lớn. Qua đó, giúp doanh nghiệp nhanh chóng triển khai ứng dụng mà không cần tự xây dựng và duy trì hạ tầng. Tài liệu tham khảo [tại đây](../../vks/)
* vDB **OpenSearch:** Vector Database dưới dạng dịch vụ, giúp Hỗ trợ PostgreSQL(**pgvector)** và **OpenSearch** làm vector database.Hỗ trợ triển khai mô hình **RAG (Retrieval-Augmented Generation)** nhanh chóng.Giúp mô hình GenAI hiểu và khai thác dữ liệu doanh nghiệp theo ngữ cảnh. Tài liệu tham khảo [tại đây](../../vdb/opensearch-cluster-database-ods/)
* **AI Platform:** Cung cấp môi trường để **thử nghiệm (notebook )**, **fine-tune** và **inference** các mô hình AI ngay trên nền tảng GPU của VNGCloud. Tài liệu tham khảo [tại đây](../../ai-stack/ai-platform/)
* **AI Gateway:** là Cổng truy cập quản trị tập trung duy nhất cho nhiều mô hình AI, hỗ trợ routing thông minh và caching để tối ưu hiệu năng và chi phí. Giúp theo dõi truy cập, sinh audit logs, giám sát hành vi sử dụng qua metrics và alerts. Tài liệu tham khảo [tại đây](../../ai-stack/ai-gateway/)
* **Model-as-a-Service:** Hỗ trợ truy cập hơn đa dạng **mô hình GenAI** hàng đầu như GPT, Claude, Gemini, DeepSeek... chỉ với 1 API thống nhất. Tài liệu tham khảo [tại đây](../../ai-stack/ai-platform/model-as-a-service/)



**Tháng 4, 2025**

**OPENSEARCH DATABASE**

vDB **OpenSearch** là **Vector Database**, tức là sử dụng dịch vụ này để **tìm kiếm gần đúng (k - Nearest Neighbor - kNN)** trên các vector embedding bằng cách tích hợp sẵn kNN plugin trên OpenSearch Cluster của bạn. Đây là một cách phổ biến để xây dựng hệ thống tìm kiếm vector cho **AI/ML, NLP, Recommendation Systems, hay Semantic Search**.

Tài liệu tham khảo [tại đây](../../vdb/opensearch-cluster-database-ods/)
{% endtab %}
{% endtabs %}











