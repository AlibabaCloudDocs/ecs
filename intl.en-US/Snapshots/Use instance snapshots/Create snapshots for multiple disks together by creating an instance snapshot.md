# Create snapshots for multiple disks together by creating an instance snapshot

You can create snapshots for multiple disks together by creating a snapshot for the ECS instance to which these disks are attached. When a business system spans multiple disks on an ECS instance, you can create a snapshot for the instance to ensure a consistent write order and crash consistency of business system data.

## Scenarios

-   If a business system spans multiple disks \(including the system disk and data disks\) on an ECS instance, you can create snapshots for these disks together by creating a snapshot for the instance. This ensures that the write order of data to each volume remains consistent. Example scenarios to which instance snapshots are applicable:

    MySQL clusters are built on ECS instances, a single Logical Volume Manager \(LVM\) logical volume is created on multiple volumes, or Oracle or SAP HANA clusters are migrated to the cloud.

-   When a business system spans multiple disks on an ECS instance, the same backup policy must be applied to the disks.

## Precautions

The amount of time required to create a snapshot for the instance depends on the sizes of the selected disks for which to create snapshots. The first snapshot of each disk is a full snapshot and takes a long time to create. Subsequent snapshots of the disk are incremental snapshots. It does not take as long to create an incremental snapshot, and the amount of time required depends on the amount of data changed since the previous snapshot. The more data that has changed, the longer it takes. If you want to use a snapshot immediately after it is created, you can enable the instant access feature. For more information, see [Enable or disable the instant access feature](/intl.en-US/Snapshots/Use snapshots/Enable or disable the instant access feature.md).

When you create a snapshot for an instance, take note of the following items:

-   The instance must be in the **Running** or **Stopped** state.
-   The instance snapshot feature can be used to create snapshots only for enhanced SSDs \(ESSDs\) that are in the **In Use** state.
-   A single instance snapshot can contain snapshots of up to 10 disks including the system disk and data disks, and cannot exceed 32 TiB in size.
-   To ensure that services are not affected, we recommend that you create instance snapshots during off-peak hours.
-   Created snapshots are stored unless you delete them. We recommend that you delete unnecessary snapshots at regular intervals to avoid unnecessary snapshot storage fees.

## Billing

Instance snapshots are billed based on their size. After the instant access feature is enabled for an instance snapshot, you are charged both the snapshot storage fee and the instant access feature fee. For more information, see [Snapshots](/intl.en-US/Pricing/Billing items/Snapshots.md).

## Procedure

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance for which you want to create a snapshot and choose **More** \> **Disk and Image** \> **Create Instance Snapshot** in the **Actions** column.

5.  In the **Create Instance Snapshot** dialog box, configure the parameters in the following table to create an instance snapshot.

    |Parameter|Description|
    |---------|-----------|
    |**Disks**|Select disks on the instance, for which to create snapshots.|
    |**Snapshot Parameters**|Instance Snapshot Name|Enter a name for the instance snapshot to make the snapshot easy to identify.|
    |Description|Enter a description for the instance snapshot to make the snapshot easy to identify.|
    |Instant Access|Turn on or off **Instant Access**. By default, Instant Access is turned off.**Note:** The instant access feature support only ESSDs. For more information, see [Enable or disable the instant access feature](/intl.en-US/Snapshots/Use snapshots/Enable or disable the instant access feature.md). |
    |Duration of Instant Access|Specify a duration during which the instant access feature takes effect. This parameter is available only when **Instant Access** is turned on. The instant access feature is automatically disabled when the specified duration expires.|

6.  Click **OK**.

    After the instance snapshot is created, you can choose **Storage & Snapshots** \> **Snapshots** in the left-side navigation pane and click the **Instance Snapshots** tab to view the snapshot.


You can use the created instance snapshot to roll back disks or create images. For more information, see [Roll back a disk by using a snapshot](/intl.en-US/Snapshots/Use snapshots/Roll back a disk by using a snapshot.md) or [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md).

