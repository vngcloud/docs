# Interconnect

VNG Cloud Interconnect service is the optimal choice for connecting to your VNG Cloud resources directly and efficiently. When using Interconnect, your data moves through the internal network system of VNG Cloud without the need to use the public Internet. This helps reduce the risk of network congestion or unexpected delays. When you need to establish a new connection, you can deploy a dedicated connection from VNG Cloud. Additionally, we allow you to transfer data between VNG Cloud Direct Connect locations to build a private network, providing flexible connections between offices and data centers in your network.

***

### Operation Method <a href="#interconnect-cachthuchoatdong" id="interconnect-cachthuchoatdong"></a>

1. **Physical Connection Setup:**
   * Establish the necessary physical connection from your organization's location to the VNG Cloud data center. This physical connection typically uses fiber optic cables or other transmission technologies to connect directly from your organization's internal network to our Direct Connect station.
2. **Physical Layer:**
   * At the Direct Connect station, there is a physical layer that provides network infrastructure to handle and route data from your physical connection.
   * Dedicated network devices and optical cable systems ensure high performance and reliability of the connection.
3. **Logical Connection (Virtual LAN):**
   * Once the data has passed through the physical layer, the organization needs to establish a logical connection using virtual LANs (VLANs).
   * These VLANs are used to determine how to connect to specific resources and services in the cloud.
4. **Data Transmission through Logical Connection:**
   * Once the logical connection is established, data can be transmitted through this connection.
   * Data travels from the organization's internal network, through the physical connection, then through the physical layer, and finally through the logical connection to reach the VNG Cloud resources and services.
5. **Using Direct Connect for Cloud Access:**
   * The organization uses Direct Connect to access VNG Cloud resources and services from the service provider.
   * This ensures higher security and performance compared to using the public Internet.

***

### UseCase <a href="#interconnect-truonghopsudung" id="interconnect-truonghopsudung"></a>

{% tabs %}
{% tab title="Connecting Offices and Branches" %}
Connect your VNG Cloud network to base networks to develop scalable applications without impacting performance.
{% endtab %}

{% tab title="Bandwidth-Intensive Applications. " %}
Applications that require high bandwidth, such as streaming video applications or computational science projects, often use Interconnect to obtain higher bandwidth and reliability than public Internet.
{% endtab %}

{% tab title="Combined Network System Setup" %}
Connect your VNG Cloud network to base networks to develop scalable applications without impacting performance.
{% endtab %}
{% endtabs %}
