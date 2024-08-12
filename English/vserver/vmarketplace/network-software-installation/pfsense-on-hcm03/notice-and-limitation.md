# Notice & Limitation

### Default MTU

The default MTU of Pfsense is 1500. You need to adjust this parameter to match the VNG Cloud configuration of 1450.

**Step 1: Access the pfSense management interface, select the "Interfaces" tab, and configure the WAN (or LAN in use) network one by one.**

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Step 2: In the MTU section, enter the value 1450.**

Finally, click "Save" to save the configuration.

Repeat these steps for all Interfaces in use.

If you encounter any difficulties during the process, please contact VNG Cloud support.
