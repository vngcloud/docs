# Install and use the vMonitor Datasource plugin for Grafana

> This guide helps you install the vMonitor Datasource Plugin on a self-hosted Grafana server, add a data source connecting to vMonitor, then query metrics/logs, build dashboards, and set up alerting.

---

## Prerequisites

- Grafana server version **12.3.0** or later.
- `sudo` access on the Grafana host.
- A GreenNode IAM **Service Account** key pair (`Client ID` + `Client Secret`) with vMonitor read access (created in the first step below).

---

## Create a Service Account key pair

The plugin authenticates with vMonitor using a Service Account key pair, not a username/password.

**Step 1: Create the Service Account**

1. Open the GreenNode IAM console.
2. Go to **Service Accounts** → **Create service account**.
3. Name and create the Service Account.

**Step 2: Attach policies**

1. Attach the **vMonitorMetricReadOnlyAccess** policy to the Service Account (required to query metrics).
2. If you need to query logs, also attach **vMonitorLogReadOnlyAccess**.

**Step 3: Generate the key pair**

1. In the Service Account you just created, choose to generate a key pair.
2. Note the **Access Key ID** — this is your `Client ID`.
3. Note the **Secret Access Key** — this is your `Client Secret`.

{% hint style="warning" %}
The Secret Access Key is shown only **once**. If you lose it, you must create a new key pair.
{% endhint %}

---

## Install the plugin on the Grafana server

The plugin is an unsigned backend build, so Grafana must be allowed to load unsigned plugins.

**Step 1: Download the plugin**

