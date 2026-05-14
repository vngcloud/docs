# Add a UDP Listener

Use this guide to add a new UDP listener to an existing Network Load Balancer (NLB).

#### Steps to Add a New UDP Listener

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer where you want to add the new listener.
3. **Go to the Listener Tab:** In the Load Balancer details page, select the "Listener" tab.
4. **Click "Add New Listener":** A pop-up window will appear, allowing you to configure the listener's information.
5. **Configure Listener Settings:**
   * **Listener Name:** Note that the listener name cannot be changed after creation.
   * **Protocol & Port:** Select the UDP protocol and choose a port (the default is port 53, and it will increment if lower ports are already in use).
   * **Default Pool and Action:** In cases where requests to the Load Balancer don't match any specific pool, the NLB will redirect that traffic to the default pool.
   * **Advanced Configuration:** Refer to the guides below for advanced configuration options:
     * Configuring Timeouts
     * Configuring IP Whitelists for Load Balancers

**Important Note:** You can only select a Pool with the UDP protocol as the default pool for a UDP Listener.

#### Additional Notes

* **Listener Names:** Choose descriptive names for your listeners to easily identify their purpose.
* **Port Selection:** If you're using the default port 53 (commonly used for DNS), ensure no other services are running on that port within your VPC.
* **Default Pool:** The default pool acts as a fallback for requests that don't match any specific routing rules.
* **Advanced Configurations:** Explore timeout and IP whitelisting options to fine-tune your listener's behavior.
