---
description: VNG Cloud Endpoint là điểm kết nối giữa VPC với các dịch vụ của VNG Cloud
---

# Tạo mới Endpoint

## How to create

{% hint style="danger" %}
**Lưu ý quan trọng:**

_<mark style="color:blue;">Tại cùng một region, tương ứng với một VPC người dùng có thể tạo được nhiều Endpoint, tuy nhiên để sử dụng được Endpoint, người dùng phải</mark>_ [_<mark style="color:blue;">AddHost</mark>_](tao-moi-endpoint.md#how-to-use) _<mark style="color:blue;">để có thể sử dụng Endpoint mong muốn</mark>_
{% endhint %}

* Người dùng login vào  [https://hcm-3-vnetwork.console.vngcloud.vn/endpoint/list](https://hcm-3-vnetwork.console.vngcloud.vn/endpoint/list)  với region = HCM
* Chọn menu “**Endpoint**” tại thanh menu bên trái màn hình
* Chọn chức năng “**Create an Endpoint**”
* Nhập thông tin **Endpoint** theo yêu cầu gồm:

&#x20;         \- **Tên Endpoint**: Tên Endpoint

&#x20;         \- **Chọn dịch vụ**: Chọn một dịch vụ của VNG Cloud mà Endpoint kết nối đến trong danh sách các dịch vụ vServer, vStorage, vMonitor, vCR, IAM.     &#x20;

&#x20;         \- **Service Package**: Gói dịch vụ Endpoint cung cấp mặc định cấu hình 1 gói Standard, người dùng không cần chọn gói dịch vụ

* Chọn VPC, Subnet muốn kết nối với các dịch vụ của VNG Cloud qua service endpoint
* Kiểm tra thông tin giá dịch vụ tại “**Summary**”
* Nhấn “**CREATE ENDPOINT**”

&#x20;Người dùng sẽ chờ hệ thống tạo Endpoint cho đến khi hoàn tất. Khi Endpoint được tạo thành công, trên màn hình danh sách Endpoint, người dùng thấy Endpoint xuất hiện tại đây.



## How to use <a href="#how-to-use" id="how-to-use"></a>

After creating Endpoint, users still cannot access Endpoint Service, do some steps below to config your Servers' access Eto ndpoint Service privately

**Access the Endpoint List and Select your Endpoint**

At detail, page will provide two main information

* Endpoint Url: This is the Public URL of the Endpoint Service
* Endpoint IP: Use this IP to add a host in the Servers that need to go with private

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FMmsmN65yCpwVKxtPZwUL%252Fimage.png%3Falt%3Dmedia%26token%3Dd2b58bd9-7cad-4166-8c77-bed404188907&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c2e20add&#x26;sv=2" alt=""><figcaption><p>Endpoint List</p></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252Fk9wUuwK8MUUV9Hw4gq1k%252Fimage.png%3Falt%3Dmedia%26token%3Da9294a84-308a-40d3-b0c4-0afa2acbdf03&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=a45880d0&#x26;sv=2" alt=""><figcaption><p>Endpoint Detail</p></figcaption></figure>

**Add host and Try to access Endpoint Url**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FH7ovuNeYajOMMFAW87q3%252Fimage.png%3Falt%3Dmedia%26token%3Da1f68119-95fc-46aa-b0db-c9ae80d2ba14&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1e34008f&#x26;sv=2" alt=""><figcaption><p>Add host</p></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F1985221522-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F7rE7M1L7GYcwQzNGd0aB%252Fuploads%252FedY062hUCSIow53Eb8lO%252Fimage.png%3Falt%3Dmedia%26token%3D2c362fdd-1732-4715-a0fd-2fd07c668c02&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=4c94202b&#x26;sv=2" alt=""><figcaption><p>Result</p></figcaption></figure>
