---
keyword: [change the network type, migration after the guarantee period expires, classic network]
---

# Migrate an ECS instance from the classic network to a VPC

This topic describes how to migrate one or more Elastic Compute Service \(ECS\) instances from the classic network to a virtual private cloud \(VPC\). After an ECS instance is migrated from the classic network to a VPC, you can enable more features for the instance, such as associating elastic IP addresses \(EIPs\).

Before you migrate an ECS instance from the classic network to a VPC, make sure that the ECS instance meets the following requirements:

-   The ECS instance is not attached with local disks. For more information, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).
-   The public bandwidth is not 0 Mbit/s. Before you migrate an ECS instance, you must upgrade its public bandwidth. For more information, see [Modify public bandwidth](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.mdChangeBandwidth).
-   The ECS instance is not located in Hangzhou Zone C.

## Impacts

The following table describes the impacts of migrating an ECS instance from the classic network to a VPC.

|Impacted item|Description|
|-------------|-----------|
|Migration duration|It takes about 15 minutes.|
|Instance restart|The ECS instance is restarted when it is migrated. We recommend that you migrate your instance during off-peak hours.|
|Network type|The ECS instance is migrated from the classic network to a VPC. For information about VPCs, see [What is a VPC?](/intl.en-US/Product Introduction/What is a VPC?.md)|
|Software authorization code|After the ECS instance is migrated, the software authorization code may change.|
|IP address|-   The public IP address of the ECS instance remains unchanged.

**Note:** The public IP address of a VPC-type ECS instance is mapped in network address translation \(NAT\) mode. You can view only the private IP address of the ECS instance. If your application is dependent on the public IP address in the operating system, reconsider whether to migrate your ECS instance from the classic network to a VPC.

-   Internal IP address
    -   If you set **Retain Internal IP Address** to **Yes**, the internal IP address of the ECS instance remains unchanged.
    -   If you set **Retain Internal IP Address** to **No**, the internal IP address of the ECS instance is randomly assigned from the CIDR block of the vSwitch. After the ECS instance is migrated, you can modify its internal IP address. For more information, see [Modify a private IP address](/intl.en-US/Network/Change IPv4 addresses/Modify a private IP address.md). |
|Disk name|The underlying virtualization technology is also upgraded for some ECS instances that are migrated from the classic network to a VPC. Therefore, the names of the disks on your ECS instance may change. In Linux instances, disk names are identified as vd\* such as vda, vdb, and vdc. -   If the disk name is already identified as vda or vdb before the instance is migrated, the disk name remains unchanged.
-   If the disk name is identified as xvd\* such as xvda and xvdb before the instance is migrated, the disk name is changed to vd\* such as vda and vdb after the instance is migrated. Alibaba Cloud automatically updates the /etc/fstab file for Linux instances. However, you must check whether other applications are dependent on the disk names that are identified before the instances are migrated. |
|I/O performance|After the ECS instance is migrated, the I/O performance may be temporarily degraded because data must be appended to the underlying layer. The snapshot and disk features are also temporarily disabled. Typically, it takes about 4 hours to append 100 GiB of data.|
|Estimated fee|You are not charged for the migration. If the migrated instance is a subscription instance, the unit price of its instance type does not change until the new subscription period starts. Based on the same configuration, you are billed less for a VPC-type instance than for a classic network-type instance.|
|Others|-   The ID, username, and logon password of the instance remain unchanged.
-   Orders for renewal and configuration change that are not in effect or unpaid are canceled. You can perform the renewal and configuration change operation again.
-   If the ECS instance is added to the vServer group of an SLB instance, the instance is not automatically associated with the SLB instance after the instance is migrated. For more information about how to add an ECS instance to a vServer group, see [Modify a VServer group](/intl.en-US/Classic Load Balancer/User Guide/Backend servers/VServer groups/Modify a VServer group.md). |

## Preparations

