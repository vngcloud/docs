# PFsense - AWS Cloud

### **AWS** <a href="#pfsense-awscloud-aws" id="pfsense-awscloud-aws"></a>

1. Login to your AWS account and go to **VPC** in the Console
2. On the sidebar underneath VPN Connections, go to **Customer Gateways**
   1. Click the **Create Customer Gateway** button
      * Enter a name for your Gateway (e.g., Seattle Office)
      * Change **Routing** to **Dynamic**
      * Enter your **BGP ASN** number (If you don’t have a public one, choose any number between 64512-65534. These are private ASN numbers). Remember this number for later.
      * Enter the **Public IP of your pfSense box**
      * Click **Yes, Create**
3. On the sidebar underneath VPN Connections, go to **Virtual Private Gateways**
   1. Click the **Create Virtual Private Gateway** button
      * Enter a name for your Virtual Private Gateway (e.g., Office VPN)
      * Click **Yes, Create**
   2. **Select** your newly created VPG and click **Attach to VPC**&#x20;
      * **Select your VPC** and click **Yes, Attach**
      *

          <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-2.53.09-PM-1024x366.png" alt=""><figcaption></figcaption></figure>
4. On the sidebar underneath Virtual Private Cloud, go to **Route Tables**
   1. For each Route Table in your target VPC:
      * Select the Route Table
      * Hit the **Route Propagation** tab on the bottom pane
      * You should see your Virtual Private Gateway listed
      * Hit the **Edit** button and hit the **Propagate Checkbox** and then hit **Save**
5. On the sidebar underneath VPN Connections, go to **VPN Connections**
   1. Click the **Create VPN Connection** button
      * Enter a name for your VPN connection (e.g., Seattle Office VPN)
      * Select your **Virtual Private Gateway** that we just created.
      * Select an **Existing Customer Gateway** and select the CGW we created earlier
      * Select **Dynamic (requires BGP)**
      *   \


          * Click **Yes, Create**

          <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-2.54.38-PM-1024x643.png" alt=""><figcaption></figcaption></figure>
   2. Select your newly created VPN and click the **Download Configuration** button.
      * For **Vendor** select **Generic**
      * Click **Yes, Download**
      *

          <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-2.55.09-PM-1024x571.png" alt=""><figcaption></figcaption></figure>
      * Click **Cancel** to close the modal window
6. **Open** the configuration file you just downloaded. We’ll use the information contained in it to configure pfSense. This will have two VPN connections listed. Whichever one you choose, make sure you’re consistent with it to make sure you are inputting the correct settings in pfSense.
7.

    <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.16.54-PM-1024x522.png" alt=""><figcaption></figcaption></figure>

### **pfSense** <a href="#pfsense-awscloud-pfsense" id="pfsense-awscloud-pfsense"></a>

1. Login to pfSense and go to **System -> Package Manager**
   * Select **Available Packages**
   * Search for “bgp”
   * Find the **OpenBGPD** package and hit **Install**, and then **Confirm**
   * Wait for the install to complete
2. Go to **Firewall -> Virtual IPs**
   1. Hit **Add**
   2. Type: **IP Alias**
   3. Interface: **Localhost**
   4. Address: **(your inside IP address)/30**
      *   In the configuration file you downloaded from AWS, scroll till you find **Inside IP Addresses** and find the **Customer Gateway** IP. This be the Virtual IP we want to put in pfSense. Don’t forget the /30!\


          <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.15.51-PM-1024x312.png" alt=""><figcaption></figcaption></figure>
   5. Add a description if you want (e.g., AWS VPN Inside Address)
   6. Leave everything else as the defaults
   7. Hit **Save** and then **Apply Changes**\

   8.

       <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.13.23-PM-1024x634.png" alt=""><figcaption></figcaption></figure>
