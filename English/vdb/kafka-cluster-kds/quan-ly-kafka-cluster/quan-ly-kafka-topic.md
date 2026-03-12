# Manage Kafka Topic

## What is a Kafka Topic?

In a Kafka cluster, a topic serves as a data transmission channel, similar to a folder or subject in a file system. Producers send data to topics, while consumers read data from those topics. Each topic has a unique name, helping to categorize and organize data by different subjects or purposes.

**How Topics Work**

1. **Partitions:**
   * Each topic is divided into multiple partitions. A partition is the basic unit of parallelism and data distribution in Kafka.
   * Each partition contains a set of records arranged in order.
   * Partitions allow horizontal scaling and improve performance by distributing data across multiple brokers in the Kafka cluster.
2. **Replicas:**
   * Each partition can have multiple replicas to ensure fault tolerance.
   * One replica is designated as the leader, responsible for handling all read and write operations for that partition.
   * The remaining replicas act as followers, replicating data from the leader to ensure data availability in case the leader encounters issues.
3. **Produce:**
   * Producers send data to topics by writing records to partitions.
   * Kafka ensures that records are written to partitions in order.
4. **Consume:**
   * Consumers read data from topics by reading records from partitions.
   * Kafka tracks each consumer's read position, allowing them to continue reading from where they left off.
5. **Retention:**
   * Kafka stores data in topics for a certain period of time or until a certain capacity limit is reached.
   * This allows consumers to re-read old data or process data on a flexible schedule.

**Topic Functions**

* **Data categorization and organization:** Topics allow you to categorize and organize data by different subjects or purposes, making it easy to manage and access data.
* **Scaling and performance:** Partitions in topics allow horizontal scaling and improve performance by distributing data across multiple brokers.
* **Fault tolerance:** Replicas in partitions ensure fault tolerance by replicating data across multiple brokers.
* **Real-time data transmission:** Kafka enables real-time data transmission between different applications.
* **Data stream processing:** Kafka supports data stream processing, allowing you to build big data analytics applications and event tracking systems.

## Manage Kafka Topic

vDB Kafka Cluster provides you with comprehensive topic management capabilities, including creating, deleting and modifying configurations. Below is a detailed step-by-step guide to perform these operations:

**1. Select Kafka Cluster**

* Log in to the vDB Kafka Cluster interface here: [https://vdb.console.vngcloud.vn/kafka/cluster](https://vdb.console.vngcloud.vn/kafka/cluster)
* From the list of available Kafka clusters, select the cluster where you want to manage topics.

**2. Access the "Topics" Section**

* After selecting the Kafka cluster, find and navigate to the "Topics" section in the management interface. This is where you will perform topic operations.

**3. Create Topic**

1. Click the "Create Topic" button to fill in the required information.
2. Fill in the following information:
   * **Topic Name:** Name the new topic. This name should clearly describe the topic's content and cannot be changed after initialization.
   * **Partition Count:** Determine the number of partitions for the topic. The number of partitions affects the scalability and parallelism of the topic (minimum partition count is 1 and maximum is 2048).
   * **Replication Factor:** Determine the number of copies of each partition. This affects the fault tolerance of the topic.
   * **Retention:** Set the maximum storage time or capacity for data in the topic. (Minimum retention hour is 1h and maximum is 2160h).
3. Click the "Create" button to complete the topic creation process.

**4. Delete Topic**

1. In the topic list, find the topic you want to delete.
2. Click the "Delete" icon corresponding to that topic.
3. Confirm the delete operation. Note that deleting a topic is irreversible and all data in the topic will be lost.

**5. Edit Topic**

1. In the topic list, find the topic you want to edit.
2. Click the "Edit" icon corresponding to that topic.
3. Change the necessary topic configurations, for example:
   * **Partition Count:** Only allows increasing the number of partitions to adjust the scalability of the topic.
   * **Retention:** Change the maximum storage time or capacity for data.
4. Click the "Save" button to apply the changes.

**Notes:**

* Changing the number of partitions of a topic may affect the performance and availability of the topic for a short period.
* Be cautious when deleting topics, as this operation is irreversible and all data in the topic will be permanently lost.

With this detailed guide, you can easily manage Kafka topics in vDB Kafka Cluster, ensuring your data processing system operates efficiently and meets scalability and reliability requirements.
