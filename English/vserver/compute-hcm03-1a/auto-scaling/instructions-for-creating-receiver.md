# Instructions for creating Receiver

Receiver is a feature that allows you to Scale (IN / OUT) 1 Group using a web hook.

**Step 1:** At the Auto-scaling group interface, select a group you want to use the receiver for

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802637/image2019-5-24_0-4-53.png?version=1&#x26;modificationDate=1685070688000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 2:** Select receiver -> Create receiver

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802637/image2019-5-24_0-5-4.png?version=1&#x26;modificationDate=1685070689000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 3:** Enter receiver name and Acion Type. There are currently 2 Actions

\- CLUSTER\_SCALE\_IN : Reduce instances, each time by 1 if there is no scaling policy attached

\- CLUSTER\_SCALE\_OUT: Increase instance, each time by 1 if there is no scaling policy attached

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802637/image2019-5-24_0-5-18.png?version=1&#x26;modificationDate=1685070718000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Select receiver to create, after successful creation you will see Receiver as shown below.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802637/image2019-5-24_0-5-32.png?version=1&#x26;modificationDate=1685070718000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

To be able to trigger (trigger) this webhook url you need the following information:

\+ Web hook url: path information for you to call in, you get it by clicking "Copy channel"

\+ User\_id: account identifier information, you get by accessing [https://portal.vngcloud.vn/account.html](https://portal.vngcloud.vn/account.html) at the Account id field.

\+ Access key: authentication information, you contact us to be provided

For example, you have the following information:

\+ Web hook url: [https://example.vinadata.vn/v1/example/6e88c3f851dc4f48b11276c79a847d1c/receiver/81935b94-fc5c-4d06-869f-61aaaa4797e6/scale?backend=4](https://example.vinadata.vn/v1/example/6e88c3f851dc4f48b11276c79a847d1c/receiver/81935b94-fc5c-4d06-869f-61aaaa4797e6/scale?backend=4)

\+ user\_id: 47777

\+ access\_key: 89fa022b-6c44-43f2-b51c-3b332fbbf462

You can use curl to enable the extension

curl -H 'Content-type: application/json' -H 'user\_id:46677-H 'access\_key: 89fa3452b-6345-43f2-0000-3b332fbbf462' -XPOST '[https://example.vinadata.vn/v1/example/](https://example.vinadata.vn/v1/example/) 6e88c3f851dc4f48b11276c79a847d1c/receiver/81935b94-fc5c-4d06-869f-61aaaa4797e6/scale?backend=4'