1.  Create a snapshot for the disks on the ECS instance and back up data. For more information about how to bind a RAM role to an ECS instance, see [Create a snapshot for a disk](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).
2.  \(Optional\) If your ECS instance is associated with an ApsaraDB service, you must enable the hybrid access mode for the ApsaraDB service in advance. In hybrid access mode, both the classic network-type and VPC-type ECS instances can access ApsaraDB services. For more information, see [Overview of the hybrid access mode of ApsaraDB](/intl.en-US/Best practices/Classic network-to-VPC migration/Hybrid access to ApsaraDB/Overview of the hybrid access mode of ApsaraDB.md).
3.  \(Optional\) If your ECS instance is associated with ApsaraDB services such as ApsaraDB RDS that provide the whitelist feature, you must add the CIDR block of the vSwitch to the ApsaraDB whitelist in advance. For more information, see [Configure a whitelist]().
4.  \(Optional\) We recommend that you enable the application service to run on startup and monitor the availability of the application service.
5.  Disable or uninstall the server security software.

    **Note:** The migration updates the device driver of the ECS instance. You must disable or uninstall the server security software on the ECS instance.

6.  Reserve at least 500 MiB in the system disk.
7.  Make sure that the vSwitch of the destination VPC has sufficient private IP addresses. The number of the private IP addresses must be greater than that of instances to be migrated.

## Step 1: Create a migration plan

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **Migration Plan**.

3.  In the top navigation bar, select a region.

4.  Click **Create Migration Plan**.

5.  In the **Configure Migration Plan** step, configure parameters such as those related to the network and click **Next**.

    1.  Configure the destination zone and VPC.

        ![Configure the network](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9469627161/p203053.png)

        |Parameter|Description|
        |---------|-----------|
        |**Plan Name**|Enter a name for the migration plan.|
        |**Select a destination zone**|Select a destination zone from the drop-down list to migrate the ECS instance. The available zones are automatically planned by the system based on resources. If you want to specify a zone for your business, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

**Note:** You can configure only one zone for a single migration plan. If you want to configure multiple zones, you must create multiple migration plans. |
        |**Destination VPC**|Select a destination VPC from the drop-down list to migrate the ECS instance.         -   Select **\(Default\) Automatically create a VPC, CIDR block: 10.0.0.0/8**: This option is suitable for scenarios where you have not created a VPC that has the 10.0.0.0/8 CIDR block and want to retain the internal IP address of the ECS instance.

If you select this option, the system automatically creates a VPC that has the 10.0.0.0/8 CIDR block.

        -   Select a VPC that has the 10.0.0.0/8 CIDR block: This option is suitable for scenarios where you have created a VPC that has the 10.0.0.0/8 CIDR block and want to retain the internal IP address of the ECS instance.
        -   Select a VPC that has a CIDR block other than 10.0.0.0/8: This option is suitable for scenarios where you have planned a VPC and do not need to retain the internal IP address of the ECS instance. |

    2.  Configure the instance network properties.

        ![Network properties](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0569627161/p203058.png)

        |Parameter|Description|
        |---------|-----------|
        |**Destination Security Group**|Select security groups for the instance to be migrated. Valid values:         -   \(Default\) Clone Security Groups of Classic Network-type Instances: The system clones the security groups of the classic network-type instance. The security group rules of the migrated VPC-type instance are the same as those of the classic network-type instance.

If you set **Destination VPC** to **\(Default\) Automatically create a VPC, CIDR block: 10.0.0.0/8**, the original security groups are automatically cloned. You cannot modify the security groups.

**Note:** Security groups with group authorization rules cannot be cloned.

        -   Specify Security Groups: Select existing security groups from the drop-down list.

