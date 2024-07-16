# Using SwiftClient

#### Common usecase <a href="#usingswiftclient-commonusecase" id="usingswiftclient-commonusecase"></a>

**Get token**

> swift auth
>
> export OS\_STORAGE\_URL=[https://hcm.vstorage.vnglab.com/v1/AUTH\_afa7086fbef044938dbb7d8d328d452a](https://hcm.vstorage.vnglab.com/v1/AUTH\_afa7086fbef044938dbb7d8d328d452a)
>
> export OS\_AUTH\_TOKEN=gAAAAABjsYvUCXdVOkJo6EttO7WIVKrqnkbc2\_nUU59RGBbzsOo4rbSra5RayTBtC\_CJzosiJzZkOj77\_nqLt-NcaShU47ggANr8dm9TGvHTY48mphfnZPRyAuFFEr4LiG7zNlJBkOxqbBPR7kDbJIpuVKTodupASxhQAYgaKP0s20zE4C77kC8

When using the SwiftClient tool, it's possible to omit exporting OS\_STORAGE\_URL and OS\_AUTH\_TOKEN. However, the request time will be longer because for each request or operation, a new token needs to be obtained. Therefore, it is recommended to export these variables for reuse multiple times.

**Verify project(account)'s metadata information**

> swift stat
>
> Account: AUTH\_afa7086fbef044938dbb7d8d328d452a
>
> Containers: 6
>
> Objects: 4
>
> Bytes: 24351437
>
> Containers in policy "archive": 1
>
> Objects in policy "archive": 0
>
> Bytes in policy "archive": 0
>
> Containers in policy "gold": 4
>
> Objects in policy "gold": 4
>
> Bytes in policy "gold": 24351437
>
> Containers in policy "silver": 1
>
> Objects in policy "silver": 0
>
> Bytes in policy "silver": 0
>
> Meta Quota-Bytes: 10000000
>
> Meta Temp-Url-Key: tx71f555cc77df46afa6568-0063a286ee
>
> Meta My-Custom-Metadata: abc
>
> Vary: Accept
>
> X-Vngcloud-Backend: 03/backend\_hcm\_vstorage\_vnglab
>
> X-Account-Project-Domain-Id: default
>
> X-Timestamp: 1668228497.92635
>
> Accept-Ranges: bytes
>
> X-Trans-Id: tx1c351a6c5467473d8e823-0063b1a74c
>
> X-Openstack-Request-Id: tx1c351a6c5467473d8e823-0063b1a74c
>
> Server: vngcloud
>
> Connection: keep-alive
>
> Content-Type: text/plain; charset=utf-8

| **Key**                    | **Ý nghĩa**                                           |
| -------------------------- | ----------------------------------------------------- |
| Account                    | Account name                                          |
| Containers                 | Number of containers                                  |
| Objects                    | Number of objects                                     |
| Bytes                      | Bytes used in account                                 |
| Containers in policy "xxx" | Number of containers belong policy xxx                |
| Objects in policy "xxx"    | Number objects belong policy xxx                      |
| Bytes in policy "xxx"      | Bytes used belong policy xxx                          |
| Meta Quota-Bytes           | quota của account                                     |
| Meta Temp-Url-Key          | temp-url-key của account được dùng để tạo ra temp-url |
| Meta My-Custom-Metadata    | Một metadata tuỳ chọn do người dùng tự đặt            |

**Thiết lập metadata cho project (account)**

> swift post –m \<key:value>

**Xóa metadata cho project (account)**

> swift post -m \<key:>

**Thiết lập custom metadata (user metadata) cho project (account)**

> Swift post –m “my\_custom\_metadata:abc”

**Liệt kê danh sách các container thuộc một project (account)**

> swift list

**Tạo một container mới**

> swift post \<container\_name>

**Xóa container**

> swift delete container

**Truy xuất thông tin metadata của một container**

> swift stat my\_container
>
> \\
>
> Account: AUTH\_afa7086fbef044938dbb7d8d328d452a
>
> Container: my\_container
>
> Objects: 0
>
> Bytes: 0
>
> Read ACL:
>
> Write ACL:
>
> Sync To:
>
> Sync Key:
>
> Last-Modified: Sun, 01 Jan 2023 13:30:13 GMT
>
> Accept-Ranges: bytes
>
> Vary: Accept
>
> Server: vngcloud
>
> X-Storage-Policy: gold
>
> Connection: keep-alive
>
> X-Timestamp: 1672579812.82240
>
> X-Trans-Id: tx0caa6b4d82d54f9c95548-0063b18b1a
>
> X-Container-Sharding: False
>
> Content-Type: text/plain; charset=utf-8
>
> X-Openstack-Request-Id: tx0caa6b4d82d54f9c95548-0063b18b1a
>
> X-Vngcloud-Backend: 03/backend\_hcm\_vstorage\_vnglab

**Thiết lập metadata cho container**

> swift post container -m \<key:value>

**Liệt kê danh sách các object của một container**

> swift list \<container\_name>

**Upload object lên một container**

> swift upload \<container\_name> \[--object-name \<object-name>] \<local\_file\_or\_directory>

**Upload một large object (multipart upload) lên một container**

> swift upload \<container\_name> \<object\_name> --segment-size \<size>
>
> swift upload container large\_file --segment-size 50M

**Download object từ một container**

> swift download \<container\_name> \<object\_name>

**Xóa một object trong container**

> swift delete \<container\_name> \<object\_name>

**Thiết lập metadata cho một object**

> swift post \<container\_name> \<object\_name> -m "\<metadata>:\<value>"

**Xóa metadata của một object**

> swift post \<container\_name> \<object\_name> -m "\<metadata>:"

***

#### Một số use case nâng cao <a href="#usingswiftclient-motsousecasenangcao" id="usingswiftclient-motsousecasenangcao"></a>

**Tạo (generate) tempURL link**

Tạo tempURL là kỹ thuật tạo ra đường dẫn public cho một object có hiệu lực trong một khoảng thời gian nhất định nhằm chia sẻ quyền truy cập object mà không cần phải công khai thông tin đăng nhập như username, password, secret key. Sử dụng tính năng tạo tempURL do SwiftClient cung cấp như sau để tạo ra các PUT/ GET tempURL.

> swift tempurl --help
>
> swift tempurl \<method> \<time> \<path> \<tempurl\_key>

**Ví dụ tạo ra GET tempURL để download một object**

> swift tempurl GET 3600 /v1/AUTH\_afa7086fbef044938dbb7d8d328d452a/container/file1 tx71f555cc77df46afa6568-0063a286ee
>
> → /v1/AUTH\_afa7086fbef044938dbb7d8d328d452a/container/file1?temp\_url\_sig=1fe9fbcdb9d6683eef8658a18aa97c7090525cec\&temp\_url\_expires=1672595887

**Sử dụng GET tempURL link được sinh ra ở trên để download object**

> wget "[https://hcm.vstorage.vnglab.com/v1/AUTH\_afa7086fbef044938dbb7d8d328d452a/container/file1?temp\_url\_sig=1fe9fbcdb9d6683eef8658a18aa97c7090525cec\&temp\_url\_expires=1672595887](https://hcm.vstorage.vnglab.com/v1/AUTH\_afa7086fbef044938dbb7d8d328d452a/container/file1?temp\_url\_sig=1fe9fbcdb9d6683eef8658a18aa97c7090525cec\&temp\_url\_expires=1672595887)"
>
> \--2023-01-01 23:58:42-- [https://hcm.vstorage.vnglab.com/v1/AUTH\_afa7086fbef044938dbb7d8d328d452a/container/file1?temp\_url\_sig=1fe9fbcdb9d6683eef8658a18aa97c7090525cec\&temp\_url\_expires=1672595887](https://hcm.vstorage.vnglab.com/v1/AUTH\_afa7086fbef044938dbb7d8d328d452a/container/file1?temp\_url\_sig=1fe9fbcdb9d6683eef8658a18aa97c7090525cec\&temp\_url\_expires=1672595887)
>
> Resolving [hcm.vstorage.vnglab.com](http://hcm.vstorage.vnglab.com/) ([hcm.vstorage.vnglab.com](http://hcm.vstorage.vnglab.com/))... 61.28.228.48
>
> Connecting to [hcm.vstorage.vnglab.com](http://hcm.vstorage.vnglab.com/) ([hcm.vstorage.vnglab.com](http://hcm.vstorage.vnglab.com/))|61.28.228.48|:443... connected.
>
> HTTP request sent, awaiting response... 200 OK
>
> Length: 12174069 (12M) \[application/octet-stream]
>
> Saving to: ‘file1?temp\_url\_sig=1fe9fbcdb9d6683eef8658a18aa97c7090525cec\&temp\_url\_expires=1672595887’
>
> \\
>
> file1?temp\_url\_sig=1fe9 100%\[===============================>] 11.61M 16.1MB/s in 0.7s
>
> \\
>
> 2023-01-01 23:58:43 (16.1 MB/s) - ‘file1?temp\_url\_sig=1fe9fbcdb9d6683eef8658a18aa97c7090525cec\&temp\_url\_expires=1672595887’ saved \[12174069/12174069]

\\

Tương tự ta có thể tạo đường dẫn tạm để cho user upload bằng cách đổi method thành "PUT".

**Thiết lập ACLs cho một container**

Để thiết lập ACLs cho một container, chúng tôi khuyến nghị bạn nên thực hiện tính năng này thông qua vStorage portal. Để thiết lập ACLs cho container qua vStorage portal, vui lòng tham khảo ở [đây](https://docs.vngcloud.vn/pages/viewpage.action?pageId=59803945). Tuy nhiên, bạn có thể sử dụng công cụ người dùng SwiftClient để thiết lập ACLs cho một container sử dụng lệnh sau của SwiftClient:

> swift post \<container> -H “\<X-Container-Write| X-Container-Read>:\<value>”

Trong đó, biến \<Value> nhận các giá trị trong bảng sau:

| **Value**                                                                                                                                 | **Description**                                                                                                                                                                                                                                                                                                                                                                          |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| .r:\*                                                                                                                                     | Any user has access to objects. No token is required in the request.                                                                                                                                                                                                                                                                                                                     |
| <p>.r:&#x3C;referrer></p><p>(Exp: .r: <a href="http://example.org/referring_page">http://example.org/referring_page</a>)</p>              | <p>The referrer is granted access to objects. The referrer is identified by the Referer request header in the request. No token is required.</p><p>Exp:</p><p><br></p><p>GET /wiki/Referrer HTTP/1.1 Host: <a href="http://de.wikipedia.org/">http://de.wikipedia.org</a> Referer: <a href="http://example.org/referring_page">http://example.org/referring_page</a></p>                 |
| <p>.r:-&#x3C;referrer></p><p>(Exp: .r: -<a href="http://example.org/referring_page">http://example.org/referring_page</a>)</p><p><br></p> | <p>This syntax (with “-” prepended to the referrer) is supported. However, it does not deny access if another element (e.g., .r:*) grants access.</p><p>Exp:</p><p><br></p><p>GET /wiki/Referrer HTTP/1.1 Host: <a href="http://de.wikipedia.org/">http://de.wikipedia.org</a> Referer: <a href="http://example.org/referring_page">http://example.org/referring_page</a></p><p><br></p> |
| .rlistings                                                                                                                                | Any user can perform a HEAD or GET operation on the container provided the user also has read access on objects (e.g., also has .r:\* or .r:\<referrer>. No token is required.                                                                                                                                                                                                           |

Để hiểu thêm về ACLs của container, vui lòng tham khảo [https://docs.openstack.org/swift/latest/overview\_acl.html](https://docs.openstack.org/swift/latest/overview\_acl.html).

{% hint style="info" %}
**Chú ý:**

* Không nên sử dụng phiên bản SwiftClient quá cũ trên các hệ điều hành có phiên bản quá cũ hoặc mới nhất vì có thể gặp lỗi.
* SwiftClient Không gây ra incomplete segment (segment rác) trong quá trình tải object lớn (multipart upload).
{% endhint %}
