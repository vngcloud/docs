# Manage Load balancer

GreenNode provides an intuitive interface for managing Load Balancers, including essential features like:

* Creating Load Balancers
* Viewing the list of Load Balancers
* Managing Load Balancer details
* Changing Load Balancer packages (Resizing)
* Duplicating Load Balancers
* Deleting Load Balancers

## 1. Creating Load Balancers

To use the vLB service on GreenNode, the first thing you need to do is create a Load Balancer according to your usage requirements. Refer to the following instructions for creating an Application Load Balancer.

**Steps to Create an Application Load Balancer:**

1. Access the Load Balancer homepage: `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`
2. On the Load Balancer homepage, click "Create a Load Balancer."
3. **Choose Load Balancer Configuration:**
   * **Load Balancer Name:** If you don't enter a name, the system will generate one automatically. Note that the Load Balancer name cannot be changed during use, so you should proactively enter a name if you need to manage it by name.
   * **Layer:** Select "Application - HTTP/HTTPS."
   * **Scheme:**
     * Choose "Internet facing" to allow access from the internet.
     * Choose "Internal" to allow access only within your private network.
   * **Load Balancer Package:** Select a package that suits your needs and usage, as this will be the main factor in calculating the cost of creating and operating your Load Balancer. This package can be changed later.
   * **Network Settings:** Choose an existing Virtual Private Cloud (VPC) and Subnet from your VPC list. If you need to create a VPC, refer to the Virtual Private Cloud (VPC) guide.
4. **Configure Listener:**
   * **Listener Name:** If you don't enter a name, the system will generate one automatically.
   * **Protocol & Port:**
     * If you choose HTTP, select the port (default is 80) and headers (default is X-Forwarded-For, X-Forwarded-Proto, X-Forwarded-Port; you can deselect headers if not needed).
     * If you choose HTTPS, select the port (default is 443) and certificate (refer to the "Upload a certificate" guide if you don't have one).
5. **Configure Default Pool:**
   * **Pool Name:** If you don't enter a name, the system will generate one automatically.
   * **Protocol:** HTTP is the default.
   * **Algorithm:** Choose a suitable load balancing algorithm.
   * **Health Check Settings:** Protocol: TCP/HTTP (enter the default path if you choose HTTP).
6. **Select Pool Members:** Add backend servers to the pool.
   * Choose pool members from a list of available backend servers that belong to the Load Balancer Network.
   * Click "Attach" to add each server.
7. **Review Creation Information:** You can review the configuration details and pricing before finalizing. This information is displayed on the right side of the input screen.
   * **Summary Tab:** Review the Load Balancer, Listener, Pool, and Pool Member configurations.
   * **Item List Tab:** Review the Load Balancer package and cost information.
8. **Complete Creation:** After configuring and reviewing, click "Create Load Balancer" to finalize.
   * For prepaid users, you will be directed to the payment page to provide a valid payment method. Refer to the Online Payment guide for more information.

**Note:** The initial creation allows you to configure one listener and one corresponding pool. After successful creation, you can access the Load Balancer details to add/edit listeners and pools as needed.

**Important:** The following information cannot be changed after creation:

* Name and identifier: Includes Load Balancer, Listener, and Pool names.
* General Load Balancer information: Includes Layer, Scheme, Network, and Subnet.
* Protocol and Port: Includes Listener, Pool, and Health Check protocols.

## 2. View the List of Load Balancers

To view a list of all available Load Balancers in the system:

1. Go to the Load Balancer homepage: `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`

The homepage will display a list of Load Balancers, including information such as:

* Load Balancer name and ID (with the option to copy the ID for Terraform or other uses)
* Load Balancer status
* Endpoint, Scheme (Internet/Internal), Type (Application/Network), Package, Creation date

You can filter, sort, and search for specific Load Balancers using the provided tools.

## 3. Manage Load Balancer Details

To view and manage the details of a specific Load Balancer:

1. Click on the Load Balancer you want to view in the list.

The details screen is divided into three main sections:

* **Availability Statistics:** Overview of the number of listeners, pools, and their health status.
* **General Load Balancer Information:** Name, ID, scheme, endpoint, subnet, package details, etc.
* **Detailed Information:** Lists of listeners and pools, monitoring metrics and logs.

For more detailed information, refer to the following articles:

* **Listener**
* **Pool**
* **Monitor your load balancers**

## 4. Change Load Balancer Package (Resize)

The "Resize Load Balancer" feature allows you to customize and update service packages to match your usage needs in terms of both cost and operation, such as:

* Increasing or decreasing connections and data transfer to accommodate changes in traffic load.
* Optimizing the Load Balancer package configuration to suit actual needs after a period of use.

To resize, click the "three dots" icon next to the Load Balancer in the list or the "Resize" button on the details page. Choose a new package, review the changes, and confirm. Note that resizing may cause a temporary interruption in service.

## 5. Duplicate Load Balancer

The "Duplicate Load Balancer" feature allows you to create an exact copy of an existing Load Balancer for various purposes, such as ensuring redundancy or creating testing environments.

To duplicate, click the "three dots" icon or the "Duplicate" button, configure the new Load Balancer's settings, and confirm. Note that duplication takes time, especially for complex configurations.

## 6. Delete Load Balancer

Before deleting a Load Balancer, consider it carefully, as it cannot be recovered once deleted.

To delete, click the "three dots" icon or the "Delete" button, and confirm the deletion. For prepaid-users, you may receive a refund for unused service time.
