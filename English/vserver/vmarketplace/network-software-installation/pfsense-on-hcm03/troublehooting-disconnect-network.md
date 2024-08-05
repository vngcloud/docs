# Troublehooting - Disconnect network

This guide aims to assist you in troubleshooting and resolving network connectivity issues in firewall applications, specifically pfSense. Network disconnections in firewall applications can occur due to various reasons, and here are some common causes:

1. **Configuration Errors:** Incorrect or incompatible configurations can lead to network disconnections.
2. **Resource Overload:** If your firewall application is operating under high load and lacks sufficient resources, it can result in network disconnections. This can happen when there are too many simultaneous requests or data flows.
3. **Software Updates:** Installing new software versions, including firmware, drivers, or security patches, can cause problems and network disconnections if not done correctly.
4. **Router Restart:** When the router is restarted, existing network connections may be interrupted and require time to re-establish. This can lead to temporary network disruptions or disconnections for computers and devices on the network.

Within the scope of this article, we specifically address network disconnections caused by router restarts and provide solutions to help you resolve this issue.

**Causes of Router Restarts**

Router restart errors can occur due to various reasons, including:

1. **Software Issues:** Software bugs, incompatibilities between software versions, computer viruses, or malware can cause router restarts.
2. **Overload or Conflicts:** When the router operates under high load, lacks resources, or experiences conflicts between configuration rules, it can lead to errors and restarts.
3. **Incorrect Setup:** Incorrect configuration or errors during the router setup process can cause restarts.
4. **Network Issues:** Network-related problems like high latency, connection loss, or IP conflicts can trigger router restarts.

**Troubleshooting Steps**

To minimize the impact of network disconnections caused by router restart errors in firewall applications, specifically pfSense, you can follow these instructions:

**Step 1: Access the pfSense management interface, select the "Interfaces" tab, and configure the WAN and LAN networks one by one.**

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

**Step 2: Configure the WAN network**

* Under "General Configuration": In the "IPv4 Configuration Type" property, select "Static IPv4" (1).
* Under "Static IPv4 Configuration": In the "IPv4 Address" property, enter the public IP of the pfSense server (viewable on the vServer website) with the subnet /26 (2 and 3).
* Next, select "Add new gateway" with the gateway IP depending on the public IP at the time of creation (4).
* Finally, click "Save" to save the selected configuration (5).

<figure><img src="../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

**Step 3: Configure the LAN network (Similar to WAN configuration)**

* Under "General Configuration": In the "IPv4 Configuration Type" property, select "Static IPv4" (1).
* Under "Static IPv4 Configuration": In the "IPv4 Address" property, enter the private IP of the pfSense server (viewable on the vServer website) with the subnet /24 (2 and 3).
* Next, select "Add new gateway" with the gateway IP (corresponding to the WAN configuration) as .1 (4).
* Finally, click "Save" to save the selected configuration (5).

**Note:** If you have followed the instructions above but the issue persists, please contact our support team for further assistance.
