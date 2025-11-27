# Volume Types

Volume type is profile for performance of volume. VNG Cloud using Volume Type to implement data QoS on volume. Volume QoS can control the bandwidth and IOPS workload on your volume, you must chose right QoS for your application to have best experience.

## Volume QoS <a href="#volumetypes-volumeqos" id="volumetypes-volumeqos"></a>

IOPS measures the number of read/write operations that can be performed per second. High IOPS is critical for transaction-intensive applications such as database applications. The following table describes all IOPS profiles:

| **Volume Type** | **IOPS max** | **Disk Type** | **Descriptions**                |
| --------------- | ------------ | ------------- | ------------------------------- |
| 200             | 200          | SSD           | <p><br></p>                     |
| 400             | 400          | SSD           | <p><br></p>                     |
| 800             | 800          | SSD           | <p><br></p>                     |
| 1000            | 1000         | SSD           | <p><br></p>                     |
| 1200            | 1200         | SSD           | <p><br></p>                     |
| 1600            | 1600         | SSD           | <p><br></p>                     |
| 3000            | 3000 shared  | SSD           | Shared IOPS with other customer |
| 3200            | 3200         | SSD           | <p><br></p>                     |
| 6400            | 6400         | SSD           | <p><br></p>                     |
| 10000           | 10000        | SSD           | <p><br></p>                     |
| custom          | custom       | SSD           | <p><br></p>                     |

You can change Volume Type at any time.

<br>
