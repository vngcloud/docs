# Listener Policies

In HTTP/HTTPS listeners, policies are crucial components that help you control and route traffic to backend servers. A policy is a set of rules consisting of two main parts:

* **Condition:** A condition checks incoming requests.
* **Action:** When a request matches the condition, the corresponding action is applied to route the request.

#### How Policies Work

1. **Request Evaluation:** When a request reaches the listener, the system checks policies sequentially to determine which rule applies.
2. **Condition Matching:** If a request matches a condition (e.g., by checking the host or path of the request), the action associated with that condition is triggered.

Overall, policies determine how the Load Balancer, specifically the listener, will handle the request. This includes routing to backend servers, performing redirects, and other actions.

#### 1. Adding a Policy

To add a policy to a listener:

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer you want to configure.
3. **Go to the Listener Tab:** In the Load Balancer details page, select the "Listener" tab.
4. **Choose the Listener:** Click on the listener where you want to add the policy.
5. **Navigate to Policy Information:** In the listener details on the left, scroll down to the "Policy Information" section.
6. **Click "Add Policy":** A pop-up window will appear, allowing you to configure the policy.
7. **Configure Policy Details:**
   * **Policy Name:** Enter a descriptive name for the policy.
   * **IF Condition:**
     * **Check Request Based on HOST/PATH:** Choose whether to check the host or path of the incoming request.
     * **Matching Method:** Select "CONTAINS" (if the value is present) or "EQUAL" (if the value matches exactly).
     * **Enter HOST/PATH Value:** Enter the host or path value you want to check.
   * **THEN Action:** When the condition is met, choose an action:
     * **Forward to Pool:** Select a pool from the list of pools associated with the Load Balancer to direct the request to.
     * **Redirect to URL:** Enter the URL you want to redirect the request to.
8. **Click "Add" to finalize:** Click the "Add" button to complete the process.

#### 2. Updating a Policy

To update the conditions and actions of a policy, follow the same steps as adding a new policy, but click the "Edit" icon next to the policy you want to change.

#### 3. Ordering Policies

The order of policies within a listener is important because it directly affects how rules and behaviors are applied to traffic. Policies are applied sequentially from top to bottom within a listener. This means that the policy at the top has higher priority than the policy below it. Ordering allows you to prioritize the application of more important rules.

To reorder policies:

1. Follow steps 1-5 from the "Adding a Policy" section to access the "Policy Information" section of your chosen listener.
2. Click the "Reorder" button next to the "Add Policy" button.
3. Drag and drop the policies to arrange them in your desired order of priority.
4. Click "Save" to finalize the new policy order.
