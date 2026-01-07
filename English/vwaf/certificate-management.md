# Certificate Management

### Overview

The **Certificates** section allows you to manage all SSL/TLS certificates used by applications protected by the WAF.

Certificates ensure secure HTTPS communication, protect data integrity, and prevent traffic from being intercepted or tampered with.

This module provides a centralized location to:

* View certificate status
* Issue free certificates
* Upload custom certificates
* Assign certificates to applications
* Renew or replace expiring certificates

***

### Certificates Overview

The certificate listing page displays all certificates associated with your account.

For each certificate, the following information is shown:

* Certificate ID
* Certificate type (Free or Uploaded)
* Domain name(s)
* Applications using the certificate
* Issuer
* Expiration date
* Available actions

This overview helps administrators quickly assess SSL/TLS status across all WAF-protected applications.

***

### Certificate Types

#### Free Certificates (Auto-issued)

Free certificates are automatically issued by the WAF using the **Let’s Encrypt** certificate authority with the **HTTP-01** validation method.

Key characteristics:

* No cost
* Automatically renewed **30 days before expiration**
* Requires domain DNS A record pointing to the WAF public IP
* No manual handling of private keys or certificate files

***

#### Uploaded Certificates

Uploaded certificates allow users to provide their own SSL/TLS certificates.

This option is suitable for:

* Enterprise or internal Certificate Authorities (CA)
* EV certificates
* Wildcard certificates
* Multi-domain certificates

When uploading a certificate, you must provide:

* Private key
* Certificate chain (PEM format)

***

### Certificates List – Columns Explained

#### ID

Unique identifier of the certificate.

#### Type

Indicates whether the certificate is **FREE** or **UPLOADED**.

#### Domain

The domain or domains covered by the certificate.

#### Applications

Lists all WAF applications currently using the certificate.

#### Issued By

Shows the certificate authority or internal system that issued the certificate.

#### Expire On

Displays the expiration date and time of the certificate.

Certificates approaching expiration should be renewed promptly to avoid service disruption.

#### Action

Provides management options, such as:

* View
* Renew / Replace
* Delete

***

### Add Certificate

The **Add Certificate** page allows you to add a new SSL/TLS certificate to the WAF.

You can either upload your own certificate or request a free auto-issued certificate.

***

### Choose Certificate Type

#### Upload your cert

Select this option to upload your own SSL certificate.

You will be required to upload:

* Private key file
* Certificate file
* (Optional) Intermediate certificate chain

Supported format: **PEM**

***

#### Get free cert

Select this option to let the WAF automatically issue a free certificate via **Let’s Encrypt**.

***

### ⚠️ Important – Before Getting a Free Certificate

**Before requesting a free certificate for a domain, you MUST complete the following steps:**

* **Create the application first** in the WAF **using the same domain**.
* Configure the application with **port 80 (HTTP)** enabled.
* **Do NOT attach any SSL certificate** to the application at this stage.
* Ensure the domain’s **DNS A record is pointing to the WAF public IP address `103.7.174.2`**.
* Wait for DNS propagation to complete.

These steps are **mandatory** for **Let’s Encrypt HTTP-01 validation**.\
If the application is not created with **port 80 and no certificate**, the free certificate issuance will fail.

***

### Add Certificate – Form Fields

#### Domain (required)

Enter one or more domains for which the certificate will be issued or uploaded.

* Multiple domains can be separated by spaces or new lines
* Wildcard (`*`) domains are supported for uploaded certificates

***

#### Email Address

_(Required for free certificates)_

Used for:

* Let’s Encrypt notifications
* Domain ownership and issuance communication

***

### Verification Requirements (Free Certificates)

The following requirements are enforced during certificate issuance:

* All domains must have their DNS A record pointing to the WAF public IP: `103.7.174.2`
* Domain must be publicly reachable
* WAF performs Let’s Encrypt **HTTP-01** validation
* Certificates are automatically renewed before expiration

If DNS configuration or connectivity is incorrect, the certificate cannot be issued.
