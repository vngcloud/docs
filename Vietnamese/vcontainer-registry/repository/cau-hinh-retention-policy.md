# Cấu hình Retention Policy

Retention policy giúp bạn tự động dọn dẹp các artifact cũ trong Repository. Bạn đặt các rule để chọn artifact cần giữ lại; vCR sẽ xoá phần còn lại theo lịch chạy hoặc khi bạn bấm **Chạy ngay**.

Tính năng này phù hợp với các team có CI push nhiều tag (ví dụ mỗi commit một tag mới) và muốn kiểm soát dung lượng lưu trữ cũng như chi phí quota.

{% hint style="warning" %}
Artifact bị retention policy xoá **không thể khôi phục**. Hãy luôn dùng **Chạy thử** để kiểm tra trước khi chạy thật hoặc đặt lịch chạy.
{% endhint %}

## Retention policy là gì

Retention policy là tập hợp các rule quy định artifact nào trong repository được **giữ lại**. Khi policy chạy, mọi artifact trong phạm vi mà không được rule nào đang bật giữ lại sẽ bị **xoá vĩnh viễn**.

Mỗi repository có tối đa **một** retention policy, gồm tối đa **15 rule** và **một lịch chạy**. Repository chưa có policy sẽ hiển thị danh sách rule trống và lịch chạy **Không**.

Nếu không có policy, mọi image bạn push sẽ được giữ mãi. Các tag build cũ tích tụ dần, chiếm dung lượng và được tính vào quota của repository.

**Các thuật ngữ trên portal**

| Thuật ngữ | Ý nghĩa | Ví dụ |
| --- | --- | --- |
| Repository | Repository của bạn trên vCR, là đơn vị tính phí | `my-team` |
| Image | Một tên image trong repository | `my-team/backend` |
| Artifact | Một phiên bản đã push của image, xác định bằng digest (có thể có một hoặc nhiều tag, hoặc không có tag) | `backend@sha256:ab12…` |
| Tag | Tên trỏ tới một artifact | `v1.4.2`, `latest` |
| Artifact không có tag | Artifact không còn tag nào, thường sinh ra khi push đè một tag đã có | — |

## Cách rule hoạt động

Mỗi rule được tính độc lập, rồi gộp kết quả lại: **artifact được giữ nếu có ít nhất một rule đang bật giữ nó.** Artifact không được rule nào giữ sẽ bị xoá. Rule đã tắt sẽ bị bỏ qua.

Mỗi rule gồm 3 phần:

1. **Image** — *khớp với* hoặc *loại trừ* một pattern. Phần này chọn image mà rule sẽ xét.
2. **Điều kiện giữ** — một trong các mẫu bên dưới, kèm một số từ 0 đến 10000.
3. **Tag** — *khớp với* hoặc *loại trừ* một pattern, cùng ô chọn **Bao gồm artifact không có tag**.

| Mẫu điều kiện (như trên portal) | Giữ lại |
| --- | --- |
| giữ N artifact được push gần nhất cho mỗi image | N artifact push mới nhất, tính theo từng image |
| giữ N artifact được pull gần nhất cho mỗi image | N artifact được pull gần nhất, tính theo từng image |
| giữ các artifact được push trong N ngày gần nhất | Artifact được push trong N ngày qua |
| giữ các artifact được pull trong N ngày gần nhất | Artifact được pull trong N ngày qua |
| luôn giữ | Mọi artifact mà rule khớp (không cần nhập số) |

**Pattern**

* `**` khớp tất cả, `*` khớp chuỗi ký tự bất kỳ, `?` khớp đúng một ký tự.
* Dùng dấu phẩy để nhập nhiều giá trị: `backend,frontend` hoặc `v1.*,release-*`.
* Ký tự cho phép: chữ, số và `. _ - / * ? { } , [ ]`, tối đa 255 ký tự. Không được để trống.

**Số 0.** Nếu nhập 0, rule đó không giữ artifact nào. Mọi artifact khớp sẽ bị xoá, trừ khi có rule khác giữ lại. Form sẽ hiện cảnh báo khi bạn nhập 0, ví dụ: *Giữ 0 artifact được push gần nhất: mọi artifact khớp trong mỗi image sẽ bị xoá, trừ khi có rule khác giữ lại.* Hãy dùng cẩn thận.

**Image hoặc tag nằm ngoài mọi rule** sẽ không bị policy đụng tới. Chỉ những artifact mà rule xét tới (theo pattern image và tag) mới có thể bị xoá.

## Hướng dẫn sử dụng trên portal

