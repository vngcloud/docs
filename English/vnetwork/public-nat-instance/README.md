# Public NAT Instance

A Public NAT instance on GreenNode is a networking service that allows instances in a private subnet to communicate with the internet while preventing inbound traffic from the internet to those instances.

Public NAT Instance **V2** is the new generation of the service. New Public NAT instances are created as V2 by default; existing V1 instances continue to operate normally.

## What's new in V2

{% hint style="success" %}
**Highly available**

V2 runs as a redundant pair (active/standby) with automatic failover. If one node fails, traffic continues through the other node with no action required, eliminating the single point of failure that existed in V1.
{% endhint %}

{% hint style="success" %}
**Automatic routing**

In V1, you had to log in to each VM and manually add a route to the NAT gateway. In V2, GreenNode automatically adds the default route to your VPC route table when the NAT is created, so every instance reaches the internet through the NAT — **no per-VM configuration is required**.
{% endhint %}

{% hint style="success" %}
**Works across the whole VPC**

In V1, only VMs on the **same subnet** as the NAT could route through it. In V2, **any VM in the same VPC (the entire /16)** can reach the internet through the NAT — not just the NAT's subnet.
{% endhint %}

{% hint style="info" %}
**How to tell V1 from V2**

In the **Public NAT** list, look at the **HA** column: **HA = Yes** means the NAT is **V2** (highly available); **HA = No** means it is a **V1** NAT.
{% endhint %}

The HA column on the Public NAT list: Yes = V2, No = V1

## Feature summary

| Capability                               | V1 (legacy)            | V2                                      |
| ---------------------------------------- | ---------------------- | --------------------------------------- |
| High availability / failover             | Single node            | Redundant pair, automatic failover      |
| Which VMs can use the NAT                | Same subnet only (/24) | Entire VPC (/16)                        |
| Routing for your VMs                     | Manual, per-VM         | Automatic, added to the VPC route table |
| Public interface                         | Created automatically  | Created automatically                   |
| Default allowed services (from your VPC) | DNS, HTTP, HTTPS, ICMP | DNS, HTTP, HTTPS, ICMP                  |
| Add / remove inbound rules               | Yes                    | Yes                                     |
