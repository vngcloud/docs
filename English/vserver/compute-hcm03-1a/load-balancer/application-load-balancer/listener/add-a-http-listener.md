# Add a HTTP listener

Use this guide to add a new HTTP listener to an existing Application Load Balancer (ALB).

#### Steps to Add a New HTTP Listener

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer where you want to add the new listener.
3. **Go to the Listener Tab:** In the Load Balancer details page, select the "Listener" tab.
4. **Click "Add New Listener":** A pop-up window will appear, allowing you to configure the listener's information.
5. **Configure Listener Settings:**
   * **Listener Name:** Note that the listener name cannot be changed after creation.
   * **Protocol & Port:** Select the HTTP protocol and choose a port (the default is port 80, and it will increment if lower ports are already in use).
   * **Request Header Configuration (Advanced):** The default headers are X-Forwarded-For, X-Forwarded-Proto, and X-Forwarded-Port. You can deselect these if they are not needed.
   * **Default Pool and Action:** If incoming requests to the listener are not covered by configured policies, they will be directed to the default pool for processing.
   * **Advanced Configuration:** Refer to the guides below for advanced configuration options:
     * Configuring Timeouts
     * Configuring IP Whitelists for Load Balancers

#### Additional Notes

* **Listener Names:** Choose descriptive names for your listeners to easily identify their purpose.
* **Port Selection:** If you're using the default port 80, ensure that no other services are running on that port within your VPC.
* **Request Headers:** The X-Forwarded headers provide valuable information to your backend servers about the original client's IP address and protocol.
* **Default Pool:** The default pool acts as a fallback for requests that don't match any specific routing rules.
* **Advanced Configurations:** Explore the timeout and IP whitelisting options to fine-tune your listener's behavior.
