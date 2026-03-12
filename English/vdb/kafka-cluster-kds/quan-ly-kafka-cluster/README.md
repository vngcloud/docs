# Manage Kafka Cluster

Kafka Cluster DB is not a traditional database. It is a cluster of Kafka servers working together to store and process real-time event streams. Kafka Cluster DB improves scalability, data durability and processing performance compared to using a single Kafka server.

**It is commonly used for:**

* Real-time data processing
* Building messaging systems
* Centralized logging

**Follow the articles below to learn more about using Kafka Cluster:**

* **Create Kafka Cluster:** To start using Kafka on the vDB platform, you need to create a Kafka cluster. This cluster will store and process your application's events.
* **Scale Up/Down Broker Count:** Scale up when data traffic increases - adding more brokers helps distribute the load, ensuring system performance and fault tolerance. Conversely, scale down when data traffic decreases to save resources.
* **Scale Up Broker Storage:** As data accumulates, increasing storage capacity ensures the Kafka cluster doesn't run out of space and continues to operate stably.
* **Edit Config Group:** Kafka has many configuration parameters that affect performance, data durability, and other aspects. Editing the config group allows you to customize Kafka according to your application's specific requirements.
* **Edit Access Method**: mTLS ensures higher security through two-way authentication between client and server; SASL provides flexible user authentication mechanisms.
* **Public Accessibility:** Allows access from outside.
* **Topic Management**: vDB Kafka Cluster provides topic management features such as create, delete, edit,...
* **User Management:** vDB Kafka Cluster provides Kafka user management features such as create, delete, edit permissions, access method, re-Generate Certificate,...

#### Note:

* Always carefully check configurations before applying changes.
* Back up important data before making major changes.
* Refer to the detailed vDB Kafka Cluster documentation for more information.
