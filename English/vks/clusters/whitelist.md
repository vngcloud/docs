# Whitelist

#### O**verview** <a href="#tong-quan" id="tong-quan"></a>

The IP Whitelist feature on VKS's Private Node Group mode allows you to only allow specific IP addresses to connect to your Cluster. This helps increase security for applications and sensitive data by restricting access from unknown sources.

**Benefit**

* **Enhanced security:** IP Whitelist helps protect your data and applications from potential threats on public networks, such as cyberattacks and data breaches.
* **Minimize risk:** By restricting access to sensitive nodes, Whitelist IP helps minimize the risk of spreading a data breach to other parts of your network.
* **Greater control:** Whitelist IP allows you to tightly control access to your nodes, ensuring only authorized users and applications can access.

**Recommendations for Using Whitelist in Cluster Models:**

## **1. Public Cluster Only Includes Public Node Group**

* **Recommendation** : Not recommended to use whitelist.
*   If you need to use Whitelist IP for security, please allow vServer's IP Range Public list according to the following list:

    Copy

    ```
    103.245.249.0/24
    103.245.251.0/24
    116.118.95.0/24
    58.84.1.0/24
    58.84.2.0/24
    61.28.226.0/24
    61.28.227.0/24
    61.28.229.0/24
    61.28.230.0/24
    61.28.231.0/24
    180.93.182.0/24
    61.28.233.0/24
    61.28.235.0/24
    61.28.236.0/24
    61.28.238.0/24
    180.93.183.0/24
    ```

## **2. Public Cluster Includes Private Node Group Going Through NAT Gateway (Pfsense, PaloAlto)**

* **Recommendation** : Can use whitelist feature.
* Need to whitelist additional IP of NAT Gateway.

## **3. Private Cluster Includes Public Node Group or Private Node Group (Coming soon)**

***

## Edit Whitelist <a href="#chinh-sua-whitelist" id="chinh-sua-whitelist"></a>

To use the IP Whitelist feature on Private Node Group mode, you need to perform the following steps:

**Step 1:** Visit [https://vks.console.vngcloud.vn/overview](https://vks.console-dev.vngcloud.tech/overview)

**Step 2: At the Overview** screen , select the **Kubernetes Cluster menu.**

**Step 3:** Select the icon ![](https://docs.vngcloud.vn/\~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fthumbnails%2F73762015%2Fimage2024-4-16\_15-51-55.png%3Fversion%3D1%26modificationDate%3D1713262579000%26api%3Dv2\&width=40\&dpr=4\&quality=100\&sign=10c09f1b\&sv=1)and select **Edit Whitelist or select the Edit** icon when viewing details of a Cluster to add a Whitelist to your Cluster.

**Step 4:** Now, the **Edit Whitelist** screen displays, you can enter the IP address you want to allow access to the Cluster then select **Add** .

**Step 5:** Repeat step 4 if you want to add more **Whitelist IPs** to your Cluster. You can also select **Delete** to delete the Whitelist IP you added previously.

**Step 6:** Select **Save** to save the information or **Cancel** to cancel saving these parameters.
