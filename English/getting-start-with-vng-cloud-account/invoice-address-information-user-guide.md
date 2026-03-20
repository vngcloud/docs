# Invoice address information user guide

### 1. Introduction <a href="#id-1-introduction" id="id-1-introduction"></a>

The **Invoice Address Information** feature allows users to:

* Add multiple invoice addresses (personal or enterprise)
* Set one address as **default** to be automatically used during checkout
* Delete addresses that are no longer needed

> ⚠️ **Note:** The Default Invoice Address will be prioritized during checkout.

### 2. How to Access <a href="#id-2-how-to-access" id="id-2-how-to-access"></a>

Access the **Invoice Address Information** screen at [https://register.vngcloud.vn/profile#invoice-address-info](https://register.vngcloud.vn/profile#invoice-address-info)

### 3. Main Screen Interface <a href="#id-3-main-screen-interface" id="id-3-main-screen-interface"></a>

The main screen displays a list of all saved invoice addresses.

#### 3.1. Information Displayed for Each Address <a href="#id-31-information-displayed-for-each-address" id="id-31-information-displayed-for-each-address"></a>

Each address in the list shows the following complete information:

<table><thead><tr><th width="208.13671875">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Recipient name (Personal) or Enterprise name</td></tr><tr><td><strong>Type</strong></td><td><code>PERSONAL</code> or <code>ENTERPRISE</code> badge</td></tr><tr><td><strong>Email</strong></td><td>Invoice receiving email address</td></tr><tr><td><strong>Phone Number</strong></td><td>Contact phone number (with country code)</td></tr><tr><td><strong>Tax Code</strong></td><td>Business tax code or Personal Identification Number (personal)</td></tr><tr><td><strong>Nationality</strong></td><td>Country</td></tr><tr><td><strong>Address</strong></td><td>Specific address</td></tr></tbody></table>

#### 3.2. Badges <a href="#id-32-badges" id="id-32-badges"></a>

* **`DEFAULT`** — Displayed next to the name of the address currently set as default. This address will be automatically selected during checkout.
* **`PERSONAL`** — Address is of personal type.
* **`ENTERPRISE`** — Address is of enterprise type.

#### 3.3. Action Buttons <a href="#id-33-action-buttons" id="id-33-action-buttons"></a>

* **Set as default** — Only shown for non-default addresses. Click to set this address as the default.
* **Delete** _(red button)_ — Only shown for non-default addresses. Click to delete this address.
* **Add Invoice Address** _(green button, bottom of page)_ — Opens a form to add a new address.

### 4. Adding a New Invoice Address <a href="#id-4-adding-a-new-invoice-address" id="id-4-adding-a-new-invoice-address"></a>

#### Step 1: Open the Add New Form <a href="#step-1-open-the-add-new-form" id="step-1-open-the-add-new-form"></a>

Scroll to the bottom of the list and click the **"Add Invoice Address"** button (green).

The **"Add Invoice Address Information"** dialog opens.

> _(Fields marked with `*` are required)_

#### Step 2: Select the Invoice Recipient Type <a href="#step-2-select-the-invoice-recipient-type" id="step-2-select-the-invoice-recipient-type"></a>

At the top of the form, select one of two types:

* 🔘 **Enterprise** — For customers that are organizations, companies, or enterprises
* 🔘 **Personal** — For individual customers

> This selection affects which information fields are displayed in the form below.

#### Step 3: Fill in the Information <a href="#step-3-fill-in-the-information" id="step-3-fill-in-the-information"></a>

**For Enterprise type**

<table><thead><tr><th width="171.39453125">Field</th><th width="142.59765625" align="center">Required</th><th>Notes</th></tr></thead><tbody><tr><td>Enterprise Name</td><td align="center">✅</td><td>Full legal name of the business</td></tr><tr><td>Email</td><td align="center">✅</td><td>Email address to receive e-invoices</td></tr><tr><td>Phone Number</td><td align="center">❌</td><td>Select country code from dropdown, then enter phone number</td></tr><tr><td>Tax Code</td><td align="center">✅</td><td>Business tax code</td></tr><tr><td>Nationality</td><td align="center">✅</td><td>Select country from the dropdown list</td></tr><tr><td>Address</td><td align="center">✅</td><td>Full address (house number, street, ward/commune, district, province/city)</td></tr></tbody></table>

**For Personal type**

<table><thead><tr><th width="189.6953125">Field</th><th width="152.62890625" align="center">Required</th><th>Notes</th></tr></thead><tbody><tr><td>Name</td><td align="center">✅</td><td>Full name of the recipient</td></tr><tr><td>Email</td><td align="center">✅</td><td>Email address to receive e-invoices</td></tr><tr><td>Phone Number</td><td align="center">❌</td><td>Select country code from dropdown, then enter phone number</td></tr><tr><td>Tax Code (12-digit Personal Identification Number)</td><td align="center">✅</td><td>Enter all 12 digits of the Personal Identification Number</td></tr><tr><td>Nationality</td><td align="center">✅</td><td>Select country from the dropdown list</td></tr><tr><td>Address</td><td align="center">✅</td><td>Full address</td></tr></tbody></table>

#### Step 4: Confirm the Information <a href="#step-4-confirm-the-information" id="step-4-confirm-the-information"></a>

Check the required checkbox:

> ☑️ **"I certify that the above information is true and approved by the recipient"** _(required)_

If this confirmation is not checked, the system will not allow saving the address.

#### Step 5 (Optional): Set as Default Address Immediately <a href="#step-5-optional-set-as-default-address-immediately" id="step-5-optional-set-as-default-address-immediately"></a>

If you want the newly added address to become the default address, check the box:

> ☑️ **"Set as default"**

#### Step 6: Save the Address <a href="#step-6-save-the-address" id="step-6-save-the-address"></a>

* Click the **"Add Invoice Address"** button (blue, bottom right) to save.
* Click **"Cancel"** to discard and return to the list.

### 5. Setting the Default Address <a href="#id-5-setting-the-default-address" id="id-5-setting-the-default-address"></a>

The default address is the one the system automatically fills in when the user proceeds to checkout.

#### How to Do It <a href="#how-to-do-it" id="how-to-do-it"></a>

1. In the address list, find the address you want to set as default.
2. Click the **"Set as default"** button to the right of that address.
3. The system updates immediately — the selected address will display the **DEFAULT** badge.

> ⚠️ **Important notes:** - Each account can only have **one** default address at a time. - The current default address does **not display** the "Set as default" button. - The current default address **cannot be directly deleted**.

### 6. Deleting an Invoice Address <a href="#id-6-deleting-an-invoice-address" id="id-6-deleting-an-invoice-address"></a>

#### How to Do It <a href="#how-to-do-it-1" id="how-to-do-it-1"></a>

1. In the list, find the address you want to delete.
2. Click the **"Delete"** button (red) to the right of that address.
3. A confirmation dialog appears with the title **"Confirm Delete Invoice Address"** and the message:

> _"Do you want to delete the Invoice Address \[Address Name]?"_

1. Choose one of the two options:
   * Click **"Delete Invoice Address"** (blue) to confirm permanent deletion.
   * Click **"Cancel"** to discard and keep the address.

> ⚠️ **Note:** You cannot delete an address that is currently set as **DEFAULT**. You must set another address as the default first, then you can delete the old address.
