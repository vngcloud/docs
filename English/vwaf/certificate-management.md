# Certificate Management

### Overview

The **Certificates** section allows you to manage all SSL/TLS certificates used by applications protected by the WAF.

Certificates ensure secure HTTPS communication, protect data integrity, and prevent traffic from being intercepted or tampered with.

This module provides a centralized location to:

* View certificate status
* Upload custom certificates
* Assign certificates to applications
* Renew or replace expiring certificates

> **⚠️ Service change:** GreenNode has **discontinued free SSL/TLS certificates (Let's Encrypt)**. The _Get free certificate_ option is no longer available when adding a new certificate.
>
> * For new applications, please **upload your own SSL/TLS certificate**.
> * Free certificates **issued previously remain active**, still appear in the list with `Type = FREE`, and can still be assigned to applications.
> * GreenNode recommends **preparing a replacement certificate before the expiry date** of any free certificate still in use, to avoid HTTPS service disruption. Track the **Expire On** column in the certificate list.

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

#### Free Certificates _(no longer issued)_

> #### Free certificate _(no longer issued)_
>
> WAF previously supported automatic issuance of free certificates via Let's Encrypt. **This feature has been discontinued** — new free certificates can no longer be requested.
>
> * Certificates issued previously still appear in the list with `Type = FREE` and remain usable by applications.
> * When such a certificate approaches expiry, **upload a replacement certificate** (see _Uploaded certificates_).

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

Indicates whether the certificate is `UPLOADED` (a certificate uploaded by the Customer) or `FREE` (a free certificate issued before this feature was discontinued). New certificates are always of the `UPLOADED` type.

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

The option to request WAF to automatically issue a free certificate has been discontinued.

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

### Add Certificate – Form Fields

#### Domain (required)

Enter one or more domains for which the certificate will be issued or uploaded.

* Multiple domains can be separated by spaces or new lines
* Wildcard (`*`) domains are supported for uploaded certificate
