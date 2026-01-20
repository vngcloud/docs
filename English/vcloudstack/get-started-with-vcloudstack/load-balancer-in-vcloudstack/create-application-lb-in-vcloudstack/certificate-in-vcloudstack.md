# Certificate in vCloudstack

GreenNode provides Certificate Manager, allowing users to upload and manage their certificates. We support the management of 2 main types of certificates:

* **TLS/SSL Certificate**
* **CA Certificate**

**1. TLS/SSL Certificate:**

* **A TLS/SSL Certificate** is a digital document containing information about a website or server's public key and authentication credentials. They are used to establish a secure connection between a user's computer and a web server, ensuring the confidentiality and integrity of data transmitted over the network.
* **What TLS/SSL Certificates Do:** TLS/SSL certificates ensure that information such as passwords, personal data, and financial transactions are encrypted and protected against security threats. They also verify the authenticity of the web server, letting users know they are visiting the right website and not a fake one.
* **TLS/SSL Certificate Types:** There are many types of TLS/SSL certificates, including free certificates, self-signed certificates, and certificates issued by a certificate authority (CA).

**2. CA (Certificate Authority) Certificate:**

* **A Certificate Authority (CA)** is an organization or company responsible for issuing, validating, and managing TLS/SSL Certificates. A CA is a trusted party that verifies and ensures the authenticity of entities requesting TLS/SSL Certificates.
* **Function of CA Certificate:** CA Certificate authenticates the identity of websites and servers by signing and issuing TLS/SSL Certificates. It ensures that the information in the TLS/SSL Certificate is authentic and secure.
* **Characteristics of CA Certificates:** Major CAs are widely trusted and recognized by web browsers and computer systems. When a website uses a TLS/SSL Certificate issued by a CA, the browser displays a padlock icon or authenticates the website, creating trust for users.

***

### **Certificate Upload Instructions** <a href="#huong-dan-tai-len-certificate" id="huong-dan-tai-len-certificate"></a>

#### 1/ Instructions for uploading TLS/SSL Certificate <a href="#uploadacertificate-1.huongdantailentls-sslcertificate" id="uploadacertificate-1.huongdantailentls-sslcertificate"></a>

* Access Certificate Manager
* Click the "Upload Certificate" button
* A pop-up interface window allows you to fill in the Certificate information, including
  * **Reminder Name** : Encourage using domain name as reminder name
  * **Select TLS/SSL Certificate Type**
  * **Fill in Certificate Input including** :
    * **Certificate content:** Is your domain Server Certificate (usually has the extension \*.crt), in standard PEM format
    * **Private Key Information:** Is the private key of the above certificate (usually has the extension \*.key), in standard PEM format
  *   **Fill in Certificate Chain:** The certificate chain includes the server certificate and intermediate certificate (if any), in standard PEM format.

      _Note the order of adding chain will be as follows:_

      \---BEGIN CERTIFICATE--- \[Your certificate] ---END CERTIFICATE--- ---BEGIN CERTIFICATE--- \[Intermidate#1 certificate]\(option) ---END CERTIFICATE--- ---BEGIN CERTIFICATE--- --- \[Intermidate#2 certificate]\(option) ---END CERTIFICATE---
  * **Passphrase** : In case the private key has a password, you need to enter the password of the private key, otherwise leave this field blank.
  * **Expiration** : Certificate expiration date.
* Click the "Upload" button at the bottom right corner of the interface window to complete the upload.

#### 2. Instructions for uploading CA Certificate <a href="#id-2.-huong-dan-tai-len-ca-certificate" id="id-2.-huong-dan-tai-len-ca-certificate"></a>

* Access Certificate Manager
* Click the "Upload Certificate" button
* A pop-up interface window allows you to fill in the Certificate information, including
  * **Reminder Name** : Encourage using domain name as reminder name
  * **Select CA Certificate Type**
  * **Fill in Certificate Input including** :
    * **Certificate Content:** Is your domain Server Certificate (usually has the extension \*.crt), in standard PEM format.
    * **Expiration** : Certificate expiration date.
* Click the "Upload" button at the bottom right corner of the interface window to complete the upload.
