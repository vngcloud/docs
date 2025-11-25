={% tabs %}
{% tab title="Nâng cấp mới" %}

**Tháng 11, 2025**

#### **VKS – Auto-scaling Enhancement**

Cải thiện cơ chế auto-scaling cho VKS cluster. Hệ thống giờ đây tự động scale nodes dựa trên CPU và Memory metrics với độ chính xác cao hơn, giảm thời gian phản hồi xuống còn 30 giây. Tích hợp với vMonitor để monitoring real-time.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vks/autoscaling)

{% endtab %}

{% tab title="Tính năng mới" %}

**Tháng 11, 2025**

#### **vServer – Live Migration**

Di chuyển vServer giữa các host mà không downtime. Giúp maintenance infrastructure dễ dàng hơn và đảm bảo uptime 99.9%.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/live-migration)

#### **vServer – Snapshot Scheduling**

Tự động tạo snapshot theo lịch định kỳ (daily/weekly/monthly). User có thể cấu hình retention policy để quản lý storage cost hiệu quả.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/snapshot-schedule)

#### **vDB-Kafka – Multi-tenancy Support**

vDB-Kafka giờ hỗ trợ multi-tenancy với namespace isolation. Mỗi tenant có quota riêng, đảm bảo fair usage và security. Admin có thể quản lý centralized qua Portal.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vdb/kafka-multitenancy)

#### **vServer – GPU Instance Support**

Hỗ trợ instance với NVIDIA A100/H100 GPU cho AI/ML workloads. Cung cấp high-performance computing cho training và inference.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vserver/gpu-instances)

#### **VKS – Multi-AZ Support**

VKS giờ đây hỗ trợ triển khai cluster trên nhiều Availability Zones, giúp tăng khả năng chịu lỗi và đảm bảo high availability cho ứng dụng. Người dùng có thể cấu hình node groups phân bổ đều trên các AZ khác nhau, tự động failover khi một AZ gặp sự cố.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/vks/multi-az)

#### **AI Stack – Rate Limiting**

Thêm tính năng rate limiting cho AI Gateway, cho phép người dùng giới hạn số request per second/minute/hour để kiểm soát chi phí. Hỗ trợ cấu hình flexible cho từng API key và model.

Tài liệu tham khảo [tại đây](https://docs.vngcloud.vn/ai-gateway/rate-limit)

{% endtab %}

{% tab title="Sản phẩm/Dịch vụ mới" %}

{% endtab %}

{% endtabs %}