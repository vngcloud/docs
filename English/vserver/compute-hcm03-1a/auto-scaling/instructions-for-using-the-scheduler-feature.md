# Instructions for using the scheduler feature

Scheduler is a feature that helps you create a schedule to run an auto-scaling group automatically at the desired time. Scheduler helps you save workload for repetitive tasks at the same time. For example, at the peak time of 8am-10am every day you need many instances to serve, you can use the scheduler to increase the number of VMs at 8am and use the scheduler to reduce the number of VMs after 10am per day.

To create a scheduler, step 1 at the Auto-scaling group management interface, select a group you want to use the scheduler for.

You will see the details of the group below, select scheduler

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802628/image2019-5-24_0-2-19.png?version=1&#x26;modificationDate=1685070427000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Select create scheduler and enter the required information

* **Name:** Can enter characters (a-z, A-Z, 0-9, '\_'), and must start with letter
* **Group:** the system automatically selects the Group you are viewing
* **Desire capacity**: Enter the number of instances you want, the scaling group will scale the number of instances accordingly
* **Min capcity:** Minimum number of instances
* **Max capcity:** The maximum number of instances.
* **Scheduler:** How (how often) the scheduler will run, including the following options
  * **One**: Scheduler runs only once
  * **Cron:** You can define how often the scheduler repeats according to the Cron job structure. See more here [http://www.cronmaker.com/](http://www.cronmaker.com/)
  * E**veryday:** Repeat every day. For example setting below, scheduler will repeat at 10:07 every day

\
Everyweek: Repeat every week. For example below, the scheduler will repeat at 20:15 every Monday

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802628/image2019-5-24_0-2-34.png?version=1&#x26;modificationDate=1685070427000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
Everymonth: Repeat every month. For example below, the scheduler will repeat at 15:10 on the 2nd day of each month (2/1, 2/2, 2/3 etc...)

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802628/image2019-5-24_0-2-48.png?version=1&#x26;modificationDate=1685070427000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
\- Run start: The date the scheduler starts running

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802628/image2019-5-24_0-3-0.png?version=1&#x26;modificationDate=1685070457000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\- Run end: After the end-time, the scheduler will finish the iteration

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802628/image2019-5-24_0-3-13.png?version=1&#x26;modificationDate=1685070457000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

After the setup is complete, select create to create the scheduler. Successfully created, you will see the Scheduler listed as shown below:

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802628/image2019-5-24_0-3-34.png?version=1&#x26;modificationDate=1685070457000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

<br>
