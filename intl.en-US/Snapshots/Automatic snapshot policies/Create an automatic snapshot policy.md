---
keyword: [scheduled backup, data backup, fault tolerance, rollback]
---

# Create an automatic snapshot policy

This topic describes how to create an automatic snapshot policy in the ECS console.

The snapshot service is activated. For more information, see [Activate ECS Snapshot](/intl.en-US/Snapshots/Use snapshots/Activate ECS Snapshot.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Snapshots**.

3.  In the top navigation bar, select a region.

4.  On the **Snapshots** page, click the **Automatic Snapshot Policies** tab.

5.  In the upper-right corner of the **Automatic Snapshot Policies** tab, click **Create Policy**.

6.  In the **Create Policy** dialog box, complete the settings of the automatic snapshot policy.

    |Parameter|Description|
    |---------|-----------|
    |**Name**|The name of the automatic snapshot policy.|
    |**Executed At**|The hour of the day at which to create automatic snapshots. You can select one or more hours from 00:00 to 23:00. **Note:** When a snapshot is being created, the I/O performance of Elastic Block Storage devices degrades by up to 10%. This can result in a transient I/O speed decrease. We recommend that you create automatic snapshots during off-peak hours. |
    |**Execution Frequency**|The days of the week on which to create automatic snapshots. You can select one or more days from Monday to Sunday.|
    |**Keep Snapshots**|The retention period of the automatic snapshots. The default retention period is 30 days. The following options are available:     -   **Keep For**: Specify the retention period of the snapshots. Unit: days. Valid values: 1 to 65536.
    -   **Always Keep**: If the maximum number of automatic snapshots for a disk is reached, the earliest snapshot created based on the automatic snapshot policy is deleted when a new snapshot is created. |
    |**Tag**|Select existing tag keys and values, or enter new tag keys and values. Automatic snapshots created based on the automatic snapshot policy are bound with these tags.|
    |**Cross-Region Replication for Snapshots**|If the Cross-Region Replication for Snapshots feature is enabled, automatic snapshots that are created based on the automatic snapshot policy are copied to the destination region. After you select **Enabled**, you must continue to set the **Destination Region** and **Retention Time of Snapshot Copies** parameters.

For information about regions that support snapshot copying and billing rules of snapshot copies, see [Copy a snapshot](/intl.en-US/Snapshots/Use snapshots/Copy a snapshot.md) and [Snapshots](/intl.en-US/Pricing/Billing items/Snapshots.md). |
    |**Destination Region**|The region to which to copy the snapshots.|
    |**Retention Time of Snapshot Copies**|The retention period of snapshot copies within the destination region.    -   **Keep For**: Specify the retention period of the snapshots. Unit: days. Valid values: 1 to 65536.
    -   **Always Keep Snapshots Regardless of the Limit of Snapshots**: The snapshot copies in the destination region are retained indefinitely. |

7.  Click **OK**.


We recommend that you specify disks to execute an automatic snapshot policy immediately after the policy is created. For more information, see [Apply or disable an automatic snapshot policy](/intl.en-US/Snapshots/Automatic snapshot policies/Apply or disable an automatic snapshot policy.md).

**Related topics**  


[CreateAutoSnapshotPolicy](/intl.en-US/API Reference/Snapshots/CreateAutoSnapshotPolicy.md)