**Note:** Inappropriate security group settings can affect your network access. Make sure that your security group rules are correct. |
        |**Mac Address Retention Policy**|Select the MAC address that you want to retain. Valid values: **\(Default\) Private Mac Address** and **Public Mac Address**. In the classic network, if an instance has a public IP address, the instance has a public MAC address and a private MAC address. In a VPC, an instance has only a private MAC address. The public IP address of the instance is mapped in NAT mode.

        -   If your business system is associated with a MAC address, retain the associated MAC address. For example, if a MAC address is configured in your business system, some software is registered by using the associated MAC address.
        -   If your business system is not associated with a MAC address, you can select \(Default\) Private Mac Address or Public Mac Address. |

    3.  Configure the instance network connectivity.

        ![Instance network connectivity](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0569627161/p203061.png)

        |Parameter|Description|
        |---------|-----------|
        |**Retain Internal IP Address**|Specify whether to retain the original internal IP address of the ECS instance and create or select a vSwitch.         -   If you select **\(Default\) Yes**, the original internal IP address of the ECS instance is retained, and you must set the **vSwitch Creation Policy** parameter.

            -   If you set **vSwitch Creation Policy** to **Automatic**, the system automatically creates a vSwitch.
            -   If you set **vSwitch Creation Policy** to **Manual**, you must create a vSwitch in the destination zone based on the internal IP addresses of all the classic network-type instances in the migration plan.
**Note:** If you set **Destination VPC** to **\(Default\) Automatically create a VPC, CIDR block: 10.0.0.0/8**, the system automatically retains the internal IP address of the ECS instance and creates a vSwitch policy. You cannot modify the Retain Internal IP Address parameter.

        -   If you select **No**, the original internal IP address of the ECS instance is not retained. You must select a vSwitch from the drop-down list.

**Note:** If you have created a vSwitch but you cannot find it in the drop-down list, the migrated instance and the vSwitch are not in the same zone. You must create a vSwitch in the destination zone. For more information, see [Work with vSwitches](/intl.en-US/VPCs and vSwitchs/Work with vSwitches.md). |
        |**Ensure interconnections between the migrated instances and the classic network-type instances specified in the plan over the internal network**|Specify whether the ECS instance to be migrated to a VPC can communicate with other ECS instances in the classic network over the internal network. Valid values: **Yes** and **\(Default\) No**. If you select **Yes**, configure the following settings based on your migration plan:

        -   If you choose to retain the internal IP address, you must select all the classic network-type instances that require connectivity over the internal network in the **Select Instances** step. These selected instances include the ECS instances to be migrated to a VPC and the ECS instances that remain in the classic network. Classic network-type instances that are not included in the migration plan cannot communicate with the instances in VPCs. After the instances are configured, you cannot add or remove ECS instances.
        -   If you choose not to retain the internal IP address, you must configure ClassicLink of classic network-type instances and enable classic network-type instances to communicate with those in VPCs. For more information about how to bind a RAM role to an ECS instance, see [Connect a classic network to a VPC](/intl.en-US/Network/Connect a classic network to a VPC.md). |

6.  In the **Select Instances** step, select the ECS instance to be migrated and click **Next**.

    If you choose to retain the internal IP address and want the migrated ECS instance to communicate with classic network-type instances, you must select all the classic network-type instances that require connectivity over the internal network. These selected instances include the ECS instances to be migrated to a VPC and the ECS instances that remain in the classic network.

    **Note:** Classic network-type instances that are not included in the migration plan cannot communicate with the instances in VPCs. After the instances are configured, you cannot add or remove ECS instances.

    ![Select Instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0569627161/p203137.png)

    -   1. Instances to be migrated to a VPC
    -   2. Instances that remain in the classic network
7.  In the **Scheduled Migration** step, set a migration time for the instance and click **Verify**.

    The ECS instance is restarted when it is migrated. We recommend that you migrate your instance during off-peak hours. You can set the migration time for a single instance, multiple instances, or all instances.

    -   To set the migration time for a single instance, click **Schedule Migration Time** in the **Actions** column corresponding to the instance.
    -   To set the migration time for multiple instances, select multiple instances in the instance list and click **Batch Schedule Migration Time**.
    -   To set the migration time for all instances, click **Set Unified Migration Time**.
    **Note:** Set a later migration time for a classic network-type instance that requires connectivity. Before the migration time arrives, evaluate whether to migrate the ECS instance.

