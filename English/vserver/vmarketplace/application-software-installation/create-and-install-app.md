# Create & Install App

vMarketplace offers a variety of pre-built applications that you can instantly launch and install on your vServer in just a few steps. To launch an application, follow these steps:

**Step 1: Select the application name and version**

**Step 2: Choose an Instance type** (a combination of CPU, RAM, and GPU)

**Step 3: Choose Volume settings**

**Step 4: Choose Network settings**, including the following actions:

* Select a VPC for the application
* Choose the priority order for the External and Internal network interfaces. Note that these interfaces will be arranged in the order you enter them.
* Choose Security settings: Select "New security group rules" to create a new group with specific parameters for your application, or select "Existing security group" to inherit rules from an existing group.

**Step 5: Choose Server Group settings**

* To enable high availability (HA) for your firewall servers, select "Dedicated SOFT ANTI AFFINITY group" to create a new server group for your firewall application, or select "Existing server group" if it already exists.

**After the virtual machine has been provisioned, modify the Security Group to open the following ports for the virtual machine:**

* **Access via vServer Console (from the web portal):** By default, the password is left blank.
* **Configure SSH/Web access (from the web portal):** By default, you will log in with a blank password, then the application will redirect you to the password change page. Please change the password immediately (leave the Old Password blank).

**Note:** Marketplace applications will launch within a few minutes.
