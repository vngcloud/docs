---
description: >-
  VPN Site-To-Site is a private connection to communicate between two or more
  private network through a secure connection and safety.
---

# Demo Site-to-Site VPN

Below is a demonstration of how to connect two LAN networks via the internet secured by a VPN connection (two VPNs at 2 sites)

* Site A: VPC 10.1.0.0/16 with VPN server using PFsense of GreenNode Market Place.
* Site B: VPC 10.200.0.0/16 with VPN server using GreenNode VPN Site-To-Site Service

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Demostration</p></figcaption></figure>

## 1.    Create a Remote Site VPN (using PFsense)

### a.      Create PFsense server

* Access link [https://marketplace.console.vngcloud.vn/overview](https://marketplace.console.vngcloud.vn/overview)
* Click Launch
* Choose Flavor (example 2x4)
* Network Settings: External Interface Priority = 1

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>vMarket Placer - pfSense </p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Request Pfsense - Config Network</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Request Pfsense - Config Network</p></figcaption></figure>

### b.    Access PFsense Dashboard

* Go to vServer page
* Show detail Created Server and open new Url with IP Public https://\<FixedIp>.
* Login with default user admin/pfsense

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Server List</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Server Detail</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Admin Dashboard</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Welcome Page</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Dashboard - DNS config</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Dashboard - Timezone config</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Dashboard - WAN config - Keep default</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (10) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Dashboard - Update Password</p></figcaption></figure>

### c.  Config pfsense Network

* Allow port 443 [**https://61.28.239.244/firewall\_rules.php?if=wan**](https://61.28.239.244/firewall_rules.php?if=wan)

<figure><img src="../../.gitbook/assets/image (11) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Firewall Rule - Allow 443</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Firewall Rule - Allow UDP any</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (13) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Firewall Rule - Allow UDP any</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (14) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Firewall Rule - Result</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (15) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**-**          Access to Assign Interface LAN 10.1.0.0/24. [**https://61.28.239.244/interfaces\_assign.php**](https://61.28.239.244/interfaces_assign.php)

<figure><img src="../../.gitbook/assets/image (16) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Interface Assignments - Add LAN Interface</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (17) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Interface Assignments - Result</p></figcaption></figure>

\- Enable LAN Interface [https://61.28.239.244/interfaces.php?if=lan](https://61.28.239.244/interfaces.php?if=lan)

<figure><img src="../../.gitbook/assets/image (18) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Interface Lan - Enable Use of LAN</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (19) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Interface Lan - Result</p></figcaption></figure>

**-**      Access **https://\<FixedIp>/firewall\_rules.php**  to config firewall rule for LAN

<figure><img src="../../.gitbook/assets/image (20) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Firewall Lan</p></figcaption></figure>

**-**          Access **https://\<FixedIp>/firewall\_rules.php**  to config firewall rule

<figure><img src="../../.gitbook/assets/image (21) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>pfSense Firewall IPSec</p></figcaption></figure>

## 2. Create a Local Site VPN (using VNGCloud VPN)

### a. Create VPN

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>VNGCloud VPN creates</p></figcaption></figure>

### b. Detail VPN

<figure><img src="../../.gitbook/assets/image (24) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>VNGCloud VPN - Detail</p></figcaption></figure>



## 3. Config pfSense VPN IPSec

### a.      Config IPSec Phase 1

* Access IPSec Dashboard _https://\<FixedIp>/vpn\_ipsec.php_. _**Figure 3 IPSec Dashboard**_
* Click “Add P1” to config Phase 1
* Fill your information
  * Key Exchange version: IKEv2
  * Protocol IPv4
  * Interface WAN
  * Remote gateway: Input \<FixedIp>
  * Pre-shared Key: Input your random preshare (anything you want) -> this key will use to input on VNG’s VPN (**Important!**)
  * Encryption Algorithm
* Method AES256 CGM, Key length 128, Hash 256, DH Group 3072 (**Important**!)
  * Life Time: 4 hours = 144000 (**Important!**)
* **Save**

<figure><img src="../../.gitbook/assets/image (25) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Figure 4 IPSec Dashboard</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (26) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (27) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (28) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (29) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### b.      Config IPSec Phase 2

* Click Add “Phase2”
* Local Network: LAN Subnet
* Remote Network: VPC GreenNode (you selected in create VPN flow) 10.200.0.0/16
* Encryption Algorithms: AES256 (**Important!**)
* Hash SHA 256 (**Important!**)
* LifeTime 16h = 57600 (**Important!**)
* SAVE
* Apply Changes

<figure><img src="../../.gitbook/assets/image (30) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (31) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<div data-full-width="true"><figure><img src="../../.gitbook/assets/image (32) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure></div>

### f.      Check Status IPSec

* Access IPSec Status link https://\<FixedIP>/status\_ipsec.php
* Click **Connect P1 and P2s**

<figure><img src="../../.gitbook/assets/image (33) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (34) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 4.    Add route on Local Site

* Access VPN Detail and copy Local Private Gateway
* Access vServer Router Tables to config routing for VPN
  * Destination: Remote Private CIDR (10.1.0.0)
  * Target: Local Private Gateway (10.200.3.3)

<figure><img src="../../.gitbook/assets/image (306).png" alt=""><figcaption><p>VPN Detail - Page</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (307).png" alt=""><figcaption><p>Update Route Table</p></figcaption></figure>



## 5.    Add route on Remote Site

<figure><img src="../../.gitbook/assets/image (35) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



## 6.    Testing Ping Between 2 Client VM

<figure><img src="../../.gitbook/assets/image (36) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>







