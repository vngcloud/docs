# Add & Update a Pool

Use this guide to add a new pool or update an existing one in your Application Load Balancer (ALB).

## Adding a New Pool

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer where you want to add the new pool.
3. **Go to the Pool Tab:** In the Load Balancer details page, select the "Pool" tab.
4. **Click "Add New Pool":** A pop-up window will appear, allowing you to configure the pool's information.
5. **Configure Pool Settings:**
   * **Pool Name:** Note that the pool name cannot be changed after creation.
   * **Protocol:** **TCP / Proxy / UDP.**
   * **Load Balancing Algorithm:** Choose a suitable algorithm (refer to Pool's algorithm for more information).
   * **Health Check Settings:** Configure health check settings for TCP/HTTP protocols (refer to Config health check setting for instructions).
   * **Add Pool Members:** Add backend servers or IP addresses to the pool (refer to Attach pool members for instructions).
6. **Click "Add" to finalize:** Click the "Add" button in the bottom right corner of the window to complete the pool creation.

## Updating a Pool

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer containing the pool you want to edit.
3. **Go to the Pool Tab:** In the Load Balancer details page, select the "Pool" tab.
4. **Click "Edit":** Hover over the pool you want to edit and click the "Edit" icon.
5. **Make Changes:** A pop-up window will appear, allowing you to edit the following:
   * **Load Balancing Algorithm**
   * **Advanced Health Check Configuration**
6. **Save Changes:** Click "Save" in the bottom right corner of the window to finalize your pool updates.

