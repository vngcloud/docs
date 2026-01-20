# Allow & Deny Rules

### Overview

The **Allow & Deny Rules** module enables administrators to define custom access control rules for their applications.

These rules allow or block specific IP addresses, IP ranges, or traffic patterns **before requests reach the application**.

This module includes:

* **Rules** – where Allow and Deny rules are created and managed
* **Events & Logs** – where activities triggered by these rules are recorded and displayed

***

### Rules Management

The **Rules** page lists all Allow and Deny rules configured by the user.

Each rule entry displays:

* Rule name
* Associated application
* Rule type (Allow or Deny)
* Number of hits today
* Rule creation time
* Rule status (Enabled / Disabled)

This page serves as the central place to manage access control rules.

***

### Rule Types

#### Allow Rule

An **Allow Rule** permits requests that match the configured conditions.

Common use cases include:

* Whitelisting trusted IP addresses
* Allowing traffic from internal networks
* Bypassing WAF inspection for specific traffic sources

***

#### Deny Rule

A **Deny Rule** blocks requests that match the configured conditions.

Common use cases include:

* Blocking known malicious IP addresses
* Preventing abusive scanners or bots
* Restricting traffic from unwanted regions or networks

***

### Rule Filtering

A filter dropdown allows users to quickly display:

* All rules
* Only Allow rules
* Only Deny rules

This makes it easier to manage large rule sets.

***

### Rule Actions

Each rule provides the following management actions:

* **Enable / Disable** – toggle rule activity without deleting it
* **Edit** – modify rule configuration
* **Delete** – permanently remove the rule

All changes take effect within **10 seconds to 1 minute** after being applied.

***

### Events & Logs

The **Events & Logs** section provides visibility into activities triggered by Allow and Deny rules.

It includes two views:

* **Events** – summarized activity grouped by source IP
* **Logs** – detailed request-level records

***

### Events View

The **Events** tab shows aggregated information for requests that matched Allow or Deny rules.

Each row displays:

* Source IP address and country
* Target application
* Hit count (number of times the rule was matched)
* Duration of the activity
* Event start time

This view helps users:

* Identify abusive or suspicious traffic sources
* Monitor how frequently rules are triggered
* Detect repeated offenders

Filters allow narrowing results by:

* IP address
* Domain
* Port
* Time range

***

### Logs View

The **Logs** tab shows every individual request that matched an Allow or Deny rule.

Typical fields include:

* Action taken (Allowed or Blocked)
* Requested URL
* Rule type (Allow Rule or Deny Rule)
* Source IP address
* Timestamp
* Detail action

This view is commonly used for detailed inspection of rule behavior and affected user traffic.

Available filters include:

* Action (Allowed / Blocked / All)
* Port
* IP address
* Domain
* Rule type
* Time range

***

### Events & Logs – Detail View

Clicking the **Detail** icon opens the full request information for a rule-triggered event.

The detail view displays:

* Full requested URL
* Action taken (Allowed or Blocked)
* Source IP address and geolocation
* Detection module (Allow Rule or Deny Rule)
* Rule name
* Timestamp
* Event ID

Below the summary, the **raw HTTP request** is shown, including:

* HTTP method and path
* Host header
* User-Agent
* Additional request headers

This view is used for:

* Verifying rule behavior
* Investigating access control decisions
* Collecting evidence for security audits or incident analysis
