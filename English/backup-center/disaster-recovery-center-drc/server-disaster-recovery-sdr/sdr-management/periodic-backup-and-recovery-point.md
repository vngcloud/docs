# Periodic Backup and Recovery Point

After you click **"Start Replication"** and the initial replication (Full Replication) is complete, the system will automatically perform scheduled periodic replication.

By default, **every 15 minutes** , the system creates a new **Recovery Point** , recording the state of the primary server's data at that time. This ensures that your data is constantly protected and you can restore to the closest possible point in time in the event of a failure.

However, to save storage costs, not all Recovery Points are retained. Only Recovery Points that match **the Interval Time** (the time between two recovery points) that you set in the **Start Replication** step are retained. Other Recovery Points will be deleted after a new Recovery Point is created.

**Specific examples:**

Let's say you have set Interval Time to 4 hours. This means the system will only retain Recovery Points created at: 0:00, 4:00, 8:00, 12:00, 16:00 and 20:00 every day.

* If a Recovery Point is created at 3:45, it will be deleted when the next Recovery Point is created at 4:00.
* If a Recovery Point is created at 4:00, it will be retained because it coincides with the Interval Time.
* Recovery Points created at 0:15, 0:30, 0:45,... will also be deleted similarly.

**In short:**

* Periodic replication occurs every 15 minutes, creating new Recovery Points.
* Only Recovery Points that match the Interval Time are kept.
* Other Recovery Points will be deleted to save storage costs.

**Benefit:**

* Ensure data is always up to date and protected.
* Save storage costs by keeping only the Recovery Points needed.
* Allows you to restore data to a specific point in time before a crash occurred.
