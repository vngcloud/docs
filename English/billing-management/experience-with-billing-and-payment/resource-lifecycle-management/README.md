# Resource lifecycle management

Use this document to understand more about the resources you are using.

Here, we provide information about the resource lifecycle and actions that users/systems can take that may affect the state of the resource being used.

Through the resource lifecycle model below, you will have an overview of the state transition of the resource, as well as the connection between the resource and the bill.

## Resource lifecycle model

### **Prepaid user actions on resources**

* **New → Active:** When the user successfully initializes the resource, the resource will have a state of Active and corresponding invoices will be generated.
* **Active → ← Stop**: Users perform the Start, Reboot / Stop action on the resource to switch between these two states.
* **Active → ← Suspense:**
  * Active → Suspense: The resource has expired and is moved to the trash to be completely deleted.
  * Suspense → Active: The user restores the resource in the trash to continue using it.
* **Active → Deleted:** The user deletes the resource.
* **Suspense → Deleted:** The resource has expired, and after a period of time in the trash, it will be permanently deleted and cannot be restored.

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Postpaid user actions on resources

* **New → Active:** When the user successfully initializes the resource, the resource will have a state of Active.
* **Active → ← Stop:** Users perform the Start, Reboot / Stop action to switch between these two states.
* **Active → Deleted:** The user deletes the resource.
* **Suspense → Deleted:** The resource has expired, and after a period of time in the trash, it will be permanently deleted and cannot be restored.
* **Invoice generation:** For postpaid users, invoices will be generated at the end of the month, recording information about the use of that resource. In the case where the user deletes the resource, usage information will also be recorded and invoices will be generated based on that information.
