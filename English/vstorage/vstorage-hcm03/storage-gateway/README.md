# Storage gateway

#### Overview <a href="#storagegateway-overview" id="storagegateway-overview"></a>

Storage Gateway is a service that provides a connection gateway between customers' physical infrastructure and storage services in the cloud. Storage Gateway supports standard storage protocols such as NFS, SMB, and CIFS. With VNG Cloud's Storage Gateway, customers can perform configurations effortlessly through a web portal interface instead of dealing with complex commands.

Deployment Model of Storage Gateway

![](https://docs.vngcloud.vn/download/attachments/69468523/image2021-4-20\_11-18-23.png?version=1\&modificationDate=1703557377000\&api=v2)

\


* Storage Gateway is built on either one vServer or on-premise server.
* The Storage Gateway acts as an intermediary between end-users and vStorage for upload/download tasks. Data resides on the cache (block disk), enabling quick access for end-users.
* Data is automatically synchronized to vStorage for optimal long-term cost-effective storage.
* Data from the gateway is encrypted before being transferred to vStorage.

***

#### Topic <a href="#storagegateway-topic" id="storagegateway-topic"></a>

From this Storage Gateway deployment model, we provide features that you can utilize, including:

* [Create and use Storage Gateway](https://docs-admin.vngcloud.vn/display/VSEN/Create+and+use+Storage+Gateway?src=contextnavpagetreemode)
* [Replacing Fileserver with Gateway Applicatio](https://docs-admin.vngcloud.vn/display/VSEN/Replacing+Fileserver+with+Gateway+Application?src=contextnavpagetreemode)
