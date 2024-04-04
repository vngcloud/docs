# Chuẩn bị kết nối đẩy log

#### Kết nối từ máy đẩy log tới hệ thống vMontior Platform.

| **Nguồn**      | **Đích**                                                                                                                                                                                                                                           | **Port**  |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| IP máy đẩy log | <p>Dải subnet:<br>61.28.234.80/28, tức<br>61.28.234.81 --> 61.28.234.94</p>                                                                                                                                                                        | 10092 TCP |
| IP máy đẩy log | <p>Domain:<br><a href="http://hcm01-loghub01.vngcloud.vn">hcm01-loghub01.vngcloud.vn</a> <a href="http://hcm02-loghub01.vngcloud.vn">hcm02-loghub01.vngcloud.vn</a> <a href="http://hcm03-loghub01.vngcloud.vn">hcm03-loghub01.vngcloud.vn</a></p> | 10092 TCP |

* Kết nối trên cần mở trong suốt quá trình agent đẩy log

Nếu các máy cần thu thập log có máy không thể mở kết nối trực tiếp trên. Tham khảo sử dụng mô hình [collector](https://opentelemetry.io/docs/collector/) để đẩy qua một host trung gian.

***

#### Phân giải domain

Do dữ liệu kênh truyền được **bảo mật** bằng chuẩn mã hóa SSL. Nếu máy đẩy log có khả năng truy vấn DNS public thì không vấn đề gì. Tuy nhiên nếu không (có thể gặp trong môi trường on-premise) thì bạn cần thêm phân giải domain theo bảng sau:

| <pre><code># IP---------------| Domain
61.28.234.82       hcm01-loghub01.vngcloud.vn 
61.28.234.83       hcm02-loghub01.vngcloud.vn 
61.28.234.84       hcm03-loghub01.vngcloud.vn
61.28.234.89       hcm04-loghub01.vngcloud.vn
61.28.234.90       hcm05-loghub01.vngcloud.vn
61.28.234.91       hcm06-loghub01.vngcloud.vn
</code></pre> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

\