8.  In the **Verify** dialog box, view the migration considerations and verify whether your migration plan meets the requirements.

    -   If your migration plan meets the requirements, select the options about migration and click **Confirm and Create**.
    -   If your migration plan does not meet the requirements, the system prompts an error message. You can create a migration plan again based on the error message.

## Step 2: Migrate the ECS instance

After the migration plan is created, the system automatically migrates the ECS instance at the specified time.

![The migration is complete](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0569627161/p201632.png)

**Note:** Disks are migrated during some migration processes. If you want to perform a physical server upgrade on your ECS instance or migrate your ECS instance across zones, data must be appended to the underlying layer of the ECS instance after the instance is restarted. Therefore, the I/O performance of your ECS instance is temporarily degraded, and the snapshot and disk features are temporarily disabled. Typically, it takes about 4 hours to append 100 GiB of data.

## Step 3: Check the migration result

1.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

2.  Find the migrated ECS instance and click its ID.

3.  On the **Instance Details** page, check whether the network type of the instance is **VPC**.

    ![View the result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0569627161/p201827.png)

4.  Check the internal network and business operating environments.

    |Scenario|Migration plan|What to do next|
    |--------|--------------|---------------|
    |Migrate all classic network-type instances to a VPC|Set **Destination VPC** to **\(Default\) Automatically create a VPC, CIDR block: 10.0.0.0/8**.|Check whether your business system runs normally.|
    |Migrate some ECS instances to a VPC and retain some ECS instances in the classic network|    -   Set **Destination VPC** to **\(Default\) Automatically create a VPC, CIDR block: 10.0.0.0/8**.
    -   Set **Ensure interconnections between the migrated instances and the classic network-type instances specified in the plan over the internal network** to **Yes**.
|Check whether your business system runs normally.|
    |Other scenarios|Set **Destination VPC** to a VPC that has a CIDR block other than 10.0.0.0/8.|    1.  Check the network connectivity.
    2.  If your business is connected by using an internal IP address, configure a new internal IP address.
    3.  Check whether your business system runs normally. |


## Post-migration operations

1.  If your ECS instance runs a Linux operating system, and the private IP address has changed after the instance is migrated, modify the /etc/hosts file of the ECS instance.

    ![Modify hosts](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0569627161/p109912.png)

    1.  Run the `vi /etc/hosts` command and enter i.
    2.  Change the original private IP address to the private IP address after the ECS instance is migrated.
    3.  Press the Esc key, enter :wq, and then press the Enter key.
