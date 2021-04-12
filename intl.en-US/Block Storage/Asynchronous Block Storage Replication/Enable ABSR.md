# Enable ABSR

This topic describes how to enable ABSR to synchronize cloud disk data to other regions and implement geo-disaster recovery of data.

ABSR is supported between the following regions:

-   Mutual replication is supported between the following regions:
    -   China \(Beijing\): Zone F and Zone G
    -   China \(Shanghai\): Zone B and Zone F
    -   China \(Heyuan\): Zone A and Zone B
-   Mutual replication is supported between the following regions:
    -   US \(Silicon Valley\): Zone A and Zone B
    -   US \(Virginia\): Zone A and Zone B

In a replication relationship, the primary disk is a data disk of the enhanced SSD \(ESSD\) disk category and cannot be a secondary disk in another replication relationship. The secondary disk is a cloud disk that has the same specifications and capacity as the primary disk. Each cloud disk \(primary or secondary disk\) can have only a single replication relationship.

The following table describes the limits on the primary and secondary disks after a replication relationship is configured.

|Item|Support for the primary disk|Support for the secondary disk|
|----|----------------------------|------------------------------|
|Read and write operations|Yes|No|
|Deletion|Yes|No|
|Re-initialization|No|No|
|Resizing|No|No|
|Attachment|Yes|No|
|Snapshot creation|Yes|Yes|
|Performance type modification|No|No|

## Step 1: Create a replication relationship

To use the ABSR feature, you must create a replication relationship first.

1.  Go to the Asynchronous Block Storage Replication page.

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Asynchronous Replication Relationship**.

2.  Click **Create asynchronous replication of cloud disks**.

3.  In the **Select the primary site resource for asynchronous replication** step, configure the parameters for the primary disk. Then, click **Next: Create Target Site Resource**.

    The following table describes the parameters to configure for the primary disk.

    |Parameter|Description|
    |---------|-----------|
    |Region and Zone|Select the region and zone of the primary disk whose data you want to synchronize.|
    |Cloud disk|Select the primary disk whose data you want to synchronize.|

4.  In the **Create target site resources** step, create a secondary disk. Then, click **Order cloud disk**.

    The following table describes the parameters to configure for the secondary disk.

    |Parameter|Description|
    |---------|-----------|
    |Region and Zone copied|The destination region and zone of the secondary disk.|
    |Billing Method|Select the billing method of the secondary disk. Only the pay-as-you-go billing method is supported.|
    |Cloud disk name|Specify the name of the secondary disk|
    |Label|Configure the tag key and value of the secondary disk. You can use tags to manage disks.|
    |Service Agreement|Read and select cloud server ECS Terms of Service.|

    After you click **Order cloud disk**, a pay-as-you-go disk that has the same category and capacity as the primary disk is created in the destination region.

5.  In the **Create a cloud disk asynchronous replication relationship** step, configure the parameters described in the following table. Then, click **Next: Order Overview**.

    |Parameter|Description|
    |---------|-----------|
    |Copy pair name|Specify a name for the replication relationship.|
    |Description|Specify a description for the replication relationship.|
    |Minimum synchronization period|Specify a minimum synchronization cycle for asynchronous replication. Data in the primary disk is synchronized to the secondary disk based on the minimum synchronization cycle.|

6.  In the **Order overview** step, confirm the information about the primary disk, secondary disk, and replication relationship. Then, click **Confirm order**.


## Step 2: Activate the replication relationship

After a replication relationship is created, it is in the **Inactive** \(`inactive`\) state. You must activate the replication relationship before data can be periodically synchronized to the secondary disk.

1.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Asynchronous Replication Relationship**.

2.  Find the replication relationship that you want to activate and click **Activation** in the **Operation** column.

    After the replication relationship is activated, data on the primary disk is automatically synchronized to the secondary disk based on the synchronization period to implement geo-disaster recovery.


