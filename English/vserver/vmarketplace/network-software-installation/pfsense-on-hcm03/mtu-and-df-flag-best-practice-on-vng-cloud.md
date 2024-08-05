# MTU & “DF flag” best practice on VNG Cloud

The default MTU on the Internet is 1500 bytes, but virtualization technology requires additional Extended Headers, which makes the actual value less than 1500 bytes.

Currently, VNG Cloud infrastructure supports Interface MTU values of 1450 bytes. Therefore, after encapsulation of protocol/application headers, the packet sent out of the VM is recommended to be ≤ 1450 bytes (1).

If the VM sends packets with an MTU larger than the supported MTU value, it leads to "packet fragmentation." The original packet will be divided into smaller packets for transmission and reassembled at the destination. This is a normal process that occurs when data is transmitted over the Internet. "Packet fragmentation" will meet most customer needs.

However, for certain specific services like Voice SIP (UDP), VPN Tunnel (IPSec/GRE), there are two issues that often lead to problems:

* Packets are transmitted with the "Do Not Fragment" (DF flag) (2).
* Custom SIP Headers or IPSec/GRE Headers are added to the original packet, making the packet size larger than 1450 Bytes.

When both conditions occur simultaneously, the infrastructure may drop the packet from the virtual machine.

Therefore, VNG Cloud encourages customers to proactively reduce the MTU value during initialization if they are using "MTU-sensitive services that require the 'DF flag'" in one of the following ways to minimize risks when using the service:

1. Modify the Application/Service configuration to remove unnecessary Headers (e.g., custom SIP Headers, IPSec Authentication and Encryption Algorithm).
2. Change the VM's MTU (for VMs using custom flavors not following the standard VNG Cloud) to 1450 (or smaller if needed).
   *   PFSense: WEB UI - Interfaces - WAN - MTU = 1450&#x20;

       <figure><img src="../../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
   *   FortiGate CLI:Bash

       ```
       FTG_GW # config system interface
       edit <interface-name>
       set mtu-override enable
       set mtu 
       next
       end
       ```

       <figure><img src="../../../../.gitbook/assets/image (8).png" alt="" width="260"><figcaption></figcaption></figure>
   *   Ubuntu/LinuxBash

       ```
       $ ifconfig <interface_name> mtu <mtu_size> up
       ```

       Hãy thận trọng khi sử dụng các đoạn mã.Or add to the interfaces configuration file:Bash

       ```
       post-up /sbin/ifconfig <interface_name> mtu <mtu_size>
       ```

       Hãy thận trọng khi sử dụng các đoạn mã.
3. Contact the support team via the Portal.

**Note:** (1) For IPSec Tunnels requiring high authentication and encryption, the Headers value can be more than 100 bytes. Therefore, depending on usage needs, customers should choose an appropriate MTU value of 1200 - 1300 - 1450 bytes. The table below illustrates an example of IPSec Headers Size added, affecting the actual MTU value for a packet with an initial Payload of 1340 bytes.

**Table 1: NAT-T and GRE not enabled**

| Payload Size | New IPv4 Header for IPsec | AH Header | Next Header - 1 | Payload - 1 | Reserved - 2 | SPI - 4 | Sequence - 4 | AH Digest | ESP Header | SPI - 4 | Sequence - 4 | ESP IV | Original IPv4 Header | Original IPv4 Payload | ESP Trailer | ESP Pad - 2 | Pad Length - 1 | Next Header - 1 | ESP ICV - 32 | Total IPsec Packet Size sending out from VM |
| ------------ | ------------------------- | --------- | --------------- | ----------- | ------------ | ------- | ------------ | --------- | ---------- | ------- | ------------ | ------ | -------------------- | --------------------- | ----------- | ----------- | -------------- | --------------- | ------------ | ------------------------------------------- |
| 1340         | 20                        | 12        | 1               | 1           | 2            | 4       | 4            | 12        | 8          | 4       | 4            | 16     | 20                   | 1320                  | 36          | 2           | 1              | 1               | 32           | 1444                                        |

**Table 2: NAT-T enabled, GRE not enabled**

| Payload Size | New IPv4 Header for IPsec | UDP Header (NAT-T) | AH Header | Next Header - 1 | Payload - 1 | Reserved - 2 | SPI - 4 | Sequence - 4 | AH Digest | ESP Header | SPI - 4 | Sequence - 4 | ESP IV | Original IPv4 Header | Original IPv4 Payload | ESP Trailer | ESP Pad - 2 | Pad Length - 1 | Next Header - 1 | ESP ICV - 32 | Total IPsec Packet Size sending out from VM |
| ------------ | ------------------------- | ------------------ | --------- | --------------- | ----------- | ------------ | ------- | ------------ | --------- | ---------- | ------- | ------------ | ------ | -------------------- | --------------------- | ----------- | ----------- | -------------- | --------------- | ------------ | ------------------------------------------- |
| 1340         | 20                        | 8                  | 12        | 1               | 1           | 2            | 4       | 4            | 12        | 8          | 4       | 4            | 16     | 20                   | 1320                  | 36          | 2           | 1              | 1               | 32           | 1452                                        |

**Table 3: NAT-T and GRE enabled**

| Payload Size | New IPv4 Header for IPsec | UDP Header (NAT-T) | AH Header | Next Header - 1 | Payload - 1 | Reserved - 2 | SPI - 4 | Sequence - 4 | AH Digest | ESP Header | SPI - 4 | Sequence - 4 | ESP IV | New IPv4 Header for GRE | GRE Header + Tunnel Key | Original IPv4 Header | Original IPv4 Payload | ESP Trailer | ESP Pad - 6 | Pad Length - 1 | Next Header - 1 | ESP ICV - 32 | Total IPsec Packet Size sending out from VM |
| ------------ | ------------------------- | ------------------ | --------- | --------------- | ----------- | ------------ | ------- | ------------ | --------- | ---------- | ------- | ------------ | ------ | ----------------------- | ----------------------- | -------------------- | --------------------- | ----------- | ----------- | -------------- | --------------- | ------------ | ------------------------------------------- |
| 1340         | 20                        | 8                  | 12        | 1               | 1           | 2            | 4       | 4            | 12        | 8          | 4       | 4            | 16     | 20                      | 8                       | 20                   | 1320                  | 40          | 6           | 1              | 1               | 32           | 1484                                        |
