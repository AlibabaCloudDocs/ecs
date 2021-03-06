---
keyword: [snapshot backup, custom image, disk, data backup, modify key files, rollback, backup, cloud disk]
---

# Create a snapshot for a disk

The Alibaba Cloud snapshot service is an agentless backup service that allows you to create crash-consistent snapshots for system disks or data disks. You can use snapshots to back up data, restore instances that were released by mistake, and create custom images. You can create snapshots of disks to improve fault tolerance for operations before you roll back a disk, modify key system files, or change the operating system of an instance. This topic describes how to create a snapshot for a disk by using the Elastic Compute Service \(ECS\) console or by calling an ECS API operation.

-   The disk is in the **In Use** or **Unattached** state.
-   If the disk is in the **In Use** state, the ECS instance is in the **Running** or **Stopped** state.

It can take several minutes to create a snapshot depending on the size of the disk. The first snapshot of each disk is a full snapshot and takes longer to create. Subsequent snapshots of the disk are incremental snapshots. It does not take as long to create an incremental snapshot, and the amount of time required depends on the amount of data changed since the previous snapshot. The more data that has changed, the longer it takes.

When you create a snapshot, take note of the following items:

-   You must not perform operations that change the status of the ECS instance such as stopping or restarting the instance.
-   Snapshots are billed resources. For more information, see [Snapshots](/intl.en-US/Pricing/Billing items/Snapshots.md).
-   We recommend that you create snapshots during off-peak hours because snapshot creation degrades the I/O performance of disks by up to 10% and slows down data reads and writes.
-   While snapshots are being created, the incremental data generated by disk operations is not included in the snapshots.
-   If you create an extended volume from a single multi-partition disk, the snapshot that you created can be used to roll back the disk.
-   When a disk is used to create a dynamic extended volume or RAID array, we recommend that you stop applications from writing data to the dynamic extended volume or RAID array and flush the cached data to the disk. Before you create a snapshot, stop all I/O operations.
-   Created snapshots are permanently stored unless you delete them. We recommend that you delete unnecessary snapshots at regular intervals to prevent extra fees incurred by snapshot storage.

## Create a snapshot in the ECS console

You can go to the **Instances** page in the ECS console and perform the following operations to create a snapshot for a disk:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance for which you want to create a snapshot and click the instance ID.

5.  On the **Instance Details** page, click the **Cloud Disk** tab.

6.  Find the disk for which you want to create a snapshot, and click **Create Snapshot** in the **Actions** column.

7.  In the dialog box that appears, configure the following parameters, and then click **Create**.

    |Parameter|Description|
    |---------|-----------|
    |**Snapshot Name**|The name of the snapshot.|
    |**Instant Access**|If you are creating a snapshot for an enhanced SSD \(ESSD\), you can turn on **Instant Access**. For more information, see [Enable or disable the instant access feature](/intl.en-US/Snapshots/Use snapshots/Enable or disable the instant access feature.md).|
    |**Duration of Instant Access**|The number of days during which the instant access feature is available. The instant access feature is automatically disabled when the duration of instant access expires.|
    |**Tag**|The tag key and value of the snapshot.|

    After the snapshot is created, you can click the **Snapshot** tab on the **Instance Details** page to view the created snapshot.


You can also create a snapshot by choosing **Storage & Snapshots** \> **Disks** in the left-side navigation pane.

## Create a snapshot by using Alibaba Cloud CLI

1.  Obtain the instance ID.

    -   Method 1: If you have connected to the ECS instance, you can obtain the instance ID from the instance metadata. For more information, see [Metadata](/intl.en-US/Instance/Manage instance configurations/Manage instance metadata/Overview of ECS instance metadata.md).

        For example, to query the ID of a Linux instance, run the following command:

        ```
        curl http://100.100.100.200/2016-01-01/meta-data/instance-id
        ```

    -   Method 2: Use Alibaba Cloud CLI to call the DescribeInstances operation to obtain the instance ID.

        ```
        aliyun ecs DescribeInstances --RegionId <TheRegionId> --output cols=InstanceId,InstanceName rows=Instances.Instance[]
        ```

2.  Call the DescribeDisks operation to obtain the disk ID.

    ```
    aliyun ecs DescribeDisks --RegionId <TheRegionId> --InstanceId i-bp1afnc98r8k69****** --output cols=DiskId rows=Disks.Disk[]
    ```

3.  Call the CreateSnapshot operation to create a snapshot based on a specified disk.

    ```
    aliyun ecs CreateSnapshot --DiskId d-bp19pjyf12hebp******
    ```

    The task to create a snapshot is initiated if the following information is returned:

    ```
    {"RequestId":"16B856F6-EFFB-4397-8A8A-CB73FA******","SnapshotId":"s-bp1afnc98r8kjh******"}
    ```

4.  Call the DescribeSnapshots operation to query the creation progress.

    ```
    aliyun ecs DescribeSnapshots --RegionId cn-hangzhou --InstanceId i-bp1afnc98r8k69****** --output cols=SnapshotId,Status rows=Snapshots.Snapshot[]
    ```

    If both `"SnapshotId"="s-bp1afnc98r8kjh******"` and `"Status":"accomplished"` are displayed, the snapshot is created.


After a snapshot is created, you can perform the following operations on the snapshot:

-   [Roll back a disk by using a snapshot](/intl.en-US/Snapshots/Use snapshots/Roll back a disk by using a snapshot.md)
-   [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md)
-   [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md)

**Related topics**  


[DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md)

[DescribeDisks](/intl.en-US/API Reference/Disk/DescribeDisks.md)

[CreateSnapshot](/intl.en-US/API Reference/Snapshots/CreateSnapshot.md)

[DescribeSnapshots](/intl.en-US/API Reference/Snapshots/DescribeSnapshots.md)

