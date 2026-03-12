# Upgrade Storage

## Why Increase Broker Storage Capacity?

Kafka is designed to store large amounts of data over time. As data accumulates, increasing the storage capacity for brokers in the Kafka cluster becomes necessary to ensure the system operates stably and avoids running out of disk space.

* **Avoid data loss:** When a broker's storage capacity is full, Kafka will not allow new writes. Increasing storage capacity helps you avoid losing important data and ensures that you can access historical data when needed.
* **Maintain performance:**&#x20;
  * When a broker is nearly full, read and write performance may be affected.&#x20;
  * Therefore, vDB Kafka Cluster will alert (via email) customers when the storage capacity on a broker exceeds the allowed threshold (80%).&#x20;
  * Customers need to proactively increase storage capacity to maintain optimal performance of the Kafka cluster, monitor alert emails and warnings from our service to make quick decisions.

**Guide to Increasing Broker Storage Capacity**

1. **Select Kafka Cluster:** Log in to vDB Kafka Cluster and select the Kafka cluster you want to adjust.
2. **Increase Storage Disk Size:**
   * Find and access the Kafka cluster management section.
   * Find the "Scale Up Broker Storage" option or similar.
   * Select a new disk size larger than the current size.
3. **Confirm Changes:** Review the changes and click the "Confirm" button or similar to start the process.
4. **Monitor Progress:** The system will automatically expand the storage capacity for the brokers. You can monitor progress through the management interface.

**Important Notes:**

* The time required to expand storage capacity may vary depending on the service provider and the new disk size.
* During the storage expansion process, the Kafka cluster can still operate normally, but performance may be temporarily affected.
* Plan storage expansion before your brokers are nearly full to avoid data loss and performance degradation.

**Conclusion**

Increasing storage capacity for brokers in the Kafka cluster is an important part of managing and maintaining the Kafka system. By following the simple steps above, you can ensure that your Kafka cluster has sufficient storage space to handle the ever-increasing data volume and operates stably over the long term.
