# Floating IP

An floating IP address (FIP) is a public IP address that you can reserve and use as an independent resource. FIPs can be retained independently and associated with or disassociated from primary interface of instances in virtual private clouds (VPCs).

### **Overview** <a href="#floatingip-overview" id="floatingip-overview"></a>

FIPs are NAT IP addresses that are located in the gateway of VNG Cloud. By means of NAT, FIPs are mapped to the primary network interfaces of the vServer instances. You can associate FIPs with vServer instances that are located in VPCs to enable the instances to communicate over the Internet. FIPs is invisible inside the operating systems of vServer instances.

### **Limits** <a href="#floatingip-limits" id="floatingip-limits"></a>

FIPs can be associated with vServer instances. An FIP can be associated only with an vServer instance that meets the following requirements:

* The vServer instance is located in a VPC.
* The vServer instance is located in the same zone as the FIP.
* The vServer instance is in the **Running** or **Stopped** state.
* No External Interface are attached

### **Operations** <a href="#floatingip-operations" id="floatingip-operations"></a>

* Create an FIP
  * You can go to {Floating IP page} to create an FIP and associate the FIP with an vServer instance that is located in a VPC and is not attached with External Interface.
* Associate an FIP with an vServer instance
  * You can log on to the {Server page} and associate an FIP with an vServer instance that is located in a VPC and is not attached External Interface.
  * You can also go to the {Floating IP page} and associate an FIP with an vServer instance that is located in a VPC and is not attached External Interface.
* Disassociate an FIP from an vServer instance
  * If your vServer instance no longer needs an FIP, you can disassociate the FIP from the instance in the {Server page}.
  * You can also disassociate the FIP from the vServer instance on the {Floating IP page}
* Release an FIP
  * Billing of an FIP continues after it is disassociated. If you no longer need the FIP, go to the {Floating IP page} to release the FIP

\
