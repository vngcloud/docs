# Data Security stored on vStorage

Encrypting the content of stored files (objects) is an effective data security solution. By encrypting data at rest, the data is transformed into a form that cannot be read by those without access. This helps protect data from unauthorized access, even if an attacker can access the system's storage gateway.

VNG Cloud currently provides the following mechanisms for encrypting the content of stored files (objects) on the vStorage service:

* **Client-side encryption:** In this mechanism, the user is responsible for managing the key and workload of the encryption process. Data will be encrypted on the user's machine or application layer.
* **Server-side encryption:** In this mechanism, VNG Cloud is responsible for managing the key and workload of the encryption process. Data will be encrypted before being stored on VNG Cloud's storage system.
