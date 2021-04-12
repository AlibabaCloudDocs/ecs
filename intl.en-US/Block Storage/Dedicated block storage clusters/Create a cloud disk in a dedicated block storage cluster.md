# Create a cloud disk in a dedicated block storage cluster

After a dedicated block storage cluster is created, you can create cloud disks in the cluster. These cloud disks are physically isolated from other public cloud disks.

Only data disks that are enhanced SSDs \(ESSDs\) of the PL1 performance level can be created in a dedicated block storage cluster.

**Note:** The dedicated block storage cluster feature is available in the China \(Heyuan\), China \(Ulanqab\), and Indonesia \(Jakarta\) regions. The number of supported regions is increasing.

## Procedure

1.  Go to the Dedicated Block Storage Cluster page.

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Dedicated Block Storage Cluster**.

    3.  In the top navigation bar, select a region.

2.  Find the cluster in which to create a cloud disk and click **Create Disk** in the **Actions** column.

3.  On the disk buy page, configure the parameters described in the following table.

    |Parameter|Description|
    |---------|-----------|
    |Attach|Specifies whether to attach the created disk to ECS instances.     -   **Not Attach**: only creates a disk and does not attach the disk to ECS instances.
    -   **Attach to ECS Instance**: creates a disk and attaches the disk to the specified ECS instance.

If you select this option, you must specify **ECS Instance** to select an ECS instance. |
    |Storage|Set the capacity of the disk.|
    |Quantity|Select the number of disks that you want to create. **Note:** You can attach a maximum of 16 data disks to an ECS instance. When you purchase disks for an instance, take note of the number of data disks attached to the instance. |
    |Terms of Service|Read and select Terms of Service.|
    |Others \(Optional\)|Specify the disk name, description, tags, and resource group for easy management.|

4.  Click **Confirm Order**.

    After the disk is created, you can choose **Storage & Snapshots** \> **Disks** to go to the Disks page. On the Disks page, search by **Dedicated Block Storage Cluster ID/Name** to view the created disks.


## What to do next

After a disk is created, you must attach the disk to an ECS instance within the same zone and format the disk before you can use it.

1.  If you set Attach to **Not Attach** when you create the disk, attach it to an ECS instance first. For more information, see [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).

    **Note:** If you set Attach to **Attach to ECS Instance** when you create the disk, skip this step.

2.  Log on to the ECS instance and format the disk. For more information, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md) or [Format a data disk for a Windows ECS instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Windows ECS instance.md).

