# Upload a certificate

To use SSL certificates, you must either have an existing SSL certificate or use a free SSL certificate provided by Let's Encrypt. VNG Cloud stores certificates securely; the storage system is encrypted, and certificates are inaccessible to anyone, including VNG Cloud employees.

The Certificate Manager supports uploading and managing two types of certificates:

* **TLS/SSL Certificates**
* **CA Certificates**

#### 1. Uploading TLS/SSL Certificates

1. **Access the Certificate Manager:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/certificate`.
2. **Click "Upload Certificate":** A pop-up window will appear for you to enter certificate information.
3. **Fill in Certificate Details:**
   * **Friendly Name:** We recommend using the domain name as the friendly name.
   * **Certificate Type:** Select "TLS/SSL."
   *   **Certificate Input:**

       * **Certificate Content:** Paste your server certificate domain (usually with the \*.crt extension) in PEM format.

       ![](<../../../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)

       * **Private Key:** Paste the private key of the certificate (usually with the \*.key extension) in PEM format.

       &#x20;![](<../../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)

       * **Certificate Chain:** Paste the certificate chain, including the server certificate and any intermediate certificates (if applicable), in PEM format.
         *   **Important:** Ensure the chain is in the correct order:

             ```
             ---BEGIN CERTIFICATE--- [Your certificate] ---END CERTIFICATE---
             ---BEGIN CERTIFICATE--- [Intermediate#1 certificate] (optional) ---END CERTIFICATE---
             ---BEGIN CERTIFICATE--- [Intermediate#2 certificate] (optional) ---END CERTIFICATE---
             ```
   * **Passphrase:** If the private key has a passphrase, enter it here. Otherwise, leave this field blank.
   * **Expiration:** The expiration date of the certificate.
4. **Click "Upload":** Click the "Upload" button in the bottom right corner to complete the upload.

#### 2. Uploading CA Certificates

1. **Access the Certificate Manager:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/certificate`.
2. **Click "Upload Certificate":** A pop-up window will appear for you to enter certificate information.
3. **Fill in Certificate Details:**
   * **Friendly Name:** We recommend using the domain name as the friendly name.
   * **Certificate Type:** Select "CA."
   *   **Certificate Input:**

       * **Certificate Content:** Paste your CA certificate (usually with the \*.crt extension) in PEM format.&#x20;

       ![](<../../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)
   * **Expiration:** The expiration date of the certificate.
4. **Click "Upload":** Click the "Upload" button in the bottom right corner to complete the upload.
