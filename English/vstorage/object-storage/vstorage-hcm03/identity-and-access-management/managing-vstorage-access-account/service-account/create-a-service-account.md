# Create a Service Account

To create a Service Account, follow the steps below:

1. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/]\(https://iam.console.vngcloud.vn/\)) using your Root User Account.
2. Select the **Service Account** menu.
3. Choose **Create a Service Account**.
4. In the **Add information** menu, enter the **Name**. The Service Account name must be between 1 (minimum) and 50 (maximum) characters long, and it can only include uppercase and lowercase letters (a-z, A-Z), numbers (0-9), periods (.), underscores (\_), hyphens (-), and spaces ( ). The Service Account name should not contain sensitive information (e.g., IP addresses, login passwords). Additionally, the Service Account name must be unique within a VNG Cloud account until the Service Account is deleted. For example, the following Service Account name is valid: SA\_Client\_tool\_01.
5. In the **Trusted relationship menu**, enter the Account Root IS if you want to add linkage information between the Service Account and Root User Account.
6. Select **Next step**.
7. In the **Add permission** menu, you can:
   1. Choose one or more policies to associate with the Service Account. The vIAM system supports attaching multiple policies to one Service Account. If these policies contain independent permissions, they will complement each other (meaning the permission lists will be merged). Conversely, if these policies contain conflicting permissions, you will not be able to access the corresponding resources based on this permission list (meaning the permission lists will be merged, and conflicting permissions will override each other). For more details, please refer to [Attach Policies with Service Account](https://docs.vngcloud.vn/display/VSEN/Attach+Policies+with+Service+Account).
   2. If the policy list does not have the desired policy, you can proceed with the steps below, and we accept the creation of policies after creating the Service Account. However, you should link them as instructed in Linking Service Account to Corresponding Policy.
8. Choose **Copy** to copy the Secret key. You are required to collect this information to access vStorage using the Service Account.
9. Choose **Download** to download this secret key and store it on your local device.
10. Choose **Back to list** to return to the screen containing the list of Service Accounts.

After completing the above 10 steps, a Service Account has been created.

\