Vào **Container Registry → danh sách Repository**, bấm vào một repository, rồi mở tab **Retention policy** (cạnh các tab Images, Users và History). Tab gồm 3 phần: **Retention rule**, **Lịch chạy** và **Lịch sử chạy**.

### Thêm rule

1. Bấm **Thêm rule**. Hộp thoại **Thêm retention rule** mở ra, gồm 2 phần được đánh số.
2. **1. Chọn image** — ở ô **Áp dụng cho image**, chọn *khớp với* hoặc *loại trừ*, rồi nhập tên image hoặc pattern (ví dụ `**` cho tất cả image).
3. **2. Chọn artifact cần giữ lại**:
   * Ở ô **Theo số lượng artifact hoặc số ngày**, chọn một mẫu điều kiện và nhập số.
   * Ở ô **Tag**, chọn *khớp với* hoặc *loại trừ*, rồi nhập tag hoặc pattern.
   * Tick **Bao gồm artifact không có tag** nếu muốn rule xét cả artifact không có tag.
4. Bấm Lưu. Rule hiển thị trong danh sách dưới dạng một câu, ví dụ: *Với image \*\*, giữ 10 artifact được push gần nhất cho mỗi image có tag \*\* (không bao gồm artifact không có tag).*

Không thể lưu hai rule giống hệt nhau trong cùng một repository.

### Sửa, tắt hoặc xoá rule

Dùng menu **Thao tác** ở dòng của rule:

* **Sửa** — thay đổi rule.
* **Tắt** / **Bật** — rule đã tắt vẫn nằm trong danh sách với trạng thái **Đã tắt**, nhưng không được dùng khi policy chạy.
* **Xoá** — xoá rule. Hộp xác nhận sẽ hiện lại nội dung rule trước khi xoá.

### Đặt lịch chạy

1. Ở phần **Lịch chạy**, bấm **Sửa**.
2. Chọn kiểu lịch:
   * **Không** — chỉ chạy khi bạn bấm Chạy ngay.
   * **Hằng giờ** — mỗi giờ, vào phút 0.
   * **Hằng ngày** — mỗi ngày lúc 00:00 UTC (07:00 giờ Việt Nam).
   * **Hằng tuần** — mỗi Chủ nhật lúc 00:00 UTC (07:00 giờ Việt Nam).
   * **Tuỳ chỉnh** — biểu thức cron 6 trường theo giờ UTC: `giây phút giờ ngày tháng thứ`. Ví dụ: `0 0 2 * * *` chạy lúc 02:00 UTC (09:00 giờ Việt Nam). Các lần chạy phải cách nhau ít nhất 1 giờ.
3. Lưu lại. Lịch chạy áp dụng cho tất cả rule của repository.

Phần Lịch chạy hiển thị giờ chạy theo UTC và theo giờ của bạn.

### Kiểm tra bằng Chạy thử (Dry run)

Chạy thử áp dụng toàn bộ rule đang bật lên repository giống hệt một lần chạy thật, nhưng **không xoá gì cả**. Dùng Chạy thử để biết trước rule sẽ tác động tới **những image nào** và **những artifact (tag) nào** sẽ bị xoá hoặc được giữ lại.

**Các bước**

1. Bấm **Chạy thử**. Một dòng mới xuất hiện trong **Lịch sử chạy** với cột **Chạy thử = Có**.
2. Chờ trạng thái chuyển sang **Thành công**. Trang tự làm mới mỗi 10 giây.
3. Bấm **Xem các tác vụ** ở dòng đó. Mỗi image mà rule xét tới là một dòng (một tác vụ). Phía trên bảng có thông báo: *Chạy thử: không có gì bị xoá. Cột "Giữ lại / Tổng" cho biết số artifact sẽ được giữ lại nếu chạy thật.*
4. Đọc cột **Giữ lại / Tổng** của từng image:

| Ví dụ | Ý nghĩa nếu chạy thật |
| --- | --- |
| `10 / 10` | Image này không mất artifact nào |
| `10 / 37` | 10 artifact được giữ, **27 artifact sẽ bị xoá** |
| `0 / 12` | **Toàn bộ 12 artifact sẽ bị xoá**. Hãy kiểm tra lại rule (ví dụ số 0 hoặc pattern tag quá hẹp) |

5. Bấm **Log** ở một image để xem chính xác **từng artifact, tag nào** sẽ bị xoá hay được giữ (xem phần bên dưới).

Image không xuất hiện trong danh sách tác vụ thì không nằm trong phạm vi của rule nào, nên sẽ không bị đụng tới.

