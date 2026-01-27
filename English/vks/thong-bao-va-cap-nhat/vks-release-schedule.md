# VKS Version Release Schedule

This page lists the release dates and end-of-support dates for Kubernetes versions on VKS (VNGCloud Kubernetes Service).

## Release Channel Overview

VKS provides the following release channels to manage Kubernetes version lifecycle:

| Release Channel    | Description                                                                         |
| ------------------ | ----------------------------------------------------------------------------------- |
| **Rapid**    | Latest version, intended for testing environments and early adopters. |
| **Stable**   | Stable version, recommended for production environments.     |
| **Extended** | Extended support period for older versions.                    |

## Version Release Schedule

The table below shows the release schedule and support timeline for Kubernetes versions on VKS. Patch versions will continue to be available until **end of standard support**, except for clusters using the **Extended channel** - where the version and its patches will continue to be available until **end of extended support**.

{% hint style="warning" %}
**Note:** The dates in the table are best estimates and are updated periodically as new information becomes available.
{% endhint %}

{% hint style="info" %}
**Legend:**

* **Available**: The date when the version can be used to create new clusters.
* **\***: Version currently supported on VKS.
{% endhint %}

| Version | Rapid Available | Stable Available | End of Standard Support | End of Extended Support |
|---------|-----------------|------------------|-------------------------|-------------------------|
| **1.27** | 17/04/2024 | 26/08/2024 | 12/05/2025 | - |
| **1.28** | 17/04/2024 | 26/08/2024 | 24/11/2025 | - |
| **1.29*** | 17/04/2024 | 20/02/2025 | 05/2026 | 11/2026 |
| **1.30*** | 02/01/2025 | 22/05/2025 | 05/2027 | 11/2027 |
| **1.31** | 03/2026 | 05/2026 | 05/2028 | 11/2028 |
| **1.32** | 03/2026 | 06/2026 | 05/2029 | 11/2029 |
| **1.33** | 05/2026 | 11/2026 | 05/2030 | 11/2030 |

{% hint style="warning" %}
**Note:** After the **End of Standard Support** date, VKS will force upgrade each cluster still running on the old version to the next supported version. Customers who need extended support please [contact us](https://vngcloud.vn/contact) for consultation and assistance.
{% endhint %}

## Release Schedule Prediction Stages

The dates in the release schedule typically go through the following stages, with increasing levels of detail and certainty:

| Stage                                 | Description                                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **TBD**                               | When an item is marked as "TBD", the date has not yet been determined.                                                                                                                                                                                                                                                                   |
| **Month or Quarter Prediction** | Dates with only month (e.g., 2025-03) or quarter (e.g., 2025-Q3) are estimates that will be updated when specific dates are known. Dates are updated from quarter to month prediction when the estimated date is less than three months away.                                                                          |
| **Day Prediction**             | *Italicized* dates with day-level detail are provided when the month prediction is less than 14 days from the last update of the release schedule table, but the specific date has not yet been determined. These italicized dates are estimates and will be updated when specific dates are known. |
| **Specific Date**                    | Non-italicized dates are best estimates, representing the highest level of certainty in the release schedule.                                                                                                                                                                                                                         |

## Version Support Policy

VKS follows these principles for Kubernetes version support:

1. **New Versions**: New Kubernetes versions are first released in the **Rapid channel** so users can test before moving to the **Stable channel**.
2. **Support Duration**: Each version of Kubernetes is supported for a specific period. After this time, the version will be marked as end-of-support.
3. **End of Standard Support**: When a version reaches end-of-support:

   * Users will not be able to create new clusters/node groups with that version.
   * Existing clusters will be automatically upgraded to the next supported version.
4. **Recommendation**: To ensure stability and security, we recommend users proactively upgrade their clusters to a new version before the current version reaches end-of-support.

## Related Documentation

* [Release Notes](release-notes.md) - View detailed updates and new features of VKS.
