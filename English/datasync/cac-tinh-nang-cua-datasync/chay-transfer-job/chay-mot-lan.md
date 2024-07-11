# Run one time

In the DataSync system, the one-time scheduled transfer job operates in the following way:&#x20;

**Step 1: Determine and configure when to run Transfer Job:**&#x20;

* You need to specify the specific time you want the transfer job to start running.&#x20;
* This time can be configured as a specific date and time provided it is greater than the current datetime.&#x20;

**Step 2: Run Transfer Job:**&#x20;

* At the specified time, the DataSync system will automatically activate the transfer job and begin the process of transferring data from source to destination according to configured parameters.

**For example**&#x20;

Suppose you want to transfer data from a bucket on cloud provider A to a container on vstorage at 3:00 a.m. on May 20, 2024. The process will be as follows:

1. Determine time: 3:00 AM, May 20, 2024.&#x20;
2. Job configuration:&#x20;

*   Choose when to run the job:&#x20;

    * Select the Run once option&#x20;
    * Select date May 20, 2024, enter time 03:00.&#x20;

    The system will automatically start the job at 3:00 AM, May 20, 2024.

{% hint style="info" %}
**Note:**

* If you change the run date and time parameters of a transfer job in the DataSync system, the system will run the job at the new time you specified. Specifically if you change the date and time to:
  * Future Time: If the new time is in the future, the job will be run at that exact time without any further action on your part.&#x20;
  * Past Time: If you change the job run time to a past time, the system may not automatically run the job. In this case, you need to reset the time to a reasonable time or trigger the job manually.
{% endhint %}
