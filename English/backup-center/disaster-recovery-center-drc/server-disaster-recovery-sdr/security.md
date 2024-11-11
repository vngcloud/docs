# Security

Security is an important factor in deploying and using the Disaster Recovery Center (DRC) service. Ensuring the safety of your data and systems during replication and recovery is essential to avoid risks of data loss, unauthorized access, and other security issues. Below are some important guidelines and security measures to keep in mind when using DRC:

**1. Access Control**

* **Access and Authorization Management (IAM):** Use VNG Cloud's IAM features to tightly control access to DRC and related resources. Grant only necessary access to individual users or groups of users based on their roles and responsibilities.
* **Strong passwords and multi-factor authentication (MFA):** Make sure to use a strong password for your VNG Cloud account and enable multi-factor authentication for added security.
* **SSH Key Management:** Use SSH keys to securely access primary and backup servers, avoiding the use of traditional passwords.

**2. Data Encryption**

* **Encryption at rest:** Data is stored on VNG Cloud's secure cloud storage systems, using advanced encryption technologies to protect data at rest.

**3. Network Segmentation & Security**

* **Use VPC (Virtual Private Cloud):** Create separate VPCs for primary and backup servers to isolate them from other resources in the cloud, minimizing the risk of attacks and unauthorized access.
* **Security Group Configuration:** Use Security Groups to control traffic flow in and out of the primary and backup servers. Allow only necessary connections and from trusted IP addresses.
* **Use a Firewall:** Consider using a Firewall to enhance network security, detect and prevent cyber attacks.

**4. Monitoring & Alerting**

* **Activity Tracking:** Use VNG Cloud's monitoring tools to track DRC activity and related resources.
* **Set up alerts:** Create alerts to receive timely notifications when unusual events or suspicious activities occur.
* **Log Analysis:** Regularly check and analyze logs to detect potential security issues.

**5. Security Policy and Procedures**

* **Develop Security Policy:** Develop and enforce clear security policies for the use of DRC, including provisions for access management, data encryption, backup and recovery.
* **Employee Training:** Train employees on security measures and how to use DRC safely.
* **Perform periodic testing:** Conduct periodic security tests to evaluate the effectiveness of security measures and detect potential vulnerabilities.

**Important Note:**

* Always update to the latest patches and versions of software and operating systems to patch known security vulnerabilities.
* Perform periodic backups of critical data and store backups in a secure location, separate from production systems.
* In the event of a security incident, take timely response measures to minimize damage and restore the system.
