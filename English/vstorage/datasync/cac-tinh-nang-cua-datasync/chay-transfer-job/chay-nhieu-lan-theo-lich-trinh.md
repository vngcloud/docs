# Run schedule

In the DataSync system, the mechanism to run periodic schedules for transfer jobs on a daily, weekly, or monthly basis helps to automate and ensure that data transfer tasks are performed regularly on a certain cycle. Here is how these periodic scheduling modes work:

**Step 1: Determine and configure when to run Transfer Job** :

* You need to specify the specific time at which you want the transfer job to start running. This time can be configured as a specific date and time with the condition that it is greater than the current **datetime** .

**Step 2: Run Transfer Job:**

* At the specified time, the DataSync system will automatically trigger the transfer job and start the process of transferring data from source to destination according to the configured parameters.

## Schedule a recurring run by Day <a href="#lap-lich-chay-dinh-ky-theo-ngay" id="lap-lich-chay-dinh-ky-theo-ngay"></a>

* The transfer job will run at a specific time every day.

**For example**

Suppose you want to set up a transfer job to transfer data from a bucket on cloud provider A to container B on vStorage on a daily basis starting from 01/05/2024 to 30/05/2024 at 03:00. The process would be as follows:

1. **Time** : 3:00 AM, from 01/05/2025 to 30/05/2024.
2. **Job configuration** :

* **Select when to run the job** :
  * **Select the Run Schedule** option
  * **Daily** Cycle
  * Select **Start date** as 01/05/2024, enter time 03:00.
  * Select **End Date** as 05/30/2024

1. Every day from 01/05/2024, at 03:00 the system will run your transfer job.

{% hint style="info" %}
**Attention:**

If you change the run cycle of a transfer job in the DataSync system, then:

* The next run time will not change when you perform an update.
* After this next run has been executed, the next run will be based on the new cycle you edited for your transfer job.

**For example:**

* Currently, you are setting up to run the transfer job with the following parameters:
  * Start date: 01/05/2024 , 03:00
  * End date: 30/05/2024
  * Period: Daily

\=> as of now before editing, the next transfer job run will be at **05/22/2024 03:00**

* Suppose you make this change on 21/05/2024 with the following parameters:
  * Start date: 01/05/2024 , 03:00
  * End date: 30/05/2024
  * Period: Weekly

\=> At this time, the next run time will still be **05/22/2024 03:00**

\=> After this run, the next run will be calculated according to the new cycle of **05/22/2024 03:00 + 7 days = 05/29/2024 03:00**
{% endhint %}

## **Schedule regular runs by week** <a href="#lap-lich-chay-dinh-ky-theo-tuan" id="lap-lich-chay-dinh-ky-theo-tuan"></a>

* Transfer job will run periodically every 7 days.

**For example**

Suppose you want to set up a transfer job to transfer data from a bucket on cloud provider A to container B on vStorage every 7 days starting from 01/05/2024 to 30/05/2024 at 03:00. The process would be as follows:

1. **Time** : 3:00 AM, from 01/05/2025 to 30/05/2024.
2. **Job configuration** :

* **Select when to run the job** :
  * **Select the Run Schedule** option
  * **Weekly** Cycle
  * Select **Start date** as 01/05/2024, enter time 03:00.
  * Select **End Date** as 05/30/2024

1. On 05/01/2024, 05/08/2024, 05/15/2024, 05/22/2024, 05/29/2024 at 03:00 the system will run your transfer job.

{% hint style="info" %}
**Attention:**

If you change the run cycle of a transfer job in the DataSync system, then:

* The next run time will not change when you perform an update.
* After this next run has been executed, the next run will be based on the new cycle you edited for your transfer job.

**For example:**

* Currently: you are setting up to run a transfer job with the following parameters:
  * Start date: 01/05/2024 , 03:00
  * End date: 30/05/2024
  * Period: Weekly

\=> as of now before editing, the next transfer job run will be at **05/22/2024 03:00**

* Suppose you make this change on 21/05/2024 with the following parameters:
  * Start date: 01/05/2024 , 03:00
  * End date: 30/05/2024
  * Period: Daily

\=> At this time, the next run time will still be **05/22/2024 03:00**

\=> After this run, the next run will be calculated according to the new cycle of **05/22/2024 03:00 + 1 day = 05/23/2024 03:00**
{% endhint %}

## **Schedule a monthly run** <a href="#lap-lich-chay-dinh-ky-theo-thang" id="lap-lich-chay-dinh-ky-theo-thang"></a>

* Transfer job will run periodically once a month.

**For example**

Suppose you want to set up a transfer job to transfer data from a bucket on cloud provider A to container B on vStorage every month starting from 01/01/2024 to 30/06/2024 at 03:00. The process will be as follows:

1. **Time** : 3:00 AM, from 01/01/2025 to 06/30/2024.
2. **Job configuration** :

* **Select when to run the job** :
  * **Select the Run Schedule** option
  * **Monthly** Cycle
  * Select **Start date** as 01/01/2024, enter time 03:00.
  * Select **End Date** as 06/30/2024

1. On 01/01/2024, 01/02/2024, 01/03/2024, 01/04/2024, 01/05/2024, 01/06/2024 at 03:00 the system will run your transfer job.

{% hint style="info" %}
**Attention:**

If you change the run cycle of a transfer job in the DataSync system, then:

* The next run time will not change when you perform an update.
* After this next run has been executed, the next run will be based on the new cycle you edited for your transfer job.

**For example:**

* Currently: you are setting up to run a transfer job with the following parameters:
  * Start date: 01/05/2024 , 03:00
  * End date: 30/06/2024
  * Period: Monthly

\=> as of now before editing, the next transfer job run will be at **06/01/2024 03:00**

* Suppose you make this change on 21/05/2024 with the following parameters:
  * Start date: 01/05/2024 , 03:00
  * End date: 30/06/2024
  * Period: Weekly

\=> At this time, the next run time will still be **06/01/2024 03:00**

\=> After this run, the next run will be calculated according to the new cycle of **06/01/2024 03:00 + 7 days = 06/08/2024 03:00**
{% endhint %}
