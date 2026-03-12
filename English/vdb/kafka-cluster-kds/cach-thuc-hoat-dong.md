# How It Works

A Kafka Cluster is a distributed system consisting of multiple Kafka servers (Kafka Brokers) working together to provide event streaming services. Data is organized into Topics, each topic is divided into multiple Partitions to increase scalability and fault tolerance.

## **Key Components and Terminology**

1. **Kafka Broker:**
   * A server in the Kafka cluster, responsible for storing and managing a portion of the topic data.
   * Receives data from Producers and provides data to Consumers.
   * Maintains cluster state and ensures data consistency.
2. **Kafka Storage:**
   * The physical storage location for Kafka data, typically on hard drives or other storage devices.
   * Kafka uses an efficient storage structure for sequential reading and writing, achieving high performance.
3. **Topic:**
   * A category or stream of related events.
   * Example: an e-commerce application might have topics like "new orders", "successful payments", "delivery completed".
4. **Partition count:**
   * The number of partitions a topic is divided into.
   * Increasing partition count improves scalability and parallel processing, but also increases system complexity.
5. **Replica Factor:**
   * The number of copies of each partition stored on different brokers.
   * Increasing the replication factor improves fault tolerance, but also increases required storage capacity.
6. **Produce & Consume:**
   * **Produce:** The process of sending data (events) to a topic by Producers.
   * **Consume:** The process of reading data from a topic by Consumers.
7. **Access method:**
   * **mTLS (Mutual TLS):** A two-way authentication mechanism requiring both client and server to authenticate each other using digital certificates. Ensures high security.
   * **SASL (Simple Authentication and Security Layer):** A flexible authentication mechanism supporting SCRAM authentication methods.
8. **Encryption:**
   * **At Rest:** Encrypts data when stored on disk, protecting data from unauthorized access when the server is inactive.
   * **In Transit:** Encrypts data when transmitted between different components (client-broker), ensuring security during data transmission.
   * **Within Cluster:** Encrypts data when transmitted between brokers within the same Kafka cluster.

## **How It Works**

1. **Producers** send data to specific **topics**.
2. Kafka distributes data into the **partitions** of the topic according to a partitioning strategy.
3. Each partition is **replicated** across multiple brokers to ensure fault tolerance.
4. **Consumers** subscribe to topics and read data from partitions.
5. Kafka ensures that each consumer reads only one copy of each event, avoiding duplicate processing.

**In summary:**

Kafka Cluster provides a powerful and flexible platform for real-time event streaming. With high scalability, data durability and security, Kafka is an essential tool for building modern data applications.
