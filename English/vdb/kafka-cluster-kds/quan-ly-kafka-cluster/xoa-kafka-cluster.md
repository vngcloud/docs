# Delete Kafka Cluster

vDB Kafka Cluster provides the ability to delete a Kafka cluster when you no longer need it, helping save resources and costs.

**Steps to perform:**

1. **Select Kafka Cluster:** Log in to vDB Kafka Cluster here [https://vdb.console.vngcloud.vn/kafka/cluster](https://vdb.console.vngcloud.vn/kafka/cluster) and select the Kafka cluster you want to delete.
2. **Delete Cluster:** Find the "Delete" option.
3. **Confirm:** The system will ask you to confirm the cluster deletion. Read the warnings and information carefully before confirming.
4. **Monitor Progress:** The system will begin the Kafka cluster deletion process. You can monitor progress through the management interface.

**Important Warnings When Deleting a Kafka Cluster:**

* **Data loss:** Deleting a Kafka cluster will result in the loss of all data in the topics of that cluster. Make sure you have backed up or migrated important data before deleting the cluster.
* **Connection loss:** Applications currently using the Kafka cluster will lose connectivity after the cluster is deleted. Notify relevant parties and update application configurations to avoid service interruption.
* **Irreversible:** Deleting a Kafka cluster is irreversible. Consider carefully before performing this operation.

**In summary:**

The Kafka cluster deletion feature in vDB Kafka Cluster helps you manage resources efficiently. However, always be cautious and ensure that you fully understand the consequences before deleting a Kafka cluster.
