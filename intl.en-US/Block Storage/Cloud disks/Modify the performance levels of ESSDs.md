---
keyword: 
---

# Modify the performance levels of ESSDs

You can upgrade the performance level of an enhanced SSD \(ESSD\) in the ECS console. Only the performance level of pay-as-you-go ESSDs can be downgraded. You can also call the ModifyDiskSpec operation to change the performance level of an ESSD. The new performance level takes effect immediately. You do not need to create an ESSD or copy the data.

When you create an ECS instance, you can set an ESSD as the system disk or data disk. You can also create a separate ESSD. For more information about ESSDs, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).

To change the performance level of an ESSD, take note of the following items:

-   Your account does not have overdue payments.
-   The performance level of PL0 ESSDs cannot be changed.
-   If your ESSD is attached to a pay-as-you-go ECS instance, make sure that the instance is not in the expired state.
-   You can change the performance level of a new ESSD only after it enters the **Unattached** \(Available\) state.
-   After the performance level is changed, the ESSD is billed based on the new performance level.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.

3.  In the top navigation bar, select a region.

4.  Find the ESSD whose performance level you want to change and choose **More** \> **Modify Performance Level** in the **Actions** column.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7872909951/p50139.png)

5.  In the Modify Performance Level dialog box, select a new **Performance Level** and click **OK**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8872909951/p50141.png)


The performance level that you can select for an ESSD is determined by its storage capacity. If the capacity of an ESSD is too small to upgrade its performance level, resize the ESSD and then upgrade its performance level. For more information, see [Resize cloud disks](/intl.en-US/Block Storage/Resize cloud disks/Overview.md).

**Related topics**  


[ModifyDiskSpec](/intl.en-US/API Reference/Disk/ModifyDiskSpec.md)