1. Download the latest ZIP (v1.0.0) from the **[Releases](https://github.com/GreenNodeHub/vmonitor-grafana-plugin/releases)** page of the `GreenNodeHub/vmonitor-grafana-plugin` repo.

**Step 2: Unpack**

1. Create the plugin directory if it does not exist (default `/var/lib/grafana/plugins`).
2. Unzip the archive into a subdirectory named `greennode-vmonitor-datasource`.

{% hint style="info" %}
Find your plugins path by checking the `plugins` key under `[paths]` in `/etc/grafana/grafana.ini`. When upgrading, remove the old plugin directory before unpacking the new build.
{% endhint %}

**Step 3: Set ownership**

1. Grafana runs as the `grafana` user. Grant ownership of the entire plugins directory:

```bash
sudo chown -R grafana:grafana /var/lib/grafana/plugins
```

**Step 4: Allow the unsigned plugin**

1. Open `/etc/grafana/grafana.ini`.
2. Add the plugin ID to the `[plugins]` section:

```ini
[plugins]
allow_loading_unsigned_plugins = greennode-vmonitor-datasource
```

The plugin ID is in `plugin.json` inside the plugin directory. Multiple unsigned plugins are comma-separated.

**Step 5: Restart and verify**

1. Restart the Grafana server.
2. Check the logs: success shows a "Plugin registered" message. Two warnings about the unsigned plugin are expected.
3. Go to **Administration → Plugins and data → Plugins**; the **GreenNode vMonitor** plugin appears in the list.

{% hint style="warning" %}
Restarting Grafana interrupts the current session. Perform this outside peak hours if needed.
{% endhint %}

---

## Add the data source and import dashboards

**Step 1: Add the data source**

1. Go to **Administration → Plugins and data → Plugins**.
2. Search for "GreenNode vMonitor" and add a new data source.

**Step 2: Fill in the fields**

| Field | Required | Description |
|---|---|---|
| API URL | No | vMonitor API base URL; leave blank for the default |
| Client ID | Yes | Access Key ID of the Service Account key |
| Client Secret | Yes | Secret Access Key; stored encrypted, read only by the backend |
| Token URL | No | IAM token-exchange endpoint; leave blank for the default |

**Step 3: Save and test**

1. Click **Save & test**.
2. The backend exchanges the key pair for a **Bearer token**, which is cached until expiry.

{% hint style="info" %}
The Client Secret never reaches the browser; only the backend holds it and uses it to exchange tokens.
{% endhint %}

**Step 4: Import dashboards**

1. Go to **Connections → Data sources** and open the data source you just created.
2. Switch to the **Dashboards** tab and import each desired dashboard.

---

## Query metrics

**Step 1: Select the mode**

1. Select the GreenNode vMonitor data source.
2. Select **Metric** mode.

**Step 2: Configure the query**

| Field | Description |
|---|---|
| Metric | The metric name, e.g. `net.if.in.bytes_sec` |
| Statistic | Aggregation function: `avg`, `min`, `max`, `sum`, `count`, `rate_1s`, `rate_1m`, `rate_5m` |
| Filter by | Dimension filters combined with AND |
| Group by | Split into separate series by dimension value |
| Alias | Display name template using `{{dimension}}` syntax |

**Step 3: Add functions (if needed)**

Click **Add Function** to add:

| Function | Description | Limitation |
|---|---|---|
| Rollup | Aggregate over a fixed time window (avg/min/max/sum/count) | Not for `rate_*` |
| Rate | Convert a cumulative counter to a rate (per_second/per_minute/per_hour) | Not for `rate_*` |
| Timeshift | Overlay the same metric from an earlier period | Not for `rate_*` |
| Rank | Keep top N (topk) or bottom N (bottomk) series at each point | Excluded series have gaps |
| Reduce | Collapse a series to a single value (last/avg/min/max/sum) for Stat/Top List panels | — |

{% hint style="info" %}
The `rate_1s`, `rate_1m`, `rate_5m` statistics do not support the Rollup, Rate, or Timeshift functions. In an alert rule that uses Rank, add **Resample** before **Reduce** to handle gaps.
{% endhint %}

**Step 4: Examples**

- **Top 5 vServers by CPU:** Metric `cpu.usage_user`, statistic `avg`, filter `product = vserver`, group by `resource_id`, Rank topk 5, alias `{{resource_id}}`.
- **Network throughput vs. last week:** Query A with the metric and `avg` statistic; Query B with the same metric plus Timeshift 1 week.

---

## Query logs

**Step 1: Select the Log project**

1. Select the data source and switch to **Logs** mode.
2. Choose a **Log project** (only ACTIVE projects are listed).

**Step 2: Choose the output format**

| Format | Used for | Display |
|---|---|---|
| logs | Explore, Logs panel | Log lines with a count histogram, each line expandable |
| table | Table panel | One row per entry, one column per field |
| timeseries | Graph panel, Alerting | Log count over time |

In Alert mode, the format is automatically set to `timeseries`.

**Step 3: Filter logs**

| Operator | Input | Meaning |
|---|---|---|
| is | 1 value | Exact match |
| is not | 1 value | Does not match |
| is one of | Multiple | Matches any |
| is not one of | Multiple | Matches none |
| is between | from, to | In range [from, to) |
| is not between | from, to | Outside range |
| exists | — | Field present |
| does not exist | — | Field absent |

Grafana variables are supported in filter values, e.g. `$selected_host`.

**Step 4: Group by (timeseries only)**

1. Select an aggregatable (keyword) field to split the log count into separate series.
2. Each unique combination of values becomes a series; maximum 20 values per field.

---

## Set up alerting and notifications

Alerting and notifications are handled by **Grafana**: you build a Grafana alert rule on vMonitor metric/log queries, then Grafana delivers alerts through its own notification policies and contact points (email, Slack, Webhook...). The plugin does not use vMonitor Alarm or Notification.

**Alert on metrics:** Build a metric query, then add **Reduce** + **Threshold** in the alert rule. If you use Rank, add **Resample** before **Reduce** to handle gaps.

**Alert on log count:** Use a log query with the `timeseries` format, add filters, then attach **Reduce** + **Threshold** to fire when the log count exceeds the threshold.

{% hint style="info" %}
During quiet periods, the log count reports `0` instead of missing data, so the rule can also fire when logs stop appearing.
{% endhint %}

**Log group by in alerts:** Each group value creates a separate Grafana alert instance. A group with no matching logs during evaluation does not produce an instance.

---

## Template variables

| Function | Returns |
|---|---|
| `metrics()` | All metric names |
| `dimensions(metricName)` | Dimension keys for a metric |
| `dimensionValues(metricName, key)` | Values for a dimension key |
| `infrastructure(product[, region])` | Resources for a product type |
| `regions(product)` | Available regions for region-aware products |

Products supported by `infrastructure()`: `host`, `vserver`, `vlb`, `vstorage`, `vstorage-bucket`, `vdb`, `vdb-kafka`, `vdb-cluster`, `vbackup`.

---

## Troubleshooting

| Symptom | Cause & fix |
|---|---|
| Plugin missing from the Plugins list | Unsigned build not allowed; check the unsigned-plugin step and inspect the logs for signature errors |
| Plugin directory skipped | Ownership issue; rerun `chown` from the ownership step |
| Plugin unavailable when querying | Backend binary failed to start; ensure `plugin.json` is directly in the plugin directory, not nested |
| Version error | Plugin requires Grafana **12.3.0+** |
| 401 Unauthorized on **Save & test** | Wrong Client ID or Client Secret |
| Connection refused on **Save & test** | Wrong API URL or network issue |
| Query returns no data | Check the time range, dimension filters, and IAM read permissions |
| Log project dropdown empty | IAM key lacks log read permission, or the project is not in ACTIVE billing status |

---

## Result

Once complete, you have a GreenNode vMonitor data source in Grafana that can query metrics and logs, use the bundled dashboards, and drive alerting from vMonitor data.

| I want to... | Go to |
|---|---|
| See vMonitor updates | [Announcements and Updates](../overview/product-updates-all/) |
| Learn about vMonitor Platform | [vMonitor Platform](README.md) |
