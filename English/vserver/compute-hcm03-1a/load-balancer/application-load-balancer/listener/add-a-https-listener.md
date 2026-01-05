# Add a HTTPS listener

Use this guide to add a new HTTPS listener to an existing Application Load Balancer (ALB).

#### Steps to Add a New HTTPS Listener

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer where you want to add the new listener.
3. **Go to the Listener Tab:** In the Load Balancer details page, select the "Listener" tab.
4. **Click "Add New Listener":** A pop-up window will appear, allowing you to configure the listener's information.
5. **Configure Listener Settings:**
   * **Listener Name:** Note that the listener name cannot be changed after creation.
   * **Protocol & Port:** Select the HTTPS protocol and choose a port (the default is port 443, and it will increment if lower ports are already in use).
   * **Default Certificate:** Choose the default SSL/TLS certificate for the listener.
   * **SNI Certificates (Optional):** Select additional certificates to use for Server Name Indication (SNI). Note that you cannot remove or change SNI certificates after creating the HTTPS listener.
   * **Request Header Configuration (Advanced):** The default headers are X-Forwarded-For, X-Forwarded-Proto, and X-Forwarded-Port. You can deselect these if they are not needed.
   * **Client Certificate Authentication (Optional):** Enable client certificate authentication to add an extra layer of security by requiring client-side SSL/TLS certificates. Learn more about Client Certificate Authentication.
   * **Default Pool and Action:** If incoming requests to the listener are not covered by configured policies, they will be directed to the default pool for processing.
   * **Advanced Configuration:** Refer to the guides below for advanced configuration options:
     * Configuring Timeouts
     * Configuring IP Whitelists for Load Balancers

#### Additional Notes

* **Certificate Management:** Ensure you have valid SSL/TLS certificates uploaded to your GreenNode account before creating an HTTPS listener.
* **SNI (Server Name Indication):** SNI allows you to host multiple HTTPS websites on a single Load Balancer using different domain names and certificates.
* **Client Certificate Authentication:** This feature is useful for applications that require strong client authentication.
* **Default Pool:** As with HTTP listeners, the default pool serves as a fallback for requests that don't match any specific routing rules.
* **Advanced Configurations:** Explore the timeout and IP whitelisting options to fine-tune your listener's behavior.
