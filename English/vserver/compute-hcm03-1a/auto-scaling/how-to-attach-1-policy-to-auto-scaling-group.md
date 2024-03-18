# How to attach 1 policy to Auto-scaling group

There are two ways to attach a policy to the Auto-scaling group

### **Method 1: Attach a policy to the created group** <a href="#howtoattach1policytoauto-scalinggroup-method1-attachapolicytothecreatedgroup" id="howtoattach1policytoauto-scalinggroup-method1-attachapolicytothecreatedgroup"></a>

**Step 1:** At the Scaling Group Management interface -> Select the group you want to attach the Policy to, you will see the details of the group appear below

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802620/image2019-5-24_0-0-38.png?version=1&#x26;modificationDate=1685069941000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 2:** Select Policy -> You will see a list of mounted policies. Here you can attach (Assign) or remove (Detach) policy

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802620/image2019-5-24_0-0-51.png?version=1&#x26;modificationDate=1685069942000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 3:** Select Assign Policy -> Select the type of policy and Policy you want to attach

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802620/image2019-5-24_0-1-9.png?version=1&#x26;modificationDate=1685069942000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Note:** _If you have created a policy but do not see it in the Policy list, you can review and change the selection of the Type policy section. The policy list displays only those policies that match the selected policy type_

Once done, select Assign to finish. You will see the newly attached policy appear in the policy management interface

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802620/image2019-5-24_0-1-22.png?version=1&#x26;modificationDate=1685069942000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### **Method 2: If you already have POLICY before creating the group, you can attach the Policy right while creating an Auto-Scaling group as follows** <a href="#howtoattach1policytoauto-scalinggroup-method2-ifyoualreadyhavepolicybeforecreatingthegroup-youcanatt" id="howtoattach1policytoauto-scalinggroup-method2-ifyoualreadyhavepolicybeforecreatingthegroup-youcanatt"></a>

In the configure step when creating the scaling group, click Advance

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802620/image2019-5-24_0-1-34.png?version=1&#x26;modificationDate=1685069942000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Select Type policy -> select policy.

**Note:** if you have created a policy but do not see it in the Policy list, you can review and change the selection of the Type policy section. The policy list displays only those policies that match the selected policy type

Once done, click next and you will see that the newly created group will have the selected policy attached

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802620/image2019-5-24_0-1-47.png?version=1&#x26;modificationDate=1685069943000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
