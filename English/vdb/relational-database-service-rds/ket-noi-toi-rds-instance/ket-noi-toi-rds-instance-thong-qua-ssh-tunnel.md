# Connect to an RDS Instance via SSH Tunnel

**Connect to an RDS Instance via SSH Tunnel**

To connect to an RDS Instance, you can use the Public Endpoint (via the Internet). However, this method carries potential security risks. To enhance security, you can configure the RDS Instance to only allow connections via the **Private Endpoint**, and then access it through a **vServer** that is on the same network as the RDS Instance and has a Public IP (this vServer acts as a terminal or jump host).

***

#### Step 1: Identify Endpoint & Port Information

On the database management interface, select the RDS Instance you want to connect to, go to the **Connectivity & Security** tab, and locate the **Endpoint & Port** section.

Example:

* **Private Endpoint** (within VPC): `10.0.116.3`
* **Public Endpoint** (accessible from Internet): `61.28.233.82`

To distinguish between Public and Private Endpoints, check the **Networking** section to determine the Network Subnet of the RDS Instance.

For example, if the RDS Instance's subnet is `10.0.116.0/24`, then `10.0.116.3` is the Private Endpoint.

***

#### Step 2: Adjust Security Group Rules to Allow Internal VPC Access Only

Security Group Rules let you restrict which remote IPs are allowed to access your RDS Instance. In this case, configure the **Remote IP Prefix** to match your VPC’s Network Subnet so only vServers or vDBs within the same VPC can access it.

After updating the rules, click **Save** and wait a moment for changes to apply.

You can verify the connectivity from the vServer terminal using a tool like `telnet`:

```bash
$ telnet 10.0.116.3 3306
```

If the connection succeeds, you're ready to set up the SSH Tunnel.

***

#### Step 3: Configure SSH Tunnel

If you're using a client tool that supports SSH Tunneling (like MySQL Workbench), you can skip the command-line part and move on to configuring within the GUI.

If your client does **not** support SSH tunneling (e.g., using `mysqlclient`), configure the SSH Tunnel manually with the following command:

```bash
ssh -N -L localhost_port:private_endpoint:3306 ssh_user@vServer_IP -p vServer_ssh_port &
```

* `localhost_port`: Port on your local machine to use for forwarding (e.g., 3306)
* `private_endpoint`: The RDS Private Endpoint (e.g., `10.0.116.3`)
* `ssh_user`: The SSH username for the vServer
* `vServer_IP`: Public IP of the vServer (jump host)
* `vServer_ssh_port`: SSH port of the vServer (default is 22)
* `-i`: Optional flag to specify a private key file
* `&`: Run the tunnel process in the background

**Example**:\
RDS Master User: `dba`\
Private Endpoint: `10.0.116.3`\
vServer IP: `61.28.224.201`\
SSH Port: `234`\
SSH User: `stackops`\
Private Key Path: `~/.ssh/id_rsa`\
Localhost Port: `3306`

Run:

```bash
ssh -N -L 3306:10.0.116.3:3306 stackops@61.28.224.201 -p 234 -i ~/.ssh/id_rsa &
```

Then connect to the database using:

```bash
$ mysql -h 127.0.0.1 -P 3306 -u dba -p
```

***

#### Using MySQL Workbench (GUI) with SSH Tunnel

In MySQL Workbench:

* **Connection Method**: Select `Standard TCP/IP over SSH`
* **SSH Hostname**: `61.28.224.201:234` (or just the IP if using default port 22)
* **SSH Username**: `stackops`
* **SSH Key File** or **Password**: Depending on your SSH configuration
* **MySQL Hostname**: `10.0.116.3`
* **MySQL Port**: `3306`
* **MySQL Username**: `dba`
* **Password**: Your RDS user password

Click **Test Connection** to verify the setup.

***

Good luck! If you encounter any issues, feel free to contact the VNG Cloud Support Team for assistance.
