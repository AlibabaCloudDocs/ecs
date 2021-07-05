---
keyword: [snapshot, cloud disk backup, snapshot copy, snapshot copy across regions, disaster recovery]
---

# Copy a snapshot

This topic describes how to copy a created snapshot from one region to another to back up data across regions.

When you copy a snapshot, take note of the following items:

-   The following regions support the snapshot copying feature:
    -   You can copy snapshots among the following regions: China \(Hangzhou\), China \(Shanghai\), China \(Qingdao\), China \(Beijing\), China \(Zhangjiakou\), China \(Hohhot\), China \(Ulanqab\), China \(Shenzhen\), China \(Heyuan\), China \(Guangzhou\), and China \(Chengdu\).
    -   You can copy snapshots among the following regions: China \(Hong Kong\), Singapore \(Singapore\), Australia \(Sydney\), Malaysia \(Kuala Lumpur\), Indonesia \(Jakarta\), Japan \(Tokyo\), Germany \(Frankfurt\), UK \(London\), US \(Silicon Valley\), US \(Virginia\), and India \(Mumbai\).
-   Billing:

    When you copy a snapshot to a new region, a snapshot copy is created. You are charged for copying snapshots and storing the copies. For more information, see [Snapshots](/intl.en-US/Pricing/Billing items/Snapshots.md).

    **Note:** The first time a disk snapshot is copied, all data stored in the disk is copied. All subsequent copies of the snapshot in the same region are incremental copies. Snapshots are billed based on snapshot sizes. Incremental copies can significantly reduce the sizes of snapshots to be copied.

-   The ID of a new snapshot is different from that of its source snapshot. The new snapshot cannot be used to roll back disks created by the source snapshot.
-   Tags added to source snapshots cannot be copied together with the source snapshots.
-   Encrypted snapshots cannot be copied.

Scenarios:

-   DevOps: You can copy snapshots to start business in new regions or migrate business systems to new regions. This helps you reduce O&M costs and improve data availability.
-   Cross-region backup: Snapshot copying meets the requirements for compliance audit and improvement of business reliability. You can restore your business systems in another region by using new snapshots in the event of a disaster. This reduces recovery time objectives \(RTOs\) and recovery point objectives \(RPOs\).

    **Note:**

    Snapshot copying is fast compared with image copying and can be used to speed up image copying and eliminate capacity constraints. To copy an image, we recommend that you copy a snapshot and use the snapshot to create an image.


## Copy a snapshot

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Snapshots**.

3.  In the top navigation bar, select a region.

4.  Find the snapshot that you want to copy and click **Copy Snapshot** in the **Actions** column.

5.  In the **Copy Snapshot** dialog box, configure the parameters.

    ![Copy a snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0252545261/p89221.png)

    |Parameter|Description|
    |---------|-----------|
    |Destination Region|The region to which to copy the snapshot.|
    |Snapshot Name|The name of the new snapshot.|
    |Description|The description of the new snapshot. We recommend that you enter information such as the purpose and environment of the snapshot to facilitate subsequent management.|
    |Tag|The tag of the new snapshot. The tag can facilitate subsequent management.|

6.  Click **OK**.


If ECS instances are affected by viruses or data loss is caused by accidental deletion, you can use snapshots in the source region or snapshots copied to the destination region to create instances or disks to restore data. For more information, see [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md).

## Cancel snapshot copying

When a snapshot is being copied, you can cancel snapshot copying in the destination region.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Snapshots**.

3.  In the top navigation bar, select a region.

4.  Select the snapshot that is being copied and click **Delete** in the lower part of the page.

5.  In the **Delete** message, click **OK**.


**Related topics**  


[CopySnapshot](/intl.en-US/API Reference/Snapshots/CopySnapshot.md)

