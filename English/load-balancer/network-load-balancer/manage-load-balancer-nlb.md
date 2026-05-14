# Manage Load Balancer (NLB)

GreenNode provides an intuitive interface for managing Load Balancers, including essential features like:

1. Creating Load Balancers
2. Viewing the List of Load Balancers
3. Managing Load Balancer Details
4. Changing Load Balancer Packages (Resizing)
5. Duplicating Load Balancers
6. Deleting Load Balancers

## 1. Creating Load Balancers

To use the vLB service on GreenNode, the first step is to create a Load Balancer based on your requirements. Refer to the instructions below for creating a Network Load Balancer.

**How to Create a Network Load Balancer**

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Click "Create a Load Balancer"** on the Load Balancer homepage.
3. **Choose Load Balancer Configuration:**
   * **Load Balancer Name:** If you don't enter a name, the system will automatically generate one. Note that the Load Balancer name cannot be changed once created, so proactively enter a name if you need to manage it by name.
   * **Layer:** Select "Network - TCP/UDP."
   * **Scheme:**
     * Choose "Internet facing" to allow access from the internet.
     * Choose "Internal" to allow access only within your private network.
   * **Load Balancer Package:** Select a suitable package for your needs and usage. This is the main factor in calculating the cost of creating and operating your Load Balancer. You can change the package later.
   * **Network Settings:** Choose an existing Virtual Private Cloud (VPC) and Subnet from your VPC list. If you need to create a VPC, refer to the Virtual Private Cloud (VPC) guide.
4. **Configure Listener:**
   * **Listener Name:** If you don't enter a name, the system will generate one automatically.
   * **Protocol & Port:**
     * If you choose TCP, select the port (default is 80).
     * If you choose UDP, select the port (default is 53).
5. **Configure Default Pool:**
   * **Pool Name:** If you don't enter a name, the system will generate one automatically.
   * **Protocol:** TCP/Proxy (for TCP Listener) or UDP (for UDP Listener)
   * **Algorithm:** Choose a suitable load balancing algorithm.
   * **Health Check Settings:** Protocol: TCP / HTTP / HTTPS (for TCP/Proxy Pool) or PING-UDP (for UDP Pool)
6. **Select Pool Members:** Add backend servers to the pool.
   * Choose pool members from a list of available backend servers that belong to the Load Balancer Network.
   * Click "Attach" to add each server.
7. **Review Creation Information:** You can review the configuration details and pricing before finalizing. This information is displayed on the right side of the input screen.
   * **Summary Tab:** Review the Load Balancer, Listener, Pool, and Pool Member configurations.
   * **Item List Tab:** Review the Load Balancer package and cost information.
8. **Complete Creation:** After configuring and reviewing, click "Create Load Balancer" to finalize.
   * For prepaid users, you will be directed to the payment page, where you need to provide a valid payment method to complete the creation of the Network Load Balancer. Refer to the Online Payment guide for more information.

The initial creation allows you to configure one listener and one corresponding pool. After successful creation, you can access the Load Balancer details to add/edit listeners and pools as needed.

**Note:** The following information cannot be changed after creation:

* Name and identifier: Includes Load Balancer, Listener, and Pool names.
* General Load Balancer information: Includes Layer, Scheme, Network, and Subnet.
* Protocol and Port: Includes Listener, Pool, and Health Check protocols.

## 2. Viewing the List of Load Balancers

Use these instructions to view a list of all available Load Balancers in the system.

**Accessing the Load Balancer List**

1. Go to the Load Balancer homepage: `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.

The homepage will display a list of Load Balancers, including information such as:

* Load Balancer name and ID (with the option to copy the ID for Terraform or other uses)
* Load Balancer status
* Other information like Endpoint, Scheme (Internet/Internal), Type (Application/Network), Package, Creation date.

You can filter, sort, and search for specific Load Balancers using the provided tools.

## 3. Managing Load Balancer Details

**Accessing Load Balancer Details**

Click on the Load Balancer you want to view in the list.

The details screen is divided into three main sections:

* **Availability Statistics:** Overview of the number of listeners, pools, and their health status.
* **General Load Balancer Information:** Name, ID, scheme, endpoint, subnet, package details, etc.
* **Detailed Information:** Lists of listeners and pools, monitoring metrics and logs.

**Learn More**

For more detailed information, refer to the following articles:

* Listener (NLB)
* Pool (NLB)
* Monitor your load balancers
