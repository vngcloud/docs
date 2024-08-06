# Working with vStorage-Log

To be able to view the vStorage Project log, you access vMonitor, then go to **Infrastructure list/vStorage Log** , where the vMonitor system has automatically synchronized all vStorage Projects in 2 Regions: HCM and Hanoi. On this screen, for each vStorage Project you will see basic information columns such as:

* **vStorage project** : name of vStorage Project
* **vStorage region** : region of vStorage Project
* **Log Project** : the project log will contain vStorage Project logs when you enable "Detailed Monitoring"
* **Log Project Usage** : information about the usage level of the Log Project that has been attached to this vStorage Project
* **Monitoring Status** : monitoring status of vStorage Project, if "Detailed Monitoring" has not been enabled then the status will be INACTIVE, if enabled then the status is ACTIVE and you can go to the attached Project Log to view vStorage Logs
* **Detailed Monitoring** : toggle vStorage Project Logs monitoring on and off.

To be able to view vStorage Project Logs, you need to click **enable** in the **Detailed Monitoring** column , the system will display a Popup and you need **to select Log Project** to contain the logs of this vStorage Project, then click " **enable** ". If you don't have any Log Project yet, you can click "Create a log project" in the popup or go through the Quota & Usage tab to create a Log Project first.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FGgItm1mi0sIAYpOqkgvc%252Fimage.png%3Falt%3Dmedia%26token%3D7cea2f5c-efbf-4a10-b3ff-409ffc855cbb&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=77de0533&#x26;sv=1" alt=""><figcaption></figcaption></figure>

After enabling, you will see the status of this vStorage Project change to **ACTIVE** , and you can access the Log Project you just selected to view the logs.

If you need to change the Log Project containing Logs, you can select the 3-dot button and select " **Edit Log Project** " to change.

If you no longer need to view vStorage Project logs, you can **disable the Detailed Monitoring** column .

***

### **Some notes:** <a href="#mot-so-chu-y" id="mot-so-chu-y"></a>

* After vStorage Project is created from vStorage Portal, it will take about minutes (maximum 10 minutes) to synchronize to vMonitor.
