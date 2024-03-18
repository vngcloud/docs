# Step 2. Configure Route Table

**Option 1: Add Route**

Select the desired  Route Table , in the "ROUTES" tab click the "ADD ROUTES" button

\
Enter the value "Destination" as an IP or a destination IP range that you want and select "Target" with 2 options of "Internet Gateway" or "Peering Connection". After completing the configuration, click the "SAVE" button to save your configuration.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59804067/worddav325b75ec09cfc25dab5a42727b9c6c9c.png?version=1&#x26;modificationDate=1686731653000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/download/attachments/59804067/worddavaa712dd25d81867d5bfe40f807ed19e1.png?version=1&#x26;modificationDate=1686731653000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
As the picture above is a simple example for you to better understand the  Route Table feature. In the "Destination" box we will enter the value "0.0.0.0/0" and "Target" chooses to go through "Internet Gateway", so we are allowing all IPv4 connections from the server to connect to the Internet. through  Internet Gateway.

\
**Option 2: Linking Route Table to Subnets**

Select the desired Route Table , in the tab "SUBNET ASSOCIATION" click the button "EDIT SUBNET ASSOCIATION"

\
Click on the "Subnet IDs" of the  Subnets  that you want to assign to the current  Route Table.. Once done, click the "SAVE" button to save the configuration.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59804067/worddav6299b75995ddbe02f88a0f209cdbb91d.png?version=1&#x26;modificationDate=1686731713000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

![](https://docs.vngcloud.vn/download/attachments/59804067/worddave3d6b933e0689f38831e767ccbcb9833.png?version=1\&modificationDate=1686731713000\&api=v2)

\*\*\* Note: \* Each Subnet can only be assigned to one Route Table at a time, however, 1 Route Table can be assigned to many desired Subnets.
