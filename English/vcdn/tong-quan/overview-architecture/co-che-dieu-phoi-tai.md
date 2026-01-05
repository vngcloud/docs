# Load Coordination Mechanism

**vCDN Request Router** is a system that coordinates load through vCDN's DNS service. Every 30 seconds, vCDN Request Router will check the health status of all Edge servers in the CDN network including at all different ISPs. This will help vCDN Request Router to capture the status of Edge servers almost instantaneously to remove faulty servers from the service network as soon as possible and coordinate traffic of the faulty server to other servers. When a user needs to access resources on the CDN system, the user will request to Public DNS such as Google, Cloudflare, OpenDNS or the local DNS Server of the ISP where the user is connected to the network. Public DNS servers will forward requests to the vCDN Request Router server. With the information obtained at the time of receiving the request such as:

* IP Client.&#x20;
* Current operating status of servers.&#x20;
* Load of connections between POPs.&#x20;
* Load of each POP.

<figure><img src="../../../.gitbook/assets/image (147).png" alt=""><figcaption></figcaption></figure>

The vCDN Request Router system will decide to send back the best possible IP Server to the user at that time. Specifically, the coordination rules will be implemented as follows (priority from top to bottom):&#x20;

* Users in any network and region will go to the server with the least load in that region belonging to that ISP.&#x20;
* In case the ISP's POP in the user's area has a problem or is overloaded, it will be transferred to another ISP's POP that is capable of serving in that area.

For users of small ISPs such as CMC, SPT, SCTV, Netnam, GreenNode's POP traffic will be prioritized at Quang Trung Software Park because here GreenNode has performed direct peering to each ISP as above. . This ensures good service for all end users.

**For regular Domectic (domestic) traffic, VNG currently does not guarantee speed for traffic from international sources. Customers can refer to the international vCDN service provided by VNGCloud for the best quality with international traffic or contact support@vng.com.vn for further instructions.**
