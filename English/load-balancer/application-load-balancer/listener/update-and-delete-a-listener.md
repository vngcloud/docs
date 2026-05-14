# Update & Delete a Listener

Use this guide to modify or remove listeners from your Application Load Balancers (ALBs).

#### Updating a Listener

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer containing the listener you want to edit.
3. **Go to the Listener Tab:** In the Load Balancer details page, select the "Listener" tab.
4. **Review Listener Details:** Click on the listener you want to edit in the list. Review its details on the right side of the screen, including:
   * Listener information
   * Policy information (if applicable)
   * Certificate information (for HTTPS listeners)
5. **Click "Edit":** Click the "Edit" icon next to the listener you want to modify.
6. **Make Changes:** A pop-up window will appear, allowing you to edit the following:
   * **Request Headers:** Modify the headers that are added to requests.
   * **Client Certificate Authentication (HTTPS):** Enable or disable client certificate authentication (see Client Certificate Authentication for details).
   * **Default Certificate (HTTPS):** Change the default SSL/TLS certificate.
   * **Default Pool:** Change the pool that handles requests not covered by policies.
   * **Advanced Configuration:**
     * Configure timeouts
     * Configure IP whitelists
7. **Save Changes:** Click "Save" to finalize your edits.

#### Deleting a Listener

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer containing the listener you want to delete.
3. **Go to the Listener Tab:** In the Load Balancer details page, select the "Listener" tab.
4. **Click "Delete":** Click the "Delete" icon next to the listener you want to remove.
5. **Confirm Deletion:** A confirmation window will appear. Click "Delete" to finalize.

#### Important Notes

* **Listener Names:** Listener names cannot be changed after creation.
* **HTTPS Listeners:** If you delete an HTTPS listener, associated certificates will not be automatically deleted.
* **Default Pool:** Ensure you have a default pool configured to handle traffic if you delete a listener that was the default for certain requests.
