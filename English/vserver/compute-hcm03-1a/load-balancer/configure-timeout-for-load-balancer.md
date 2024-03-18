# Configure Timeout for Load Balancer

One of the high features of HCM 03 is allowing users to customize the "timeout" for the Load Balancer (LB).

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802731/timoutLB.jpg?version=1&#x26;modificationDate=1685081820000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

In the  Listener  section we are allowed to customize the following "timeout" related parameters:

* client: Inactivity time from client to LB is in seconds. This value is limited from 1 to 3600 seconds.
* Member: Inactivity time from LB to member is in seconds. This value is limited from 1 to 3600 seconds.
* Connection: Timeout for creating connections to members. This value is limited from 1 to 3600 seconds.

\
