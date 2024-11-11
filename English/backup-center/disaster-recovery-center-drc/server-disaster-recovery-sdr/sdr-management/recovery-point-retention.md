# Recovery Point Retention

During the process of using Disaster Recovery (DR) service, managing Recovery Points is an important factor to ensure effective data recovery while optimizing storage costs. VNG Cloud Disaster Recovery Center (DRC) provides flexible options for you to manage Retention Recovery Points, helping you balance your data protection needs and budget.

Below is a detailed description of DRC's Retention Recovery Point policies, to help you better understand how they work and how to choose the right one for your needs.

**DRC Retention Recovery Point Description**

DRC applies the following Retention Recovery Point policy: Daily, Weekly, retention time and total limit on the number of Points allowed to be stored.

## Daily <a href="#daily" id="daily"></a>

* **Execution time:** 00:00 every day (guaranteed to run after the job to create point)
* **Storage rules:**
  * When a new \[n]th Point Daily is created, all recovery points & snapshots corresponding to \[n]th day and \[n-1]th day will be retained.
  * From day \[n-2], only keep points & snapshots marked "contain Daily" (usually the point at 0:00m of that day).
* **For example:** At 0:00 on Tuesday:
  * All points from day 2 will be retained.
  * From the 1st day onwards, points and snapshots will be deleted, only the point marked "contain Daily" (the point at 0:00m on the 1st day) will be kept.

## Weekly <a href="#weekly" id="weekly"></a>

* **Implementation time:** 00:00 every Sunday.
* **Storage rules:**
  * When the \[n]th Weekly Point is created, the Daily points of the \[n - 2]th week will be deleted, only the \[n - 2]th Weekly point will be kept.

**For example:**

* When you create the 3rd Weekly point, the Daily points of the 1st week will be deleted, only the point marked as "Weekly" will be kept.

### Total storage time <a href="#tong-thoi-gian-luu-tru" id="tong-thoi-gian-luu-tru"></a>

* **Storage rules:**
  * Recovery points are stored at DRC for a maximum of 30 days.
  * Points with storage time exceeding 30 days will be automatically deleted by the system.

## Total Point <a href="#total-point" id="total-point"></a>

* **Storage rules:**
  * The system only allows to save a maximum of 63 points.
  * When the 64th point is created, the oldest point (farthest back in time) will be deleted.

**Summary:**

* **Daily:** Keep all points from the previous day and "contain Daily" points from previous days.
* **Weekly:** Keep "Weekly" points and delete "Daily" points of weeks older than 2 weeks.
* **Total Point:** Limit the maximum number of points to 63, delete the oldest point when the limit is exceeded.

**Note:**

* These storage rules help optimize storage space usage while ensuring data resiliency over different time periods.
* You can adjust parameters (like **Interval Time** ) to suit your needs and storage policies.
