# Instructions for creating a Scaling group

### **You need to complete the following steps to be able to create a Scaling group:** <a href="#instructionsforcreatingascalinggroup-youneedtocompletethefollowingstepstobeabletocreateascalinggroup" id="instructionsforcreatingascalinggroup-youneedtocompletethefollowingstepstobeabletocreateascalinggroup"></a>

**Step 1:**  At the Scaling Group Management interface, select group configure

In the scaling group configuration, enter the necessary information

* Group name (Required): Set a name to help you remember and manage when there are many groups. The group name allows to put characters (a-z, A-Z, 0-9, '\_'), starting with letters and limited to 6-20 characters
* Profile (Required): Each scaling group is required to be associated with 1 profile. Click drop down list to see the list of created profiles and select the desired profile. If there is no option, you need to return to the profile management interface and create a profile first.
* Desire Capacity: Enter the number of instances you want, the scaling group will scale the number of instances up accordingly. Desire number cannot be less than Min Capacity or greater than Max.
* Min capcity: The minimum number of instances you want this group to have
* Max capcity: The maximum number of instances. When using the receiver to scale automatically, the Min / Max index will ensure that the instance does not go out of the number you want.
* Timeout: The unit is seconds (s), if the group creation time exceeds the Timeout, this group will be faulty, normally you do not need to adjust this parameter.\
  If you already have a pre-made policy and want to attach it, you can click Advance and select it in the policy list. You can skip this section and add it later.\
  _**Note:** if you have created a policy but do not see it in the Policy list, you can review and change the selection of the Type policy section. The policy list displays only those policies that match the selected policy type_

**Step 2:** Click next to go to the Summary interface, here please check the information you have entered again. Note that you cannot change the profile & group name after creating the group successfully

**Step 3:** Select configure group to create, after successful creation, you will see the group appear in the Auto-scaling group management interface with Status as CREATING. After a while, you will see the group with Status as ACTIVE (press Refresh in Action or F5)

**Step 4:** If you want to see the detailed information of the Group, click on the tickbox right at the Scaling Group Management screen to see it

\
