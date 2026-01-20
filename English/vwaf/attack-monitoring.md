# Attack Monitoring

### Overview

The **Attacks** section provides visibility into malicious activities detected by the WAF.\
It helps users monitor attack sources, review blocked or allowed malicious requests, and investigate security incidents.

This section includes three main views:

* **Events** – summarizes attack activity grouped by source IP
* **Logs** – displays every individual malicious request
* **Detail View** – shows full information for a specific attack event

***

### Attacks – Events View

The **Events** tab provides a high-level overview of detected attacks, grouped by attacker IP address.

For each source IP, users can see:

* Source IP address and country
* Targeted application
* Number of detected attacks
* Attack duration
* Time when the attack started

Filtering options allow users to narrow down results by:

* IP address
* Domain
* Port
* Time range

This view is useful for:

* Identifying repeated attackers
* Detecting large-scale or ongoing attack waves
* Quickly assessing the severity of an attack source

***

### Attacks – Logs View

The **Logs** tab provides request-level visibility into every detected malicious request.

For each request, users can review:

* Action taken by the WAF (Blocked or Allowed)
* Detected attack type (e.g., XSS, SQL Injection)
* Full request path containing the malicious payload
* Attacker’s IP address
* Timestamp of the request

Logs can be filtered by:

* Action (Blocked / Allowed / All)
* Port
* IP address
* Domain
* Attack type
* Time range

This view is commonly used for:

* Deep threat investigation
* Analyzing false positives
* Fine-tuning WAF security rules

***

### Attack Detail

The **Attack Detail** view provides full information for a single malicious request.

It displays:

* Full URL that triggered detection
* Action taken (Blocked or Allowed)
* Attack type
* Attacker IP address and geolocation
* Detected payload
* Detection module
* Timestamp
* Attack ID

Below the summary information, the interface shows the **raw HTTP request**, including:

* HTTP method
* Request headers
* Request payload

Depending on system configuration, a **Response** tab may also be available.

This view is used for:

* Verifying whether the WAF correctly detected and handled the attack
* Understanding the structure and intent of malicious payloads
* Collecting evidence for security incident reports
* Investigating repeated or advanced attack patterns
