# vCR

### \[vCR] vCR có hỗ trợ Retention Policy không?

Hiện tại vCR không hỗ trợ Retention policy.

### \[vCR] Muốn xoá image cũ hoặc giữ lại n image tag gần nhất thì làm như thế nào?

Muốn xóa image cũ Quý khách cần truy cập vào vCR Console.  Xem hướng dẫn truy cập tại đây [https://docs.vngcloud.vn/vng-cloud-document/vn/vcontainer-registry/bat-dau-voi-vcr](https://docs.vngcloud.vn/vng-cloud-document/vn/vcontainer-registry/bat-dau-voi-vcr).

Sau đó Quý khách vào chi tiết của repository muốn xóa image. Tại tab Images Quý khách nhấn vào tên  image muốn xóa và thực hiện xóa tất cả Artifacts của image đó bằng cách nhấn vào dấu ba chấm, chọn nút xóa. Sau khi xóa tất cả Artifacts thành công, Quý khách thực hiện xóa image đó. Như vậy Quý khách đã xóa image thành công. Còn các images không bị xóa sẽ vẫn tồn tại.

### \[vCR] Tại sao tôi không thể renew container registry của vCR

Vì vCR là dạng holding (không có thời gian kết thúc) nên không có tính năng renew.
