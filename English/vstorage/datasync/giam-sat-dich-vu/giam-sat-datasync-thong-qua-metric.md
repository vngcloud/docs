# Monitoring DataSync Through Metrics

#### **What is a metric?**

A metric (or indicator) is a data point obtained through measurement — by setting up measurements and tracking and evaluating some activity in a given context.

#### **Why are metrics useful?**

Metrics provide an overall picture of your system. You can use them to assess the health of your system at the current moment. For DataSync, metrics can help you tune storage scale and responsiveness, adjust to demand, and pinpoint the amount of resources you need to consume — helping you save money or improve performance.

#### **Monitoring DataSync through DataSync metrics on the vMonitor Platform**

Monitoring DataSync through metrics is easy with the vMonitor Platform. We push metric parameters from DataSync to the vMonitor Platform regularly, every 5 minutes. The vMonitor Platform is also a product in the GreenNode ecosystem. You can use it to configure monitoring features based on these parameters. To do so, you need to purchase the metric quota package of the vMonitor Platform service; for details, refer to [vMonitor Platform](https://docs.greennode.ai/vmonitor.md). Below is the list of DataSync metrics we provide for monitoring:

<table data-header-hidden><thead><tr><th width="55.828125"></th><th width="278.60546875"></th><th width="329.13671875"></th><th width="84.765625"></th></tr></thead><tbody><tr><td>No.</td><td>Metric</td><td>Description</td><td>Interval</td></tr><tr><td>1</td><td>datasync_bytes_transferred_total</td><td>Total bytes transferred.</td><td>1 phút</td></tr><tr><td>2</td><td>datasync_checked_files_total</td><td>Total files checked.</td><td>1 phút</td></tr><tr><td>3</td><td>datasync_dirs_deleted_total</td><td>Total directories deleted.</td><td>1 phút</td></tr><tr><td>4</td><td>datasync_errors_total</td><td>Total error files recorded.</td><td>1 phút</td></tr><tr><td>5</td><td>datasync_fatal_error</td><td>Total errors that occurred.</td><td>1 phút</td></tr><tr><td>6</td><td>datasync_files_deleted_total</td><td>Total files deleted.</td><td>1 phút</td></tr><tr><td>7</td><td>datasync_files_renamed_total</td><td>Total files renamed.</td><td>1 phút</td></tr><tr><td>8</td><td>datasync_files_transferred_total</td><td>Total files transferred.</td><td>1 phút</td></tr><tr><td>9</td><td>datasync_http_status_code</td><td>Number of statuses that occurred during the data transfer process.</td><td>1 phút</td></tr><tr><td>10</td><td>datasync_retry_error</td><td>Total files that failed during retry.</td><td>1 phút</td></tr><tr><td>11</td><td>datasync_speed</td><td>Average speed in bytes per second since the start of the data transfer process.</td><td>1 phút</td></tr></tbody></table>
