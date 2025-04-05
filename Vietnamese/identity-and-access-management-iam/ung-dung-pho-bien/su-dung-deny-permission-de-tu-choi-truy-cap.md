# Sử dụng Deny permission để từ chối truy cập

Khi có nhu cầu phân quyền truy cập cho phép tất cả action chỉ trừ một vài action cụ thể, bạn cần tạo Policy và sử dụng Deny Permission để đơn giản hoá trong việc phân quyền . Ở hướng dẫn này chúng tôi sẽ hướng dẫn bạn **phân quyền cho phép User: System1 được thực hiện tất cả action của vServer (Full Access), nhưng không cho phép thực hiện action:Delete trên Resource:server**, **để đảm bảo User: System1 không xoá bất kì servers nào**.&#x20;

Để thiết lập IAM theo mô hình trên chúng ta sẽ có các bước như sau:

**Bước 1**: Tạo User: System1 nếu chưa có User Account (lưu ý rằng nếu đã có sẵn User: System1, cần đảo bảo User: System1 không có quyền gì hoặc không có các quyền chồng lấn với hướng dẫn)

**Bước 2**: Tạo Policy với tên vServerFullAccessExceptDeleteServer cho phép truy cập toàn bộ Resource của vServer, nhưng không cho phép Delete Server&#x20;

**Bước 3**: Gắn Policy: vServerFullAccessExceptDeleteServer cho User: System1

**Bước 4**: Đăng nhập và kiểm tra quyền của User: System1

Chi tiết các bước như sau

**Bước 1: Tạo User: System1 nếu chưa có User Account (lưu ý rằng nếu đã có sẵn User: System1, cần đảo bảo User: System1 không có quyền gì hoặc không có các quyền chồng lấn với hướng dẫn)**

Tiến hành tạo User Account bằng cách truy cập vào tab User Account ở trang quản lý IAM tại [đây](https://hcm-3.console.vngcloud.vn/iam/user-accounts), nhấn **Create a User Account,** điền thông tin Username và Password, sau đó nhấn **Create User Account**&#x20;

Sau khi tạo thành công User Account, sẽ được liệt kê ở trang User Account.

**Bước 2: Tạo Policy với tên vServerFullAccessExceptDeleteServer cho phép truy cập toàn bộ Resource của vServer, nhưng không cho phép Delete Server**&#x20;

Để tạo Policy bạn qua tab Policy ở trang IAM tại [đây](https://hcm-3.console.vngcloud.vn/iam/policies), nhấn **Create a Policy**, **đặt tên** cho Policy: **vServerFullAccessExceptDeleteServer** và nhấn **Next step**

Nhấn chọn JSON để chuyển sang chế độ JSON và tạo Policy với đoạn JSON có sẵn

Sử dụng đoạn JSON dưới đây và sao chép vào Policy

| <pre class="language-json"><code class="lang-json"><strong>{
</strong>    "statements": [
        {
            "effect": "allow",
            "actions": [
                "vserver:*"
            ],
            "resources": [
                "*"
            ],
            "condition": {}
        },
        {
            "effect": "deny",
            "actions": [
                "vserver:DeleteServer"
            ],
            "resources": [
                "*"
            ],
            "condition": {}
        }
    ]
}
</code></pre> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

Nhấn **Create policy** để tạo Policy

**Bước 3**: Gắn Policy: vServerFullAccessExceptDeleteServer cho User: System1

Sau khi tạo thành công Policy: vServerFullAccessExceptDeleteServer, bạn tiến hành gắn Policy này cho User: System1, bạn có thể thực hiện ở User Account hoặc Policy, ở đây chúng tôi sẽ hướng dẫn ở Policy, **nhấn vào tên của Policy** để vào trang chi tiết Policy

**Chọn tab Policy usage** và **nhấn Attach** để thêm User: System1

**Chọn User: System1** và **nhấn Add**

**Bước 4**: Đăng nhập và kiểm tra quyền của User: System1

Lúc này bạn có thể đăng nhập vào User: System1 để kiểm tra quyền

Truy cập vào vServer tại [đây](https://hcm-3.console.vngcloud.vn/vserver/v-server/cloud-server), khi chưa đăng nhập bất kì tài khoản nào bạn sẽ được chuyển hướng sang trang sign-in chọn "**Sign-in With IAM User Account**"

Điền thông tin root user account email mà User: System1 trước đó đã được tạo, thông tin IAM username và password của User: System1, nhấn **Sign-in with IAM User Account**

Lúc này bạn sẽ thấy User: System1 sẽ có toàn quyền trên vServer nhưng không thể xoá được bất kì Resource: server nào



Như vậy là bạn đã hoàn thành việc phân quyền cho phép User: System1 được thực hiện tất cả action của vServer (Full Access), nhưng không cho phép thực hiện action:Delete trên Resource:server, để đảm bảo User: System1 không xoá bất kì servers nào.

\
