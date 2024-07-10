# Manage Certificate vCDN

Support Customers to upload SSL Cert and SSL Key including ChainCA key

<figure><img src="../../.gitbook/assets/image (203).png" alt=""><figcaption></figcaption></figure>

After logging in, click on “Certificate” as shown below.

<figure><img src="../../.gitbook/assets/image (204).png" alt=""><figcaption></figcaption></figure>

The Certificate management interface appears with a list of certificates including the following columns:&#x20;

* Domain,&#x20;
* Issuer (Name of certificate issuer),&#x20;
* Valid From (Validity period of the certificate),&#x20;
* Expires On (Certificate Expiration),&#x20;
* CDN Using (Number of CDNs using this certificate, click to see details),&#x20;
* Status: The status of the certificate is being activated or deactivated&#x20;
* Action buttons include Edit (Update certificate) and Delete (Delete certificate)&#x20;
* At the top of the page, summary information about the number of certificates (Total), the number of certificates that are being activated and ready to use (Active) and the number of certificates that have been temporarily deactivated (Inactive).&#x20;
* To add/upload a certificate, click the “Upload” button, the certificate upload interface will be as follows:

<figure><img src="../../.gitbook/assets/image (205).png" alt=""><figcaption></figcaption></figure>

(1): Click Upload Private Key to upload the Certificate's private key, or you can also paste the private key into the textbox below.&#x20;

(2): Upload Certificate to upload the CRT/PEM file of the Certificate.&#x20;

(3): Upload CA Root Chain to upload certificate information of the certificate provider. Can be left blank if no information is available.\*

_Some older browser versions may report an invalid Certificate error if CA Root Chain information is missing._&#x20;

After entering/uploading all information, click "Save and Deploy"(5) to save and activate the certificate, ready for CDNs to use. If the certificate is not ready to use immediately, click “Save as Draf”(4) to save it.

{% hint style="info" %}
**Note:**

* vCDN provided by VNG Cloud is a content distribution service via HTTP protocol that supports TLS/SSL (HTTPS). Therefore, TLS Certificates - uploaded by customers for the purpose of encrypting the HTTP transmission channel between the user and the CDN server system - are simultaneously stored and managed by the customer and VNG Cloud until the customer execute the delete command through the Web Portal/API interface.&#x20;
* VNG Cloud commits not to share these TLS Certificates with any third party.
{% endhint %}
