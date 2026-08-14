# Có giao diện (GUI)

> Công cụ AI Coding có giao diện đồ hoạ — chỉ cần điền Base URL và API key, không phải gõ lệnh. Phù hợp cho **người mới bắt đầu**.

Trước khi cài, xem [Điều kiện cần](../bat-dau.md).

{% hint style="warning" %}
Phần cấu hình của mỗi công cụ có **tab riêng cho PAYG và Token Plan**. Xác định loại dịch vụ của bạn trước (theo nơi bạn lấy key), rồi chỉ copy từ tab đó — key và Base URL lệch loại dịch vụ sẽ trả về `401 Unauthorized`.
{% endhint %}

| Công cụ | Ghi chú |
|---|---|
| [Codex Desktop](codex-desktop.md) | Cấu hình qua file `config.toml` trong Settings |
| Claude Desktop | Hiện chỉ cho kết nối model **Anthropic thật** (`claude-*`) khi cấu hình third-party inference — model self-host của hãng khác (GLM, v.v.) chưa dùng được qua giao diện này. Cần dùng model self-host hãng khác, chuyển sang [Claude Code (CLI)](../dong-lenh/claude-code.md). |
