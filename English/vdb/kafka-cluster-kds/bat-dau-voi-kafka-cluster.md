# Getting Started with Kafka Cluster

With vDB Kafka Cluster, you can quickly deploy and manage Kafka clusters efficiently, focusing on application development and leveraging the power of real-time event streaming. Follow the guide below to get started with the Kafka Cluster service.

## Step 1: Access and Login

1. Open a web browser and access the vDB Kafka Cluster interface at: [https://vdb.console.vngcloud.vn/kafka/cluster](https://vdb.console.vngcloud.vn/kafka/cluster)
2. If you already have an account, enter your login credentials.

Refer to the GreenNode login guide [here](../../identity-and-access-management-iam/cac-loai-dinh-danh-iam/tai-khoan-user-accounts/cach-dang-nhap-vao-vng-cloud.md).

## Step 2: Create a Kafka Cluster

1.  Click the "Create Kafka Cluster" button.&#x20;

    <figure><img src="../../.gitbook/assets/image (744).png" alt="" width="228"><figcaption></figcaption></figure>
2. Fill in the following information:
   * **Name:** Name your Kafka cluster for easy identification and management.
   * **Kafka Version:** Choose the Kafka version that suits your needs. Different versions may have different features and performance.
   * **Flavor (CPU, RAM):** Select the hardware configuration (CPU and RAM) for brokers in the Kafka cluster. This configuration affects the processing capability and performance of the cluster.
   * **Number of Brokers:** Determine the number of brokers in the Kafka cluster. The number of brokers affects the fault tolerance and scalability of the cluster.
   * **Storage per Broker (IOPS and Capacity):** Choose the storage capacity and IOPS (Input/Output Operations Per Second) for each broker. This affects the data storage capacity and read/write performance of the cluster.
   * **Network (VPC, Subnet):** Select the virtual network (VPC) and subnet where the Kafka cluster will be deployed. When initialized, the Kafka cluster will be in private mode (accessible only from within the VPC). After successful initialization, you can enable public access if needed.
   * **Access Method Control (mTLS, SASL):** Choose the authentication and authorization method for clients connecting to the Kafka cluster. mTLS uses client and server certificates, SASL uses username and password.
   * **Encryption Mode:** Choose the data encryption mode. By default, encryption in transit (data encrypted when transmitted between client and broker) and within cluster (data encrypted when stored on brokers) are enabled.
   * **Config Group:** Select the configuration group to apply to the Kafka cluster. The configuration group contains detailed settings for Kafka operations.
3.  Click the "Create" button to start the Kafka cluster creation process.&#x20;

    <figure><img src="../../.gitbook/assets/image (745).png" alt=""><figcaption></figcaption></figure>

## Step 3: Create a Topic

1. After the Kafka cluster is successfully created, access the management page of that Kafka cluster.
2. Find and click the "Create Topic" section.

<figure><img src="../../.gitbook/assets/image (748).png" alt=""><figcaption></figcaption></figure>

3. Fill in the following information:

* **Name:** Name your topic. Note that this name cannot be changed after initialization.
* **Partition Count:** Determine the number of partitions for the topic. The number of partitions affects the scalability and parallelism of the topic.
* **Replication Factor:** Determine the number of copies of each partition. This affects the fault tolerance of the topic.
* **Retention Hour/Byte:** Determine the maximum storage time or capacity for data in the topic.

4. Click the "Create" button to create the topic.

## Step 4: Create Kafka User and Assign Permissions

1. In the Kafka cluster management page, find and click the "Create Kafka User" section.

<figure><img src="../../.gitbook/assets/image (749).png" alt=""><figcaption></figcaption></figure>

2. Fill in the following information:

* **Name:** Name the Kafka user.
* **Permissions:** In the permission section, click "Add Permission" to select Produce (write data to topic) and Consume (read data from topic) permissions for each topic this user needs to access.

<figure><img src="../../.gitbook/assets/image (750).png" alt=""><figcaption></figcaption></figure>

* **Access Method:** Choose the access method for the Kafka user (mTLS or SASL) depending on the method enabled for the Kafka cluster.

3. Click the "Create" button to create the Kafka user.

## Step 5: Connect to the Kafka Cluster

There are multiple ways to connect to the Kafka cluster. The following guide will introduce you to connecting to the Kafka cluster through a private client.

Note: The installation guide below is performed on an Ubuntu 22.04 client server.

1. Initialize a Server. See detailed server initialization guide [here](../../vserver/compute-hcm03-1a/server/tao-may-chu-bang-bang-dieu-khien.md).
2. Connect to the newly initialized server. See detailed guide [here.](../../vserver/compute-hcm03-1a/server/ket-noi-vao-may-chu-ao/)
3. Install Java and necessary packages on the server with the following command:

```bash
sudo apt-get update && sudo apt-get install default-jre tar unzip -y
```

4. Next, download Apache Kafka with the following command:

```bash
wget https://archive.apache.org/dist/kafka/{Your Kafka Cluster Version}/kafka_2.13-{Your Kafka Cluster Version}.tgz
tar -xzf kafka_2.13-{YOUR MSK VERSION}.tgz
```

Example

```bash
wget https://archive.apache.org/dist/kafka/3.7.0/kafka_2.13-3.7.0.tgz
tar -xzf kafka_2.13-3.7.0.tgz
```

5.  Next, download the TLS certificates to access the Kafka cluster.&#x20;

    <figure><img src="../../.gitbook/assets/image (746).png" alt=""><figcaption></figcaption></figure>
6. On the newly initialized server, upload and extract the TLS certificates and unzip using the command below:

Note: The User ID will be the directory name after extracting the downloaded certificate

```bash
unzip vng-manage-key.zip
cd {User ID}/mtls
```

Example

```bash
unzip vng-manage-key.zip
cd user-4436a54a-feaa-4afd-bfe7-4bd3d2cae33a/mtls/
```

7. Allow access to the Kafka cluster

You need to allow this server to access the Kafka cluster as a private client by allowing the IP. Follow the guide below:

* 7.1 View the Private IP of the newly initialized server, for example the server has private IP 10.255.0.5
* 7.2 Allow this IP to access the Kafka cluster:
  * 7.2.1 Access the Kafka cluster management interface
  * 7.2.2 Navigate to **Connectivity & Security**, add a rule as shown below

Note: Port 9094 for mTLS and 9096 for SASL

<figure><img src="../../.gitbook/assets/image (751).png" alt=""><figcaption></figcaption></figure>

8. Produce message to Kafka topic

After allowing access from the client to the Kafka cluster, connect to the previously initialized client and execute the following command:

```bash
{Path To Your Kafka Installation}/bin/kafka-console-producer.sh --bootstrap-server {Your Kafka Cluster Private endpoint}  --producer.config config.properties  --topic {Your Kafka Topic}
```

Example

```bash
/home/stackops/kafka_2.13-3.7.0/bin/kafka-console-producer.sh --bootstrap-server 10.5.0.6:9094,10.5.0.3:9094,10.5.0.5:9094 --producer.config config.properties --topic kafka-cluster-tutorial
```

9. Consume message from Kafka topic

After allowing access from the client to the Kafka cluster, connect to the previously initialized client and execute the following command:

```bash
{Path To Your Kafka Installation}/bin/kafka-console-consumer.sh --bootstrap-server {Your Kafka Cluster Private endpoint} --consumer.config config.properties  --topic {Your Kafka Topic}  --from-beginning
```

Example

```bash
/home/stackops/kafka_2.13-3.7.0/bin/kafka-console-consumer.sh --bootstrap-server 10.5.0.6:9094,10.5.0.3:9094,10.5.0.5:9094 --consumer.config  config.properties   --topic kafka-cluster-tutorial    --from-beginning
```

## Step 6: Delete Kafka Cluster

1. When you no longer need the Kafka cluster, access the Kafka cluster management page.
2. Find and click the "Delete Kafka Cluster" button.
3. Confirm the deletion of the Kafka cluster to avoid data loss and unnecessary costs.
