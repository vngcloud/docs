# Listener policy

You can add a policy for a listener by: Select **load balancer** → Select **listerner** → Select **Add policy**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802696/image2019-5-12_20-51-14.png?version=1&#x26;modificationDate=1685076054000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Add policy**&#x20;



<figure><img src="https://docs.vngcloud.vn/download/attachments/59802696/image2019-5-12_20-50-0.png?version=1&#x26;modificationDate=1685076054000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Policy name:** Set a reminder name to help you manage the policy. Policy name needs at least 6 characters, A-Z, 0-9

**Condition:** One condition includes

* **Mệnh đề if** : Host or Path
* **Rule:**&#x20;
  * Contains contains condition that is satisfied
  * Match: exact condition
* **Điều kiện**: Input the condition you want to check.

**Action**: When the above condition is met, the action you set will be performed. Action includes:

* **Forward to pool:** When the condition is met, the connection will be pushed to the pool in the list you selected
* **Redirect to:** Enter the URL you want to redirect the connection to until the condition is met
