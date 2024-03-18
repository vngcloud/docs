# Upload Certificates

#### **SSL Certificate Configuration** <a href="#uploadcertificates-sslcertificateconfiguration" id="uploadcertificates-sslcertificateconfiguration"></a>

To be able to use an SSL certificate, you must have an existing SSL certificate or use a free SSL certificate provided by Let's Encrypt. The certificates are stored by VNG CLOUD in a secure, safe place, the certificate storage system is encrypted and cannot be accessed by anyone including VNG CLOUD employees.

There are two ways to create a Certificate:

* Certificate management page
* Created on Listener initialization

#### Access the Certificate management page: <a href="#uploadcertificates-accessthecertificatemanagementpage" id="uploadcertificates-accessthecertificatemanagementpage"></a>

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802687/image2020-5-11_11-23-38.png?version=1&#x26;modificationDate=1685075613000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

To create a new certificate, click **UPLOAD CERTIFICATE.**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802687/image2020-5-11_15-6-6.png?version=1&#x26;modificationDate=1685075613000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


Enter the information:

* Friendly Name: The name of the Certificate.
* Certificate: is your server certificate domain (usually with the extension \*.crt), in the standard PEM format.

&#x20;               &#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802687/image2020-5-11_15-52-15.png?version=1&#x26;modificationDate=1685075613000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Private Key: is the private key of the above certificate (usually with the extension \*.key), in the standard PEM format.

&#x20;              &#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802687/image2020-5-11_15-51-38.png?version=1&#x26;modificationDate=1685075614000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Certificate Chain: is a chain of certificates including server certificate and intermediate certificate (if any), in standard PEM format.

&#x20;              &#x20;

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802687/image2020-5-11_15-53-12.png?version=1&#x26;modificationDate=1685075614000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

&#x20;            _Note that the order of adding chain will be as follows:_

&#x20;            \---BEGIN CERTIFICATE---\
&#x20;            \[Your certificate]\
&#x20;            \---END CERTIFICATE---\
&#x20;            \---BEGIN CERTIFICATE---\
&#x20;            \[Intermidate#1 certificate]\(option)\
&#x20;            \---END CERTIFICATE---\
&#x20;            \---BEGIN CERTIFICATE---\
&#x20;           \[Intermidate#2 certificate]\(option)\
&#x20;            \---END CERTIFICATE---

* Passphrase: in case the private key has a password, you need to enter the password of the private key, otherwise leave this field blank.
* Expiration: Expiration date of Certificate.

After entering all the certificate information, click **IMPORT**.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802687/image2020-5-11_14-57-29.png?version=1&#x26;modificationDate=1685075614000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


On the SSL Certificate management page as above, you will now see a list of the Certificates that have been uploaded, along with the certificate's creation and expiration date.
