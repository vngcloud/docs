# Getting Start with Synthetic

### Step 1: Create a Synthetic Test quota <a href="#batdauvoisynthetics-buoc1-khoitaosynthetictestquota" id="batdauvoisynthetics-buoc1-khoitaosynthetictestquota"></a>

To start using the service, you need to create a Synthetic Test quota. A Synthetic Test quota is a term on the vMonitor Platform representing a monitoring package with a specific number of tests that you purchase on VNG Cloud. At any given time, you can own one Synthetic Test quota and use it to monitor your system's operations.

Follow the steps below to create a project:

1. Login into [https://hcm-3.console.vngcloud.vn/vmonitor](https://hcm-3.console.vngcloud.vn/vmonitor).&#x20;
2. Select **Quota & Usage**.
3. Select **Mua Synthetic test quota.**
4. Select **Class** you need. Currently, we only provide the Basic class for you to experience.
5. If you choose the **Basic** class, you will not be able to customize the package configuration. For more detailed information about the classes, please refer to Synthetic Test Quota Class.
6. Select **Buy Synthetic Test Quota**.
7. Follow the steps to **Checkout** the cart, and after successful payment, the **Synthetic test quota** will be created.

The cost calculation for each Synthetic Test quota package is publicly available on the VNG Cloud homepage, please refer to Cost Calculation.

***

### Step 2: Install API Test with HTTP(s) <a href="#batdauvoisynthetics-buoc2-caidatapitestvoihttp-s" id="batdauvoisynthetics-buoc2-caidatapitestvoihttp-s"></a>

API HTTP tests allow you to send HTTP(s) requests to your service or application to **verify responses or defined conditions** such as "status code, header, or body content" that you established when creating the API test.

**To perform API Testing using HTTP(s) method, follow the instructions below:**

1. Login into vMonitor Platform.
2. Select menu **Synthetic test.**
3. Select  **API test.**
4. Select **Create an API test.**
5. Input the informations:

* **Test Information**: define the basic information, choose the HTTP method, and specify the URL to be tested
  * **Test name:** name of API test
  * **Test type**: testing protocol, you choose HTTP(s)
  * **Verify** **ssl**: Choose whether to check SSL (True or False)
  * **Method:**&#x43;hoose a method to check your endpoint (Get, Post, Put, Delete)
  * **URL**: Fill in the service information you want to check, for example [https://google.com](https://google.com/)

<figure><img src="../../.gitbook/assets/image (38) (1) (1).png" alt=""><figcaption></figcaption></figure>

* After filling in the Test Information, you can select **Run Test or Test Again** if you have tested before to check. You can see the returned information such as status code, header, and body.

<figure><img src="../../.gitbook/assets/image (39) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Test Assertion**
  * Assertions define what you expect from the API Test results. If the returned results match your definition, the API Test will indicate that the URL being tested is successful; otherwise, it will indicate failure. The system will automatically add an assertion for the status code after you run the test; you need to define at least one assertion for the API test. In addition to the status code assertion automatically added by the system, you can add any other assertions we support, such as Response Time, Header, Body, and Certificate.

<figure><img src="../../.gitbook/assets/image (40) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Location**
  * Select a Location to run HTTP Tests to your URL. HTTP tests can be executed from both Public Locations (managed by VNG Cloud) and Private Locations (self-installed and managed by customers) based on your need to run tests from outside (internet) or inside your network. Public Locations managed by VNG Cloud currently include two locations: HCM and HN.

<figure><img src="../../.gitbook/assets/image (41) (1) (1).png" alt=""><figcaption></figcaption></figure>

*   **Alarm conditions:** Set up alarm conditions to identify scenarios where the checks fail and trigger an alert.

    * **Interval**: how often the API Test will check, default is 1 minute
    * **Time of failure**: How many consecutive failures will trigger an alert?
    * **Locations with failure**: How many failed locations trigger an alert?

    For example, when you select Time of failure: 1 and Locations with failure: 2, it means you will be alerted if a test fails once consecutively in 2 out of 2 locations.

    * **Notifications**: choose notification channels for when the status changes to In-alarm, Up, or Undetermined. The system will notify according to this list.

<figure><img src="../../.gitbook/assets/image (42) (1) (1).png" alt=""><figcaption></figcaption></figure>

6. Then click the "**Create**" button to create an API test. Once created, you will see the API test in an Undetermined state. The status will be updated accurately in the next interval.

<figure><img src="../../.gitbook/assets/image (43) (1) (1).png" alt=""><figcaption></figcaption></figure>

* The API Test has changed to the Up status when the URL is functioning normally.

<figure><img src="../../.gitbook/assets/image (44) (1) (1).png" alt=""><figcaption></figcaption></figure>

* To view details about the API Test:

<figure><img src="../../.gitbook/assets/image (45) (1) (1).png" alt=""><figcaption></figcaption></figure>
