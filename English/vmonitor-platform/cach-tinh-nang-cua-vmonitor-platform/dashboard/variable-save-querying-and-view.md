# Variable, Save Querying and View

### Variable

**Variable** allows you to dynamically display tracking information on a dashboard. With a single dashboard, you can select a value for the variable to view information on various objects.

To create a variable in a dashboard, follow the instructions below:

1. Access the Dashboard where you want to create a Variable, and select **Create a variable**
2. Select **Add a variable**

<figure><img src="../../../.gitbook/assets/image (81) (1).png" alt=""><figcaption></figcaption></figure>

3\. Select/enter the following information:

* **Dimension Key**: choose a dimension key that will provide a list of values for your variable, for example, hostname.
* **Name**: name the variable, the system will automatically generate a suitable name based on the selected dimension key
* **Filter**: you can filter the values of this variable with other dimension keys or variables
* **Default value**: default value for the variable
* **Values**: list of values for the variable, taken from the selected dimension key.

<figure><img src="../../../.gitbook/assets/image (82) (1).png" alt=""><figcaption></figcaption></figure>

Suppose here we choose the dimension key as **hostname.** You will see the values of the variable will be a list of all hosts in the system. Here you can select **Dynamic by time range** for the system to automatically include all hostnames based on the selected time range, or you can choose specific hostnames from the displayed list. For optimal performance, we recommend using **Dynamic by time range.**

<figure><img src="../../../.gitbook/assets/image (83) (1).png" alt=""><figcaption></figcaption></figure>

4\. To apply this variable to widgets, you can manually add/edit the widget and include it in the filter section, or use the auto-add feature here. When you click +, the system will automatically add this variable to all widgets in the dashboard. Similarly, clicking - will automatically remove it.

<figure><img src="../../../.gitbook/assets/image (84) (1).png" alt=""><figcaption></figcaption></figure>

5\. Select "**Save**" to create a variable

<figure><img src="../../../.gitbook/assets/image (85) (1).png" alt=""><figcaption></figcaption></figure>

You will notice that using the auto-add feature ( + ), the widgets on the dashboard will automatically add $hostname to the filter. However, when using this feature, you should also review the list of selected dimensions to ensure they are appropriate and make adjustments accordingly.

<figure><img src="../../../.gitbook/assets/image (86) (1).png" alt=""><figcaption></figcaption></figure>

If you do not use the auto-add feature, you can manually add to the filter as usual, and the system will display the variable as a dimension key.

<figure><img src="../../../.gitbook/assets/image (87) (1).png" alt=""><figcaption></figcaption></figure>

When the variable is successfully created, you will see it displayed on the dashboard and can select a value to display the dashboard according to the selected value.

<figure><img src="../../../.gitbook/assets/image (88) (1).png" alt=""><figcaption></figcaption></figure>

From here, you can choose different hosts to monitor parameters very flexibly without needing to create or view multiple dashboards.

***

### View

**View** allows you to create perspectives for the dashboard, saving variable values for later use.

To create a **View** for a dashboard, follow the instructions below:

1. After you have a variable and want to save its value for convenient access later, use the **View** feature and click "**Save view**" to save it.

<figure><img src="../../../.gitbook/assets/image (89) (1).png" alt=""><figcaption></figcaption></figure>

2\. Name the view, and when you select this view, the system will automatically populate the list of variables below.

<figure><img src="../../../.gitbook/assets/image (90) (1).png" alt=""><figcaption></figcaption></figure>

3\. After successfully creating views, you will see a list of views to choose from. Suppose there are two views: host-storagegw and host-nginx

<figure><img src="../../../.gitbook/assets/image (91) (1).png" alt=""><figcaption></figcaption></figure>

4\. When you select view: host-nginx, the system will automatically load a list and different values for the variable.

<figure><img src="../../../.gitbook/assets/image (92) (1).png" alt=""><figcaption></figcaption></figure>

5. To manage Views and Variables, you can click on the gear icon:

<figure><img src="../../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>

***

### Save query

vMonitor Platform provides you the ability to reuse a query that you have previously created through the Save query feature that we offer.

#### Save query

To save a query, follow the instructions below:

1. In the query command area, click the **Save** icon.

<figure><img src="../../../.gitbook/assets/image (140).png" alt=""><figcaption></figcaption></figure>

2. Enter the **Query name**.
3. Select **Save**

<figure><img src="../../../.gitbook/assets/image (141).png" alt="" width="342"><figcaption></figcaption></figure>

The query is now saved with the memorable name you entered.

### Reuse existing queries

After you have saved the query, you can reuse this query by:

1. In the query command area, select the dropdown icon <img src="../../../.gitbook/assets/image (142).png" alt="" data-size="original"> (this icon is located next to the Save query icon).

<figure><img src="../../../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>

2. At this point, the system displays a list of saved queries, allowing you to reuse them by selecting the desired query.

<figure><img src="../../../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>

3. You can edit this query and save it as a new independent query from the one you reused by selecting Save as new query.

<figure><img src="../../../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>

### Query management

You can view the saved queries or delete a query by selecting Manage saved queries and choosing the **Delete** icon.

<figure><img src="../../../.gitbook/assets/image (146).png" alt=""><figcaption></figcaption></figure>
