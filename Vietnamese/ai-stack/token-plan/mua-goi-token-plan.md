# Mua gói Token Plan

> Hướng dẫn browse Packages catalog, xem chi tiết gói, và mua 1 gói Token Plan.

---

## Điều kiện cần

- Tài khoản GreenNode với vai trò **Root** hoặc **Admin** — chỉ 2 role này được mua gói
- Tổ chức có đủ **Credits** cho giá gói đã chọn (thanh toán bằng credit, 1 credit = 1 VND)

---

## Browse & xem chi tiết gói

**Bước 1: Mở Packages**

1. Vào **AI Platform** → sidebar → **API Key** → **Token Plan** → **Packages**
2. Danh sách hiển thị các Plan Type dạng card, ví dụ **Token Plan Alpha**: giá `1.080.000 VND / 30 ngày`, model đi kèm (GLM 5.2), số subscription-key tối đa (5 keys)

![Danh sách Packages](../../.gitbook/assets/Package-plan/packages-list.png)

**Bước 2: Xem chi tiết trước khi mua**

1. Nhấn vào 1 Plan Type để mở **Package Detail**
2. Xem đầy đủ: số Max keys, số Model, Duration, hạn mức token/request mỗi chu kỳ, danh sách **Included Models** (Model, Status, Model code, Provider), mục **What happens when activated**, và **Subscription Endpoint** (`https://tokenplan.api.greennode.ai/v1`, tương thích OpenAI SDK)

{% hint style="warning" %}
Gói đã mua **không thể đổi sang Plan Type khác hoặc trả lại theo yêu cầu tùy ý**. Nếu cần dừng gói giữa chu kỳ, dùng action **Delete** — phần hạn mức chưa dùng của chu kỳ hiện tại sẽ được hoàn lại pro rata vào Credits (xem [Quản lý Token Plan](quan-ly-token-plan.md)).
{% endhint %}

---

## Mua gói

**Bước 1: Bắt đầu mua**

1. Nhấn **Buy Now** trên card Plan Type trong danh sách Packages (hoặc mở Package Detail rồi nhấn **Buy package**)

**Bước 2: Xác nhận & thanh toán**

Màn **Confirm & checkout** hiển thị:

| Trường | Giá trị ví dụ | Ghi chú |
|---|---|---|
| **Plan name** (bắt buộc) | `ENG-GLM-1` | Chỉ chữ a-z, A-Z, số 0-9, `_`, `-`, `.`; tối đa 50 ký tự |
| **Plan price / Duration / VAT / Total** | `1.080.000 VND` / `30 days` / `Included` / `1.080.000 VND` | Tự tính theo Plan Type đã chọn |
| **Auto-renew** | Bật ON (mặc định) | Tự gia hạn cuối mỗi chu kỳ — có thể tắt sau khi mua |
| **Payment method** | Credits (1 credit = 1 VND) | Trừ trực tiếp từ Credits của tổ chức |
| **Balance** | Số dư Credits hiện tại | Hiển thị để đối chiếu trước khi xác nhận |

1. Điền **Plan name**
2. Kiểm tra lại giá và **Balance** còn đủ
3. Nhấn **Confirm & Pay**

{% hint style="warning" %}
Xác nhận sẽ **trừ ngay số tiền hiển thị ở Total** từ Credits của tổ chức. Provisioning chạy nền — gateway endpoint và subscription-key chỉ hiển thị đầy đủ trên Plan Detail sau khi provisioning hoàn tất.
{% endhint %}

---

## Kết quả

Gói xuất hiện trong **My Token Plans** với trạng thái `ACTIVE`, **Auto-renew** bật ON, và hệ thống tự tạo sẵn 1 subscription-key mặc định tên `default-key` với quyền gọi toàn bộ model trong gói — sẵn sàng dùng ngay sau khi provisioning hoàn tất.

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Tạo thêm subscription-key & quản lý gói | [Quản lý Token Plan](quan-ly-token-plan.md) |
| Xem tổng quan Token Plan | [Token Plan](README.md) |
