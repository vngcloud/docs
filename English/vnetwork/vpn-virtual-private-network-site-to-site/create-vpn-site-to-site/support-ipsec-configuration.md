# Support IPSEC Configuration

Currently, VPN site-to-site service supports almost all popular IPSEC configurations widely. User can reference the table below

#### Authenticated Encryption (AEAD) Algorithms <a href="#authenticated_encryption_aead_algorithms" id="authenticated_encryption_aead_algorithms"></a>

| Keyword      | Description                      | Note          |
| ------------ | -------------------------------- | ------------- |
| aes256gcm128 | 256 bit AES-GCM with 128 bit ICV | default value |
| aes192gcm128 | 192 bit AES-GCM with 128 bit ICV |               |
| aes128gcm128 | 128 bit AES-GCM with 128 bit ICV |               |
| aes256gcm96  | 256 bit AES-GCM with 96 bit ICV  |               |
| aes192gcm96  | 192 bit AES-GCM with 96 bit ICV  |               |
| aes128gcm96  | 128 bit AES-GCM with 96 bit ICV  |               |
| aes256gcm64  | 256 bit AES-GCM with 64 bit ICV  |               |
| aes192gcm64  | 192 bit AES-GCM with 64 bit ICV  |               |
| aes128gcm64  | 128 bit AES-GCM with 64 bit ICV  |               |
| aes256ccm128 | 256 bit AES-CCM with 128 bit ICV |               |
| aes192ccm128 | 192 bit AES-CCM with 128 bit ICV |               |
| aes128ccm128 | 128 bit AES-CCM with 128 bit ICV |               |
| aes256ccm96  | 256 bit AES-CCM with 96 bit ICV  |               |
| aes192ccm96  | 192 bit AES-CCM with 96 bit ICV  |               |
| aes128ccm96  | 128 bit AES-CCM with 96 bit ICV  |               |
| aes256ccm64  | 256 bit AES-CCM with 64 bit ICV  |               |
| aes192ccm64  | 192 bit AES-CCM with 64 bit ICV  |               |
| aes128ccm64  | 128 bit AES-CCM with 64 bit ICV  |               |
| aes256       | 256 bit AES-CBC                  |               |
| aes192       | 192 bit AES-CBC                  |               |
| aes128       | 128 bit AES-CB                   |               |

#### Integrity Algorithms (Hashing) <a href="#integrity_algorithms" id="integrity_algorithms"></a>

_Hash is ignored with GCM algorithms_

| Keyword   | Description                   | isDefault     |
| --------- | ----------------------------- | ------------- |
| sha2\_256 | SHA2\_256\_128 HMAC (128 bit) | default value |
| sha2\_384 | SHA2\_384\_192 HMAC (192 bit) |               |
| sha2\_512 | SHA2\_512\_256 HMAC (256 bit) |               |
| sha       | SHA1 HMAC (96 bit)            | weak security |
| md5       | MD5 HMAC (96 bit)             | weak security |

#### Diffie Hellman Groups <a href="#diffie-hellman-groups" id="diffie-hellman-groups"></a>

| Keyworkd | Description   | Note          |
| -------- | ------------- | ------------- |
| modp8192 | 18 (8192 bit) |               |
| modp6144 | 17 (6144 bit) |               |
| modp4096 | 16 (4096 bit) |               |
| modp3072 | 15 (3072 bit) |               |
| modp2048 | 14 (2048 bit) | default value |
| modp1536 | 5 (1536 bit)  | weak security |
| modp1024 | 2 (1024 bit)  | weak security |
| modp768  | 1 (768 bit)   | weak security |
