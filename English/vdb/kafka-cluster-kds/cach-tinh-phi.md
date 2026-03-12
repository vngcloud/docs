# Pricing

The pricing for vDB Kafka Cluster is based on the number of brokers in a Kafka cluster, where each broker includes the following components:

1. **Compute:** Computing cost based on the CPU and RAM configuration of each broker.
2. **Storage:** Storage cost based on the disk capacity you allocate for each broker.
3. **Encryption Volume (if applicable):** If you use the data encryption feature, there may be additional costs for encrypted storage capacity.

**Total pricing formula:**

```
Total cost = (Cost per broker) x (Number of brokers)
```

**Cost per broker:**

```
Cost per broker = (Compute cost) + (Storage cost) + (Encryption volume cost, if applicable)
```

**Example:**

Suppose you have a Kafka cluster with 3 brokers, each broker with the following configuration:

* Compute: 4 CPU, 16GB RAM
* Storage: 100GB
* Encryption Volume: Not used

And GreenNode has the following pricing:

* Compute (4 CPU, 16GB RAM): 1,500,000 VND/month
* Storage: 2,000 VND/GB/month

**Cost calculation:**

* Compute cost per broker: 1,500,000 VND
* Storage cost per broker: 100GB x 2,000 VND/GB/month = 200,000 VND
* Cost per broker: 1,500,000 VND + 200,000 VND = 1,700,000 VND
* Total cost: 1,700,000 VND/broker x 3 brokers = 5,100,000 VND/month

**Conclusion:**

This pricing model helps you easily estimate the cost of using vDB Kafka Cluster based on your needs. Choose the appropriate configuration and number of brokers to optimize cost and performance for your system.
