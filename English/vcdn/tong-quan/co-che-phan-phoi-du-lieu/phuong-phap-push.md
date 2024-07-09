# PUSH

**Input signal**:

* Initialize a Live Entrypoint to receive signals. Live Entrypoint supports multiple receiving points at different DCs and operates according to Active-Backup mechanism.

<figure><img src="../../../.gitbook/assets/image (148).png" alt=""><figcaption></figcaption></figure>

***

**Output signal**:

* Support HTTPS protocol: by default all CDNs created on the system support SSL on the CDN domain. However, customers can upload their own Certificate to use with any name (refer to the certificate management section).&#x20;
* Streaming via HLS with format: https:// //index.m3u8.
* Supports Adaptive Bitrate feature: The packaging system automatically combines channels with the same name with different qualities into ABR channels. Customers can create multiple Live Entrypoints and manage them through the portal interface.

<figure><img src="../../../.gitbook/assets/image (149).png" alt=""><figcaption></figcaption></figure>
