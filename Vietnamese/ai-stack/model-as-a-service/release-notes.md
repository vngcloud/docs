# Release Notes

Tổng hợp các bản cập nhật và thay đổi quan trọng của dịch vụ Model as a Service (MaaS).

***

## Tháng 8, 2026 - Cập nhật danh mục model & bảng giá

Để mang lại trải nghiệm tốt hơn, GreenNode cập nhật danh mục model trên MaaS, gồm hai nhóm:

* **Model do GreenNode trực tiếp self-host.**
* **Model third-party từ đối tác đã ký kết hợp đồng chính thức.**

**Mốc thời gian chuyển đổi**

| Sự kiện                                                                            | Thời điểm      |
| ------------------------------------------------------------------------------------ | -------------- |
| Dừng cung cấp các model hiện tại & công bố danh mục model mới trên portal            | 03/08/2026     |
| Gia hạn tự động 30 ngày — tiếp tục dùng model hiện tại đến hết                       | 02/09/2026     |
| Sau thời điểm này, request đến model cũ sẽ trả về lỗi và không thực hiện được        | Từ 03/09/2026  |

**Quý khách cần làm gì**

* Đối chiếu **model đang sử dụng** với [danh mục model mới](cac-model-duoc-cung-cap.md). Nếu model hiện tại vẫn còn trong danh mục, **không cần thay đổi**. Chỉ khi model không còn trong danh mục, mới cần tham khảo [bảng giá](bang-gia-model.md) và chọn model thay thế phù hợp.
* **Kiểm tra kỹ thuật khi chuyển đổi** (nếu cần thay thế model): model thay thế có thể khác về model ID/endpoint cũng như đặc điểm output. Vui lòng kiểm thử trước và điều chỉnh cấu hình, prompt cho phù hợp để tránh gián đoạn.
* Nếu cần **thêm thời gian chuyển đổi** ngoài mốc 02/09/2026, hoặc có nhu cầu đặc biệt về một model cụ thể, vui lòng liên hệ đội ngũ GreenNode để được tư vấn.

**Lợi ích sau chuyển đổi**

* **Minh bạch nguồn model:** trên portal hiển thị rõ model nào thuộc GreenNode self-host và model nào là third-party.
* **Chi phí tối ưu hơn:** nhiều model trong danh mục mới có giá tốt hơn trước — xem chi tiết tại [Bảng giá Model](bang-gia-model.md).
* **Danh mục đầy đủ & liên tục mở rộng:** đáp ứng đa số model open-source và closed-source top tier (Claude, GPT,…).

{% hint style="info" %}
Cần hỗ trợ trong quá trình chuyển đổi? Liên hệ qua email [support@greennode.ai](mailto:support@greennode.ai), hotline **19001549**, hoặc [Trung tâm hỗ trợ](https://helpdesk.greennode.ai/portal/vi/home).
{% endhint %}

* Xem danh mục model mới tại [Các Model được cung cấp](cac-model-duoc-cung-cap.md).
* Xem bảng giá chi tiết tại [Bảng giá Model](bang-gia-model.md).
