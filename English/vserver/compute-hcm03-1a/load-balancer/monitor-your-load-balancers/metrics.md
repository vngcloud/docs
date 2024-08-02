# Metrics

Currently, vMonitor Platform allows you to view metrics for all vLB instances using the default dashboard (a pre-built dashboard with a limited set of metrics) and a 1-day retention period, completely free of charge. To create dashboards with an unlimited number of metrics, view metrics with longer retention periods, and set up alarms to alert you when metrics like connections, 5xx responses, 4xx responses, etc., reach critical levels, you need to enable detailed monitoring. This requires you to subscribe to a quota package with vMonitor Platform. You can find more information at: Quota & Usage: Purchase Metric Package.

After enabling detailed monitoring, you can clone the default dashboard and add other widgets as needed, or create new dashboards altogether. Refer to Creating Dashboards and New Widgets for instructions.

At this point, you can select vLB metrics using the format: `vlb.<metric_name>`. For example: `vlb.listener.bin`, `vlb.listener.bout`, `vlb.listener.hrsp_5xx`, and so on.

vLB metrics support the following dimensions, allowing you to filter metrics for each vLB instance by ID, name, layer, listener, pool, etc.:

* `loadbalancer_id`: ID of the vLB instance.
* `loadbalancer_name`: Name of the vLB instance.
* `layer`: 4 or 7, corresponding to Network Load Balancer or Application Load Balancer.
* `role`: Standalone (if your vLB is from the older generation), Master/Backup (if your vLB is from the new generation).
* `zone`: Zone of the resource, such as HCM-03.
* `listener_id`: ID of the Listener.
* `listener_name`: Name of the Listener.
* `pool_id`: ID of the pool.
* `pool_name`: Name of the pool.
* `member_id`: ID of the member.

You can also create alarms using these metrics. See Setting Up Alerts for Metrics.

#### Related Topics

* Quota & Usage: Purchase Metric Package
* Creating Dashboards and New Widgets
* Setting Up Alerts for Metrics

