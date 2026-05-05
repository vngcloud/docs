# Pricing

In the journey of building modern AI applications, understanding operational costs is essential for optimizing budgets and ensuring return on investment. With the AI Stack at GreenNode, we provide a powerful ecosystem for developers, AI Engineers, Data Scientists, and enterprises — from Notebook for development, Inference for model deployment, to Network Volume for flexible data storage.

This guide will help you understand how pricing is calculated for each resource in the AI Stack, along with the available payment models, so you can effectively manage costs from the start.

## 1. Notebook Instance

* **Pricing Method:**
  * Based on compute type (flavor): number of CPUs, RAM, GPUs.
  * Based on the size of Local Block Storage attached to the notebook.
* **Payment Options:**
  * Prepaid: The system charges immediately upon notebook creation. If the notebook is deleted early, the remaining balance will be automatically refunded.
  * Postpaid: Use first, pay later at the end of each billing cycle, typically at the end of the month.

## 2. Inference Endpoint

* **Pricing Method:**
  * Based on compute type (flavor): number of CPUs, RAM, GPUs used to run the model.
  * If auto-scaling is enabled, costs are multiplied by the actual number of running instances.
* **Payment Options:**
  * Prepaid: Charges are applied upon endpoint creation. Unused time will be refunded if the endpoint is deleted early.
  * Postpaid: Use first, pay later at the end of each billing cycle, typically at the end of the month.

## 3. Network Volume

* **Pricing Method:**
  * Based on actual storage usage (GB) — helping you optimize costs by paying only for what you use.
* **Payment Option:**
  * Hold Credit: The system reserves a portion of your credit and deducts it gradually based on usage.

## 4. Payment Methods on GreenNode

GreenNode supports three flexible payment models:

* **Prepaid** – Pay upfront, with refunds for unused resources.
* **Postpaid** – Pay after usage based on actual consumption.
* **Hold Credit** – The system temporarily holds a balance and deducts it based on usage.

For more details [Introduction to Payment Methods on GreenNode](https://docs.vngcloud.vn/vng-cloud-document/billing-management/experience-with-billing-and-payment)
