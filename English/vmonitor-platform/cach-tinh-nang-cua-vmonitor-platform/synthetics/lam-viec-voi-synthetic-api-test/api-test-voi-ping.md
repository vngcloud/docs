# API Test with Ping

The Ping tests API allows you to send ICMP packets to your server or devices, allowing you to monitor the availability of the server or devices and diagnose network problems.

**To perform API Test creation with Ping method, follow the instructions below:**

1. Log in to vMonitor Platform [here.](https://hcm-3.console.vngcloud.vn/vmonitor)
2. Select the Synthetic test folder **.**
3. Select **API test.**
4. Select **Create an API test.**
5. Enter information including:

* **Test Information: define basic information, select Ping method and specify hostname to test**
  * **Test name:** name of the API test
  * **Test type** : test protocol, you choose Ping
  * **Hostname:** select the server or device you need to check, can be domain name or IP address

<figure><img src="../../../../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* After filling in the Test Information, you can choose **Run Test or Test Again** if you have tested before to check, you can see returned information such as whether Ping was successful or not, packet loss rate or packet latency.

<figure><img src="../../../../.gitbook/assets/image (9) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Test Assertion**
  * Assertion defines what you expect about the API Test results. If the returned results meet what you define, API Test will show that the hostname you are testing is successful, and vice versa, API Test will show that the hostname you are testing is successful. test is failed. The system will automatically add the Assertion status code for you after you Run the test, you need to define at least one Assertion for the API test.

<figure><img src="../../../../.gitbook/assets/image (10) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Location**
  * Select the Location that will run Ping Tests to your hostname. Ping tests can be run from both Public Locations (managed by VNG Cloud) and Private Locations (installed and managed by customers) based on your needs for running tests from outside (internet) or inside the network. your. Public Locations managed by VNG Cloud currently has 2 locations: HCM and Hanoi.

<figure><img src="../../../../.gitbook/assets/image (11) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Alarm conditions:** Set up alarm conditions to define the cases where you want the test to fail and trigger the alarm.
  * **Interval** : how often API Test will test once, default will be 1p
  * **Time of failure** : how many consecutive failures will alert
  * **Locations with failure** : how many locations fail to warn
  * For example, when you select Time of failure: 1 and Locations with failure: 2, it will be understood as: you will be warned if the Test fails 1 time in a row from 2 out of 2 locations.
  * **Notifications** : you choose notification channels when switching to In-alarm, Up or Undertermine states, the system will notify according to this list.

<figure><img src="../../../../.gitbook/assets/image (12) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

6\. Then press the " **Create** " button to initialize the API test. After creating, you will see the API test is in Undertermine state, until the next inteval the Test API will be updated to the correct state.

<figure><img src="../../../../.gitbook/assets/image (13) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* API Test has entered the Up state when the hostname is working normally

<figure><img src="../../../../.gitbook/assets/image (14) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
