# Access Management via Policy

IAM Policies are JSON documents that define permissions and rules for accessing resources. These policies are attached to IAM User Accounts, User Groups, and Service Accounts to control the actions they can perform on specific resources. IAM Policies adhere to the "allow" or "deny" principle, meaning they explicitly grant or deny access to resources and actions.

#### 1. Create a Policy (Policy) <a href="#customermanagedpolicy-1.taochinhsach-policy" id="customermanagedpolicy-1.taochinhsach-policy"></a>

**To create a Policy, follow these steps:**

1. Access the IAM Console: https://iam.console.vngcloud.vn/
2. Click on "Policy" in the left menu.
3. Click on "Create a policy.
4. Provide the policy name and optional description.
5. Click on "Next step" to continue configuring permissions.
6. By default, the interface will display the "Visual editor" tab. Use the Visual editor feature to continue the initialization process.
7. Select a specific Product in the GreenNode system that needs configuration.
8. Specify the allowed Actions on the resources of the product.
9. Select the resources for which the actions apply (All resources / Specific resource).
10. Provide optional conditions when applying.
11. To add a new set of Actions to apply to a new set of Resources within the same Policy, click on "Add Rule" as shown below, and continue to follow the instructions from step 6 → 9.
12. Review the settings and click on "Create policy."

{% hint style="info" %}
**Note**

For Policies to function properly, you need to assign them to a specific object (IAM user account, Service account, Group), refer to the instructions below for Policy usage management.
{% endhint %}

#### 2. Create and Edit Policy với JSON <a href="#customermanagedpolicy-2.taovachinhsuapolicyvoijson" id="customermanagedpolicy-2.taovachinhsuapolicyvoijson"></a>

**In addition to creating and editing Policies with the Visual editor, you can also use the "JSON" tab to create/edit Policies.**&#x20;

Use the instructions below for more details:&#x20;

Here is the corresponding sample JSON when selecting:&#x20;

* Product: vMonitor Effect: Allow Permission&#x20;
* Action: All vMonitor actions&#x20;
* Resource: All resources&#x20;
* Request conditions: Not installed

Example JSON Expand source

JSON Attribute Explanation&#x20;

* Statement: Policy&#x20;
* Each object in the Statement corresponds to a Rule, including:\

  * Effect: Allow / Deny Permission&#x20;
  * Action: List of Actions allowed / denied on the Resource&#x20;
  * Resource: List of Resources that will apply the above&#x20;
  * Actions Conditon: Request conditions

Relationship between Visual editor and JSON&#x20;

* Visual editor and JSON are 2 Policy editors, provided by IAM GreenNode Services.&#x20;
* Once you Create/Edit a policy from Visual editor/JSON, the data will be automatically updated between the 2 tabs.&#x20;
* To shorten the process of creating/editing a Policy, you can use the Visual editor/JSON feature back and forth&#x20;
* Note that all actions/edits from the 2 tabs are synchronized with the remaining tab.

{% hint style="info" %}
**Note**

To avoid accidentally deleting a Policy that is being used by IAM objects, we recommend that you unattach the Policy from the IAM objects instead of deleting it directly. Once a Policy is deleted, it cannot be restored.
{% endhint %}
