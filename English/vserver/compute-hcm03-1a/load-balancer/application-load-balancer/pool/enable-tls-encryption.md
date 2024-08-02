# Enable TLS encryption

The "Enable TLS Encryption" feature is a crucial aspect of network security, allowing you to protect data transmitted from the Load Balancer to your backend servers. When enabled, transmitted data is encrypted and secured throughout the transmission process.

#### How It Works

1. **Client Connection:** When a client connects to the Load Balancer and requests access to your website or application, the data transmitted between the client and the Load Balancer is encrypted using the TLS (Transport Layer Security) protocol before being forwarded to the backend server.
2. **Backend Server Support:** The backend server also needs to support TLS to decrypt the data sent from the Load Balancer.
3. **Secure Transmission:** This process ensures that the transmitted data cannot be intercepted or understood if it is captured during transmission.

#### Benefits of Enabling TLS Encryption

* **High Security:** TLS Encryption provides a high level of security for your data, helping to prevent man-in-the-middle attacks and data theft.
* **Secure Integration:** It allows you to provide a secure experience for your customers by protecting their personal and account information as it's transmitted to the Load Balancer.
* **Reliability:** TLS Encryption offers reliability in data transmission over the network, ensuring that data is not lost or altered during transmission from the Load Balancer to the backend server.
* **Allows Self-Signed Certificates:** The TLS Encryption feature supports both HTTP and HTTPS. For HTTPS, when this feature is enabled, the Load Balancer will not verify the validity of the SSL/TLS certificate. This allows you to use self-signed certificates on your member servers.

#### How to Enable TLS Encryption

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer you want to configure.
3. **Go to the Pool Tab:** In the Load Balancer details page, select the "Pool" tab.
4. **Edit Pool:** Hover over the pool you want to modify and click the "Edit" icon.
5. **Edit Pool Window:** A pop-up window will appear, allowing you to edit the pool settings.
6. **Toggle TLS Encryption:** In the pool information section, find the "Enable TLS Encryption" checkbox. Check or uncheck it to enable or disable TLS encryption.
7. **Save Changes:** Click "Save" in the bottom right corner of the window to finalize your changes.
