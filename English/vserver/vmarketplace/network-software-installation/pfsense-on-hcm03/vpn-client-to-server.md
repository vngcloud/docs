# VPN Client to Server

**OpenVPN**

OpenVPN, written by James Yonan and released under the GNU GPL open-source license, offers several advantages for VPN deployment:

* **Operates at Layer 2 and Layer 3:** It can transport frames, packets, and NETBIOS (Windows Network Browsing packets), addressing common issues in other VPN solutions.
* **High Compatibility:** OpenVPN connections are compatible with most firewalls and proxies. If you can connect to remote computers via HTTPS, you can also use OpenVPN.
* **UDP and TCP Support:** OpenVPN can operate with either UDP or TCP, using port 1194 UDP and 443 TCP.
* **High Performance:** OpenVPN supports data compression at the endpoints before transmission (using the LZO library).
* **Cross-Platform Installation:** Deploying OpenVPN on both the server and client sides is relatively easy compared to IPSec. OpenWrt/FreeWrt, operating systems integrated into hardware devices, also work well with OpenVPN.

**OpenVPN in pfSense**

Setting up OpenVPN in pfSense is straightforward, involving the following steps:

1. Create a CA (Certificate Authority) and Certificates in System -> Cert Manager.
2. Create a user for VPN login in System -> User Manager.
3. Configure the OpenVPN Server in VPN -> OpenVPN, specifying authentication methods, CA, Certificates, network, firewall rules, etc.
4. Install the openvpn-client-export package and extract the OpenVPN login configuration.
5. On the computer connecting to the VPN, download the exported file and import it into the OpenVPN software (downloaded from openvpn.net), then log in using the created username and password.

**Setting up OpenVPN on pfSense**

* The connection model for deploying OpenVPN on pfSense involves pfSense 2 as the OpenVPN Server and a Windows 7 computer as the OpenVPN Client.
* From the pfSense 2 web configuration interface, start by creating a CA in System -> Cert Manager.
* Next, add a certificate for the OpenVPN Server in the Certificates tab, selecting the previously created CA and Server Certificate as the Certificate Type.
* Create a VPN User in System -> User Manager -> Users, and then create a User Certificate for this user in System -> Certificate Manager -> Certificates.
* Assign the created certificate to the user in System -> User Manager -> Users.
* Install the openvpn-client-export package to export the OpenVPN configuration file for the client.
* Configure the OpenVPN Server in VPN -> OpenVPN -> Wizards, selecting Local User Access and specifying tunnel network, local network, and concurrent connections.
* Create corresponding firewall rules.
* Export the configuration file for the OpenVPN Client and import it into the OpenVPN software on the Windows 7 computer.
* Connect to the OpenVPN Server using the created username and password.

Upon successful connection, you should be able to ping the LAN IP of pfSense 2.
