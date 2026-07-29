# Data Security stored on vStorage

Encrypting the content of stored files (objects) is an effective data-security solution. By encrypting data at rest, the data is transformed into a form unreadable to anyone without access rights, protecting it from unauthorized access even if an attacker can reach the system's storage gateway.

GreenNode currently provides the following mechanism for encrypting the content of files (objects) stored on the vStorage service:

* **Client-side encryption:** the user is responsible for managing the key and the encryption workload. Data is encrypted on the user's machine or at the user's application layer.

Therefore, if a customer wants to encrypt the content of files (objects) stored on GreenNode's vStorage service, GreenNode recommends using the client-side encryption mechanism.
