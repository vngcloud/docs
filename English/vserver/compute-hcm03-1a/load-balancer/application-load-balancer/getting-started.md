# Getting Started

This section will guide you through the basic steps of creating and managing an Application Load Balancer (ALB) on VNG Cloud, providing a comprehensive overview of ALB usage.

## Prerequisites

* **Virtual Private Cloud (VPC):** You need at least one VPC to get started. Refer to the Virtual Private Cloud (VPC) guide for instructions.
* **VNG Cloud Portal Access:** Understand how to access the VNG Cloud Portal with either a Root User Account or an IAM User Account. Refer to the "How to Login into VNG Cloud" guide.
* **IAM User Account (Optional):** If you prefer to use an IAM User Account, refer to the "IAM for vServer" guide.
* **TLS/SSL Certificate:** For Application Load Balancers, you'll need at least one TLS/SSL certificate when configuring an HTTPS listener. Refer to the "Upload a certificate" guide.

## 1. Access the vLB Console

The vLB Console is a web-based interface that allows you to manage Load Balancers in your cloud environment. It provides an intuitive interface for controlling and managing your ALBs.

**How to Access the vLB Console:**

* **From the vConsole Homepage:** Go to `https://dashboard.console.vngcloud.vn/`. Under "VNG Cloud Service," click "vServer," then click "vLB" from the list of products/services on the right.
* **From the vServer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/`. On the vServer homepage, navigate to the vLB portal by clicking "Load Balancers" under "Load Balancing" in the left menu.
* **Direct Access:** Go directly to the vLB Portal at `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.

## 2. Create an ALB

**Steps to Create an Application Load Balancer:**

1. On the Load Balancer homepage, click "Create a Load Balancer."
2. **Choose Load Balancer Configuration:**
   * **Load Balancer Name:** If you don't enter a name, the system will automatically generate one.
   * **Layer:** Select "Application - HTTP/HTTPS."
   * **Scheme:**
     * Choose "Internet facing" to allow access from the internet.
     * Choose "Internal" to allow access only within your private network.
   * **Load Balancer Package:** Select a package that suits your needs and usage, as this will be the main factor in calculating the cost of creating and operating your Load Balancer.
   * **Network Settings:** Choose an existing Virtual Private Cloud (VPC) and Subnet from your VPC list. If you haven't created a VPC yet, refer to the Virtual Private Cloud (VPC) guide.
3. **Configure Listener:**
   * **Listener Name:** If you don't enter a name, the system will automatically generate one.
   * **Protocol & Port:**
     * If you choose HTTP, select the port (default is 80) and headers (default is X-Forwarded-For, X-Forwarded-Proto, X-Forwarded-Port; you can deselect headers if not needed).
     * If you choose HTTPS, select the port (default is 443) and certificate (refer to the "Upload a certificate" guide if you don't have one).
4. **Configure Default Pool:**
   * **Pool Name:** If you don't enter a name, the system will automatically generate one.
   * **Protocol:** HTTP is the default.
   * **Algorithm:** Choose a suitable load balancing algorithm.
   * **Health Check Settings:** Protocol: TCP/HTTP (enter the default path if you choose HTTP).
5. **Select Pool Members:** Add backend servers to the pool.
   * Choose pool members from a list of available backend servers that belong to the Load Balancer Network (in the same subnet as the LB).
   * Click "Attach" to add each server.
6. **Review Creation Information:** You can review the configuration details and pricing before finalizing. This information is displayed on the right side of the input screen.
   * **Summary Tab:** Review the Load Balancer, Listener, Pool, and Pool Member configurations.
   * **Item List Tab:** Review the Load Balancer package and cost information.
7. **Complete Creation:** After configuring and reviewing, click "Create Load Balancer" to finalize.
   * For prepaid users, you will be directed to the payment page, where you need to provide a valid payment method to complete the creation of the Application Load Balancer. Refer to the Online Payment guide for more information.

## 3. Observe and Test Your ALB

After successful creation, the system will redirect you to the Load Balancer list page, where you can track the creation status from "Creating" to "Active."

Once active, you can access the Load Balancer details page to observe and test its functionality.

These are the basic steps for quickly creating an Application Load Balancer. There are also advanced configurations for different Load Balancer use cases. Learn more about the operation and advanced features of an Application Load Balancer through the following articles:

* **Related Topics:**
  * Manage Load Balancer
  * Listener
  * Pool
  * Certificate
  * Monitor your load balancers
