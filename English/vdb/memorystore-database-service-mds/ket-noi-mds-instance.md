# Connect MDS Instance

**How to Connect to Your Redis DB Instance**

You have several options for connecting to your Redis DB Instance:

**1. Using a Graphical User Interface (GUI):**

* Download and install AnotherRedisDesktopManager from [https://www.electronjs.org/apps/anotherredisdesktopmanager](https://www.electronjs.org/apps/anotherredisdesktopmanager).
* Follow the video tutorial (starting at 1:00) for instructions on how to connect.

[https://www.youtube.com/watch?v=1kvJi3Hg4wM\&t=6s](https://www.youtube.com/watch?v=1kvJi3Hg4wM\&t=6s)

**2. Using the Command Line Interface (CLI) with redis-cli:**

* **Download and install redis-cli:**
  *   On Linux, you can download the source code and build it:Bash

      ```
      wget http://download.redis.io/redis-stable.tar.gz
      tar xvzf redis-stable.tar.gz
      cd redis-stable
      make distclean  # Ubuntu systems only
      make   
      sudo make install
      ```

      Hãy thận trọng khi sử dụng các đoạn mã.
*   **Step 1: Identify Endpoint & Port:**

    * Go to the Database management interface, select your newly created MemoryCache Database instance, go to the Connectivity & Security tab, and look under Endpoint & Port.
    * For security reasons, MDS Instances only have a Private Endpoint. You can only connect to it from a vServer in the same Network or from Networks with open ACLs.



    <figure><img src="../../.gitbook/assets/image (232).png" alt=""><figcaption></figcaption></figure>

    * Alternatively, you can set up an SSH Tunnel on a vServer in the same Network as this MDS Instance and connect remotely via the Internet.
*   **Step 2 (Optional): Customize Security Group Rules:**

    * The Security Group Rules section allows you to restrict which Remote IPs can access your DB Instance.
    * By default, VNG Cloud allows unrestricted access from anywhere (0.0.0.0/0) to your DB Instance. It's recommended to customize this to allow access only from trusted IPs.



    <figure><img src="../../.gitbook/assets/image (233).png" alt=""><figcaption></figcaption></figure>

    * To change the rules, select EDIT and enter the appropriate IP (in CIDR format). You can also add new rules by clicking ADD RULE.
    * After editing, click Save and wait for the changes to be applied.
    * Use tools like telnet to ensure a smooth connection.
* **Step 3: Connect using redis-cli:**
  *   Once you have the endpoint information (IP and port), you can connect using redis-cli:Bash

      ```
      redis-cli -h <your_db_instance_ip> -p <your_db_instance_port>
      ```

      Hãy thận trọng khi sử dụng các đoạn mã.For example:Bash

      ```
      redis-cli -h 10.23.0.5 -p 6379
      10.23.0.5:6379> 
      ```

      Hãy thận trọng khi sử dụng các đoạn mã.

Congratulations, you have successfully connected to your Redis DB Instance!
