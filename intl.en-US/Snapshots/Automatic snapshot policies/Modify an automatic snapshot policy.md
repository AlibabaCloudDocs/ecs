---
keyword: [scheduled backup, data backup, fault tolerance, rollback]
---

# Modify an automatic snapshot policy

You can modify the name, creation time, execution frequency, and retention period of an automatic snapshot policy at any time after the policy is created.

At least one automatic snapshot policy is created. For more information, see [Create an automatic snapshot policy](/intl.en-US/Snapshots/Automatic snapshot policies/Create an automatic snapshot policy.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Snapshots**.

3.  In the top navigation bar, select a region.

4.  On the **Snapshots** page, click the **Automatic Snapshot Policies** tab.

5.  On the **Automatic Snapshot Policies** tab, find the automatic snapshot policy that you want to modify and click **Modify Policy** in the **Actions** column.

6.  In the **Modify Policy** dialog box, configure the parameters for the automatic snapshot policy.

    |Parameter|Description|
    |---------|-----------|
    |**Name**|The name of the automatic snapshot policy.|
    |**Executed At**|The hour of the day at which to create automatic snapshots. You can select one or more hours from 00:00 to 23:00. **Note:** When a snapshot is being created, the I/O performance of Elastic Block Storage devices degrades by up to 10%. This can result in a transient I/O speed decrease. We recommend that you create automatic snapshots during off-peak hours. |
    |**Execution Frequency**|The days of the week on which to create automatic snapshots. You can select one or more days from Monday to Sunday.|
    |**Keep Snapshots**|The retention period of the automatic snapshots. The default retention period is 30 days. The following options are available:     -   **Keep For**: Specify the retention period of the snapshots. Unit: days. Valid values: 1 to 65536.
    -   **Always Keep**: If the maximum number of automatic snapshots for a disk is reached, the earliest snapshot created based on the automatic snapshot policy is deleted when a new snapshot is created. |
    |**Cross-Region Replication for Snapshots**|If the Cross-Region Replication for Snapshots feature is enabled, automatic snapshots that are created based on the automatic snapshot policy are copied to the destination region. After you select **Enabled**, you must specify the **Destination Region** and **Retention Time of Snapshot Copies** parameters.

For information about regions that support snapshot copying and billing rules of snapshot copies, see [Copy a snapshot](/intl.en-US/Snapshots/Use snapshots/Copy a snapshot.md) and [Snapshots](/intl.en-US/Pricing/Billing items/Snapshots.md). |
    |**Destination Region**|The region to which to copy the snapshots.|
    |**Retention Time of Snapshot Copies**|The retention period of snapshot copies within the destination region.     -   **Keep For**: Specify the retention period of the snapshots. Unit: days. Valid values: 1 to 65536.
    -   **Always Keep Snapshots Regardless of the Limit of Snapshots**: The snapshot copies in the destination region are permanently retained. |

7.  Click **OK**.


**Related topics**  


[ModifyAutoSnapshotPolicyEx](/intl.en-US/API Reference/Snapshots/ModifyAutoSnapshotPolicyEx.md)

