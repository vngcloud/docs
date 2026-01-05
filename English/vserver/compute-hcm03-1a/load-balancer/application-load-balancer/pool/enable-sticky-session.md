# Enable sticky session

As we know, HTTP is stateless (subsequent requests do not depend on previous request results), so sessions are used to store data between pages.

The most common example is an authentication token stored in a session to confirm a user has logged into the system. User authentication information is stored in the session, which resides on a specific server and is not synchronized across web servers. This causes logged-in users to be logged out if their request is routed to a different web server than the one that handled their login request.

To address this, you can:

* Use a cluster for your web server application, with sessions stored in a central location accessible to all servers.
* Store session information in a shared database or a file system server on the application server.
* **Drawback:** Building a cluster system or a database requires significant system expertise.

That's why GreenNode offers the Sticky Session feature, which directs all requests from a user within a session to the same server, simplifying things for users.

## Introduction to Enable Sticky Session

The Enable Sticky Session feature is a crucial part of the Load Balancer, allowing you to maintain session continuity for clients on your application. When enabled, the Load Balancer ensures that requests from the same client are always forwarded to the same backend server for a specified period.

#### How it Works

1. **Client Identification:** When a client connects to your application through the Load Balancer, the Load Balancer tracks information to identify that client (usually based on cookie data or IP address).
2. **Request Routing:** Subsequent requests from the same client are forwarded to the same backend server for a predetermined duration.
3. **Session Continuity:** This ensures that the client's state and information are maintained consistently throughout their session.

#### Benefits of Enabling Sticky Sessions

* **Enhanced User Experience:** Sticky Sessions improve the end-user experience by maintaining consistent session state, preventing data loss or the need to re-login.
* **Support for State-Dependent Applications:** Applications that rely on session state, such as online shopping carts, benefit from this feature.

## How to Enable/Disable Sticky Sessions

1. **Access the Load Balancer Homepage:** Go to `https://hcm-3.console.vngcloud.vn/vserver/load-balancer/vlb`.
2. **Select Your Load Balancer:** Click on the Load Balancer you want to configure.
3. **Go to the Pool Tab:** In the Load Balancer details page, select the "Pool" tab.
4. **Edit Pool:** Hover over the pool you want to modify and click the "Edit" icon.
5. **Edit Pool Window:** A pop-up window will appear, allowing you to edit the pool settings.
6. **Toggle Sticky Session:** In the pool information section, find the "Enable sticky session" checkbox. Check or uncheck it to enable or disable Sticky Sessions.
7. **Save Changes:** Click "Save" in the bottom right corner of the window to finalize your changes.
