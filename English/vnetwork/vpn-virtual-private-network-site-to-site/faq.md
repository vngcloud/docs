# FAQ



## How can we know VPN Tunnel is successfully ESTABLISHED

VPN service will support the status at Phase 1 and Phase 2 in the closest release. Therefore, users can know the status of each phase

Besides that, we also provide an "log" tab to help users have an overview of the connection log.

## VPN Tunnel is ESTABLISHED, but cannot ping between 2 client

Maybe you did not add the route table at your VPC to routing traffic to go through VPN via the VPN gateway IP. Check more at the final step of creating a VPN tunnel[#step-4-create-a-route-to-route-traffic-to-remote-lan-cidr-through-vpn-private-gateway-ip-view-at-det](create-vpn-site-to-site/#step-4-create-a-route-to-route-traffic-to-remote-lan-cidr-through-vpn-private-gateway-ip-view-at-det "mention")

## Example to config VPN in real world

Yes, we have a [demo-site-to-site-vpn.md](demo-site-to-site-vpn.md "mention") that demo full steps of iniailize a connection between **PFsense** and GreenNode VPN. You can watch it here





