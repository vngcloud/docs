# Pricing

GLB pricing is calculated based on the number of Connections and the amount of Data transferred. For prepaid users, the system will hold credits based on the current usage forecast for the next 3 days. For postpaid users, payment will be processed at the beginning of the following month.

Specifically:

## Connection-Based Pricing

* **Formula:**\
  `Total of (Maximum hourly connections - Free allowance) from the beginning of the month until now / 720`
* If the result < 100 → Round up to 100.
* If the result ≥ 100 → Keep the original value.
* #### Example:
  * **Free allowance**: 4.000 connection.
  * **Day 1:** Using 10.000 connection → `(10.000 - 4.000) / 720 ≈ 8.33` → Rounded up to 100.
  * **Day 30:** Total for 30 days → `(10.000 - 4.000) × 30 / 720 = 250` → Keep as 250.

***

## Data Transfer-Based Pricing

* **Formula:**\
  `Total of (Maximum daily traffic - Free allowance) from the beginning of the month until now`
  * If the result is negative → Rounded to 0.
* **Example:**
  * **Free allowance:**
    * Domestic traffic: 500GB
    * International traffic: 50GB
  * **Day 1:**
    * Using 50GB (Domestic) → `50 - 500 = -450` → Rounded to 0.
    * Using 5GB (International) → `5 - 50 = -45` → Rounded to 0.
  * **Day 11:**
    * Using 550GB (Domestic) → `550 - 500 = 50` → Charged for 50GB.
    * Using 55GB (International) → `55 - 50 = 5` → Charged for 5GB.

**Important Notes**

* When charges are incurred, the system will calculate and accumulate them into the hold amount for the following days.
