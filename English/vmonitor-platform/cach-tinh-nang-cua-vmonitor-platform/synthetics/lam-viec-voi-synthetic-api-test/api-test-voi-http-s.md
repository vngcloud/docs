# API Test with HTTP(s)

API HTTP tests allow you to send HTTP request(s) to your service or application to **verify the response or specified conditions** such as "status code, header or body content" that you set when creating the API test

**To perform API Test creation with HTTP(s) method, follow the instructions below:**

1. Log in to vMonitor Platform [here.](https://hcm-3.console.vngcloud.vn/vmonitor)
2. Select the Synthetic test folder **.**
3. Select **API test.**
4. Select **Create an API test.**
5. Enter information including:

*   **Test Information: define basic information, select HTTP method and specify URL to test**

    * **Test name:** name of the API test
    * **Test type** : test protocol, you choose HTTP(s)
    * **Verify** ssl: choose whether to check ssl or not (True or False)
    * **Method:** select the method that will test your endpoint (Get, Post, Put, Delete)
    * **URL** : fill in the service information you want to check, for example [https://google.com](https://google.com/)

    ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fattachments%2F59803715%2Fimage2022-8-29_16-20-38.png%3Fversion%3D1%26modificationDate%3D1686544451000%26api%3Dv2\&width=768\&dpr=4\&quality=100\&sign=c3ead0cc\&sv=1)

    <figure><img src="../../../../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
* After filling in the Test Information, you can choose **Run Test or Test Again** if you have previously tested, you can see returned information such as status code, header and body.

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Test Assertion**
  * Assertion defines what you expect the API Test result to be, if the returned result meets what you define API Test will show the URL you are testing as successful, and vice versa API Test will show the URL you are testing test is failed. The system will automatically add the Assertion status code for you after you Run the test, you need to define at least one Assertion for the API test. In addition to the Assertion status code that the system automatically adds, you can add any other Assertion that we support as below: Response time, Header, Body, Certificate

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

*   **Location**

    * Select the Location that will run HTTP Tests to your URL. HTTP tests can be run from both Public Locations (managed by VNG Cloud) and Private Locations (installed and managed by customers) based on your needs for running tests from outside (internet) or inside the network. your. Public Locations managed by VNG Cloud currently has 2 locations: HCM and Hanoi.

    ![](https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2Fdocs-admin.vngcloud.vn%2Fdownload%2Fattachments%2F59803715%2Fimage2022-8-29_16-42-28.png%3Fversion%3D1%26modificationDate%3D1686544452000%26api%3Dv2\&width=768\&dpr=4\&quality=100\&sign=4b6253a4\&sv=1)

    <figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
* **Alarm conditions:** Set up alarm conditions to define the cases where you want the test to fail and trigger the alarm.
  * **Interval** : how often API Test will test once, default will be 1p
  * **Time of failure** : how many consecutive failures will alert
  * **Locations with failure** : how many locations fail to warn
  * For example, when you select Time of failure: 1 and Locations with failure: 2, it will be understood as: you will be warned if the Test fails 1 time in a row from 2 out of 2 locations.
  * **Notifications** : you choose notification channels when switching to In-alarm, Up or Undertermine states, the system will notify according to this list.

<figure><img src="../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

6\. Then press the " **Create** " button to initialize the API test. After creating, you will see the API test is in Undertermine state, until the next inteval the Test API will be updated to the correct state.

<figure><img src="../../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* API Test has entered the Up state when the URL is working properly

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* You can see details about API Test:

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