2.  Remove the abandoned private IP address from the whitelists of other cloud services such as [ApsaraDB RDS](/intl.en-US/Product Introduction/What is ApsaraDB for RDS?.md), [SLB](/intl.en-US/Classic Load Balancer/Product Introduction/What is CLB?.md), [OSS](/intl.en-US/Product Introduction/What is OSS?.md), and [Container Service for Kubernetes](/intl.en-US/Product Introduction/What is Container Service.md).
3.  The zone of the ECS instance may change. Associated services including ApsaraDB RDS, ApsaraDB for Redis, and ApsaraDB for MongoDB are affected. Adjust your application configurations in a timely manner to ensure your business availability. For more information, see [Migrate an ApsaraDB RDS for MySQL instance across zones in the same region](/intl.en-US/RDS MySQL Database/Instance Change/Migrate an ApsaraDB RDS for MySQL instance across zones in the same region.md).
4.  If you have not restarted or upgraded the kernel for an extended period of time, problems may occur after your ECS instance is migrated. For example, a file system check may be performed, related configuration changes may become invalid, and the kernel may fail to be restarted.
5.  \(Optional\) The authorization code of your software changes because the network interface controller \(NIC\) is deleted. If the software on your ECS instance is associated with the MAC address of the NIC and the software vendor approves the migration certificate issued by Alibaba Cloud, you can re-authorize the software. If an error occurs, you must modify or roll back the ECS instance based on the actual situation.
6.  \(Optional\) If your ECS instance has not been restarted for an extended period of time or has not been restarted after its kernel is upgraded, the system checks the file system and updates related configurations when the instance is restarted. If your ECS instance fails to be restarted, contact Alibaba Cloud [Submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

## References

**Why am I unable to open websites, use services, or read and write data after my ECS instance is migrated?**

This may be because the corresponding communication port is disabled for the new security group. You can try to clone the original security group rules. For more information, see [Clone a security group](/intl.en-US/Security/Security groups/Manage security groups/Clone a security group.md).

**Why am I unable to use the software after my ECS instance is migrated? I am prompted that the authorization code expires, the authorization code is invalid, or no authorization code exists.**

The following reasons may apply:

-   Your software does not have a migration license plan. In this case, you can contact the software vendor or channel partner to submit a verification form for re-authorization.
-   Some software is registered to a valid environment by associating the MAC address of the NIC. After your ECS instance is migrated to a VPC, only one MAC address can be retained. The associated MAC address may be deleted. You can contact the software vendor to check whether your software is registered to your instance by associating the MAC address of the NIC. If so, you must rebind the NIC to the instance. For more information, see [ENI overview](/intl.en-US/Network/Elastic Network Interfaces/ENI overview.md).

**Why am I unable to use the FTP service after my ECS instance is migrated?**

After your ECS instance is migrated, the public NIC is deleted. Therefore, the FTP service is unavailable. You can perform the following operations:

1.  [Convert the public IP address of a VPC-type instance to an elastic IP address](/intl.en-US/Network/Change IPv4 addresses/Convert the public IP address of a VPC-type instance to an Elastic IP address.md).
2.  [Associate an EIP with a secondary ENI in cut-through mode](/intl.en-US/User Guide/Associate an EIP with a cloud instance/Bind an EIP to a secondary ENI/Associate an EIP with a secondary ENI in cut-through mode.md).

**Note:** Some retired instance types and previous-generation entry-level instance types do not support elastic network interfaces \(ENIs\). Upgrade the instance type of your ECS instance to a compatible one before you perform the preceding operations. For more information, see [Retired instance types](https://www.alibabacloud.com/help/faq-detail/55263.htm), [Instance families](/intl.en-US/Instance/Instance families.md), and [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md).

**What do I do when I cannot find data disks on some Windows instances after the instances are migrated?**

After some Windows instances are migrated, the disks attached to these Windows instances are offline. You can use the following method to batch configure disks to make them automatically online. For more information, see [Methods for processing offline disks in Windows ECS instances](https://www.alibabacloud.com/help/zh/doc-detail/197813.htm).

1.  In the left-side navigation pane of the [ECS console](https://ecs.console.aliyun.com), choose **Maintenance & Monitoring** \> **ECS Cloud Assistant**.
2.  Click **Create or Run Command** to create and run the following Cloud Assistant command. For more information, see [Immediate execution](/intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Immediate execution.md).

    The following table describes the parameters for the Cloud Assistant command. For other parameters, use the default values.

    |Parameter|Value|
    |---------|-----|
    |**Command Type**|PowerShell|
    |**Command**|    ```
@("san policy=onlineall") |diskpart
    ``` |
    |**Select Instances**|Select one or more Windows instances to be repaired.|

3.  Click **Execute and Save**.

## References

-   [Switch to VPC network](/intl.en-US/User Guide/Manage instances/Network connection management/Change the network type from classic network to VPC.md)
-   [Change the network type of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Change the network type of an ApsaraDB RDS for MySQL instance.md)
-   [Configure the hybrid access solution for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/Configure the hybrid access solution for an ApsaraDB RDS for MySQL instance.md)