{% hint style="info" %}
Hãy Chạy thử lại mỗi khi thêm, sửa, bật hoặc tắt rule, và luôn Chạy thử trước khi bấm **Chạy ngay** hoặc đặt lịch chạy. Kết quả của lần chạy thật sẽ khớp với kết quả Chạy thử nếu bạn không push hoặc pull thêm artifact giữa hai lần chạy.
{% endhint %}

### Xem log retention trên portal vCR

Bạn có thể xem log chi tiết của từng image ngay trên portal vCR, không cần vào Harbor. Log có cho cả lần **Chạy thử** và lần **Chạy ngay** / chạy **Theo lịch**.

1. Trong **Lịch sử chạy**, bấm **Xem các tác vụ** ở lần chạy cần xem.
2. Bấm **Log** ở dòng của image. Cửa sổ **Log retention của image &lt;tên image&gt;** mở ra.

Log gồm phần đầu cho biết repository, cách gộp rule và lần chạy có phải Chạy thử hay không (`Dry Run: true`), sau đó là bảng liệt kê từng artifact. Các cột chính:

| Cột | Ý nghĩa |
| --- | --- |
| Digest | Digest của artifact |
| Tag | Các tag của artifact (trống nếu là artifact không có tag) |
| PushedTime / PulledTime | Lần push / pull gần nhất, dùng cho các mẫu điều kiện theo push / pull |
| Retention | Kết quả: `RETAIN` = được giữ, `DEL` = bị xoá (hoặc sẽ bị xoá nếu là Chạy thử), `ERR` = xoá thất bại |

Ví dụ minh hoạ log của một lần Chạy thử:

```
Run retention process.
 Repository: my-team/backend
 Rule Algorithm: or
 Dry Run: true
+-----------------+--------+-------+--------+---------------------+---------------------+---------------------+-----------+
|     DIGEST      |  TAG   | KIND  | LABELS |     PUSHEDTIME      |     PULLEDTIME      |     CREATEDTIME     | RETENTION |
+-----------------+--------+-------+--------+---------------------+---------------------+---------------------+-----------+
| sha256:ab12...  | v1.4.2 | image |        | 2026/11/18 09:12:01 | 2026/11/19 02:00:13 | 2026/11/18 09:12:01 | RETAIN    |
| sha256:cd34...  | v1.4.1 | image |        | 2026/11/10 08:01:44 |                     | 2026/11/10 08:01:44 | DEL       |
| sha256:ef56...  |        | image |        | 2026/10/02 15:30:10 |                     | 2026/10/02 15:30:10 | DEL       |
+-----------------+--------+-------+--------+---------------------+---------------------+---------------------+-----------+
```

{% hint style="warning" %}
**Lưu ý về log**

* Log chỉ xem được trên portal vCR (tab Retention policy). Không dùng Harbor UI để xem hay sửa retention policy.
* Ở lần Chạy thử, `DEL` nghĩa là artifact **sẽ** bị xoá nếu chạy thật; chưa có gì bị xoá.
* Ở lần chạy thật, nếu có dòng `ERR` hoặc dòng "Retention error for artifact", artifact đó **chưa** bị xoá. Tác vụ vẫn có thể hiện **Thành công**, nhưng sẽ kèm cảnh báo *N artifact xoá thất bại*.
* Nếu log trống, cửa sổ sẽ hiện **Không có log**. Hãy chờ lần chạy kết thúc rồi mở lại.
{% endhint %}

### Chạy ngay

Bấm **Chạy ngay**. Hộp thoại **Chạy retention policy ngay** cảnh báo rằng các artifact không được rule nào giữ lại sẽ bị xoá vĩnh viễn. Bạn có thể bấm **Chạy ngay** để tiếp tục, hoặc **Chạy thử** để kiểm tra trước.

{% hint style="info" %}
Nút **Chạy ngay** và **Chạy thử** bị khoá cho tới khi repository có ít nhất một rule đang bật.
{% endhint %}

### Theo dõi lần chạy

Bảng **Lịch sử chạy** gồm các cột:

| Cột | Ý nghĩa |
| --- | --- |
| Trạng thái | Đang chờ, Đã lên lịch, Đang chạy, Thành công, Đã dừng, Lỗi hoặc Thất bại |
| Chạy thử | Có nếu là chạy thử, Không nếu là chạy thật |
| Kiểu chạy | Thủ công (bạn bấm nút) hoặc Theo lịch |
| Thời gian bắt đầu | Thời điểm bắt đầu chạy |
| Thời lượng | Hiển thị khi lần chạy đã kết thúc |

