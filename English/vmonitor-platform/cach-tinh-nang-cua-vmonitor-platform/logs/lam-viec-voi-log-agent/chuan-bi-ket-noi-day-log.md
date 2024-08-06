# Prepare to initiate log push connection

**Connect from the log pusher to the vMontior Platform system.**

| **Source**    | **Destination**                                                                                                                                                                                            | **Port**  |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| Log pusher IP | Subnet range: 116.118.93.130/28, i.e. 116.118.93.128 -> 116.118.93.143                                                                                                                                     | 10092 TCP |
| Log pusher IP | Domain: [hcm01-loghub01.vngcloud.vn ](http://hcm01-loghub01.vngcloud.vn/)[hcm02-loghub01.vngcloud.vn ](http://hcm02-loghub01.vngcloud.vn/)[hcm03-loghub01.vngcloud.vn](http://hcm03-loghub01.vngcloud.vn/) | 10092 TCP |

* The above connection needs to be open during the agent pushing logs

If the machines need to collect logs, some machines cannot open a direct connection. Refer to using the [collector](https://opentelemetry.io/docs/collector/) model to push through an intermediate host.

***

**Domain resolution**

Because the transmission channel data is **secured** by SSL encryption standard. If the log pusher is capable of querying public DNS, there is no problem. However, if not (which may occur in an on-premise environment), you need to add domain resolution according to the following table:

| <pre><code># IP---------------| Domain
116.118.93.131      hcm01-loghub01.vngcloud.vn 
116.118.93.132      hcm02-loghub01.vngcloud.vn 
116.118.93.133      hcm03-loghub01.vngcloud.vn
116.118.93.134      hcm04-loghub01.vngcloud.vn
116.118.93.135      hcm05-loghub01.vngcloud.vn
116.118.93.136      hcm06-loghub01.vngcloud.vn
</code></pre> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
