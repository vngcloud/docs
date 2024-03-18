# Instructions for creating policy

At the Policy management interface, select create Policy

![](https://docs.vngcloud.vn/download/attachments/59802601/image2019-5-23\_23-58-51.png?version=1\&modificationDate=1685005676000\&api=v2)

\


**Step 1:** At Policy configuration, enter the necessary information

![](https://docs.vngcloud.vn/download/attachments/59802601/image2019-5-23\_23-59-5.png?version=1\&modificationDate=1685005706000\&api=v2)

\


* Policy name: allows to set characters (a-z, A-Z, 0-9, '\_'), starting with letters and limited to 6-20 characters
* Policy description: Enter a policy description, this description depends on your policy management needs, does not affect how the policy works.
* Policy type: There are 2 types of policy:

Load balancer policy: This policy helps you define load balancer values and automatically add created instances to the respective pool.

![](https://docs.vngcloud.vn/download/attachments/59802601/image2020-6-30\_10-0-17.png?version=1\&modificationDate=1685005736000\&api=v2)

You will need to select which Network Load Balancer policy belongs to, then the system will automatically list all Load Balancers belonging to that Network and all Pool IDs of the selected Load Balancer.\
Policy scaling: Set the properties of the scale instance action. Currently the scaling type only supports the Change\_In\_Capacity form (changing the number of instances) with 2 Event types:\
CLUSTER\_SCALE\_IN: Reduce the number of Instances in the Group\
CLUSTER\_SCALE\_OUT: Increase the number of Instances in the Group

* **Number:** Number of instances scaled each time
* **Cooldown:** The unit is seconds (S), this is the interval between each scale.

After the setup is done, press NEXT to continue

**Step 2:** Summary. Check the policy information. Note that Policy configurations cannot be edited later.

Click configure policy to create a policy

![](https://docs.vngcloud.vn/download/attachments/59802601/image2019-5-23\_23-59-55.png?version=1\&modificationDate=1685005783000\&api=v2)

After successful creation, you will see the newly created policy appear in the management interface
