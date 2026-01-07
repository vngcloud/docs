# IP Group Management

### Overview

The **IP Groups** module allows administrators to organize multiple IP addresses or CIDR ranges into reusable groups.

These groups simplify security management by enabling predefined IP sets to be reused across different WAF features.

IP Groups are currently applied in:

* **Allow & Deny Rules**
* **Anti-Bot configurations**

This approach ensures consistent enforcement and makes it easier to update trusted or blocked IP sources in one place.

***

### IP Groups Overview

The IP Groups list displays all created IP groups with the following information:

* **Name** – The IP group identifier
* **Content** – IP addresses or CIDR ranges included in the group
* **Updated at** – Timestamp of the most recent modification
* **Action** – Available actions such as Edit or Delete

IP Groups help centralize IP management across applications and security rules.

***

### Use Cases for IP Groups

IP Groups are useful in the following scenarios:

* Blocking known malicious IP addresses or IP ranges
* Allowlisting trusted networks or internal systems
* Grouping suspicious IPs for Anti-Bot tuning
* Maintaining consistent IP sets across multiple security rules

Any update to an IP Group will automatically apply to all rules that reference it.

***

### Add IP Group

Selecting **Add IP Group** opens the configuration dialog for creating a new IP group.

***

### IP Group Configuration

#### Name (required)

Provide a descriptive name for the IP group.

Examples:

* `Blocked group`
* `Trusted networks`
* `Suspicious scanners`

***

#### Reference (optional)

An optional URL pointing to an external source that contains a list of IP addresses.

If provided, the system stores this link as a reference for the IP group.

> Note: This field does **not** automatically update IP content and contains no example.

***

#### Content

Enter IP addresses or CIDR ranges, **one entry per line**.

Supported formats include:

```
192.168.1.10
68.22.141.0/24
103.245.252.19
```

Notes:

* Each IP or CIDR range must be entered on a separate line
* Both single IP addresses and CIDR notation are supported

***

### Available Actions

#### Edit

Modify the IP group name, reference link, or IP/CIDR content.

Changes take effect immediately and apply to all rules using the group.

***

#### Delete

Permanently remove the IP group.

Any rule that references the deleted group should be reviewed to avoid unintended access control behavior.
