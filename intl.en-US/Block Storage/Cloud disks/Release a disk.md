---
keyword: [release a disk, delete a disk, deletedisk, Alibaba Cloud, ECS]
---

# Release a disk

You can manually release disks that you no longer need. When a disk is released, all data stored on the disk is also released, and billing for the disk is stopped. By default, disks attached to ECS instances are released together with the instances. You can disable the Release Disk with Instance feature to retain disks. This topic describes how to release a disk in the ECS console and how to enable or disable the Release Disk with Instance feature.

-   A snapshot of the disk is created to back up important data of the disk. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).
-   The disk to be manually released or the pay-as-you-go data disk for which you want to enable or disable the Release Disk with Instance feature is in the **Unattached** state. For more information, see [Detach a data disk](/intl.en-US/Block Storage/Cloud disks/Detach a data disk.md).

-   If the Delete Automatic Snapshots While Releasing Disk feature is enabled for a disk, the automatic snapshots of the disk are released together with the disk. You can disable the Delete Automatic Snapshots While Releasing Disk feature for a disk when you attach the disk to an instance. For more information, see [Delete automatic snapshots while releasing a disk](/intl.en-US/Snapshots/Automatic snapshot policies/Delete automatic snapshots while releasing a disk.md).
-   Manual snapshots are not released together with the disk from which the snapshots are created.
-   You can manually release a disk or enable the Release Disk with Instance feature for the disk. The following table describes how different types of disks can be released.

    |Disk type|Subscription|Pay-as-you-go|
    |---------|------------|-------------|
    |System disk|By default, the Release Disk with Instance feature is enabled for subscription system disks. You can disable this feature.|By default, the Release Disk with Instance feature is enabled for pay-as-you-go system disks. You can disable this feature.|
    |Data disk|    -   By default, the Release Disk with Instance feature is enabled for subscription data disks. You can disable this feature.
    -   After subscription data disks are converted to pay-as-you-go data disks, they can be manually released.
|    -   Pay-as-you-go data disks can be released together with their attached instances. By default, the Release Disk with Instance feature is enabled for pay-as-you-go data disks that are created together with instances. For separately created pay-as-you-go data disks, you must manually enable the feature.
    -   Pay-as-you-go data disks can be manually released. |

-   When you enable or disable the Release Disk with Instance feature for a system disk or data disk, take note of the following items:
    -   When the Release Disk with Instance feature is enabled, the disk is automatically released when its attached ECS instance is released.
    -   When the Release Disk with Instance feature is disabled, the disk is retained as a pay-as-you-go data disk 15 days after its attached ECS instance expires, 15 days after a payment becomes overdue for the instance, or when the instance is manually released. If your disks are created in regions inside mainland China, you must complete real-name verification for your account to ensure that the disks can be retained.

        **Note:** The retained data disk is billed on a pay-as-you-go basis. You can log on to the Billing Management console and view the consumption details based on the disk ID.


## Manually release a disk

Perform the following operations to manually release a pay-as-you-go data disk:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.

3.  In the top navigation bar, select a region.

4.  Find the disk that you want to release and choose **More** \> **Release** in the **Actions** column.

5.  In the message that appears, confirm the information and click **Confirm Release**.


## Enable or disable the Release Disk with Instance feature for disks when you create an instance

Perform the following operations to enable or disable the Release Disk with Instance feature for data disks or the system disk when you create an ECS instance in the ECS console:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  Click **Create Instance**.

4.  In the Basic Configurations step, scroll down to the **Storage** section and select or clear **Release with Instance** for data disks or the system disk.

    For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

    ![Release with Instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4972909951/p63822.png)


## Enable or disable the Release Disk with Instance feature for a disk on the Disks page

Perform the following operations to enable or disable the Release Disk with Instance feature for a pay-as-you-go data disk on the Disks page in the ECS console:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.

3.  In the top navigation bar, select a region.

4.  Find the disk for which you want to enable or disable the feature and choose **More** \> **Modify Disk Property** in the **Actions** column.

5.  In the Modify Disk Property dialog box, select or clear **Release Disk with Instance** and click **OK**.

    **Note:** After you clear **Release Disk with Instance**, a disk is retained as a pay-as-you-go data disk 15 days after the attached ECS instance expires, 15 days after a payment becomes overdue for the instance, or when the instance is manually released.

    ![Release Disk with Instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4972909951/p63856.png)


**Related topics**  


[DeleteDisk](/intl.en-US/API Reference/Disk/DeleteDisk.md)

