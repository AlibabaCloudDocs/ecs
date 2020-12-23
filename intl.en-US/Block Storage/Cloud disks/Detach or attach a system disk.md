---
keyword: [detach a system disk, slow boot, slow boot, ECS, Alibaba Cloud]
---

# Detach or attach a system disk

You can detach a system disk from an ECS instance. If an instance fails to start because its system disk contains corrupted files, you can detach the disk from the instance and attach it to another instance as a data disk for repair. After the disk is repaired, you can attach it back to the original instance.

Before you detach a system disk from an instance, make sure that the involved resources meet the following requirements:

-   The instance is in the **Stopped** state.
-   The image used to create the instance is not deleted.

Before you attach a detached system disk to an instance, make sure that the instance meets the following requirements:

-   The instance is in the **No System Disk** state.
-   The instance is the same instance from which the system disk was detached.

After a system disk is detached from an instance, the instance and the system disk do not support the following operations:

-   Start the instance
-   Change the billing method of the instance
-   Change the instance type
-   Change the public bandwidth
-   Create a custom image
-   Release the system disk separately
-   Replace the system disk
-   Resize the system disk
-   Change the billing method of the disk

## Detach a system disk

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance from which you want to detach the system disk and make sure that the instance is in the **Stopped** state. Click the instance ID to go to the **Instance Details** page.

5.  On the **Instance Details** page, click the **Cloud Disk** tab.

6.  In the **Actions** column corresponding to the **system disk**, choose **More** \> **Detach**.

    ![Operations of detaching the system disk](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0366076061/p72653.png)

7.  In the message that appears, click **OK**.

    **Note:** If you clear **Release Disk with Instance** in the message, the system disk is retained as a data disk when its attached instance is released. The disk is then charged on a pay-as-you-go basis.

8.  Check whether the system disk is detached.

    1.  On the Instances page, the instance is in the **No System Disk** state and is bound with a tag.

        ![Results of detaching the system disk](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1785947061/p72656.png)

    2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.

    3.  The system disk is converted to a data disk, the disk is bound with three tags, and the billing method remains unchanged.

        ![Results of detaching the system disk](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1785947061/p72662.png)

    The tags that are bound to the instance and the disk can help you search for the resources. The following table describes the tags.

    |Tag key|Description|Tag value|
    |-------|-----------|---------|
    |acs:ecs:sourceSystemDiskId|The system disk of the instance.|The ID of the disk.|
    |acs:ecs:sourceInstanceId|The instance to which the system disk was attached.|The ID of the instance.|
    |acs:ecs:diskDeleteProtection|The release protection feature is enabled for the disk. The disk cannot be manually released.|true.|
    |acs:ecs:diskPayType|The billing method of the disk.|The billing method of the disk remains unchanged. Valid values:     -   PrePaid: subscription
    -   AfterPay: pay-as-you-go |


## Attach as a system disk

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance that is in the **No System Disk** state. Click **Attach Disk** in the **Actions** column.

    ![Attach Disk](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1785947061/p72684.png)

5.  In the Attach Disk dialog box, perform the following operations:

    1.  Copy the value of **Source System Disk** and paste it to the **Target Disk** field.

    2.  Configure the parameters described in the following table for the system disk.

        |Parameter|Description|Example|
        |---------|-----------|-------|
        |**Logon Credentials**|The logon credentials for the instance.         -   **Key Pair**: Select this option only for Linux instances.
        -   **Custom Password**: You can select this option for both Windows Server and Linux instances. However, this option takes effect only when the default administrator and root usernames are used.
|**Key Pair**|
        |**Release Disk with Instance**|Specifies whether to retain the disk when the instance is released.         -   If this option is selected, the disk is also released when the instance is released.
        -   If this option is not selected, the disk is retained as a data disk and billed on a pay-as-you-go basis.
|Clear|
        |**Delete Automatic Snapshots While Releasing Disk**|Specifies whether to retain the automatic snapshots of the disk when the disk is released.         -   If this option is selected, the automatic snapshots are deleted when the disk is released.
        -   If this option is not selected, the automatic snapshots are retained when the disk is released.
|Select|

    3.  Click **OK**.

    4.  Confirm the settings and click **Attach**.


## Attach as a data disk

After a system disk is detached, you can attach it to another instance within the same zone as a data disk. For more information, see [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).

**Related topics**  


[DetachDisk](/intl.en-US/API Reference/Disk/DetachDisk.md)

[AttachDisk](/intl.en-US/API Reference/Disk/AttachDisk.md)

