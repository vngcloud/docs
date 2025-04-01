---
description: >-
  vNetwork is a network service that provides a secure and isolated network
  environment for your virtual machines (VMs) in the VNG Cloud platform.
---

# vNetwork

### \[vNetwork] How can private VMs access the internet without external interfaces or floating IPs?

Private VMs can access the internet through NAT (Network Address Translation) service. NAT provides secure internet access while protecting your VMs from direct internet access.

### \[vNetwork] How can I modify NAT bandwidth?

VNGCloud NAT supports bandwidths up to 10 Gbps. By default, networks are limited to 300 Mbps. You can upgrade your bandwidth package to scale according to your needs.

### \[vNetwork] Why can't I access the internet even after creating NAT successfully?

To enable internet access through NAT, you need to add a route in either:

* Your VPC Route Table, or
* The VM's routing table

### \[vNetwork] How can VMs communicate with vStorage privately?

You can use [Endpoint Service ](../vnetwork/endpoint/create-endpoint.md)to establish private communication between VMs and vStorage.

### \[vNetwork] Why can't I access VNG Endpoint Service after creating it successfully?

To resolve Endpoint Service connectivity issues:

1. [Add the host](../vnetwork/public-nat-instance/create-nat.md) entry in your VMs
2. Configure the system to resolve the Endpoint Domain as a private IP

### \[vNetwork] Why can't I establish a connection with Remote VPN?

Check the VPN connection logs in your VPN details for specific error information.

### \[vNetwork] Why can't two VMs connect to each other even when the VPN connection is ESTABLISHED?

Check your [Route Table configuration ](../vnetwork/vpn-virtual-private-network-site-to-site/create-vpn-site-to-site/#step-4-create-a-route-to-route-traffic-to-remote-lan-cidr-through-vpn-private-gateway-ip-view-at-det)to ensure proper routing between the VMs.
