---
description: >-
  The system availability commitment (SLA) for GreenNode MaaS, covering the
  monthly uptime commitment, the definition of Downtime, the calculation
  formulas and the excluded cases.
---

# SLA

## Monthly uptime commitment

| Committed rate | Unit of measurement | Equivalent Downtime |
|---|---|---|
| **99.9%** | Time the API requests are not served (server stops operating) | No more than 43 minutes 50 seconds per month |

## Definitions

| Term | Definition |
|---|---|
| **Monthly Uptime Period** | The total number of minutes in the month minus the total number of minutes in that month during which the Service system is in the Unavailable State due to Party A's fault, excluding maintenance windows, Service suspension caused by a Force Majeure Event and other excluded cases |
| **Unavailable State** (Downtime) | The state in which one or more of the cases listed in the Unavailable State section below occurs |
| **Monthly Uptime Rate** | 100% minus the Monthly Downtime Rate |
| **Monthly Downtime Rate** | The total time in the month during which the system is in the Unavailable State, divided by the total time in the month, multiplied by 100 |

## Unavailable State (Downtime)

The system is in the Unavailable State when one or more of the following cases occurs:

| Case | Description |
|---|---|
| a | The system stops responding |
| b | Server down time |

## Calculation formulas

| Metric | Formula |
|---|---|
| Monthly Downtime Rate | (Total time in the Unavailable State during the month ÷ Total time in the month) × 100 |
| Monthly Uptime Rate | 100% − Monthly Downtime Rate |
| Monthly Uptime Period | Total minutes in the month − Total minutes in the Unavailable State due to Party A's fault |

## Exclusions from Downtime

| Excluded case | Description |
|---|---|
| Maintenance windows | System maintenance periods |
| Force Majeure Event | Service suspension caused by a Force Majeure Event |
| Causes outside Party A's fault | Downtime is counted only when the Unavailable State arises from Party A's fault |
| Other cases | Other cases excluded under the terms of the service contract |

{% hint style="info" %}
The capitalized terms on this page (Unavailable State, Force Majeure Event, Party A) are defined in the service contract. For the full terms, contact [support@greennode.ai](mailto:support@greennode.ai), hotline **19001549** or the [Help Center](https://helpdesk.greennode.ai/portal/en/home).
{% endhint %}
