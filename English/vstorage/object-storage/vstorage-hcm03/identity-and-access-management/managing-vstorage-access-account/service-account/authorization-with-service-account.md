# Authorization with Service Account

To use the vStorage APIs, users will use the client ID and the client secret keys to be authorized via the authorization server ([https://iamapis.vngcloud.vn/accounts-api/v2/auth/token](https://iamapis.vngcloud.vn/accounts-api/v2/auth/token)) using the OAuth2 method.

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

If the credentials are authorized, an **access\_token** will be returned. Users will use this **access\_token** to access resources from the resource server.



**Example:**

> curl -X POST 'https://iamapis.vngcloud.vn/accounts-api/v2/auth/token'\
> -H 'Content-Type: application/json'\
> -H 'Authorization: Basic ZGM3MTYxNTYtMjQwMi00MDg2LTliYWItZGU5OTIxODVlYjU1OmJhYjYzYTZmLWYzOGUtNDZmNC05NjIyLTYzNTQwNGQ4MDFlNQ=='\
> -d '{ "grant\_type": "client\_credentials", "scope":"email" }'
>
>
>
> {"token\_type":"Bearer","access\_token":"eyJhbGciOiJSUz......GWug","expires\_in":1800,"refresh\_expires\_in":0}

