# Enable or disable the instant access feature

The more data you store in a disk, the longer it takes to create a snapshot for the disk. For enhanced SSDs \(ESSDs\), you can use the instant access feature to create snapshots within seconds.

**Note:**

On December 14, 2020, the local snapshot feature for ESSDs is upgraded to the instant access feature for ESSDs.

## Scenarios

The instant access feature has the following benefits:

-   Instant access to snapshots: After instant access is enabled for a snapshot, the snapshot can be used to roll back and create disks even when the snapshot is being created. This feature ensures instant access to a new snapshot for an ESSD regardless of the ESSD size.
-   Disk rollback without performance loss: You can use snapshots for which instant access is enabled to roll back ESSDs without performance loss or increase in the I/O latency of the ESSD.

We recommend that you enable the instant access feature in the following scenarios to accelerate the creation of snapshots.

|Scenario|Description|
|--------|-----------|
|DevOps scenario|-   Build a development and test environment based on snapshots.
-   Perform ECS O&M operations by using Operation Orchestration Service \(OOS\). |
|Scenario where snapshots need to be created to back up data before high-risk operations are performed|-   Replace system disks or resize disks.
-   Update business systems.
-   Perform diagnosis in the ECS console. |

## Considerations

Before you enable instant access, take note of the following items:

-   This feature is applicable only to ESSDs.
-   Up to 10 snapshots that have instant access enabled can be retained for a single ESSD. If an ESSD already has 10 snapshots for which instant access is enabled, you cannot enable instant access for more snapshots of the ESSD.
-   ESSDs whose snapshots have instant access enabled cannot be re-initialized.
-   You can enable instant access only when you manually create a snapshot for an ESSD.

When you disable instant access, take note of the following items:

-   After instant access is enabled for a snapshot, you cannot disable the feature when the snapshot is being created. After the snapshot is created, you can disable the feature.
-   When you delete snapshots, instant access is automatically disabled if this feature is enabled for the snapshots.
-   When you delete an ESSD, instant access is automatically disabled if this feature is enabled for snapshots of the ESSD.

## Billing

After the instant access feature is enabled, you are charged both the storage fee for the snapshots and the fee for the instant access feature. The billable items of the instant access feature include the number of times the feature is enabled, the size of snapshots for instant access, and billing duration. For more information, see [Snapshots](/intl.en-US/Pricing/Billing items/Snapshots.md).

**Note:** The instant access feature is billed separately. You can disable the feature to save costs after a snapshot is created. You are still charged for the storage of the snapshot.

## Enable the instant access feature

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the specified ECS instance and click its ID.

5.  Click the **Cloud Disk** tab on the **Instance Details** page.

6.  Find the ESSD for which you want to create a snapshot, and click **Create Snapshot** in the **Actions** column.

7.  In the **Create Snapshot** dialog box, configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Snapshot Name**|Enter a name for the snapshot.|
    |**Instant Access**|Turn on **Instant Access**.|
    |**Duration of Instant Access**|Specify the number of days during which the instant access feature is available. The instant access feature is automatically disabled when the duration of instant access expires.|
    |**Tag**|Configure the tag key and value of the snapshot.|

8.  Click **Create**.


After the snapshot is created, choose **Storage & Snapshots** \> **Snapshots** in the left-side navigation pane to check whether instant access takes effect on the new snapshot.

After the instant access feature is enabled for a snapshot, you can use the snapshot to create a new disk without waiting for the snapshot to be created. For more information, see [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md).

## Disable the instant access feature

You must set the **Duration of Instant Access** parameter when you enable the instant access feature. This feature is automatically disabled when the period specified by the parameter expires. After a snapshot is created, you can also manually disable instant access by performing the following operations.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the specified ECS instance and click its ID.

5.  Click the **Snapshot** tab on the **Instance Details** page.

6.  Find the snapshot for which you want to disable instant access and click **Disable Instant Access** in the **Actions** column.

7.  In the **Disable Instant Access** message, click **OK**.


## References

-   [CreateSnapshot](/intl.en-US/API Reference/Snapshots/CreateSnapshot.md)
-   [ModifySnapshotAttribute](/intl.en-US/API Reference/Snapshots/ModifySnapshotAttribute.md)

