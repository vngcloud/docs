# Registration of Partner Discount

* Partner discount is an amount of discount VNG Cloud offers partners in order to expand service distribution channel.
* Partners can use this function on partner portal to register the desired amount of discount, after being approved by VNG Cloud, partners will be able to apply it when a customer order is created at the time the discount is in “Active” status.

\


**Step 1**: Select “Partner discount”

<figure><img src="https://docs.vngcloud.vn/download/attachments/59805226/image2023-7-12_9-27-22.png?version=1&#x26;modificationDate=1689128842000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Screen displayed as below:

<figure><img src="https://docs.vngcloud.vn/download/attachments/59805226/image2023-7-12_9-29-19.png?version=1&#x26;modificationDate=1689128959000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Screen Description:**

(1): Discount is being applied, status = Active

(2): Discount history, list discounts form past to present except active discounts

(3): Instruction

**Step 2**:  Register discount

<figure><img src="https://docs.vngcloud.vn/download/attachments/59805226/image2023-7-12_10-32-50.png?version=1&#x26;modificationDate=1689132770000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* Choose “Register discount”, screen displayed as below:

| <p><br></p>                                                                                                                               | <p><br></p>                                                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><br></p>                                                                                                                               | <p><br></p>                                                                                                                                                                                                                                                                                                                                                      |
| ![](https://docs.vngcloud.vn/download/thumbnails/59805226/image2023-7-12\_10-33-59.png?version=1\&modificationDate=1689132839000\&api=v2) | <ul><li>% discount is automatically derived from current discount by the system, user can update new information</li><li>For unregistered discounts, user can input value=0</li><li>Active date: Input desired date to apply discount, this date must be +3 business days bigger than current date.</li></ul><p>Select “Register” to register input discount</p> |

After selecting “Register”, discount created will change to “Awaiting approval” status as below, at the same time user will receive an email announcing that discount registration request is being considered by VNG Cloud

<figure><img src="https://docs.vngcloud.vn/download/attachments/59805226/image2023-7-12_10-37-25.png?version=1&#x26;modificationDate=1689133045000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Within 3 business days, discount registered will be considered by VNG Cloud to either approve or reject.

* If VNG Cloud approves, status will be changed to “Awaiting activate”.
* For discounts with the status “Waiting to be activated”, when reaching active date, the status will be changed to “Active”
* For discount with the status “Active”, when a new discount’s status is change from “Waiting to be activated” to “Active”, current discount’s status will be changed to “Expired”.

_**Note:**_

* _If the date VNG Cloud approve discount is > than active date registered by user, discount’s active date will be updated equal to approved date_
* _Partner discount is applied when a new order is created by customer during the discount period_
* _At one time, there will be only one discount with the status “Active” and on discount with the status “Awaiting approval”_
* _When a new discount’s status is changed from “Awaiting Active” to “Active”, current discount’s status will be changed to “Expired”_

\
