# Chứng thực với Service Account

Để sử dụng vStorage APIs, người dùng sẽ sử dụng khóa **client ID** và **client secret** để được chứng thực thông qua máy chủ ([https://iamapis.vngcloud.vn/accounts-api/v2/auth/token](https://iamapis.vngcloud.vn/accounts-api/v2/auth/token)) dùng phương thức OAuth2.

**Header**

> 'Authorization':'Basic Base64(clientID:clientSecret)'

**Request body**

> 'grant\_type':'client\_credentials'&#x20;
>
> 'scope':'email'

**Response**

> 'token\_type':'bearer'\
> 'access\_token':'koxoQrfdAhCFIRl1Sy897kRuHcOlswcW'\
> 'expires\_in':7200

Nếu thông tin đăng nhập được xác thực, một **access\_token** sẽ được trả về. Người dùng sẽ sử dụng **access\_token** để truy cập tài nguyên.



**Ví dụ:**

> curl -X POST 'https://iamapis.vngcloud.vn/accounts-api/v2/auth/token'\
> -H 'Content-Type: application/json'\
> -H 'Authorization: Basic ZGM3MTYxNTYtMjQwMi00MDg2LTliYWItZGU5OTIxODVlYjU1OmJhYjYzYTZmLWYzOGUtNDZmNC05NjIyLTYzNTQwNGQ4MDFlNQ=='\
> -d '{ "grant\_type": "client\_credentials", "scope":"email" }'
>
>
>
> {"token\_type":"Bearer","access\_token":"eyJhbGciOiJSUz......GWug","expires\_in":1800,"refresh\_expires\_in":0}

