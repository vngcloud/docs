# Supported Metrics List

## Linux/Windows metrics <a href="#danhsachmetricshotro-linux-windowsmetrics" id="danhsachmetricshotro-linux-windowsmetrics"></a>

vMonitor Platform's Metric Agent is built based on Telegraf software. By default, when installing Metric Agent, we will open plugin inputs such as:

* system. system
* disk. disk
* kernel
* net
* diskio
* meme
* processes. processes
* swap
* cpu

You can see detailed information about the Metrics and Units of the above plugins here [,](https://github.com/influxdata/telegraf/tree/master/plugins/inputs) and you can open additional plugin inputs to push more Metrics to vMonitor.

***

## Product metrics <a href="#danhsachmetricshotro-productmetrics" id="danhsachmetricshotro-productmetrics"></a>

When Resources on VNG Cloud are created, by default there will be 2 types of monitors: Basic and Detail

<table data-header-hidden><thead><tr><th width="225"></th><th></th></tr></thead><tbody><tr><td><strong>Monitoring type</strong></td><td><strong>Describe</strong></td></tr><tr><td><p><strong>Basic monitoring</strong></p><p>(Default)</p></td><td><ul><li>In this mode, a number of default metrics will be pushed and stored on the vMonitor Platform system. For details, refer to the detailed parameter table below.</li><li>Data is available automatically at 1 minute intervals.</li></ul></td></tr><tr><td><p><strong>Detailed monitoring</strong></p><p>(Advanced)</p></td><td><ul><li>In this mode, all existing metrics on the Resource are pushed and stored on the vMonitor Platform system. For details, refer to the detailed parameter table below.</li><li>Data is available automatically at 1 minute intervals.</li></ul></td></tr></tbody></table>

To know what each type of monitoring can do, please refer to [the List of Supported Metrics](https://docs-vngcloud-vn.translate.goog/vng-cloud-document/v/vn/vmonitor/dashboards/metrics/danh-sach-metrics-ho-tro/danh-sach-metrics-cua-host) .
