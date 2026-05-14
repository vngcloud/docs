# Client Certificate Authentication

"Client Certificate Authentication" is a crucial part of network and application security. It allows you to ensure that only clients or devices with valid certificates can access your applications or services.  &#x20;

[1. What is Client Certificate Authentication - Portnox](https://www.portnox.com/cybersecurity-101/client-certificate-authentication/)[![Biểu tượng nguồn](https://encrypted-tbn3.gstatic.com/favicon-tbn?q=tbn:ANd9GcTh8IjI048UPQ9K3INIzEV9YcRXy6zg2ErB1cZsvHs\_qCDmnod-GW3rr2YJFQPo-i3fFwwYy1C7xOqevL0FxY5DVv5eZ8myJPmr)www.portnox.com](https://www.portnox.com/cybersecurity-101/client-certificate-authentication/)

#### How It Works

1. **Certificate Request:** When a client or device attempts to access your application, the system requests a unique digital certificate for authentication.
2.  **Certificate Issuance:** This certificate is typically generated and managed by a Certificate Authority (CA) or a Public Key Infrastructure (PKI).  &#x20;

    [1. What is Certificate-Based Authentication? - InstaSafe](https://instasafe.com/glossary/what-is-certificate-based-authentication/)[![Biểu tượng nguồn](https://encrypted-tbn1.gstatic.com/favicon-tbn?q=tbn:ANd9GcTG\_P6DyXgZSbZoYDKQdUOotlZ2L5CSJkDV7dvUoReRHg7wKB3FONZ4r6lzdvMSLpFXnWzOzmUq3w8KejK\_cT3ks9IYS5lClw)instasafe.com](https://instasafe.com/glossary/what-is-certificate-based-authentication/)
3. **Certificate Validation:** The system verifies the certificate to ensure it is valid and can identify the client or device.
4. **Access Granted (or Denied):** If the certificate is valid, the client or device is granted access to the application or service. If not, access is denied.

#### Benefits

*   **Enhanced Security:** Certificate authentication provides a strong layer of security by ensuring that only identified and authorized users or devices can access your resources.  &#x20;

    [1. What is Client Certificate Authentication - Portnox](https://www.portnox.com/cybersecurity-101/client-certificate-authentication/)[![Biểu tượng nguồn](https://encrypted-tbn3.gstatic.com/favicon-tbn?q=tbn:ANd9GcTh8IjI048UPQ9K3INIzEV9YcRXy6zg2ErB1cZsvHs\_qCDmnod-GW3rr2YJFQPo-i3fFwwYy1C7xOqevL0FxY5DVv5eZ8myJPmr)www.portnox.com](https://www.portnox.com/cybersecurity-101/client-certificate-authentication/)
* **Granular Access Control:** You can manage access for each client or device based on their individual certificates, allowing for fine-grained permissions.
* **Compliance:** It helps you comply with strict security regulations and standards that often require strong authentication mechanisms.

#### How to Enable/Disable Client Certificate Authentication

For HTTPS listeners, you can easily enable or disable Client Certificate Authentication at any time.

**Steps to Enable/Disable Client Certificate Authentication:**

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer you want to modify.
3. **Go to the Listener Tab:** In the Load Balancer details page, select the "Listener" tab.
4. **Edit HTTPS Listener:** Click the "Edit" icon next to the HTTPS listener where you want to enable/disable Client Certificate Authentication.
5. **Advanced Settings:** In the pop-up window, locate the "Advanced Settings" section.
6. **Toggle Client CA:** Check or uncheck the "Enable Client CA" checkbox. If you enable it, you'll need to select a certificate from the list of available certificates in your system.
7. **Save Changes:** Click "Save" in the bottom right corner of the window to finalize your changes.
