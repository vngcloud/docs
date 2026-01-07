# Traffic Statistics & Analysis

## Traffic Statistics

The **Traffic Statistics** page provides a comprehensive overview of all HTTP and HTTPS traffic processed by the Web Application Firewall (WAF) within a selected time range.\
This section helps users monitor traffic volume, security events, error rates, and client behavior.

***

### Overview

Traffic Statistics enables you to:

* Monitor total and blocked requests
* Analyze 4xx and 5xx error rates
* Identify traffic sources and client characteristics
* Detect abnormal traffic patterns or potential attacks
* Evaluate the effectiveness of WAF protection rules

***

### Filters & Scope

#### Application Selector – **All Applications**

Allows you to filter traffic statistics by:

* A specific protected application, or
* **All Applications** to view aggregated traffic across all applications protected by the WAF

This is useful when managing multiple applications under a single WAF account.

#### Time Range Selector – **1 day**

Filters displayed data by time period, such as:

* 1 day
* 7 days
* 1 month

All metrics and charts are updated dynamically based on the selected time range.

***

### Traffic Analysis

#### Key Metrics

<table><thead><tr><th width="164.54296875">Metric</th><th>Description</th></tr></thead><tbody><tr><td><strong>Requests</strong></td><td>Total number of HTTP/HTTPS requests processed by the WAF</td></tr><tr><td><strong>Views</strong></td><td>Number of page views counted from valid requests</td></tr><tr><td><strong>Visitors</strong></td><td>Number of unique visitors, identified by cookies or IP addresses</td></tr><tr><td><strong>Unique IP</strong></td><td>Number of distinct client IP addresses</td></tr><tr><td><strong>Blocked</strong></td><td>Number of requests blocked by WAF rules</td></tr><tr><td><strong>IP Address</strong></td><td>Number of IP addresses that generated blocked requests</td></tr></tbody></table>

These metrics provide a high-level overview of traffic volume and security activity.

***

### Error & Block Statistics

#### 4xx Errors

Number of requests that resulted in client-side errors, such as **403 Forbidden** or **404 Not Found**.

#### Error Rate

Percentage of 4xx errors relative to the total number of requests.

#### 4xx Blocked

Requests actively blocked by the WAF that resulted in 4xx responses, typically **403 Forbidden**.

#### Blocked Rate

Percentage of total requests that were blocked by the WAF.

#### 5xx Errors

Number of server-side errors, including:

* 500 Internal Server Error
* 502 Bad Gateway
* 504 Gateway Timeout

#### 5xx Error Rate

Percentage of server-side errors relative to total requests.\
A high 5xx error rate usually indicates backend application or infrastructure issues rather than WAF-related blocking.

***

### Query Per Second (QPS)

Displays the number of requests processed per second.

**Use cases:**

* Detect sudden traffic spikes
* Identify potential DDoS or bot-generated traffic
* Monitor overall request load trends

***

### Request Status (Requests)

Shows the number of incoming requests over time.

**Useful for:**

* Detecting abnormal traffic surges
* Analyzing user access patterns
* Identifying automated or scripted behavior

***

### Blocking Status (Blocked)

Shows the number of requests blocked by the WAF over time.

**Useful for:**

* Detecting attack attempts
* Evaluating the effectiveness of security rules
* Identifying periods of high protection activity

***

### Geo Location

Displays the geographic origin of incoming requests, grouped by country or region.

**Benefits:**

* Analyze traffic distribution by location
* Detect suspicious traffic from unexpected regions
* Support geo-based security policies

***

### User Client – User Agent Statistics

Displays client information such as:

* Operating systems (Windows, Linux, macOS)
* Browsers (Chrome, Firefox, Safari)
* Tools or automated clients (curl, wget, custom bots)

This information helps distinguish between legitimate users and automated or potentially malicious traffic.

***

### Response Status

Breakdown of requests by HTTP response category:

* **2xx** – Successful responses
* **3xx** – Redirect responses
* **4xx** – Client-side errors
* **5xx** – Server-side errors

This view provides a quick summary of application health and request outcomes.

***

### Summary

The **Traffic Statistics** page serves as a central observability dashboard for WAF-protected applications.\
By analyzing traffic volume, errors, blocked requests, and client behavior, users can:

* Monitor application health
* Detect and respond to attacks early
* Optimize WAF rule configurations
* Improve overall security visibility
