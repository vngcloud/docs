# Create an IAM User Account

To create an IAM User Account for accessing vStorage resources, please follow the detailed guide below. Refer to the provided steps to create an IAM User Account:

1\. Log in to [https://iam.console.vngcloud.vn/](https://iam.console.vngcloud.vn/]\(https://iam.console.vngcloud.vn/\)) using your Root User Account.\
2\. Select **User Account** from the menu.\
3\. Choose **Create a User Account.**\
4\. In the **Account username** section, enter the **Account username**. IAM User Account names must be between 5 (minimum) and 50 (maximum) characters, and can only include uppercase and lowercase letters (a-z, A-Z), numbers (0-9), dots (.), underscores (\_), and hyphens (-). IAM User Account names should not contain sensitive information (e.g., IP addresses, login passwords), and each IAM User Account name must be unique within a VNG Cloud account until the IAM User Account is deleted. Example valid IAM User Account name: IAM\_Business\_Dept\_01.\
5\. Select **Add a username.**\
6\. In the **Account password** section, you can:

* Enter a **password** of your choice. Passwords must be between 8 (minimum) and 50 (maximum) characters and include at least 1 uppercase letter (A-Z), 1 lowercase letter (a-z), 1 number (0-9), and 1 special character (!@#$%,...).
* Choose **Auto-generate** if you want the system to create a password for you.

7\. Select **Copy** to copy the password. You must collect this information to access vStorage using the IAM User Account.\
8\. Choose **Create User Account.**

After completing the above 8 steps, an IAM User Account has been created. However, the newly created IAM User Account doesn't have policies yet, so all access attempts will be denied. Therefore, you need to proceed to create policies as instructed in the [Create Policies for IAM User Account](https://docs.vngcloud.vn/display/VSEN/Create+Policies+for+IAM+User+Account) guide.
