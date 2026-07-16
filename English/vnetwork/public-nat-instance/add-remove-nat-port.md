# Add/ Remove NAT Port

Inbound rules control which ports and protocols are allowed through the NAT. Every NAT is created with a set of default rules that allow common outbound services from your VPC — DNS (UDP 53), HTTP (TCP 80), HTTPS (TCP 443), and ICMP (ping). You can add more rules when needed, or remove rules you no longer need.

Open the NAT from the NAT list and go to its detail screen to see the Inbound Rules section, along with the NAT's NAT Gateway IP and Public IP.

## Add NAT port

* In the NAT list, select the NAT to which you want to add a port.
* Click the NAT name to open its detail screen.
* Go to the Inbound Rules section and click "Create an Inbound Rule".
* Fill in the fields: Protocol, Ether Type, Port range, Description.
* Click "Create".

## Delete NAT port

{% hint style="info" %}
You cannot delete system-created rules (the default DNS / HTTP / HTTPS / ICMP rules).
{% endhint %}

* In the NAT list, select the NAT from which you want to delete a port.
* Click the NAT name to open its detail screen.
* Go to the Inbound Rules section.
* Find the rule you want to delete and click the delete icon.
