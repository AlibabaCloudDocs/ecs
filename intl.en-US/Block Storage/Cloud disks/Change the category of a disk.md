---
keyword: [cloud disk, disk, ESSD, ECS, change configurations, upgrade or downgrade configurations]
---

# Change the category of a disk

Alibaba Cloud offers different categories of disks to meet the storage performance and cost requirements in different scenarios. You can change the categories of your disks based on your needs. For example, you have created a standard SSD. If you want the standard SSD to deliver a higher input/output operations per second \(IOPS\), you can change this standard SSD into an enhanced SSD \(ESSD\).

Snapshots of the disk whose category you want to change are created. For more information, see [Create a snapshot for a disk](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).

For information about the performance of different disk categories, see [EBS performance](/intl.en-US/Block Storage/Performance/EBS performance.md).

Before you change the category of a disk, take note of the following items:

-   Only the following disk category change operations are supported. Other operations such as disk category downgrade are not supported.

    |Category of the original disk|Description of supported category change|
    |-----------------------------|----------------------------------------|
    |Ultra disk|You can convert ultra disks into standard SSDs, PL0 ESSDs, PL1 ESSDs, PL2 ESSDs, or PL3 ESSDs. **Note:** You cannot convert ultra disks into standard SSDs in the following zones:

    -   China \(Qingdao\): Zone B
    -   China \(Beijing\): Zone B, Zone D, and Zone E
    -   China \(Hangzhou\): Zone B, Zone D, Zone E, and Zone F
    -   China \(Shanghai\): Zone A and Zone C
    -   China \(Shenzhen\): Zone B and Zone C
    -   UAE \(Dubai\): Zone A
    -   Australia \(Sydney\): Zone A |
    |Standard SSD|You can convert standard SSDs into PL1, PL2, or PL3 ESSDs.|
    |ESSD|PL0|You can convert PL0 ESSDs into PL1, PL2, or PL3 ESSDs.|
    |PL1, PL2, and PL3|You can convert PL1, PL2, and PL3 ESSDs based on their billing methods:    -   If the original ESSDs use the pay-as-you-go billing method, you can convert the ESSDs between PL1, PL2, and PL3.
    -   If the original ESSDs use the subscription billing method, you can upgrade the ESSDs only from the low-performance mode to the high-performance mode. |

    **Note:**

    -   Before you convert a disk on an instance into an ESSD, check whether the instance type supports ESSDs. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).

        If the instance type does not support ESSDs, you must upgrade the instance type to support ESSDs and then convert the disk. For more information, see [Instance families that support instance type changes](/intl.en-US/Instance/Change configurations/Instance families that support instance type changes.md).

    -   You can select a performance level for an ESSD based on the capacity of the ESSD. If you cannot select a higher performance level for an ESSD, you can resize the ESSD and then upgrade its performance level. For more information, see [Overview](/intl.en-US/Block Storage/Resize cloud disks/Overview.md).
-   When you change the category of a disk, the performance of the disk may also change. We recommend that you change the categories of your disks during off-peak hours.
-   It may take an extended period of time to change the category of a disk. The amount of time required is determined based on the storage capacity, original category, and throughput of the disk during the change. After you submit the request to change the category of a disk, we recommend that you view the change progress by going to the **Tasks** page in the ECS console or by calling the [DescribeTaskAttribute](/intl.en-US/API Reference/Others/DescribeTaskAttribute.md) operation.
-   Disk categories may fail to change if resources are insufficient. If a failure occurs, try again later.

## Limits

|Phase|Limit|
|-----|-----|
|Before the category change|Before you change the category of a disk, make sure that the following requirements are met:-   Up to five disk category change tasks can be concurrently performed within the same region and account.
-   You cannot change the category of a disk attached to an instance that is being migrated. |
|During the category change|The following limits apply when the category of a disk is being changed:-   You cannot cancel the disk category change task after it is initiated.
-   You cannot create snapshots for the disk.
-   You cannot resize the disk.
-   You cannot partition or format the disk.
-   You cannot re-initialize the disk.
-   You cannot roll back the disk by using snapshots.
-   You cannot attach the disk to an instance or detach it from an instance.
-   If the disk is an ESSD, you cannot change its performance level.
-   If the disk is a system disk, you cannot replace the operating system of the system disk. |
|After the category change|A disk can have its category changed only once within seven days.|

## Billing

After the category of a disk is changed, the billing of the disk has the following changes:

-   After the category of a pay-as-you-go disk is changed, you are billed for the disk based on the new disk category.
-   After the category of a subscription disk is changed, the price difference is calculated based on the remaining subscription duration and the new disk category. You must pay for the difference.

For information about disk pricing, see [Elastic Block Storage devices](/intl.en-US/Pricing/Billing items/Elastic Block Storage devices.md).

## Procedure

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.

3.  In the top navigation bar, select a region.

4.  Find the disk whose category you want to change and choose **More** \> **Change Category** in the **Actions** column.

5.  In the **Change Disk Category** dialog box, set **Category after Change** and confirm the price.

6.  Click **OK**.


## Results

Use one of the following methods to view the change progress and the status of the disk:

-   Method 1: Go back to the **Disks** page and view the category of the disk in the **Disk Category** column.
-   Method 2: In the left-side navigation pane, choose **Maintenance & Monitoring** \> **Tasks**. Find the change task and view the change progress in the **Status** column.

**Related topics**  


[ModifyDiskSpec](/intl.en-US/API Reference/Disk/ModifyDiskSpec.md)

[DescribeDisks](/intl.en-US/API Reference/Disk/DescribeDisks.md)

[DescribeTaskAttribute](/intl.en-US/API Reference/Others/DescribeTaskAttribute.md)

