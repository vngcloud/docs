# Use Case

Suppose a business has two branches, one in Ho Chi Minh City and one in Hanoi. The system already has a VPC in the Ho Chi Minh region and a VPC in the Hanoi region. To allow these two branches to communicate with each other through a private network, the Cross Connect connection will link the VPCs of the two branches in Ho Chi Minh and Hanoi.

### **Implementation Solution:**

1. Each branch has its own VPC (if not, at least one VPC must be created at each branch);
2. Create a Cross Connect connection between Ho Chi Minh and Hanoi;
3. Select and purchase the appropriate bandwidth package for the connection between the two regions;
4. Link the two VPCs through the Cross Connect connection;
5. Set up communication between the two VPCs via Cross Connect.

### **Advantages:**

* **Easy to use**: With a few simple steps, businesses can establish inter-regional connections between VPCs;
* **High performance**: Cross Connect leverages the global network infrastructure of GreenNode to provide high-quality, low-latency connections with bandwidth that can be flexibly adjusted to meet changing business needs.

**Limitations:**

* A Cross Connect connection cannot be created between VPCs with overlapping CIDR blocks;
* Bandwidth adjustment for connections between regions is limited depending on the region connection.
