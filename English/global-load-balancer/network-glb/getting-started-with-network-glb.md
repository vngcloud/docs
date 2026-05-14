# Getting Started with Network GLB

In this section, we will learn how to use and manage a Network GLB in the most basic way, providing an overall understanding of how Network GLB works.

#### Trước khi bắt đầu <a href="#gettingstarted-nlb-truockhibatdau" id="gettingstarted-nlb-truockhibatdau"></a>

* Tìm hiểu cách **truy cập GreenNode Portal** với Root User Account hoặc IAM User Account, tham khảo hướng dẫn [How to Login into GreenNode](../../identity-and-access-management-iam/).

#### 1. Access the GLB Console <a href="#gettingstarted-nlb-1.truycapvlbconsole" id="gettingstarted-nlb-1.truycapvlbconsole"></a>

The GLB Console is a web-based user interface that allows you to manage Global Load Balancers in your cloud environment. It provides an intuitive interface for controlling and managing your GLBs.

**How to Access the GLB Console**

* Access from the vConsole homepage: [https://dashboard.console.vngcloud.vn/](https://dashboard.console.vngcloud.vn/)
  * Under the “GreenNode Service” section in the interface, select “vServer”, then choose “GLB” from the corresponding product/service list on the right.
* Or directly access the vLB Portal via:: [https://glb.console.vngcloud.vn/overview](https://glb.console.vngcloud.vn/overview)

#### 2. Create a Network GLB <a href="#gettingstarted-nlb-2.khoitaonlb" id="gettingstarted-nlb-2.khoitaonlb"></a>

**How to Create a Network GLB**

1. From the Global Load Balancer homepage, click “Create Global Load Balancer”.
2. Select Load Balancer Configuration
   * **Global Load Balancer Name:** If the user does not manually provide a GLB name, the system will automatically generate one.
   * **Layer:** Select “Network - TCP”.
3. Configure Listener
   * **Listener Name:** If the user does not manually provide a Listener name, the system will automatically generate one.
   * Protocol & Port
     * If **Protocol = TCP**, the user must select a Port (Port 80 is pre-filled by default).
4. Configure Global Pool
   * **Global Pool Name:** If the user does not manually provide a Pool name, the system will automatically generate one.
   * **Protocol:** TCP/Proxy (for TCP Listener).
   * **Algorithm:** Select an appropriate load balancing algorithm.
   * **Health Check Settings:** Protocol options include TCP / HTTP / HTTPS (for TCP/Proxy Pool).
5.  Select Global Pool Member&#x73;**:** Add backend servers to the Global Pool Member.

    Global Pool Members allow users to add backend servers from multiple Regions.

    * Select Region and VPC for the Global Pool Member.
    * Next, attach backend servers (from subnets within the same VPC) to the pool.
6.  Review Configuration Informatio&#x6E;**:** Users can review the configuration information before completing the creation process. This information will be displayed on the right side of the input screen.

    * “Summary” Tab:&#x20;

    Review the configuration details for:

    * GLB
    * Global Listener
    * Global Pool
    * Global Pool Member
7. Complete the Creation Proces&#x73;**:** After completing the configuration and reviewing the information, click “Create Global Load Balancer / Create Load Balancer” to finish creating the GLB.

#### 3. Monitor and Verify NGLB <a href="#gettingstarted-nlb-3.quansatvakiemtranlb" id="gettingstarted-nlb-3.quansatvakiemtranlb"></a>

* After successful creation, the system will redirect users to the Global Load Balancer list page. Here, users can monitor the GLB status from **Creating** to **Active** (successfully created).
* Once the creation process is complete, users can access the Global Load Balancer detail page to monitor and verify the correctness of the GLB configuration.
