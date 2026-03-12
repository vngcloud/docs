# Edit Access Methods

## Access Control for Kafka Cluster

Access Method options and functions

* **mTLS (Mutual TLS):** Ensures high security by requiring both client and server to authenticate each other through digital certificates. This helps prevent unauthorized connections and protect sensitive data.
* **SASL (Simple Authentication and Security Layer):** Provides a flexible user authentication mechanism, allowing the use of different authentication methods such as username/password.
* **Public Accessibility:** Allows access from outside your VPC (Virtual Private Cloud), for example from other applications not within the vDB Kafka Cluster. This option is typically used when you need to integrate Kafka with external services.

## Edit Public Accessibility

**1. Select Kafka Cluster:** Log in to vDB Kafka Cluster here [https://vdb.console.vngcloud.vn/kafka/cluster](https://vdb.console.vngcloud.vn/kafka/cluster) and select the Kafka cluster you want to adjust.

**2. Enable/Disable Public Access:** On the Kafka Cluster management page, find the "Edit Accessibility" feature option and enable or disable this option to allow or block access from outside the VPC.

**3. Save Changes:** After making your selection, click the "Save" button or similar to apply the changes.

**Notes:**

* Enabling "Public Accessibility" may increase security risks. Consider carefully before enabling this option and ensure that you have applied appropriate security measures.
* If you disable "Public Accessibility", applications outside the VPC will no longer be able to connect to the Kafka cluster. Make sure you have updated the configuration of these applications to use other connection methods (e.g., through VPN) if necessary.

## Edit Access Method (mTLS, SASL)

**1. Select Kafka Cluster:** Log in to vDB Kafka Cluster here [https://vdb.console.vngcloud.vn/kafka/cluster](https://vdb.console.vngcloud.vn/kafka/cluster) and select the Kafka cluster you want to adjust.

**2. Select Authentication Methods:** On the Kafka Cluster management page, find and select the "Edit Access Control Method" feature.

* **mTLS:** Enable or disable the mTLS option. If enabled, you may need to additionally configure digital certificates for client and server.
* **SASL:** Enable or disable the SASL option. If enabled, you may need to additionally configure specific authentication mechanisms (e.g., username/password).

**3. Save Changes:** After making your selection, click the "Save" button or similar to apply the changes.

**Notes:**

* Changing the authentication method may affect the connectivity of existing applications to the Kafka cluster. Make sure you have updated your application configurations to use the new authentication method if necessary.
* If you encounter any connection errors after making changes, please recheck your access method configuration and application configuration.

**Conclusion**

Editing access methods allows you to more tightly control access to the Kafka cluster, ensuring data security and safety. By selecting appropriate access methods, you can create a secure and reliable Kafka environment for your applications.
