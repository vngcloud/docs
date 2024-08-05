# Create Juniper vSRX

To initialize, go to vMarketPlace at the following link: [https://marketplace.console.vngcloud.vn/app-package/detail/4/30/1284a184-2119-4950-bd1c-af9161c52c01](https://marketplace.console.vngcloud.vn/app-package/detail/4/30/1284a184-2119-4950-bd1c-af9161c52c01)

**Initialize Juniper vSRX**

1. Select "Launch on Compute Engine."
2. Enter the name, select the image type as vSRX, configure the VM (Flavor, Storage), and specify the correct VPC & Subnet to be associated with this vSRX Instance.
   * **Note:** Resources (vServer, vLB, vDB) in the Subnet that want to route traffic through this vSRX Instance need to add a route with the gateway through the Internal IP of this vSRX Instance.
3. After selecting the appropriate information, choose "Next."
4. Review the information and select "CREATE SERVER."
5. After creation (Status ACTIVE), select the Instance to view the connection IP information.

**Update Security Group**

By default, the created vSRX Instance is not attached to a Security Group. Follow the instructions below to update it:

1. Access the newly created server instance.
2. Next, select ACTION > Update Security and choose the appropriate New security group.
3. You can "Allow all INBOUND & OUTBOUND" from 0.0.0.0/0 for initial setup and then tighten the IP WhiteList as needed.
4. Remember to also check the Network ACL (in the VPC section) to configure it to synchronize with this Security group.

**Next, you need to perform the initial setup for the vSRX instance.**

1. Select ACTION > Console to open the instance console.
2. By default, the instance is not set up with a root password or configured with interfaces, IP addresses, routes, security zones, or security policies. You need to configure this information.
3.  To set up the root password, go to the console, log in as the root user, and configure as follows:Bash

    ```
    # Enter CLI mode
    cli
    # Enter configuration mode
    configure
    # Configure the root password as a plain-text password
    set system root-authentication plain-text-password
    New password: your-super-password
    Retype new password: your-super-password
    # Check validity
    commit check
    configuration check succeeds
    # Commit configuration
    commit
    commit complete
    ```

    Hãy thận trọng khi sử dụng các đoạn mã.
4.  To configure the Interface & get the IP Address, configure as follows:Bash

    ```
    # ge-0/0/0.0 and ge-0/0/1.0 are the external (to the Internet) and internal interfaces of the vSRX instance, respectively.
    set interfaces ge-0/0/0 unit 0 family inet dhcp-client
    set interfaces ge-0/0/1 unit 0 family inet dhcp-client

    # Allow all traffic initially for configuration, then WhiteList IP/Application appropriately.
    set security zones security-zone untrust interfaces ge-0/0/0.0
    set security zones security-zone untrust interfaces ge-0/0/0.0    host-inbound-traffic system-services all
    set security zones security-zone untrust interfaces ge-0/0/0.0 host-inbound-traffic protocols    all

    # Allow all traffic initially for configuration, then WhiteList IP/Application appropriately.
    set security zones security-zone trust interfaces ge-0/0/1.0
    set security zones security-zone trust interfaces ge-0/0/1.0 host-inbound-traffic system-services all
    set security zones security-zone trust interfaces ge-0/0/1.0 host-inbound-traffic protocols    all

    # Allow all traffic initially for configuration, then WhiteList IP/Application appropriately.
    set security policies from-zone untrust to-zone trust policy default-permit match source-address any
    set security policies from-zone untrust to-    untrust to-zone trust policy default-permit match untrust to-zone trust policy default-permit then permit

    # Commit config.
    commit check
    commit
    ```

    Hãy thận trọng khi sử dụng các đoạn mã.
5.  After configuration, you need to reboot the instance:Bash

    ```
    # Exit configuration mode
    exit
    # Reboot
    request system reboot
    ```

    Hãy thận trọng khi sử dụng các đoạn mã.The reboot process may take 10-15 minutes.
6. After rebooting, log in to the console using the root user and the password configured above.
7.  Check the route to the Internet:Bash

    ```
    cli
    show route
    ```

    Hãy thận trọng khi sử dụng các đoạn mã.Note the Gateway to the Internet of this vSRX Instance at 0.0.0.0/0.
8.  Configure the route to the Internet:Bash

    ```
    cli
    configure
    set routing-options static route 0.0.0.0/0 next-hop <your_gateway_ip>
    commit check
    commit
    ```

    Hãy thận trọng khi sử dụng các đoạn mã.

After this step, you can SSH into the instance from the Internet (via Public IP) or Internal IP from the vServer using the root user, port 22, and the password configured above.

You can also configure SSH using a public key with the command:

Bash

```
set system root-authentication ssh-rsa "ssh-rsa XXXRSA-KEYXXXXX"
```
