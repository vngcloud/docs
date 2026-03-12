# Create Kafka Cluster

Creating a Kafka cluster is the first important step to building a distributed data processing system with high scalability and fault tolerance. This guide will help you step by step initialize a new Kafka cluster on the cloud platform, using an intuitive management interface and flexible configuration options.

By following this guide, you will be able to quickly deploy a ready-to-use Kafka cluster, laying a solid foundation for building powerful and reliable data applications.

## **Step 1: Access the Kafka Management Interface**

1. Open a web browser and access the GreenNode Kafka management interface here: [https://vdb.console.vngcloud.vn/kafka/cluster](https://vdb.console.vngcloud.vn/kafka/cluster)
2. Log in to your account. If you don't have an account yet, register a new one.

## **Step 2: Start Creating a Kafka Cluster**

Find and click the "Create Kafka Cluster" button, configure the Kafka Cluster information as follows:

1. **Cluster Name:**
   * Enter a descriptive name for your Kafka cluster. This name will help you easily identify and manage the cluster in the future.
   * Note that this name cannot be changed after initialization.
2. **Kafka Version:**
   * Select the Kafka version you want to use. Note that different versions may have different features and compatibility.
   * Note that currently, vDB Kafka Cluster does not support version upgrade for active Kafka Clusters. This feature will be supported in the near future.
3. **Hardware Configuration (Flavor):**
   * Select the hardware configuration (flavor) for the brokers in your Kafka cluster. Flavors typically include options for CPU, RAM and Network. Choose a flavor that matches your expected workload.
4. **Number of Brokers:**
   * Determine the number of brokers you want in your Kafka cluster. The number of brokers affects the fault tolerance, scalability and performance of the cluster.
5. **Storage per Broker:**
   * Select the storage capacity and IOPS (Input/Output Operations Per Second) for each broker. Note that storage requirements may vary depending on the volume of data you plan to process.
6. **Network (VPC and Subnet):**
   * Select the virtual network (VPC) and subnet where you want to deploy your Kafka cluster. Make sure that the VPC and subnet are properly configured and allow necessary communication.
7. **Access Method Control:**
   * Select the authentication and authorization method you want to use for your Kafka cluster. Common options include mTLS and SASL.
8. **Encryption Mode:**
   * Select the data encryption mode. By default, encryption in transit (data encrypted when transmitted between client and broker) and within cluster (data encrypted when stored on brokers) are enabled.
9. **Configuration Group:**
   * If available, select a configuration group to apply specific configuration settings for your Kafka cluster.

## **Step 3: Review and Initialize**

1. Review all the configurations you have selected to ensure they are correct.
2. Review the corresponding costs for the configuration you just selected.
3. Click the "Initialize" button to start the Kafka cluster initialization process.

## **Step 4: Monitor Progress**

1. Monitor the Kafka cluster initialization progress through the management interface. This process may take some time depending on the configuration you selected.
2. After the Kafka cluster is successfully initialized, you can start using it to create topics, produce and consume data.
