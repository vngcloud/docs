---
description: >-
  Rate Limit is a mechanism used to control the number of requests or tokens
  within a specified period of time. It helps protect the system from abuse,
  ensures fairness when multiple users share the
---

# Rate Limit

### 1. Access the Rate Limit Feature <a href="#id-1.-truy-cap-tinh-nang-gioi-han-rate" id="id-1.-truy-cap-tinh-nang-gioi-han-rate"></a>

1. After creating an Authentication Token, navigate to the token list and select the icon in the **Action** column, as illustrated below, to open the Rate Limit configuration panel.

<figure><img src="../../../.gitbook/assets/image (483).png" alt=""><figcaption></figcaption></figure>

2. Or you may select **Configure Rate Limit** directly when creating an Authentication Token.

<figure><img src="../../../.gitbook/assets/image (484).png" alt=""><figcaption></figcaption></figure>

### 2. Create a New Rate Limit Configuration <a href="#id-2.-tao-moi-rate-limit-token" id="id-2.-tao-moi-rate-limit-token"></a>

1. Limit by (Select one or both options)

* **Requests**: Set a limit for the number of API requests.
  * Minimum: 1 request
  * Maximum: 1,000,000 requests
  * Supported time windows:
    * 1 Minute
    * 1 Hour
    * 1 Day
    * 1 Month
  * **Window Time Type:** Currently supports **Fixed Window** only.
* **Tokens**: Set a limit for the number of tokens consumed
  * Minimum: 100 tokens
  * Maximum: 5,000,000,000 tokens
  * Supported time windows:
    * 1 Minute
    * 1 Hour
    * 1 Day
    * 1 Month
  * **Window Time Type:** Currently supports **Fixed Window** only.

### 3 Nhấn **Lưu** cấu hình.

<figure><img src="../../../.gitbook/assets/image (485).png" alt=""><figcaption></figcaption></figure>
