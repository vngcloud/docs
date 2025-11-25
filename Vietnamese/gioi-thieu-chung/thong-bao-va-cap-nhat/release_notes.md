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

{% endtab %}

{% tab title="Tính năng mới" %}
**Tháng 9, 2025**

#### **VKS - HỖ TRỢ MULTI-AZ NODE GROUP**

Multi-AZ Node Group cho phép người dùng triển khai worker nodes – nơi chạy các ứng dụng và workloads – trên nhiều Availability Zone (AZ) khác nhau. Cách triển khai này giúp hệ thống Kubernetes đạt được tính sẵn sàng cao và khả năng chịu lỗi mạnh mẽ, phù hợp cho các ứng dụng quan trọng của doanh nghiệp.

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

{% endtab %}
{% endtabs %}
