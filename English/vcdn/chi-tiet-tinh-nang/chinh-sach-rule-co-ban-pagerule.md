# Page Rule

## Overview <a href="#tong-quan" id="tong-quan"></a>

**Page Rules** are a powerful tool in the vCDN system that allows you to customize how the CDN handles requests to your website based on predefined rules. With Page Rules, you can apply specific settings to one or more URLs, helping to optimize performance, enhance security, or improve user experience.

## Detail <a href="#chi-tiet" id="chi-tiet"></a>

When initializing Live Stream, Object Download,... you can initialize Page Rule by selecting **Create Page Rule** . A Rule will be executed when there is a URI request that matches the conditions defined in the Rule.

<figure><img src="../../.gitbook/assets/image (375).png" alt=""><figcaption></figcaption></figure>

After you select Create Page Rule, the screen displays as follows:

<figure><img src="../../.gitbook/assets/image (376).png" alt="" width="375"><figcaption></figcaption></figure>

In there:

* **URL Pattern:** enter the URL pattern to apply Page Rule, vCDN supports the declaration type “\*” representing a string of multiple characters. For example: /trang\_landing\_cu.html
* **Actions when conditions are met:** Each Rule when the condition is met for the requested URI can optionally execute one of the following actions:
  * Always Use HTTPS
  * Auto Minify
  * Automatic HTTPS Rewrites
  * Server Cache TTL
  * Browser Cache TTL
  * Bypass Cache by Cookie
  * Bypass Cache By Device Type
  * Forwarding URL
  * Add Response Header
  * Brotli
  * Gzip
  * Origin Override

For details, please refer to the table below.

Each Page Rule will have different actions shown in the table below. “Order” is to arrange the position of the rules, the smaller the number, the higher the priority of execution.

<figure><img src="../../.gitbook/assets/image (377).png" alt="" width="279"><figcaption></figcaption></figure>

Once created, select **Save changes** to update the changes.

***

The table describes the action types:

| **Rule**                        | **Action**                                                                            | **Describe**                                                                                                                                                                                                                                                                       |
| ------------------------------- | ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Always Use HTTPS**            | ON/OFF                                                                                | Enable/Disable “Always use HTTPS protocol” option on the specified page.                                                                                                                                                                                                           |
| **Auto Minify**                 | Javascript / CSS / HTML                                                               | Option to override minify function on specified page.                                                                                                                                                                                                                              |
| **Automatic HTTPS Rewrites**    | ON/OFF                                                                                | Enable or disable the feature to automatically replace HTTP URLs to HTTPS in the specified page.                                                                                                                                                                                   |
| **Server Cache TTL**            |                                                                                       | Re-select cache time on Edge Servers or “Bypass Cache” on specified page.                                                                                                                                                                                                          |
| **Browser Cache TTL**           |                                                                                       | Similar to “Server Cache TTL”, but specifies the cache time on the End-user browser.                                                                                                                                                                                               |
| **Bypass Cache By Cookie**      | Enter the values ​​“cookie\_name” and “cookie\_value”                                 | <p>If there is a cookie specified from the end-user, the system will perform the bypass cache command on the specified page.</p><p>If the “cookie_value” value is empty, the system only considers if “cookie_name” exists and does not care about the value of “cookie_value”</p> |
| **Bypass Cache By Device Type** | Enter “Agent Text” values, multiple values ​​supported, separated by “Tab” or “Enter” | If the end-user browser used has information that matches one of the Agent Texts, the system will automatically bypass the cache on the specified page.                                                                                                                            |
| **Forwarding URL**              | Redirect code (301/302) and destination URL.                                          | Automatically redirects the specified URL to the new destination URL.                                                                                                                                                                                                              |
| **Host Header Override**        | Header\_name and header\_value                                                        | Automatically add headers returned to end-user browsers on specified pages.                                                                                                                                                                                                        |
| **Brotli**                      | ON/OFF                                                                                | Brotli enable/disable option on specified page.                                                                                                                                                                                                                                    |
| **Gzip**                        | ON/OFF                                                                                | Option to enable/disable Gzip on specified page.                                                                                                                                                                                                                                   |
| **Resolve Origin Override**     | IP New Origin                                                                         | Option to change Origin Server IP on specified page.\*                                                                                                                                                                                                                             |
