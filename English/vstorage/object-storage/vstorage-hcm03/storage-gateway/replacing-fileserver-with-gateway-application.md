# Replacing Fileserver with Gateway Application

One of the common applications of storage gateway is to use it as a file management storage, replacing traditional Fileserver solutions. In this scenario, the gateway is deployed on a server at GreenNode or on-premise to act as an intermediary for managing permissions and sharing data using available mechanisms such as SMB/NFS. User-uploaded data is cached at the gateway and simultaneously written to vStorage for long-term storage. Leveraging the cache helps achieve comparable latency to that of a traditional file server.

Your data is encrypted with AES-256 and primarily stored in vStorage, ensuring its safety through vStorage's security mechanisms, such as Replication on 3 different physical servers and the versioning feature to protect against data loss due to upload errors like overwrites from duplicate names or accidental deletions. Especially when your data is substantial, using the gateway and vStorage can significantly reduce storage costs, thanks to the lower cost of vStorage compared to storing on a conventional SSD drive.

**Model:**

<figure><img src="../../../../.gitbook/assets/image (225).png" alt=""><figcaption></figcaption></figure>

**Feature**

* Support for NFS, SMB.
* Access control with read/write permissions on each folder using SMB/NFS mechanisms.
* AES-256 encryption support at the gateway before transferring data to vStorage.
* Unlimited user permission assignments.
* High Availability (HA) gateway with an Active-Standby mechanism."

***

**Benefit:**

* Utilizing the gateway cache enables swift data access.
* The data synchronization process from the gateway to storage is entirely automatic.
* The synchronization takes place within the internal VNG network, without impacting the client's general internet connectivity.
* Storing data on object storage significantly reduces costs.
* In the event of a sudden increase in demand, you can scale the storage capacity of vStorage on the portal within 5 minutes with no service downtime.
* On-premise deployment is possible.

***

**Tips:**

* It is advisable to place the gateway on-premise to optimize costs, access speed, and overall user experience.
* The minimum configuration for the gateway should be 4 CPUs x 8 GB RAM x 100 SSD.
* SSD is utilized for caching data during user uploads, and the minimum SSD capacity should accommodate data from a single user upload.
* Depending on the concurrent user access (CCU), the CPU quantity should be configured accordingly, with 1 CPU capable of handling 3-5 CCU.
* For the best experience, the gateway's bandwidth (BW) should be set at a threshold of 1 Gbps.
* A single gateway should handle a maximum of 250 CCU (simultaneous upload/download) for optimal performance.
* Cloud-based gateways should only serve CCU demands <20.
* Additionally, you can enhance user experience by configuring additional SSD to allow the gateway to cache more data.

"To initialize the gateway and try it out, you can find detailed instructions here: [Storage gateway](https://docs.vngcloud.vn/display/VSEN/Storage+gateway)