3. Go to **VPN -> IPSec**
   1. Click **Add P1** (Add Phase 1) _(Note: The next bit of information will be found in the configuration file you downloaded from AWS)_
      1. In pfSense, set **Remote Gateway** to the IP found in your configuration file:
         * In the configuration file you downloaded from AWS, scroll till you find **Outside IP Addresses** and find the **Virtual Private Gateway** IP. This be the Public IP we want to put in pfSense for the Remote Gateway.
      2. In your configuration file, find the section that says **#1: Internet Key Exchange Configuration**. You’ll need to double check the algorithms because they may change, but the rest should be the same.
         * In pfSense, set **Pre-Shared Key** to the key found in your configuration file
         * For **Encryption Algorithm** choose **AES** and **128 bits**
         * Ensure **Hash Algorithm** is set to **SHA1**, **DH Group** is set to **2 (1024 bit)** and **Lifetime (Seconds)** is set to **28800**
         * Feel free to set a description (e.g., AWS VPN Tunnel #1)
         * Leave all other settings as their defaults and hit **Save**
         *

             <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.17.27-PM-1024x530.png" alt=""><figcaption></figcaption></figure>
   2. In pfSense, underneath your newly created VPN, click **Show Phase 2 Entries** and then click **Add P2**
      1. For **Local Network**, select **Network** and enter your **Inside IP Address** for **Customer Gateway** that’s found in the **#3: Tunnel Interface Configuration** section of the file you downloaded. Don’t forget the /30!
      2. For **Remote Network**, select **Network** and enter your **Inside IP Address** for **Virtual Private Gateway** that’s found in the **#3: Tunnel Interface Configuration** section of the file you downloaded. Don’t forget the /30!
      3. Enter a description if you’d like (e.g., AWS VPN Tunnel #1 Phase 2)
      4. Double check that the following settings match the **#2: IPSec Configuration** section of your downloaded configuration file:
         * Ensure **Protocol** is set to **ESP**
         * For **Encryption Algorithms**, ensure that only **AES is checked** and set to **128 bits**
         * For **Hash Algorithms**, ensure that only **SHA1 is checked**
         * For **PFS key group**, set **2 (1024 bit)**. This corresponds to the Perfect Forward Secrecy section of the configuration file.
         * Make sure **Lifetime** is set to **3600** seconds
      5.  Hit **Save**\


          <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.19.13-PM-1024x924.png" alt=""><figcaption></figcaption></figure>
   3. In pfSense, underneath your VPN connection, click **Show Phase 2 Entries** and then click **Add P2** again
      1. Leave **Local Network** as **LAN subnet**
      2. For **Remote Network** enter your **VPC CIDR Block** (e.g., 172.31.0.0/16)
      3. Enter a description if you’d like (e.g., AWS VPN Tunnel #1 VPC Subnet)
      4. Make sure all the **Phase 2 Proposal** settings match those in the last Phase 2 we added
         * Ensure **Protocol** is set to **ESP**
         * For **Encryption Algorithms**, ensure that only **AES is checked** and set to **128 bits**
         * For **Hash Algorithms**, ensure that only **SHA1 is checked**
         * For **PFS key group**, set **2 (1024 bit)**. This corresponds to the Perfect Forward Secrecy\
           section of the configuration file.
         * Make sure **Lifetime** is set to **3600** seconds
      5. Hit **Save** and then **Apply Changes**
      6.

          <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.21.07-PM-1024x923.png" alt=""><figcaption></figcaption></figure>
4. Go to **Firewall -> Rules**&#x20;
   1. Select **IPSec** and hit **Add** (Doesn’t matter which button)
      * Leave all settings as default, except **Protocol** change to **Any**
      * Hit **Save** and **Apply Changes**
5. Go to **Services -> OpenBGPD** _(All the following information can be found in the #4 Border Gateway Protocol (BGP) Configuration section of the downloaded configuration file)._
   1. Under the **Settings** section set the following:
      1.  Autonomous System (AS) Number: **(The number you set in your Customer Gateway in AWS)**\


          <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.22.28-PM-1024x421.png" alt=""><figcaption></figcaption></figure>
      2. Holdtime: **30**
      3. Listen on IP: **(Your inside IP Address for your Customer Gateway)**
         * You **don’t** need the /30 here!
      4. Networks: **(Your local subnet, e.g., 192.168.1.0/24)**
         * If you wish to add more local subnets to be propagated to AWS, click the **Add** button for as many networks as you have and enter your additional subnet(s)
      5.  Click **Save**\


          <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.24.33-PM-1024x823.png" alt=""><figcaption></figcaption></figure>
   2. Click on **Groups**
      1. Click **Add**
      2. Give it a name (e.g., AWS\_VPC)
      3. Enter the **Remote AS** number found in your configuration file (e.g., 7224)
      4. Give it a description if you’d like
      5. Click **Save** and then **Save** again
      6.

          <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.23.07-PM-1024x587.png" alt=""><figcaption></figcaption></figure>
   3. Click **Neighbors**
      1. Click **Add**
      2. Give it a description if you’d like (e.g., AWS VPC Neighbor)
      3. For **Neighbor**, enter the **Neighbor IP Address** found in your configuration file
      4. Make sure **Group** is set to what you named the group in the previous step
      5.  Leave the rest of the settings as default and hit **Save**\
          \


          <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.23.34-PM-1024x627.png" alt=""><figcaption></figcaption></figure>
6. Go to **Status -> IPsec**
   1. If your VPN isn’t connected already, click **Connect**
   2. After a couple of seconds, refresh the page and ensure the VPN status is **ESTABLISHED**. If it’s stuck on CONNECTING, double check your settings and try again.
   3.

       <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.37.13-PM-1024x499.png" alt=""><figcaption></figcaption></figure>
7. Go back to **Services -> OpenBGPD**
   1. Click **Status**
   2.

       <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.25.08-PM-1024x540.png" alt=""><figcaption></figcaption></figure>
   3. If everything worked right, you should see a connection time on the Up/Down column of the OpenBGPD Summary table and route information being exchanged.&#x20;
   4.

       <figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.25.23-PM-1024x348.png" alt=""><figcaption></figcaption></figure>

### **Testing Connectivity** <a href="#pfsense-awscloud-testingconnectivity" id="pfsense-awscloud-testingconnectivity"></a>

<figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.25.57-PM-1024x350.png" alt=""><figcaption></figcaption></figure>

Back in AWS, we can go check our route tables for our VPC. In the console, inspect a route table. When you click the **Routes** tab, you should now see your routes from pfSense being propagated to AWS. Cool!

On your EC2 instances, if your security groups are configured to allow ICMP and/or SSH from your on-prem network, you should be able to ping and/or SSH between instances in your on-prem network and AWS VPC!\


<figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.28.03-PM-300x139.png" alt=""><figcaption></figcaption></figure>

In my example, I have a Ubuntu VM running in my Vng Cloud network and an EC2 instance running in my VPC. After configuring security groups, I can successfully ping between the two machines!\
\


<figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.28.48-PM-300x104.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://s3-us-west-2.amazonaws.com/1s-blog/pfsense-vpn-screenshots/Screen-Shot-2017-08-21-at-3.31.45-PM-300x127.png" alt=""><figcaption></figcaption></figure>

\
