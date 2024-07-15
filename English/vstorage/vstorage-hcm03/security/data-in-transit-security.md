# Data in Transit Security

In-transit encryption is an effective and widely used data security solution. By encrypting data in transit, the data is transformed into a form that is unreadable to those without access. This helps protect data from unauthorized access during transmission over a network. In the case of Object Storage, in-transit encryption is typically implemented using HTTPS. HTTPS is a secure protocol based on HTTP that uses TLS/SSL encryption to protect data in transit.

Both S3 and OpenStack Swift support HTTPS. However, S3 and Swift also have some mechanisms related to subdomains. For example, S3 allows users to create buckets with subdomain names. In this case, SSL will require more certificates to be issued to accommodate the diverse name and domain structures that users need to interact with.

Here are some of the benefits of using in-transit encryption to secure data on vStorage:

* **Helps protect data from unauthorized access:** In-transit encryption helps protect data from unauthorized access during transmission over a network. This helps reduce the risk of data breaches.
* **Helps ensure data integrity:** In-transit encryption helps ensure that data is not changed or modified during transmission. This helps protect data from being tampered with or altered.
* **Helps meet regulatory requirements:** Many regulations require the use of encryption to protect sensitive data. By using in-transit encryption, businesses can meet these regulatory requirements.
