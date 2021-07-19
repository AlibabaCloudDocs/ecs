---
keyword: [ECS instances, ECS console, wizard]
---

# Create an instance by using the wizard

The Elastic Compute Service \(ECS\) console provides a wizard for creating instances. The wizard lists all configuration information used to create an instance and guides you to create an instance.

## Preparations

1.  Create an Alibaba Cloud account and complete the account information.

    -   [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/doc-detail/50482.htm).
    -   [Add a payment method](https://www.alibabacloud.com/help/doc-detail/50517.htm).
    -   Complete real-name verification before you purchase ECS instances in mainland China regions. For more information, see [Real-name registration FAQs](https://www.alibabacloud.com/help/doc-detail/52595.htm).
2.  Go to the [Custom Launch](https://ecs-buy.aliyun.com/wizard/#/) tab in the ECS console.


## Step 1: Complete the settings in the Basic Configurations step

The settings in the Basic Configurations step include the basic requirements for purchasing an instance, such as the billing method, region, and zone, and the basic resources required by the instance, such as the instance type, image, and storage. After you complete the settings in the Basic Configurations step, click **Next**.

1.  Select a billing method.

    Different billing and charging rules apply to the instance based on the selected billing method. The state changes of instance resources also vary based on the billing method.

    |Billing method|Description|References|
    |--------------|-----------|----------|
    |**Subscription**|A billing method in which you pay for resources before you use them.|[Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md)|
    |**Pay-As-You-Go**|A billing method in which you use resources first and pay for them afterward. The billing cycles of pay-as-you-go instances are accurate to the second. You can purchase and release instances on demand. **Note:** We recommend that you use the pay-as-you-go billing method together with savings plans andreserved instances to reduce costs.

|    -   [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md)
    -   [Savings plans](/intl.en-US/Pricing/Billing methods/Savings plans.md)
    -   [Reserved instances](/intl.en-US/Pricing/Billing methods/Reserved instances.md) |
    |**Preemptible Instance**|A billing method in which you use resources first and pay for them afterward. You place a bid for available instance resources to create preemptible instances at a discount compared with pay-as-you-go instance pricing. Preemptible instances may be automatically released due to fluctuations in market price or insufficient resources of instance types.|[Preemptible instances](/intl.en-US/Pricing/Billing methods/Preemptible instances.md)|

2.  Select a region and a zone.

    Select a region that is close to your geographical location to reduce latency. After an instance is created, the region and the zone of the instance cannot be changed. For more information, see [Regions and zones]().

3.  Select an instance type and complete the relevant configurations.

    1.  Select an instance type.

        The available instance types vary based on the selected region. You can go to the [ECS Instance Types Available for Each Region](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) page to view the instance types available in each region.

        If you have specific configuration requirements for the instance, for example, if you want the instance to have multiple bound elastic network interfaces \(ENIs\), use enhanced SSDs \(ESSDs\), or use local disks, make sure that the selected instance type meets the requirements. For more information about the features, applicable scenarios, and specifications of instance types, see [Instance families](/intl.en-US/Instance/Instance families.md).

        If you purchase instances for specific scenarios, click the **Scenario-based Selection** tab to view the recommended instance types. For example, you can set Business Scenarios to Web Development and Test, Big Data Cluster, or AI Machine Learning.

    2.  If you set **Billing Method** to **Preemptible Instance**, configure the Use Duration and Maximum Price for Instance Type parameters.

        The usage duration is the protection period of a preemptible instance. After the protection period ends, the instance may be released due to insufficient resources or lower bids than the market price. The following table describes the valid values of the Use Duration parameter.

        |Value|Description|
        |-----|-----------|
        |**One Hour**|After the preemptible instance is created, it enters a 1-hour protection period during which it cannot be automatically released.|
        |**None**|The preemptible instance is created without a protection period. Preemptible instances without a protection period are less expensive than preemptible instances with a protection period.|

        The following table describes the valid values of the Maximum Price for Instance Type parameter.

        |Value|Description|
        |-----|-----------|
        |**Use Automatic Bid**|Uses the real-time market price of the instance type. This price never exceeds the price of the corresponding pay-as-you-go instance. Automatic bidding can prevent the instance from being released due to lower bids than the market price, but cannot prevent the instance from being released due to insufficient resources.|
        |**Set Maximum Price**|Sets a maximum price. If the real-time market price exceeds the maximum price or if resources are insufficient, the preemptible instance is released.|

    3.  Specify the number of instances to create.

        You can create a maximum of 100 instances each time by using the wizard. In addition, the number of instances within your account cannot exceed the quota. The quota displayed on the buy page prevails. For more information, see [View and increase instance quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase instance quotas.md).

4.  Select an image.

    Images contain the information that is required to run instances. Alibaba Cloud provides a variety of image types for you to access image resources. The following table describes the image types.

    |Image type|Description|References|
    |----------|-----------|----------|
    |Public Image|Public images are base images provided by Alibaba Cloud. Public images are licensed and include Windows Server OS images and mainstream Linux OS images.|[Overview](/intl.en-US/Images/Public image/Overview.md)|
    |Custom Image|You can create or import custom images. Custom images contain the system environment, application environment, and related software configurations. This eliminates the need for repeated manual configurations.|[Overview](/intl.en-US/Images/Custom image/Overview.md)|
    |Shared Image|Shared images are custom images shared by other Alibaba Cloud accounts and allow you to use the same image to create instances across accounts.|[Share or unshare custom images](/intl.en-US/Images/Custom image/Share or unshare custom images.md)|
    |Marketplace Image|An extensive range of images are provided in Alibaba Cloud Marketplace. Alibaba Cloud Marketplace images are thoroughly reviewed by Alibaba Cloud and can be used to create instances for website building and application development purposes without additional configurations.|[Alibaba Cloud Marketplace images](/intl.en-US/Images/Alibaba Cloud Marketplace images.md)|

5.  Complete the storage and related settings.

    Instances obtain storage capabilities by attaching system disks, data disks, and Apsara File Storage NAS file systems. ECS provides disks and local disks to meet the requirements of different scenarios.

    Disks can be used as system disks or data disks and include ESSDs, standard SSDs, and ultra disks. For more information, see [Cloud disks](/intl.en-US/Block Storage/Block Storage overview/Cloud disks.md).

    **Note:** The billing method of a disk that is created along with an instance is the same as that of the instance.

    Local disks can be used only as data disks. If an instance family \(such as instance family with local SSDs and big data instance family\) is equipped with local disks, the information of the local disks is displayed. For more information, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

    **Note:** Local disks cannot be attached to instances on your own.

    1.  Select a system disk.

        System disks are used to install operating systems. The default capacity of a system disk is 40 GiB. However, the actual minimum capacity is related to the image. The following table describes the capacities of system disks for different images.

        |Image|System disk capacity \(GiB\)|
        |:----|:---------------------------|
        |Linux \(excluding CoreOS and Red Hat\)|\[max\{20, image size\}, 500\]|
        |FreeBSD|\[max \{30, image size\}, 500\]|
        |CoreOS|\[max \{30, image size\}, 500\]|
        |Red Hat|\[max \{40, image size\}, 500\]|
        |Windows|\[max \{40, image size\}, 500\]|

    2.  Select a data disk.

        You can create an empty disk or create a disk from a snapshot. A snapshot is a point-in-time backup of a disk. You can import data in a quick manner by creating a disk from a snapshot. When you choose a data disk, you can encrypt the disk to meet the requirements of scenarios such as data security and regulatory compliance. For more information about data encryption, see [Encryption overview](/intl.en-US/Block Storage/Encrypt a disk/Encryption overview.md).

        **Note:** The number of data disks that can be attached to a single instance is limited. For more information, see the "Elastic Block Storage \(EBS\) limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).

    3.  Select a NAS file system.

        If you have a large amount of data for sharing by multiple instances, we recommend that you use a NAS file system to reduce costs in data transmission and synchronization.

        Select an existing NAS file system or click **Create a General Purpose NAS File System** in the NAS console. For more information about how to create a NAS file system, see [Create a General-purpose NAS file system in the NAS console](). After a NAS file system is created, go back to the ECS instance creation wizard and click the ![refresh](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0572966261/p278001.png) icon to query the most recent NAS file system list. For more information about how to mount NAS file systems, see [Mount NAS file systems when you purchase an ECS instance]().

6.  Configure the snapshot service.

    You can use automatic snapshot policies to periodically back up disks to prevent risks such as accidental data deletion.

    Select an existing snapshot policy or click **Create Automatic Snapshot Policy** to create an automatic snapshot policy on the Snapshots page. For more information about how to create an automatic snapshot policy, see [Create an automatic snapshot policy](/intl.en-US/Snapshots/Automatic snapshot policies/Create an automatic snapshot policy.md). After an automatic snapshot policy is created, go back to the ECS instance creation wizard and click the ![refresh](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0572966261/p278001.png) icon to query the most recent automatic snapshot policy list.


## Step 2: Complete the settings in the Networking step

You can make network and security group configurations to allow the instance to communicate with the Internet and other Alibaba Cloud resources and safeguard the instance in the network. After you complete the settings in the Networking step, click **Next**.

1.  Select a network type.

    We recommend that you select VPC. Virtual private clouds \(VPCs\) are physically isolated from each other to ensure security and support features such as elastic IP addresses \(EIPs\) and elastic network interfaces \(ENIs\).

    |Network type|Description|References|
    |------------|-----------|----------|
    |**VPC**|A VPC is an isolated network dedicated for your use. You have full control over your VPC. For example, you can specify a private CIDR block and configure route tables and gateways for the VPC. If you have not created a VPC in the region selected in the Basic Configurations step, you can skip this step. The system creates a default VPC and vSwitch in that region.

Select an existing VPC and an existing vSwitch. Alternatively, click **go to the VPC console** to go to the VPC console to create a VPC and a vSwitch. After the VPC and the vSwitch are created, go back to the ECS instance creation wizard and click the ![refresh](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0572966261/p278001.png) icon to query the most recent VPC and vSwitch lists.

|    -   [What is a VPC?](/intl.en-US/Product Introduction/What is a VPC?.md)
    -   [t2435.md\#section\_znz\_rbv\_vrx](/intl.en-US/VPCs and vSwitchs/Work with VPCs.md)
    -   [t2436.md\#section\_ts9\_t3s\_8vw](/intl.en-US/VPCs and vSwitchs/Work with vSwitches.md) |
    |**Classic**|Instances of the classic network type are deployed in the public infrastructure of Alibaba Cloud, and planned and managed by Alibaba Cloud. **Note:** If you purchase an instance for the first time after 12:00 on June 16, 2016 \(UTC+8\), you can no longer select the classic network.

|[Network types](/intl.en-US/Network/Network types.md)|

2.  Assign a public IP address to the instance.

    To enable the instance to access the Internet, you must assign a public IP address to the instance. You can select Assign Public IP Address when you create an instance to have an public IP address automatically assigned to the instance, or you can configure an EIP or a NAT gateway to enable the instance to access the Internet. You can purchase EIPs and NAT gateways on your own. For more information, see [What is Elastic IP Address?](/intl.en-US/.md) and [What is NAT Gateway?](/intl.en-US/Product Introduction/What is NAT Gateway?.md).

    1.  Select **Assign Public IPv4 Address**.

    2.  Select a billing method for network usage.

        For more information about the billing methods for network usage, see [Public bandwidth](/intl.en-US/Pricing/Billing items/Public bandwidth.md).

        |Billing method for network usage|Description|
        |--------------------------------|-----------|
        |**Pay-By-Bandwidth**|You are charged based on the specified bandwidth. This billing method for network usage is applicable to scenarios that require stable network bandwidth.|
        |**Pay-By-Traffic**|You are charged for the amount of traffic that is actually consumed. You can configure maximum bandwidths for inbound and outbound traffic to avoid unmanageable fees incurred by traffic bursts. This billing method for network usage is applicable to scenarios that require highly variable network bandwidths, such as a scenario where traffic is low most of the time but spikes in traffic intermittently occur.|

    3.  Set Bandwidth or Peak Bandwidth.

3.  Select a security group.

    A security group is a virtual firewall that is used to control the inbound and outbound traffic of instances in the security group. For more information, see [Overview](/intl.en-US/Security/Security groups/Overview.md).

    If you do not configure parameters in a security group when you create an instance, you can skip the step. The system creates a default security group. The default security group allows inbound traffic over Secure Shell Protocol \(SSH\) port 22, Remote Desktop Protocol \(RDP\) port 3389, and Internet Control Message Protocol \(ICMP\). You can modify the security group configurations after the group is created.

    1.  To create a security group, click **Create Security Group**.

        For more information about how to configure the security group, see[Create a security group](/intl.en-US/Security/Security groups/Create a security group.md).

    2.  Click **Reselect Security Group**.

    3.  In the **Select Security Group** dialog box, select one or more security groups and click **Select**.

4.  Configure an ENI.

    ENIs include primary ENIs and secondary ENIs. Primary ENIs cannot be unbound from instances. They can be created and released only along with instances. Secondary ENIs can be bound to or be unbound from instances to allow traffic to be switched between instances. To create a secondary ENI when you create an instance, click the ![add-nic](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0572966261/p278943.png) icon and select a vSwitch to which the secondary ENI belongs.

    **Note:** You can bind only one secondary ENI when you create an instance. You can also create the secondary ENIs and bind them to an instance after the instance is created. For more information about the number of ENIs that can be bound to instances of different instance types, see [Instance families](/intl.en-US/Instance/Instance families.md).


## Step 3: \(Optional\) Complete the settings in the System Configurations \(Optional\) step

The system configurations include the logon credentials, instance name, and user data, which are used to customize the information or usage of the instance in the ECS console and operating system. Complete the settings in the System Configurations \(Optional\) step and click **Next**.

1.  Configure logon credentials.

    Logon credentials are used to log on to instances. For more information about how to connect to instances, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

    |Logon credential|Description|
    |----------------|-----------|
    |**Key Pair**|Select an existing key pair or click **Create Key Pair** to create a key pair. After a key pair is created, go back to the ECS instance creation wizard and click the ![refresh](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0572966261/p278001.png) icon to query the most recent key pair list. For more information, see [Create an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Create an SSH key pair.md). **Note:** Key pairs can be used to log on only to Linux instances. |
    |**Password**|Enter and confirm the password. When you log on to an instance by using a username and password, the default username for Linux is `root` and that for Windows is `administrator`.|
    |**Set Later**|After the instance is created, bind the key pair or reset the instance password. For more information, see [Bind an SSH key pair to an instance](/intl.en-US/Security/Key pairs/Use an SSH key pair/Bind an SSH key pair to an instance.md) and [Reset the logon password of an instance](/intl.en-US/Instance/Manage instance attributes/Reset the logon password of an instance.md).|

2.  Specify the instance name that you want to display in the ECS console and the hostname that can be obtained from within the operating system.

    If you want to create multiple instances, you can set sequential instance names and hostnames to facilitate management. For more information about how to configure sequential instance names and hostnames, see [Batch configure sequential names or hostnames for multiple instances](/intl.en-US/Best Practices/Batch configure sequential names or hostnames for multiple instances.md).

3.  Configure advanced options.

    1.  Select an instance Resource Access Management \(RAM\) role.

        Instance RAM roles enable ECS instances to assume roles with specific access permissions. The instance can access the APIs of specific Alibaba Cloud services and manage specific Alibaba Cloud resources based on a Security Token Service \(STS\) temporary credential. This ensures security.

        Select an existing instance RAM role or click **Create Instance RAM Role** to create an instance RAM role. After an instance RAM role is created, go back to the ECS instance creation wizard and click the ![refresh](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0572966261/p278001.png) icon to query the most recent instance RAM role list. For more information, see [Bind an instance RAM role](/intl.en-US/Security/Instance RAM roles/Bind an instance RAM role.md).

    2.  Select an access mode of instance metadata.

        ECS instance metadata contains the information of instances in Alibaba Cloud. You can view the metadata of running instances and configure or manage the instances based on their metadata. You can access instance metadata in normal or security-hardening mode. For more information, see [View instance metadata](/intl.en-US/Instance/Manage instance configurations/Manage instance metadata/View instance metadata.md).

    3.  Configure user data.

        User data can be run as scripts on instance startup to automate instance configurations, or can be used as common data and passed into instances for use. For more information, see [Manage the user data of Linux instances](/intl.en-US/Instance/Manage instance configurations/Manage instance user data/Manage the user data of Linux instances.md) and [Manage the user data of Windows instances](/intl.en-US/Instance/Manage instance configurations/Manage instance user data/Manage the user data of Windows instances.md).

        Enter the user data that you prepared in the User Data field. If the user data is encoded in Base64, select **Enter Base64 Encoded Information**.


## Step 4: \(Optional\) Complete the settings in the Grouping \(Optional\) step

Grouping configurations provides ways such as tags and resource groups to batch manage instances. Complete the settings in the Grouping \(Optional\) step and click **Next**.

1.  Add tags.

    Each tag consists of a tag key and a tag value. You can add tags to resources that have identical characteristics, such as resources that belong to the same organization and resources that serve the same purpose. You can use tags to search for and manage resources in an efficient manner. For more information, see [Overview](/intl.en-US/Tag & Resource/Tags/Overview.md).

    Select an existing tag, or enter a key and a value to create a tag.

2.  Select a resource group.

    Resource groups allow you to manage cross-region and cross-service resources based on your business requirements and manage the permissions of resource groups. For more information, see [Resource groups](/intl.en-US/Tag & Resource/Resource/Resource groups.md).

    Select an existing resource group, or click **click here** to create a resource group on the Resource Group page. After a resource group is created, go back to the ECS instance creation wizard and click the ![refresh](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0572966261/p278001.png) icon to query the most recent resource group list. For more information, see [Create a resource group]().

3.  Select a deployment set.

    Deployment sets support the high-availability policy. After you apply a high-availability policy to a deployment set, all the instances within the deployment set are distributed across different physical servers to ensure business availability and disaster recovery at the underlying layer.

    Select an existing deployment set or click **manage the deployment set** to create a deployment set. After the deployment set is created, go back to the ECS instance creation wizard and click the ![refresh](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0572966261/p278001.png) icon to query the most recent deployment set list. For more information, see [Create a deployment set](/intl.en-US/Elasticity/Deployment sets/Create a deployment set.md).

4.  Select a dedicated host.

    A dedicated host is a cloud host whose physical resources are exclusively reserved for a single tenant. Dedicated hosts meet strict regulatory compliance requirements and support bring your own license \(BYOL\) when you migrate services to Alibaba Cloud.

    Select an existing dedicated host or click **create a DDH** to create a dedicated host. After the dedicated host is created, go back to ECS instance creation wizard and click the ![refresh](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0572966261/p278001.png) icon to query the most recent dedicated host list. For more information, see [Create a dedicated host](/intl.en-US/Quick Start/Create a dedicated host.md).

5.  Select a private pool.

    After an elasticity assurance or a capacity reservation is created, the system generates a private pool to reserve resources for a specific number of instances that have specific attributes. During the validity period of the elasticity assurance or the capacity reservation, you always have access to the resources reserved in the private pool when you want to create instances. For more information, see [Overview of Resource Assurance](/intl.en-US/Instance/Instance purchasing options/Resource assurances/Overview of Resource Assurance.md).

    **Note:** Only pay-as-you-go instances can be created from the resources reserved by elasticity assurances or capacity reservations.

    |Private pool|Description|
    |------------|-----------|
    |**Open**|The capacity in open private pools has a priority over public pool resources. If no capacity is available in private pools, the system attempts to use public pool resources.|
    |**None**|The capacity in private pools is not used.|
    |**Targeted**|The capacity in a specified or open private pool is used to create instances. If no capacity is available in the specified private pool, the instances cannot be created.|


## Step 5: Confirm the order

Before an instance is created, make sure that the selected configurations such as the usage duration meet your requirements.

1.  Check the selected configurations.

    To modify a configuration, click ![edit](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1572966261/p279222.png) to go to the corresponding page. You can save the selected configurations as a template. Then, you can use the template to create instances that have similar configurations. The following table describes the buttons that can be used to save the configurations as a template.

    |Operation|Description|References|
    |---------|-----------|----------|
    |**Save as Launch Template**|Saves the configurations as a launch template. Then, you can create instances from this launch template without making these configurations again.|[Create an instance by using a launch template](/intl.en-US/Instance/Create an instance/Create an instance by using a launch template.md)|
    |**View Open API**|Generates the API best-practice workflow and SDK examples for your reference.|    -   [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md)
    -   [Batch create ECS instances](/intl.en-US/SDK Reference/Java example/Create an ECS instance/Batch create ECS instances.md)
    -   [Create multiple ECS instances at a time](/intl.en-US/SDK Reference/Python example/Create multiple ECS instances at a time.md) |
    |**Save as ROS Template**|Saves the configurations as a Resource Orchestration Service \(ROS\) template. Then, you can create stacks from this template in the ROS console to deliver resources with a single click.|[Create a stack](/intl.en-US/Stack Management/Create a stack.md)|

2.  Configure the usage duration of the instance.

    -   Pay-as-you-go instances: Set an automatic release time for the instance. You can also manually release the instance or set an automatic release time for the instance after it is created. For more information, see [Release an instance](/intl.en-US/Instance/Manage instance status/Release an instance.md).
    -   Subscription instance: Set Duration and optionally select Auto-renewal. You can also manually renew the instance or enable auto-renewal for the instance after it is created. For more information, see [Renewal overview](/intl.en-US/Pricing/Renew instances/Renewal overview.md).
3.  Read *ECS Terms of Service* and *Product Terms of Service*. If you agree to them, select **ECS Terms of Service and Product Terms of Service**.

4.  View the total fees of the instance in the lower part of the page. Confirm the configurations of the instance and complete the payment.


After the instance is created, go to the Instances page to check the status of the instance. When the instance state changes to **Running**, it can be accessed.

-   You can format data disks by connecting to instances. You can connect to instances by using Workbench, Virtual Network Computing \(VNC\), and third-party client tools. For more information about how to connect to instances by using VNC, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md) and [Connect to a Windows instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Windows instance by using password authentication.md).
-   If you add data disks when you create instances, you must format and partition the data disks before you can use them. For more information, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md) and [Format a data disk for a Windows ECS instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Windows ECS instance.md).
-   You can build an FTP site on an ECS instance to upload local files to the instance. For more information about how to deploy the FTP service, see [Manually build an FTP site on a CentOS 8 instance](/intl.en-US/Tutorials/Build an application/Build an FTP site on an ECS instance/Manually build an FTP site on a CentOS 8 instance.md) and [Manually build an FTP site on a Windows instance](/intl.en-US/Tutorials/Build an application/Build an FTP site on an ECS instance/Manually build an FTP site on a Windows instance.md).
-   To ensure the security of your instance after you create the instance, we recommend that you perform security compliance inspection and security hardening configurations. For more information, see [Harden operating system security for Linux](https://www.alibabacloud.com/help/doc-detail/49809.htm) and [Harden operating system security for Windows](https://www.alibabacloud.com/help/doc-detail/49781.htm).

