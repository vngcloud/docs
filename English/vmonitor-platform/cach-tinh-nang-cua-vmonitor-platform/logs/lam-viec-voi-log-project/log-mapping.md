# Log mapping

Centralizing logs from different technologies and applications can create dozens or hundreds of different attributes in a log management environment, especially when multiple teams are working in the same environment.

For example, Host server name information can have many other names such as beat.hostname, hostname, host, syslog.hostname,...

To unify the names for these properties, use Log mapping. Log mapping is pre-defined by us through common properties including:

| **Portal reserved attributes** | **System fields**                                                                                 |
| ------------------------------ | ------------------------------------------------------------------------------------------------- |
| Nội dung                       | message, request.body                                                                             |
| Date                           | date, Timestamp, @timestamp, syslog.timestamp, eventTime, published\_date, \_timestamp, timestamp |
| Host                           | beat.hostname, hostname, host, syslog.hostname                                                    |
| Service                        | fields.service, service, syslog.appname                                                           |

If you would like to add mapping for a certain property, please contact us. Adding this Log mapping attribute can be accommodated by us if your mapping attribute is reasonable through our review.
