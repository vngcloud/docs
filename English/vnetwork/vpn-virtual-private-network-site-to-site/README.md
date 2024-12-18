---
description: >-
  VPN Site to Site is a private connection to communicate between  two or more
  private network through a secure connection and safety.
---

# VPN (Virtual Private Network) Site To Site

## Overview

Default, the VMs are created in a VPC that cannot communicate with a remote private network. Therefore, to access the remote private network from a VPC, the VNGCloud private VPN service creates a **Virtual Private Network (VPN) Site-to-Site** and configures routing traffic through this connection. Besides that, this connection is secure connection and safe cause using the **IPSEC** algorithm for authentication and encrypting data at two terminal VPNs local and remote.

Connection Site-to-Site VPN supports connecting with Protocol Internet Protocol security (IPsec).

## Connection between sites

To understand more about the connection between sites, let's take a look at detailed describe

For example, we have 3 network sites, that are Hồ Chí Minh (HCM03), Hà Nội (HAN01), and Private Network (on-premise), each site already setup VPCs

Region HCM03 has VPCs:

* VPC1 (10.1.0.0/16);
* VPC2 (10.2.0.0/16).

Region HAN01 has VPCs:

* VPC1 (172.16.0.0/16);

At Site On-Premise has network:

* 192.168.1.0/24
* 192.168.2.0/24&#x20;
* 192.168.3.0/24

Create VPN Connections:

* VPNGW-01 of HCM03 <> VPNGW-01 of HAN01;
* VPNGW-01 of HCM03 <> Router of On-Premise;
* VPNGW-02 of HCM03 <> Router of On-Premise.

After finishing create VPN between above connections:

* HCM03 VPC01 includes route 172.16.0.0/16 of HAN01 and 192.168.1.0/24 of On-Premise System.
* HCM03 VPC02 includes route 192.168.1.0/24 and 192.168.2.0/24 of On-Premise System.



<figure><img src="../../.gitbook/assets/image (37) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Basic Diagram VPN</p></figcaption></figure>

***

VNG Cloud provides users VPN service with the below actions:

* [Create VPN Site-to-Site](create-vpn-site-to-site/)
* [VPN Connect Condition](create-vpn-site-to-site/vpn-connect-condition.md)
* [Change VPN Bandwidth](change-vpn-bandwidth.md)
* [VPN Packages](vpn-packages.md)
* [Delete VPN](delete-vpn.md)
