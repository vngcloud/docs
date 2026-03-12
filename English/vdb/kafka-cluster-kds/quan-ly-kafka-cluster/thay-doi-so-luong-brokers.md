# Change Number of Brokers

## Why Change the Number of Brokers?

In the ever-evolving world of data, adjusting the number of brokers in a Kafka cluster is essential to accommodate changes in data traffic and ensure optimal performance.

* **Scale Up (Increase Broker Count):** When data traffic increases, adding more brokers helps distribute the load across multiple servers, preventing overload on a single broker. This ensures that the system can handle larger data volumes without performance degradation and maintains high fault tolerance.
* **Scale Down (Decrease Broker Count):** When data traffic decreases, reducing the number of brokers helps save resources and operational costs. By removing unnecessary brokers, you can optimize resource usage without affecting system performance.

**Topic Re-balance Mechanism**

When you change the number of brokers, Kafka needs to redistribute the partitions of topics across the new brokers to ensure load balancing and fault tolerance. This process is called re-balance.

* **Automatic Re-balance:** vDB Kafka Cluster provides an option to automatically re-balance topics after changing the number of brokers. This simplifies the process and ensures data is evenly distributed across brokers.
* **Re-balance Considerations:** The re-balance process may temporarily affect the performance of the Kafka cluster, as data needs to be moved between brokers. Consider the timing of re-balance to minimize impact on your applications.

## Guide to Changing Broker Count

1. **Select Kafka Cluster:** Log in to vDB Kafka Cluster here [https://vdb.console.vngcloud.vn/kafka/cluster](https://vdb.console.vngcloud.vn/kafka/cluster) and select the Kafka cluster you want to adjust.
2. **Change Broker Count:**
   * Find and access the Kafka cluster management section.
   * Select the "Edit number of broker" option to increase or decrease the number of brokers.
   * Enter the desired new number of brokers.
   * Select "Automatic Re-balance Topic" if you want the system to automatically redistribute partitions after the change.
3. **Confirm Changes:** Review the changes in broker count as well as the cost difference and click the "Confirm" button to start the process.
4. **Monitor Progress:** The system will automatically add or remove brokers and perform topic re-balance if you selected this option. You can monitor progress through the management interface.
