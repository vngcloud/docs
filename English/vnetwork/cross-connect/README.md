# Cross Connect

## Overview

**Cross Connect** is a network connection between two VPCs that allows you to route traffic between them using private IPv4 addresses connected to different regions. Virtual Machines (VMs) assigned to VPCs can communicate with each other if they are all connected via a shared connection across different regions.

To establish a **Cross Connect** connection, you need to pair a connection request from a VPC in one region (**Requester**) with the approval of a VPC in another region (**Accepter**). Once the connection is established, you can route traffic between the VPCs, allowing the Virtual Machines (VMs) in one VPC to access resources in a VPC in another region.

## VPC Connection in Cross Connect

To understand the VPC connection between two regions, see the detailed description below of a Cross Connect between two VPCs in the Hanoi and Ho Chi Minh regions:

Assume there are two data regions, Ho Chi Minh (HCM03) and Hanoi (HAN01), each with pre-established VPCs.\
Region HCM03 has the following VPCs:

* HCM-VPC01 (10.10.0.0/16);
* HCM-VPC02 (10.11.0.0/16);

Region HAN01 has the following VPCs:

* HAN-VPC01 (10.13.0.0/16);
* HAN-VPC02 (10.14.0.0/16);

Perform the creation of Cross Connect 1 to establish a connection between the Ho Chi Minh and Hanoi regions, thereby connecting the following VPC pairs across the two regions:

* HCM-VPC01 connects with HAN-VPC01;
* HCM-VPC01 connects with HAN-VPC02;
* HCM-VPC02 connects with HAN-VPC02.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption><p>A basic connection diagram of a Cross Connect link between HCM03 and HAN01.</p></figcaption></figure>

***

VNG Cloud provides users with the Cross Connect service, which can perform the following tasks:

* [Create Cross Connect](create-cross-connect.md);
* [Create a VPC Connection](create-a-vpc-connection.md);
* [Detele Cross Connect](delete-cross-connect.md);
* [VPC Connection Conditions](vpc-connection-conditions.md).
