---
keyword: [quick start, ECS, starter, user guide, Alibaba Cloud, Alibaba Cloud Linux]
---

# Quick start for Linux instances

This topic describes how to create and manage a Linux instance in the Elastic Compute Service \(ECS\) console. In this topic, Apache is configured for an ecs.g6.large instance that runs the Alibaba Cloud Linux 2.1903 LTS 64-bit operating system.

## Preparations

1.  Create an account and complete the account information.

    -   Create an Alibaba Cloud account. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/doc-detail/50482.htm).
    -   Add your credit card or PayPal account. For more information, see [Add a payment method](https://www.alibabacloud.com/help/doc-detail/50517.htm).
    -   To purchase ECS instances in mainland China regions, complete real-name verification. For more information, see [Real-name verification FAQ](https://www.alibabacloud.com/help/doc-detail/52595.htm).
2.  Create a virtual private cloud \(VPC\). Alibaba Cloud provides a default VPC. If you do not want to use the default VPC, you can create a VPC and a vSwitch in the region where you want to create an ECS instance.

    For more information, see [Create an IPv4 VPC](/intl.en-US/Quick Start/Create an IPv4 VPC.md).

3.  Create a security group. Alibaba Cloud provides a default security group. If you do not want to use the default security group, you can create a security group in the region where you want to create an ECS instance.

    For more information, see [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md).


## Step 1: Create an ECS instance

1.  Go to the [Custom Launch](https://ecs-buy.aliyun.com/wizard/#/) tab in the ECS console.

2.  In the first four steps of the instance creation wizard on the Custom Launch tab, configure parameters for the instance.

    The following table describes the parameters used in this topic. For parameters that are not described in this topic, use the default values.

    |Step|Parameter|Example|Description|
    |----|---------|-------|-----------|
    |**Basic Configurations**|**Billing Method**|Pay-As-You-Go|The pay-as-you-go billing method allows more flexible operations. For more information, see [Billing overview](/intl.en-US/Pricing/Billing overview.md). **Note:** If an Internet content provider \(ICP\) filing is required for your domain name, you must select **Subscription**. |
    |**Region**|    -   Region: China \(Hangzhou\)
    -   Zone: Random
|You cannot change the region or zone after the instance is created. Proceed with caution when you set this parameter.|
    |**Instance Type**|    -   Instance family: General Purpose Type g6
    -   Instance type: ecs.g6.large
|Instance types that are available are determined by the region that you select and the resource inventory in the region. You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region. |
    |**Image**|    -   Type: Public Image
    -   Version: Alibaba Cloud Linux 2.1903 LTS 64-bit
|After the instance is created, the operating system and application data of the image is copied to the system disk.|
    |**Networking**|**VPC**|\[Default\]vpc-bp1opxu1zkhn00g\*\*\*\*|Select an existing VPC. Resources that are automatically created in the ECS console have the prefix **\[Default\]**.|
    |**Public IP Address**|Assign Public IPv4 Address|The system assigns a public IPv4 address if you select Assign Public IP Address.|
    |**Bandwidth Billing**|Pay-By-Traffic|In **Pay-by-traffic** mode, you are charged based on the network usage. For more information, see [Public bandwidth](/intl.en-US/Pricing/Billing items/Public bandwidth.md).|
    |**Peak Bandwidth**|2 Mbps|N/A|
    |**Security Group**|\[Default\]sg-bp1bhjjsoiyx44hd\*\*\*\*|Select an existing security group. Resources that are automatically created in the ECS console have the prefix **\[Default\]**.|
    |**System Configurations \(Optional\)**|**Logon Credentials**|Password|**Password** is selected in this topic. You must set a password for remote connection and logon to the ECS instance.|
    |**Logon Password**|Ecs123456|If you set **Logon Credentials** to **Password**, you must set the Logon Password and Confirm Password parameters. You must use the `root` username and corresponding password that you set when you connect to the ECS instance.|
    |**Instance Name**|EcsQuickStart|In this topic, EcsQuickStart is used as the instance name.|
    |**Grouping \(Optional\)**|**Tags**|ECS:Documentation|If multiple instances are created, we recommend that you add tags to facilitate management.|

3.  Click **Next: Preview**. In the Preview step, confirm the configurations in the **Configurations Selected** section or click the ![Edit icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1953230061/p77356.png) icon to modify configurations.

4.  Click **Save as Launch Template**. In the Save as Launch Template dialog box, set Template Name and Version Description.

    **Note:** Save the instance configurations that you made as a launch template. You can create an instance by using the template without the need to configure the specified parameters again.

5.  Read and select **ECS Terms of Service**. Click **Create Instance**.

6.  In the **Created** message, click **Console** to view the creation progress on the Instances page.

    If the instance is in the **Running** state, it is created. Copy the public IP address of the instance to use when you connect to the ECS instance.


## Step 2: Add security group rules

If you did not add rules to the default security group or added the instance to a new security group when you create the instance, perform the following steps:

1.  Click the instance ID to go to the instance details page.

2.  On the Instance Details page, click the **Security Groups** tab. Click the ID of a security group to go to the security group details page.

3.  In the **Access Rule** section, click the **Inbound** tab.

4.  Click **Quick Add** to add security group rules as described in the following table. For parameters that are not described in this topic, use the default values.

    |Action|Port range|Authorized object|
    |------|----------|-----------------|
    |Allow|    -   SSH 22
    -   RDP 3389
    -   HTTP 80
    -   HTTPS 443
|0.0.0.0/0|

    **Note:**

    -   For **Port Range**, select the ports that need to be enabled for applications that run on the ECS instance. For example, if you want to use SSH and Apache, select SSH \(22\) and HTTP \(80\) used in [Step 4: Configure Apache](#ApacheConfig). Otherwise, the instance does not respond in subsequent operations.
    -   0.0.0.0/0 indicates that all CIDR blocks are allowed to access the specified ports. If you know the IP address of the requester, we recommend that you set Authorization Object to a specific IP address range that contains this IP address.
5.  Click **OK**.


## Step 3: Connect to the ECS instance

1.  Go back to the Instances page and find the EcsQuickStart instance.

2.  In the **Actions** column, click **Connect**.

3.  In the **Enter VNC Password** dialog box, click **Modify VNC Password**.

4.  Modify the password. In the **Modify VNC Password** dialog box, enter your new password and click **OK**.

5.  Configure the logon credentials.

    -   **test login**: Enter root.
    -   **Password**: Enter the **Logon Password** value that you set in the **Logon Credentials** section when you create the instance. `Ecs123456` is used in this example.
    When you are entering the password, the section next to Password: remains black and no messages appear.

    ![login](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7547276061/p127216.png)


## Step 4: Configure Apache

1.  Install Apache.

    ```
    yum install -y httpd
    ```

2.  Start Apache.

    ```
    systemctl start httpd
    ```

3.  Configure Apache to run on system startup.

    ```
    systemctl enable httpd
    ```

4.  Check whether Apache is running.

    ```
    systemctl status httpd
    ```

    If `active (running)` is returned, Apache is running.

5.  Open a web page in the current browser. Enter the public IP address of the instance in the address bar. Press the Enter key.

    ```
    http://<Public IP address of the instance>
    ```

    ![apache](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2086707061/p127217.png)


## Step 5: \(Optional\) Resolve domain names

Direct access to Apache by using the public IP address of the instance may compromise server security. If you already have a domain name or want to register one for the Apache website, perform the following steps:

1.  Register the domain name.

    For more information, see [Register a generic domain name](/intl.en-US/Quick Start/Register a generic domain name.md).

2.  If the website to which the domain name points is hosted on an ECS instance in a mainland China region, you must apply for an ICP filing for the domain name.

3.  Resolve the domain name to point to the public IP address of the instance.

    Domain name resolution is a prerequisite for using domain names to access your website. For more information about the procedures, see [Add and manage records](https://www.alibabacloud.com/help/doc-detail/58131.htm).

4.  Use the resolved domain name to access Apache. Example: https://ecs-quickstarts.info.


## Step 6: \(Optional\) Release the ECS instance

You can release the instance if you no longer need it. After the instance is released, billing stops and its data cannot be recovered.

**Note:** Only pay-as-you-go instances can be released by using the method desribed in this section.

1.  Go back to the Instances page and find the EcsQuickStart instance.

2.  In the **Actions** column, choose **More** \> **Instance Status** \> **Release**.

3.  In the Release dialog box, set Release Mode to **Release Now** and click **Next**.

4.  In the Release message, verify the instance to be released and click **OK**.


## Step 7: View bills

1.  In the top navigation bar, choose **Expenses** \> **User Center**.

2.  In the left-side navigation pane, choose **Spending Summary** \> **Spending Summary**. On the Bills page, click the **Details** tab.

3.  Set **Instance Name** to EcsQuickStart and press the Enter key to start a search.


-   For more information about ECS instance families that are available for purchase, see [Instance families](/intl.en-US/Instance/Instance families.md).
-   For more information about how to create an ECS instance, see [Creation method overview](/intl.en-US/Instance/Create an instance/Creation method overview.md).
-   For more information about images, see [Image overview](/intl.en-US/Images/Image overview.md).
-   For more information about security groups, see [Overview](/intl.en-US/Security/Security groups/Overview.md).
-   For more information about VPCs, see [What is a VPC?](/intl.en-US/Product Introduction/What is a VPC?.md)
-   For more information about the common operations of ECS, see [Quick reference](/intl.en-US/Best Practices/Quick reference.md).
-   For more information about the API operations provided by ECS, see [List of operations by function](/intl.en-US/API Reference/List of operations by function.md).

