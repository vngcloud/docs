# HTTP Flood Protection

### Overview

The **Rate Limiting** module protects applications from excessive or abusive traffic by controlling how many requests a client can send within a defined time window.

This module is a critical defense mechanism against:

* HTTP Flood attacks
* Brute-force attempts
* Automated scanning
* Abnormal or sudden traffic spikes

The **Rate Limiting** page provides visibility into clients that exceed configured thresholds and shows the actions taken by the WAF.

***

### Rate Limiting Page Overview

This page lists all IP addresses that have triggered rate-limit rules on any protected application.

For each entry, users can view:

* Source IP address and geolocation
* Target application
* Triggered rule details (request count and time window)
* Block duration applied
* Total number of blocked requests
* Start time of the rate-limit event
* Current block state (Blocked / Unblocked)

This overview enables operators to quickly identify abusive clients and evaluate the effectiveness of rate-limit rules.

***

### Filters

To narrow down visible rate-limit events, the following filters are available:

#### IP Address

Displays events triggered by a specific source IP.

#### Application

Filters events by the protected application.

#### Start At / End At

Filters events by date and time range.

#### Clear Filters

Resets all filters and returns to the full event list.

These filters simplify investigations when handling a large number of rate-limited clients.

***

### Rate Limiting Table Details

Each row in the table contains summarized diagnostic information:

#### IP Address

The client IP that exceeded rate-limit thresholds.\
Country information is shown for geographic context.

#### Application

The application receiving excessive traffic from the IP.

#### Detail

Summarizes the triggered rule, for example:

> “2 requests within 10 seconds – Basic Access Limit was triggered”

This information describes:

* Number of requests received
* Time window in which the requests occurred
* Which rate-limit rule blocked the traffic

#### Blocked

Total number of requests blocked during the rate-limit event.

#### Start At

Timestamp when the rate-limit event began.

#### State

Indicates the current status of the IP:

* **Blocked** – the IP is still under a rate-limit penalty
* **Unblocked** – the penalty period has expired

***

### Bulk Actions

The Rate Limiting page allows administrators to perform bulk operations.

#### Unblock All

Immediately removes all active rate-limit blocks.

This action is useful when:

* Updating or tuning rate-limit thresholds
* Testing traffic behavior or rule changes
* Resetting blocks after maintenance or security incidents
