# VPC Connection Conditions

To enable communication between two regions via Cross Connect, it is necessary to configure the connection between two VPCs. For a successful connection between the two VPCs, certain conditions must be met; otherwise, the system will display an error and not allow the connection to be established.

**The conditions for two VPCs to connect are:**

<table><thead><tr><th width="94">No.</th><th>Conditions</th><th>Error Code</th></tr></thead><tbody><tr><td>1</td><td>The two VPCs from different regions must not have overlapping CIDR blocks.</td><td>Overlaping cidr each others (code 2009)</td></tr><tr><td>2</td><td>Connecting two VPCs that already have an existing connection is not allowed. Even if creating a different Cross Connect, the connection cannot be established.</td><td>Existing a VPC Connect for this couple of VPCs (code 2010)</td></tr><tr><td>3</td><td>It is not allowed to create a VPC connection when a VPC in the Requester role has an existing connection with a VPC in the Accepter role that has overlapping CIDR blocks.</td><td>Existing a VPC Connection in Cross Connect opens from this CIDR (code 2011)</td></tr><tr><td>4</td><td>It is not allowed to create a VPC connection when a VPC in the Accepter role has an existing connection with a VPC in the Requester role that has overlapping CIDR blocks.</td><td>Existing a VPC Connection in Cross Connect opens to this CIDR (code 2013)</td></tr><tr><td>5</td><td>The two VPCs connected to each other must not be in the same region.</td><td>Not able to create VPC Connect in the same Region (code 2012)</td></tr></tbody></table>

## Example of error codes when creating a VPC connection:&#x20;

### <mark style="color:blue;">\[Error Code 2010] An existing VPC connection pair already exists.</mark>

<figure><img src="../../.gitbook/assets/image (289).png" alt=""><figcaption></figcaption></figure>

From the diagram, we can see that:

* At time T, the user can successfully create a connection from HCM-VPC01 to HAN-VPC01 between the two regions via Cross Connect 1.
* At time T+1, the system no longer allows the creation of a connection between HCM-VPC01 and HAN-VPC01, as this connection was previously established in the same Cross Connect.
* Creating a connection pair between HCM-VPC01 and HAN-VPC01 in a different Cross Connect at a later time (T+2) is also not possible, as the system will check whether the VPC pair already exists in another Cross Connect.

### <mark style="color:blue;">\[Error Code 2011] Overlapping CIDR of a VPC connection in the Cross Connect at the Requester.</mark>

<figure><img src="../../.gitbook/assets/image (290).png" alt=""><figcaption></figcaption></figure>

From the diagram, we can see that:

* At time T, the user can successfully create a connection from HCM-VPC02 to HAN-VPC01 between the two regions via Cross Connect 1.
* At time T+1, the system does not allow the creation of a connection from HCM-VPC03 to HAN-VPC03, due to the CIDR block 10.15.0.0/16 of HCM-VPC02 (which was previously connected to HAN-VPC01) **overlapping with the CIDR of HAN-VPC03** that HCM-VPC03 is attempting to connect to.

### <mark style="color:blue;">\[Error Code 2013] Overlapping CIDR of a VPC connection in the Cross Connect at the Accepter.</mark>

<figure><img src="../../.gitbook/assets/image (291).png" alt=""><figcaption></figcaption></figure>

From the diagram, we can see that:

* At time T, the user can successfully create a connection from HCM-VPC01 to HAN-VPC02 between the two regions via Cross Connect 1.
* At time T+1, the system does not allow the creation of a connection from HCM-VPC03 to HAN-VPC03, because the CIDR block 10.14.0.0/16 of HAN-VPC02 (which was previously connected to HCM-VPC01) **overlaps with the CIDR of HCM-VPC03** that is attempting to connect to HAN-VPC03.
