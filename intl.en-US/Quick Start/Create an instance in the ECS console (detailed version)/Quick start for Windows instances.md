---
keyword: [quick start, ECS, starter, user guide, Alibaba Cloud, Alibaba Cloud Linux]
---

# Quick start for Windows instances

This topic walks you through the procedure to configure Internet Information Services \(IIS\) for a Windows Server 2016 instance of the ecs.g6.large instance type. You can use this topic to familiarize yourself with operations in the ECS console.

## Preparations

1.  Create an account and complete the account information.

    -   Create an Alibaba Cloud account. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/doc-detail/50482.htm).
    -   Bind your credit card or PayPal account. For more information, see [Add a payment method](https://www.alibabacloud.com/help/doc-detail/50517.htm).
    -   To purchase ECS instances in mainland China regions, you must complete real-name verification. For more information, see [Real-name registration FAQs](https://www.alibabacloud.com/help/doc-detail/52595.htm).
2.  Alibaba Cloud provides a default VPC. If you do not want to use the default VPC, you can create a VPC and a vSwitch in the region where you want to create an instance.

    For more information, see [Create an IPv4 VPC network](/intl.en-US/Quick Start/Create an IPv4 VPC network.md).

3.  Alibaba Cloud provides a default security group. If you do not want to use the default security group, you can create a security group in the region where the instance is created.

    For more information about how to create a security group, see [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md).


## Step 1: Create an ECS instance

1.  Go to the [Custom Launch](https://ecs-buy.aliyun.com/wizard/#/) tab in the ECS console.

2.  In the first four configuration steps of the buy page, complete the instance launch configuration.

    The following configurations are used in this topic. Keep the default settings for parameters that are not described in this topic.

    |Step|Parameter|Example|Descripition|
    |----|---------|-------|------------|
    |**Basic Configurations**|**Billing Method**|Pay-As-You-Go|The pay-as-you-go billing method allows more flexible operations. For more information, see [Billing overview](/intl.en-US/Pricing/Billing overview.md). **Note:** If an ICP filing is required for your domain name, you must select **Subscription**. |
    |**Region**|    -   Region: China \(Hangzhou\)
    -   Zone: Random
|You cannot change the region or zone after the instance is created. Exercise caution when you configure this parameter.|
    |**Instance Type**|    -   Family: General Purpose Type g6
    -   Instance Type: ecs.g6.large
|Instance types that are available are determined by the region you select and the inventory in the region. You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region. |
    |**Image**|    -   Type: Public Image
    -   Version: Windows Server 2016 Datacenter 64-bit
|After the instance is created, the operating system and application data of the image is copied to the system disk.|
    |**Networking**|**VPC**|\[Default\]vpc-bp1opxu1zkhn00g\*\*\*\*\*\*|Resources that are prefixed with **\[Default\]** are automatically created in the ECS console.|
    |**Public IP Address**|Select this option|The system allocates a public IPv4 address if you select Assign Public IP Address.|
    |**Bandwidth Billing**|Pay-By-Traffic|In **Pay-by-traffic** mode, bandwidth is billed based on the network usage. For more information, see [Public bandwidth](/intl.en-US/Pricing/Billing items/Public bandwidth.md).|
    |**Peak Bandwidth**|2 Mbps|None|
    |**Security Group**|    -   Security Group ID: \[Default\]sg-bp1bhjjsoiyx44\*\*\*\*\*\*
    -   Rule: Select ICMP, SSH 22, RDP 3389, HTTP 80, and HTTPS 443.
|Resources that are prefixed with **\[Default\]** are automatically created in the ECS console.|
    |**System Configurations \(Optional\)**|**Logon Credentials**|Password|Record the password. It is the password for the administrator and is required when you connect to the ECS instance. For more information, see the [Connect to the ECS instance](#Connect) section.|
    |**Instance Name**|    ```
EcsQuickStart
    ```

|In this topic, EcsQuickStart is used as the instance name.|
    |**Grouping \(Optional\)**|**Tags**|ECS:Documentation|If multiple instances are created, we recommend that you add tags to help facilitate management.|

3.  Click **Next: Preview**. On the Preview step, confirm **Configurations Selected** or click the ![Edit - Icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1953230061/p77356.png) icon to modify configurations.

    ![Quick start - Windows](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3957219951/p77397.png)

4.  Click **Save as Launch Template**. In the Save as Launch Template dialog box, set Template Name and Version Description.

    **Note:** Save the configurations selected for the current instance as a launch template. You can create an instance in one click next time by using the template.

5.  Read and select **ECS Terms of Service**. Click **Create Instance**.

6.  In the **Created** message, click **Console** to view the creation progress on the Instances page.

    If the instance is in the **Running** state, it is created. Copy the public IP address of the instance to use when you connect to the ECS instance.


## Step 2: Add security group rules

If you do not add rules to the default security group when you create an instance or the instance is added to a new security group, perform the following steps:

1.  Click the instance ID to go to the instance details page.

2.  On the Instance Details page, click the **Security Groups** tab, click the ID of a security group, and then go to the details page.

3.  On the **Security Groups Rules** page, click the **Inbound** tab.

4.  Click **Quick Rule Creation** and add security group rules as described in the following table. Keep the default settings for parameters that are not described in this tutorial.

    |Action|Common Port \(TCP\)|Authorized object|
    |------|-------------------|-----------------|
    |Allow|    -   SSH \(22\)
    -   RDP \(3389\)
    -   HTTP \(80\)
    -   HTTPS \(443\)
|0.0.0.0/0|

    **Note:**

    -   For the **Common Port \(TCP\)** section, select the port that must be enabled for the applications that run on the ECS instance. For example, select HTTP 80 when you perform the operations in the [Step 4: Configure IIS](#IISConfig) section.
    -   0.0.0.0/0 indicates that devices in all CIDR blocks are allowed to access the specified ports. If you know the IP address of the requester, we recommend that you set Authorization Object to a specific IP address range that contains this IP address.
5.  Click **OK**.


## Step 3: Connect to the ECS instance

1.  Go back to the Instances page and find the EcsQuickStart instance.

2.  In the **Actions** column, click **Connect**.

3.  In the **Enter VNC Password** dialog box, click **Modify VNC Password**.

4.  Modify the password. In the **Enter VNC Password** dialog box, enter your new password and click **OK**.

5.  In the upper-left corner of the VNC page, choose **Send Remote Call** \> **Ctrl+Alt+Delete**.

    ![CTRL+ALT+DELETE](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4957219951/p65866.png)

6.  Go to the logon page of the Windows instance and configure the logon credentials.


## Step 4: Configure IIS

1.  Launch Command Prompt.

2.  Enter powershell to switch to PowerShell.

3.  Install IIS and the management tools.

    ```
    Install-WindowsFeature -name Web-Server -IncludeAllSubFeature -IncludeManagementTools
    ```

4.  After IIS is installed, open a web page in the current browser. Enter the public IP address of the instance in the address bar. Press Enter.

    ```
    http://<Public IP address of the instance>
    ```

    ![Quick start - Windows - Test page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4957219951/p77430.png)


## Step 5: \(Optional\) Resolve domain names

Direct access to IIS by using the public IP address of the instance may degrade server security. If you have an existing domain name or want to register one, perform the following steps:

1.  Register the domain name.

    For more information, see [Register a generic domain name](/intl.en-US/Quick Start/Register a generic domain name.md).

2.  If the website to which the domain name points is hosted on an ECS instance in a mainland China region, you must apply for an ICP filing for the domain name.

3.  Resolve the domain name to point to the public IP address of the instance.

    Domain name resolution is a prerequisite for using domain names to access your website. For more information about the procedures, see[Add and manage records](https://www.alibabacloud.com/help/doc-detail/58131.htm).

4.  Use the resolved domain name to access IIS. Example: https://ecs-quickstarts.info.


## Step 6: \(Optional\) Release the ECS instance

You can release the instance if you no longer need it. After the instance is released, billing stops and data cannot be recovered.

**Note:** You can release only pay-as-you-go instances by following the instructions in this section.

1.  Go back to the Instances page and find the EcsQuickStart instance.

2.  In the **Actions** column, choose **More** \> **Instance Status** \> **Release**.

3.  In the Release dialog box, set Release Mode to **Release Now** and click **Next**.

4.  Verify the instance to be released and then click **OK**.


## Step 7: View bills

1.  In the top navigation bar, choose **Expenses** \> **User Center**.

2.  In the left-side navigation pane, choose **Spending Summary** \> **Instance Spending Detail**.

3.  Set **Search By** to **Instance ID**. Enter the ID of the EcsQuickStart instance. Press the Enter key to start the search.


-   For more information about ECS instance families that are available for purchase, see [Instance families](/intl.en-US/Instance/Instance families.md).
-   For more information about how to create an ECS instance, see [Creation method overview](/intl.en-US/Instance/Create an instance/Creation method overview.md).
-   For more information about images, see [Image overview](/intl.en-US/Images/Image overview.md).
-   For more information about security groups, see [Overview](/intl.en-US/Security/Security groups/Overview.md).
-   For more information about VPCs, see [What is a VPC?](/intl.en-US/Product Introduction/What is a VPC?.md)
-   For more information about the common operations of ECS, see [Quick reference](/intl.en-US/Best Practices/Quick reference.md).
-   For more information about the APIs operations provided by ECS, see [List of operations by function](/intl.en-US/API Reference/List of operations by function.md).

