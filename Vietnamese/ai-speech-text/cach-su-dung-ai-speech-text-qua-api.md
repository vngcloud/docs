# Cách sử dụng AI Speech Text qua API

### Bước 1: Tạo Policy có quyền với ai-stt-tts

* Truy cập portal IAM tại [https://iam.console.vngcloud.vn/policies](https://iam.console.vngcloud.vn/policies)
* Chọn Create a Policy
* Chọn các action thuộc product ai-stt-tts

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Bước 2: Tạo Service Account có quyền với ai-stt-tts

* Truy cập giao diện quản lý IAM của hệ thống tại [https://iam.console.vngcloud.vn/service-accounts](https://iam.console.vngcloud.vn/service-accounts)
* Tạo một service account mới và attach policy vừa cấp quyền ai-stt-tts
* Sau khi tạo xong, bạn sẽ nhận được:
  * `client_id`&#x20;
  * `client_secret`  &#x20;

> > Hai giá trị này sẽ được dùng để lấy `access_token`. Bạn hãy nhớ lưu Secret Key lại.

<figure><img src="../.gitbook/assets/image (7) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Bước 3: Thực hiện encode Service Account thành Token

Chạy lệnh

```
echo -n 'clientID:secretId' | base64
```

Ví dụ:

```
echo -n 'cdfecb82-9c5b-4af7-84fc-03f9dff03547:b0459f5f-dab4-49b5-be0b-e501c372ea93' | base64
```

Kết quả trả về như sau:&#x20;

```
echo -n 'cdfecb82-9c5b-4af7-84fc-03f9dff03547:b0459f5f-dab4-49b5-be0b-e501c372ea93' | base64
Y2RmZWNiODItOWM1Yi00YWY3LTg0ZmMtMDNmOWRmZjAzNTQ3OmIwNDU5ZjVmLWRhYjQtNDliNS1iZTBiLWU1MDFjMzcyZWE5Mw==
```

### Bước 4: Lấy Token

Lấy token qua request:&#x20;

```json
curl --location 'https://iamapis.vngcloud.vn/accounts-api/v2/auth/token' \
--header 'Authorization: Basic <<Chuỗi encode>>'
--header 'Content-Type: application/json' \
--data '{
    "grant_type":"client_credentials",
    "scope":"email"
}'
```

&#x20;Ví dụ:

```
curl --location 'https://iamapis.vngcloud.vn/accounts-api/v2/auth/token' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic Y2RmZWNiODItOWM1Yi00YWY3LTg0ZmMtMDNmOWRmZjAzNTQ3OmIwNDU5ZjVmLWRhYjQtNDliNS1iZTBiLWU1MDFjMzcyZWE5Mw==' \
--data '{
    "grant_type": "client_credentials"
}'
```

Kết quả trả về:

```
{"token_type":"Bearer","access_token":"eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJlckVaZFpkNkRsc21pdjhsMDZIaVB3bHZYWnotLVlGYXlZcVJiczlxc09rIn0.eyJleHAiOjE3NTA4MzY4ODIsImlhdCI6MTc1MDgzNTA4MiwianRpIjoiOWU2Njk3ZmYtYzU4Yi00YjFkLTk4NjgtMDA3ZGYyM2UwMWM5IiwiaXNzIjoiaHR0cHM6Ly9zaWduaW4udm5nY2xvdWQudm4vYXV0aC9yZWFsbXMvaWFtIiwic3ViIjoiZWJiYTY3MTctNzAyMC00MzlhLTkwMDMtZjMwOTQ2MjcyZmFjIiwidHlwIjoiQmVhcmVyIiwiYXpwIjoiY2RmZWNiODItOWM1Yi00YWY3LTg0ZmMtMDNmOWRmZjAzNTQ3Iiwic2NvcGUiOiIiLCJjbGllbnRIb3N0IjoiMTAuMTY2LjIuOSIsImF1dGhBY2NvdW50SWQiOjUzNDYxLCJjbGllbnRBZGRyZXNzIjoiMTAuMTY2LjIuOSIsImNsaWVudF9pZCI6ImNkZmVjYjgyLTljNWItNGFmNy04NGZjLTAzZjlkZmYwMzU0NyIsImF1dGhVc2VyVHlwZSI6InVzZXItc2EifQ.SKoTm4n9kqQJrRerE0OYKzKIEa3GKyfraTvahtyGSojh055Pgo9LxmmJgOO4-mex3DKArb4jhtAPsXvWOll0gVSe_rJ1AE2ixYPzAlDAxBxguqq7en8mSUcW3yGVY0nyXdNJ-TwwE7maXDg2ATVjKSwU6s2Y-tRRDbuWlpSFA_pV1hpZH4zkBLp21B7OhR-KeUC3os1Y2etyunwHmdNNplm-Y16natrJpixQ3v1G5ObxYocn1zuDiB2I0XhMb7Svngy0jYoNKyHgt3Y8MDUTorq2HEYWXk5pAx-i6ygP-s7N_TlV2bjJPxH6YmuMTh8QpY7lxA2-13oWP8Vx4m16gw","expires_in":1800,"refresh_expires_in":0}
```

### &#x20;Bước 5: Gọi AP tới TTS, STT với Access Token

Sau khi đã có `token`, bạn có thể gọi API tới TTS, STT qua API qua lệnh:

```
curl --request POST \
  --url https://ai-speech-text.api.vngcloud.vn/speech-api/api/v1/texttospeech/sync \
  --header 'Authorization: Bearer REPLACE_BEARER_TOKEN' \
  --header 'content-type: application/json' \
  --data '{"input":"đầu vào","speed":1,"speaker_id":1,"encode_type":0}'
```

&#x20;Ví dụ:

```
curl --request POST \
  --url https://ai-speech-text.api.vngcloud.vn/speech-api/api/v1/texttospeech/sync \
  --header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJlckVaZFpkNkRsc21pdjhsMDZIaVB3bHZYWnotLVlGYXlZcVJiczlxc09rIn0.eyJleHAiOjE3NTA4MzY4ODIsImlhdCI6MTc1MDgzNTA4MiwianRpIjoiOWU2Njk3ZmYtYzU4Yi00YjFkLTk4NjgtMDA3ZGYyM2UwMWM5IiwiaXNzIjoiaHR0cHM6Ly9zaWduaW4udm5nY2xvdWQudm4vYXV0aC9yZWFsbXMvaWFtIiwic3ViIjoiZWJiYTY3MTctNzAyMC00MzlhLTkwMDMtZjMwOTQ2MjcyZmFjIiwidHlwIjoiQmVhcmVyIiwiYXpwIjoiY2RmZWNiODItOWM1Yi00YWY3LTg0ZmMtMDNmOWRmZjAzNTQ3Iiwic2NvcGUiOiIiLCJjbGllbnRIb3N0IjoiMTAuMTY2LjIuOSIsImF1dGhBY2NvdW50SWQiOjUzNDYxLCJjbGllbnRBZGRyZXNzIjoiMTAuMTY2LjIuOSIsImNsaWVudF9pZCI6ImNkZmVjYjgyLTljNWItNGFmNy04NGZjLTAzZjlkZmYwMzU0NyIsImF1dGhVc2VyVHlwZSI6InVzZXItc2EifQ.SKoTm4n9kqQJrRerE0OYKzKIEa3GKyfraTvahtyGSojh055Pgo9LxmmJgOO4-mex3DKArb4jhtAPsXvWOll0gVSe_rJ1AE2ixYPzAlDAxBxguqq7en8mSUcW3yGVY0nyXdNJ-TwwE7maXDg2ATVjKSwU6s2Y-tRRDbuWlpSFA_pV1hpZH4zkBLp21B7OhR-KeUC3os1Y2etyunwHmdNNplm-Y16natrJpixQ3v1G5ObxYocn1zuDiB2I0XhMb7Svngy0jYoNKyHgt3Y8MDUTorq2HEYWXk5pAx-i6ygP-s7N_TlV2bjJPxH6YmuMTh8QpY7lxA2-13oWP8Vx4m16gw' \
  --header 'content-type: application/json' \
  --data '{"input":"đầu vào","speed":1,"speaker_id":1,"encode_type":0}'
```

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;
