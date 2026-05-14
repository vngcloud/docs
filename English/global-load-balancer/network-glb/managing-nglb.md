# Managing NGLB

GreenNode provides an intuitive interface for managing NGLB, including important features such as:

* Create Global Load Balancer
* View Global Load Balancer list
* Manage Global Load Balancer details
* Delete Global Load Balancer

### 1. Create a Global Load Balancer

To use the GLB service on GreenNode, the first thing you need to do is create a Global Load Balancer according to your usage needs. Refer to the guide below for creating a Network Global Load Balancer.

#### How to Create a Network Global Load Balancer

Access the Global Load Balancer homepage here:\
[https://glb.console.vngcloud.vn/glb/list](https://glb.console.vngcloud.vn/glb/list)

On the GLB homepage, click “Create Global Load Balancer”.

#### Select Global Load Balancer Configuration

* **Load Balancer Name:** If the user does not manually enter a Load Balancer name, the system will automatically generate one. Note that the Load Balancer name cannot be changed after creation, so users should proactively enter a name if they need easier management.
* **Layer:** Select “Network - TCP/UDP”.

#### Configure Listener

* **Listener Name:** If the user does not manually enter a Listener name, the system will automatically generate one.

**Protocol & Port**

* If **Protocol = TCP**, the user must select a Port (Port 80 is pre-filled by default).

#### Configure Default Global Pool

* **Pool Name:** If the user does not manually enter a Pool name, the system will automatically generate one.
* **Protocol:** TCP/Proxy (for TCP Listener).
* **Algorithm:** Select an appropriate load balancing algorithm.
* **Health Check Settings:** Protocol options include TCP / HTTP / HTTPS (for TCP/Proxy Pool).

#### Select Global Pool Members

Add backend servers to the Global Pool.

Global Pool Members allow users to add backend servers from multiple Regions.

* Select Region and VPC for the Global Pool Member.
* Next, attach backend servers (from subnets within the same VPC) to the pool.

#### Review Configuration Information

Users can review the configuration information before completing the creation process. This information will be displayed on the right side of the input screen.

**“Summary” Tab**

Review the configuration details for:

* Load Balancer
* Listener
* Pool
* Pool Member

#### Complete the Creation Process

After completing the configuration and reviewing the information, click “Create Global Load Balancer / Create Load Balancer” to finish creating the GLB.

The initial creation process allows configuration of one Global Listener and one corresponding Global Pool. After successful creation, users can access the Global Load Balancer details page to add or modify Global Listeners and Global Pools as needed.

#### Notes

Please note that the following information cannot be changed after creation:

* **Names and identifiers:** Including Global Load Balancer, Global Listener, and Global Pool names.
* **Protocols and Ports:** Including Global Listener, Global Pool, and Health Check protocols and ports.

***

### 2. View Global Load Balancer List

Use this guide to view the list of all available Load Balancers in the system.

#### Access the Global Load Balancer List

Access the Global Load Balancer homepage here:\
[https://glb.console.vngcloud.vn/glb/list](https://glb.console.vngcloud.vn/glb/list)

On the Global Load Balancer homepage, a GLB list will appear with information such as:

* **Global Load Balancer name and identifier:** Supports copying the GLB identifier for Terraform or other purposes.
* **GLB Status:** Displays the current status of the Global Load Balancer.
* **Other information:** Endpoint, Type (Application/Network), Creation Date.

#### Filter and Sort Load Balancers

Users can sort the Global Load Balancer list by clicking on the desired column name in the list table, such as sorting by Name, Status, Endpoint, or Load Balancer Type.

#### Search Load Balancers

To accurately search for one or multiple Global Load Balancers with similar names, users can enter the Global Load Balancer name into the search box located at the top-right corner of the Load Balancer list table.

***

### 3. Manage Global Load Balancer Details

Access the Load Balancer to view and manage detailed information.

#### Access Load Balancer Details

Click on the desired Global Load Balancer from the Load Balancer list screen.

#### Viewing Global Load Balancer Information

The Load Balancer detail screen is divided into 3 main sections:

**Availability Statistics**

* Total number of Global Listeners in the G Load Balancer.
* Total number of G Pools in the G Load Balancer.

**General Information of the G Load Balancer**

* G Load Balancer name and identifier.
* Endpoint.

**Detailed Information**

* **G Listener:** List and detailed information of each G Listener.
* **G Pool:** List and detailed information of each G Pool.

***

### 4. Delete a G Load Balancer

Before deleting a G Load Balancer, users should carefully consider the action, as deleted G Load Balancers cannot be restored.

#### How to Delete a G Load Balancer

There are 2 ways to delete a G Load Balancer:

* **From the Load Balancer list screen:** Click the “three dots” icon at the end of the desired G Load Balancer row, then select the “Delete” action.
* **From the G Load Balancer detail screen:** Click the “Delete” action at the top-right corner of the detail screen.

After clicking “Delete”, a confirmation dialog will appear to confirm the deletion action.

Click “Delete” again to complete the deletion process.

#### How to Delete Multiple Load Balancers

* Access the G Load Balancer list screen.
* Select the Load Balancers to delete using the checkbox at the beginning of each row.
* Click the “Delete” button at the top-left corner of the Load Balancer list table.
* A confirmation dialog will appear to confirm the deletion action.
* Click “Delete” to complete the deletion of the selected Load Balancers.