Trang tự làm mới mỗi 10 giây khi có lần chạy đang diễn ra.

Bấm **Xem các tác vụ** để xem mỗi image một tác vụ, gồm trạng thái, **Giữ lại / Tổng**, thời gian bắt đầu và thời lượng. Bấm **Log** ở một tác vụ để đọc log retention của image đó.

**Xoá thất bại.** Một tác vụ có thể hiện **Thành công** dù vẫn có artifact không xoá được. Khi đó tác vụ sẽ hiện cảnh báo *N artifact xoá thất bại*. Mở **Log** và tìm các dòng "Retention error for artifact" hoặc cột **Retention = ERR** để xem lý do.

### Dừng lần chạy

Bấm **Dừng** ở lần chạy đang chạy và xác nhận. Lần chạy sẽ dừng sau ít giây và chuyển sang trạng thái **Đã dừng**. Nếu lần chạy đã xong trước đó, kết quả được giữ nguyên. Các artifact đã bị xoá sẽ không được khôi phục.

## Ví dụ

| Mục tiêu | Cách đặt rule | Kết quả |
| --- | --- | --- |
| Giữ 10 bản build mới nhất của mọi image | Image khớp với `**` · giữ 10 artifact được push gần nhất cho mỗi image · tag khớp với `**` | Mỗi image giữ 10 artifact mới nhất; các artifact cũ hơn bị xoá |
| Giữ bản release mãi mãi, dọn bản build dev | Rule 1: image `**` · luôn giữ · tag khớp với `v*,release-*`. Rule 2: image `**` · giữ các artifact được push trong 14 ngày gần nhất · tag khớp với `**` | Tag release không bao giờ bị xoá; các tag khác được giữ 14 ngày |
| Chỉ xoá artifact không có tag | Rule 1: image `**` · giữ 0 artifact được push gần nhất cho mỗi image · tag `**` + bao gồm artifact không có tag. Rule 2: image `**` · luôn giữ · tag `**`, không bao gồm artifact không có tag | Mọi artifact có tag được giữ; artifact không có tag bị xoá |
| Chỉ dọn một image | Image khớp với `backend` · giữ 5 artifact được push gần nhất cho mỗi image · tag `**` | Chỉ `backend` được dọn; các image khác không bị đụng tới |
| Dọn mọi image trừ một image | Image loại trừ `base` · giữ 5 artifact được push gần nhất cho mỗi image · tag `**` | Mọi image trừ `base` được dọn |
| Giữ những gì còn được dùng | Image `**` · giữ các artifact được pull trong 30 ngày gần nhất · tag `**` | Artifact không được pull trong 30 ngày sẽ bị xoá |

{% hint style="info" %}
Sau khi thêm hoặc sửa rule, hãy **Chạy thử** và kiểm tra cột **Giữ lại / Tổng** trước khi đặt lịch chạy.
{% endhint %}

## Giới hạn

| Mục | Giới hạn |
| --- | --- |
| Số retention policy mỗi repository | 1 |
| Số rule mỗi repository | 15 |
| Số lịch chạy mỗi repository | 1 |
| Số lượng / số ngày trong rule | 0 đến 10000 |
| Độ dài pattern | 1 đến 255 ký tự |
| Cron tuỳ chỉnh | 6 trường, giờ UTC, các lần chạy cách nhau ít nhất 1 giờ |
| Rule trùng nhau | Không cho phép |

## Câu hỏi thường gặp

**Có khôi phục được artifact đã xoá không?** Không. Artifact đã xoá không thể khôi phục. Luôn Chạy thử trước.

**Vì sao lịch chạy dùng giờ UTC?** Registry chạy theo giờ UTC. Cộng thêm 7 giờ để ra giờ Việt Nam. Portal cũng hiển thị lịch chạy theo giờ của bạn.

**Xoá một rule thì sao?** Rule bị xoá ngay. Lần chạy sau chỉ dùng các rule đang bật còn lại.

**Có đặt lịch chạy trước khi thêm rule được không?** Được. Nhưng policy chỉ xoá artifact khi có ít nhất một rule đang bật, và Chạy ngay / Chạy thử cũng cần ít nhất một rule đang bật.

**Vì sao tác vụ báo Thành công nhưng một số artifact vẫn còn?** Có thể một số artifact xoá thất bại. Xem cảnh báo *artifact xoá thất bại* ở tác vụ và đọc **Log**. Xem phần [Theo dõi lần chạy](#theo-doi-lan-chay).
