# Storage gateway

Storage Gateway is a service that provides a connection gateway between customers' physical infrastructure and storage services in the cloud. Storage Gateway supports standard storage protocols such as NFS, SMB, and CIFS. With GreenNode's Storage Gateway, customers can perform configurations effortlessly through a web portal interface instead of dealing with complex commands.

Deployment Model of Storage Gateway:

<figure><img src="../../../../.gitbook/assets/image (29) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Storage Gateway is built on either one vServer or on-premise server.
* The Storage Gateway acts as an intermediary between end-users and vStorage for upload/download tasks. Data resides on the cache (block disk), enabling quick access for end-users.
* Data is automatically synchronized to vStorage for optimal long-term cost-effective storage.
* Data from the gateway is encrypted before being transferred to vStorage.
