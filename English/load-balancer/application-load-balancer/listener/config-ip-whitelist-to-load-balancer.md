# Config IP whitelist to load balancer

The IP Source Whitelist feature is an essential part of network security. It allows you to define specific source IP addresses from which the Load Balancer will accept traffic. Any IP addresses not included in the allowed range will be denied access.

#### How It Works

1. **IP Address Check:** When a request reaches the Load Balancer, the system checks the source IP address of the request.
2. **Whitelist Comparison:** If the source IP address is within the allowed CIDR ranges, the request is accepted and forwarded to the backend servers.
3. **Access Denied:** If the source IP address is not within the allowed CIDR ranges, the request is denied and not forwarded.

#### Why Configure IP Whitelists?

* **Enhanced Security:** This feature strengthens security by tightly controlling access from unknown or unauthorized source IP addresses.
* **Attack Prevention:** It helps prevent attacks from suspicious or unwanted IP addresses.
* **Access Management:** IP whitelisting allows you to manage access to your Load Balancer in a granular and effective way.

#### Configuration Instructions

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer you want to configure.
3. **Go to the Listener Tab:** In the Load Balancer details page, select the "Listener" tab.
4. **Edit Listener:** Click the "Edit" icon next to the listener you want to configure.
5. **Advanced Configuration:** In the pop-up window, scroll down to the "Advanced Configuration" section.
6. **Allowed CIDRs:** In the "Allowed CIDRs" field, enter the IP ranges that are permitted to access the Load Balancer.
   * **Example:** Entering "192.168.0.0/24, 172.16.0.0/24" means only IP addresses within these two ranges will be allowed access.
7. **Save Changes:** Click "Save" in the bottom right corner of the window to finalize your changes.

#### Additional Notes

* **CIDR Notation:** Use Classless Inter-Domain Routing (CIDR) notation to specify IP ranges (e.g., 192.168.1.0/24).
* **Multiple Ranges:** You can enter multiple CIDR ranges, separated by commas.
* **Security Best Practices:** Regularly review and update your IP whitelists to ensure they reflect your current security requirements.
