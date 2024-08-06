# Working with Log Agent

We use the standard **Kafka** log receiving protocol for vMonitor Platform Logs. Therefore, we support you in configuring push logs from all popular existing log agents such as filebeat, fluentd, logstash, rsyslog, vector, etc. If you are still wondering, our advice is to install **Filebeat** - lightweight and efficient. high functionality, or **Logstash** - with more complex log parsing needs.

| **Environment** | **Version**      | **Logstash VNG version has been tested for compatibility** | Filebeat VNG version **has been tested** for compatibility |
| --------------- | ---------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| Centos          | 7, 8             | logstash-8.6.2                                             | filebeat-8.7                                               |
| Debian          | 7,8,9            | logstash-8.6.2                                             | filebeat-8.7                                               |
| Ubuntu          | 14,16,18,20,22   | logstash-8.6.2                                             | filebeat-8.7                                               |
| Docker          | From 18 and up   | logstash-8.6.2                                             | filebeat-8.7                                               |
| Kubernetes      | From 1.18 and up | logstash-8.6.2                                             | filebeat-8.7                                               |
| Windows         | 2016, 2019, 2022 | logstash-8.6.2                                             | filebeat-8.7                                               |
