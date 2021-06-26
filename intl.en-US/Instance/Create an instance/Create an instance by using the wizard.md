# Create an instance by using the wizard

This topic describes how to create an Elastic Compute Service \(ECS\) instance by using the wizard in the ECS console. To create an ECS instance, you must specify the instance type, image, storage, network, and security group. The wizard provides a variety of extended configuration features to meet your custom deployment and management requirements.

The following preparations are made:

1.  Create an account and complete the account information.
    -   Create an Alibaba Cloud account. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/doc-detail/50482.htm).
    -   Bind your credit card or PayPal account. For more information, see [Add a payment method](https://www.alibabacloud.com/help/doc-detail/50517.htm).
    -   To purchase ECS instances in mainland China regions, you must complete real-name verification. For more information, see [Real-name registration FAQ](https://www.alibabacloud.com/help/doc-detail/52595.htm).
2.  Alibaba Cloud provides a default virtual private cloud \(VPC\) in each region. If you do not want to use the default VPC, you can create a VPC and a vSwitch within the region in which to create the instance. For more information, see [Create an IPv4 VPC](/intl.en-US/Quick Start/Create an IPv4 VPC.md).
3.  Alibaba Cloud provides a default security group in each region. If you do not want to use the default security group, you can create a security group within the region in which to create the instance. For more information, see [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md).

If you need other extended features, you must complete the corresponding preparations:

-   To bind a Secure Shell \(SSH\) key pair when you create a Linux instance, you must create the SSH key pair in the corresponding region. For more information, see [Create an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Create an SSH key pair.md).
-   To add user data for the instance, you must first prepare user data. For more information about how to prepare user data, see [Overview of ECS instance user data](/intl.en-US/Instance/Manage instances/Manage instance user data/Overview of ECS instance user data.md).
-   To associate an ECS instance with an instance Resource Access Management \(RAM\) role, you must create the RAM role, attach permissions policies to the role, and then assign the role to the instance. For more information, see [Bind an instance RAM role](/intl.en-US/Security/Instance RAM roles/Bind an instance RAM role.md).

1.  Go to the [Custom Launch](https://ecs-buy.aliyun.com/wizard/#/) tab in the ECS console.

2.  Perform the following operations in the Basic Configurations step:

    1.  Set **Billing Method** to **Subscription**, **Pay-As-You-Go**, or [Preemptible Instance](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Overview.md).

        **Note:** For information about how to create a preemptible instance, see [Create a preemptible instance](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Create a preemptible instance.md).

    2.  Select a region and zone.

        By default, a zone is randomly assigned by the system. You can select a zone. For more information about regions and zones,see [Regions and zones](https://www.alibabacloud.com/help/doc-detail/40654.htm).

        **Note:** The region and zone cannot be changed after you create the instance.

    3.  Select an instance type and specify the number of instances.

        The instance types that are available are determined by the selected region. You can go to the [ECS Instance Types Available for Each Region](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) page to view the instance types available in each region. For information about the application scenarios for each instance type, see [Instance families](/intl.en-US/Instance/Instance family.md).

        **Note:**

        -   The quota value of pay-as-you-go or preemptible instances for your account is displayed on the page.
        -   To use elastic network interfaces \(ENIs\), select an enterprise-level instance type that has two or more vCPUs or an entry-level instance type that has four or more vCPUs. For more information about the maximum number of ENIs that can be bound to an instance of each instance type, see [Instance families](/intl.en-US/Instance/Instance family.md).
        -   To use a standard SSD, select an I/O optimized instance type.
    4.  Select an image. You can select a public image, a custom image, a shared image, or an Alibaba Cloud Marketplace image.

        **Note:**

        -   To use an SSH key pair, you must select a Linux image.
        -   To configure user data, you can select only specific images. For more information, see [Overview of ECS instance user data](/intl.en-US/Instance/Manage instances/Manage instance user data/Overview of ECS instance user data.md).
        -   To use a Red Hat public image, make sure that the instance family supports Red Hat images. For more information, see the "Which instance families do Red Hat Enterprise Linux \(RHEL\) images support?" section in [Image FAQ](/intl.en-US/Images/Image FAQ.md).
        -   Public images contain only initial system environments. You can find more images in Alibaba Cloud Marketplace.
    5.  Configure the storage.

        -   **System Disk**: required. You must create a system disk where to install the operating system. Select a disk category and specify the system disk size.
            -   Disk category: Categories are available based on the selected region and instance type.
            -   Size: The default size of the system disk is 40 GiB. If the selected image is greater than 40 GiB in size, the default size of the system disk is equal to the image size. The minimum size of the system disk is related to the image. The actual size is displayed on the buy page.

                |Image|System disk capacity \(GiB\)|
                |:----|:---------------------------|
                |Linux \(excluding CoreOS and Red Hat\)|\[max\{20, image size\}, 500\]|
                |FreeBSD|\[max \{30, image size\}, 500\]|
                |CoreOS|\[max \{30, image size\}, 500\]|
                |Red Hat|\[max \{40, image size\}, 500\]|
                |Windows|\[max \{40, image size\}, 500\]|

        -   **Data Disk**: optional. To create data disks concurrently with an instance, select disk categories and specify the sizes and quantity of the disks. You must also determine whether to encrypt the disks. For more information, see [Encryption overview](/intl.en-US/Block Storage/Encrypt a disk/Encryption overview.md). You can create an empty data disk or create a data disk from a snapshot.

            **Note:** Data disks created together with an instance have the following features:

            -   The billing method of the data disks is the same as that of the instance.
            -   Subscription data disks can be released only together with the instance. Pay-as-you-go data disks can be released separately or together with the instance.
            -   For the maximum number of data disks that can be attached to a single instance, see the "Elastic Block Storage \(EBS\) limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).
        -   **NAS File System**: optional. You can select existing file systems. Up to five file systems can be selected. For more information, see [Mount NAS file systems when you purchase an ECS instance]().
        -   If you have selected an instance family equipped with local disks \(such as i1, d1, or d1ne\), the local disk information is displayed. You cannot specify the quantity or category of the local disks because these settings are determined by the selected instance type. For more information about the local disks that are supported by different instance types, see [Instance families](/intl.en-US/Instance/Instance family.md).
    6.  Configure the snapshot service. Select an automatic snapshot policy and specify the data source to back up. The valid values of the Data Source parameter are All Disks, Only System Disks, and Only Data Disks.

        **Note:** You can use automatic snapshot policies to periodically back up disks to prevent data loss risks arising from various situations such as virus attacks and accidental data deletion. The data source specified for the selected automatic snapshot policy includes only the disks created in the previous step. If you subsequently create new data disks, you must separately apply automatic snapshot policies to the disks.

3.  Click **Next: Networking** and configure the network settings and security groups for the instance.

    1.  Select the network type.

        -   **VPC**: You must select a VPC and a vSwitch. If you have not created a VPC or a vSwitch, you can use the default ones.

            **Note:** Some instance families do not support advanced VPC features. For a list of these instance families, see [Instance families that do not support advanced VPC features](/intl.en-US/Instance/Instance type families/Instance families that do not support advanced VPC features.md). If you select an instance type from an instance family that does not support advanced VPC features and advanced features are enabled for a VPC, the VPC is dimmed and cannot be selected. You can move the pointer over the dimmed VPC to view the prompt and reselect a different instance type that supports the advanced VPC features based on the prompt.

        -   **Classic**: If you purchase an ECS instance for the first time after 12:00 on June 16, 2016 \(UTC+8\), you can no longer select the classic network.
    2.  Configure the public bandwidth.

        -   To assign a public IP address to the instance, you must select **Assign Public IPv4 Address**. Then, select **Pay-By-Traffic** or **Pay-By-Bandwidth** as the billing method for network usage and specify the bandwidth value. The public IP addresses assigned in this manner cannot be disassociated from the instance. For more information about the billing methods for network usage, see [Public bandwidth](/intl.en-US/Pricing/Billing items/Public bandwidth.md).
        -   If your instance does not need to access the Internet or if your instance is located in a VPC and uses an elastic IP address \(EIP\) to access the Internet, you do not need to assign a public IP address. You can associate an EIP with or disassociate an EIP from an instance at any time.
    3.  Select a security group.

        If you have not created a security group, you can use the default security group. For more information about rules of the default security group, see [Overview](/intl.en-US/Security/Security groups/Overview.md).

    4.  Add an ENI.

        If the instance type that you selected supports ENIs, you can add an ENI and specify a vSwitch for the ENI.

        **Note:** By default, the added ENI is released together with the instance. You can unbind the ENI from the instance by using the [ECS console](/intl.en-US/Network/Elastic Network Interfaces/Unbind an ENI.md) or by calling the [DetachNetworkInterface](/intl.en-US/API Reference/Elastic network interfaces/DetachNetworkInterface.md) operation.

4.  Click **Next: System Configurations** and complete the following configurations:

    1.  Select and configure logon credentials.

        Select a credential based on the image:

        -   Linux: A password or an SSH key pair can be used as the logon credential.
        -   Windows: Only a password can be used as the logon credential.
        Alternatively, you can set a logon credential after the instance is created. For more information, see [Reset the logon password of an instance](/intl.en-US/Instance/Manage instances/Reset the logon password of an instance.md).

    2.  Specify the instance name that you want to display in the ECS console and the hostname that can be obtained from within the guest operating system.

        If you want to create multiple instances, you can set sequential names for the instances to better manage the instances. For more information, see [Batch configure sequential names or hostnames for multiple instances](/intl.en-US/Best Practices/Batch configure sequential names or hostnames for multiple instances.md).

    3.  Configure advanced options.

        -   RAM Role: Assign a RAM role to the instance.
        -   User Data: Customize the startup behavior of the instance or pass data into the instance.
5.  Click **Next: Grouping** and group the instance.

    1.  Add tags.

        If you have multiple instances, you can use tags to make the instances easy to manage. For more information, see [Overview](/intl.en-US/Tag & Resource/Tags/Overview.md).

    2.  Select a resource group.

        Resource groups are provided for enterprise users. Enterprise users can use the resource group feature to organize and manage resources owned by multiple accounts and assigned to multiple projects. For more information, see [Resource groups](/intl.en-US/Tag & Resource/Resource/Resource groups.md).

    3.  Select a deployment set.

        Deployment sets are used to manage how instances are deployed. Instances in the same deployment set can be assigned to different physical servers to ensure high availability of services and disaster recovery of the infrastructure. For more information, see [Create a deployment set](/intl.en-US/Elasticity/Deployment sets/Create a deployment set.md).

    4.  Select a dedicated host.

        You can select **Random DDH Supporting Automatic Deployment / AutoPlacement** or specify a dedicated host.

        Dedicated hosts are flexible and elastic. They provide you with exclusive access to their resources. For more information, see [Features](/intl.en-US/Product Introduction/Features/Features.md).

6.  Confirm the order.

    1.  In the **Configurations Selected** section, confirm all the configurations. You can also click the Edit icon to change the configurations.

        -   \(Optional\) Click **Save as Launch Template** to save your configurations as a launch template for later use. For more information, see [Launch templates](/intl.en-US/Elasticity/Launch template/Launch templates.md).
        -   \(Optional\) Click **View Open API** to view best-practice API scripts. On the left side of the dialog box, the **API Workflow** section describes the API operations related to the current operation and lists the request parameters and their values. Programming language-specific SDK examples are provided on the right side of the dialog box. Examples in **Java** and **Python** are available. For more information, see [Introduction](/intl.en-US/API Reference/Introduction.md).
        -   \(Optional\) Click **Save as ROS Template** to save your configurations as a Resource Orchestration Service \(ROS\) template that can be used to create stacks. For more information, see [Create a stack](/intl.en-US/Stack Management/Create a stack.md).
    2.  If the billing method is **Pay-As-You-Go**, you can select **Automatic Release**.

    3.  If the billing method is **Subscription**, you can specify the subscription period and optionally select **Enable Auto-renewal**.

    4.  Confirm the fees.

        The following table describes the billing methods for instances and network usage that are used to calculate the fees you must pay.

        |Instance billing method|Billing method for network usage|Fee|
        |:----------------------|:-------------------------------|:--|
        |Pay-as-you-go or preemptible instance|Pay-by-traffic|Internet traffic fee and configuration fee. The total configuration fee consists of the sum of fees for the instance type \(vCPUs and memory\), the system disk, data disks \(if any\), and local disks \(if any\).|
        |Pay-by-bandwidth|The total configuration fee consists of the sum of fees for the instance type \(vCPUs and memory\), the system disk, data disks \(if any\), local disks \(if any\), and the public bandwidth.|
        |Subscription|Pay-by-bandwidth|The total configuration fee consists of the sum of fees for the instance type \(vCPUs and memory\), the system disk, data disks \(if any\), local disks \(if any\), and the public bandwidth.|
        |Pay-by-traffic|Internet traffic fee and configuration fee. The configuration fee consists of fees for the instance type \(vCPUs and memory\), the system disk, data disks \(if any\), and local disks \(if any\).|

    5.  Read and select **ECS Terms of Service**.

7.  Confirm to create the instance.

    -   Subscription instance: Click **Create Order**.
    -   Pay-as-you-go instance: Click **Create Instance**.

After the instance is created, click **Console** to view the instance details in the ECS console. On the **Instances** page, you can view the information of the new instance, such as the instance name, public IP address, internal IP address, and private IP address.

-   You can build an FTP site on the ECS instance to upload files to the instance. For more information, see [Manually build an FTP site on a Windows instance](/intl.en-US/Tutorials/Build an application/Build an FTP site on an ECS instance/Manually build an FTP site on a Windows instance.md).
-   To ensure the security of your created instance, we recommend that you perform a security compliance inspection and security hardening configurations:
    -   For Linux instances, see [Harden operating system security for Linux](https://www.alibabacloud.com/help/doc-detail/49809.htm) in *Security Advisories*.
    -   For Windows instances, see [Harden operating system security for Windows](https://www.alibabacloud.com/help/doc-detail/49781.htm) in *Security Advisories*.
-   If you added data disks when you created the instance, you must format and partition the data disks before they can be used. For more information, see [Format a data disk for a Windows ECS instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Windows ECS instance.md) or [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md).

