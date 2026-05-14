# Pool Members

Pool Members are the individual servers within a server group (Pool) on a Load Balancer. They are responsible for serving requests from users or other devices through the Load Balancer. Let's explore how Pool Members work and their key attributes:

#### Weight

* **Explanation:** Weight determines the priority of each Pool Member in handling requests. Members with higher weights will receive more requests than those with lower weights.
* **Example:** If you have two members with weights of 3 and 1, the member with weight 3 will receive approximately 75% of requests, while the member with weight 1 will receive about 25%.

#### Port

* **Explanation:** The port on which the member will listen for incoming requests. This port is usually associated with the specific service that the member provides.
* **Example:** If you have a web application running on a member, you might use port 80 for HTTP and port 443 for HTTPS.

#### Monitor Port

* **Explanation:** This is the port the Load Balancer uses to perform health checks on the member. The Load Balancer sends test requests to this port to ensure that the member is functioning correctly. If not specified, the Monitor Port defaults to the same port used for receiving incoming requests.
* **Example:** If you want to check the health of a web server, you could use port 80 or 443 to check its availability.

#### Backup Role

* **Explanation:** This attribute defines the role of the member within a Pool. There are two main roles: Primary and Backup. Primary members receive regular traffic from users, while Backup members only receive requests when the Primary members are unavailable.
* **Example:** If you have two members in a Pool, Member A with the Primary role and Member B with the Backup role, requests will be sent to Member A first. If Member A becomes unavailable, the Load Balancer will redirect requests to Member B.

#### Overall Mechanism

This mechanism allows you to customize how the Load Balancer distributes traffic among members in a Pool. By using weights, you can fine-tune the distribution of traffic. Additionally, the Backup role helps ensure the availability and reliability of your system in case a Primary member fails.

#### Related Topics

* **Attaching Pool Members**
