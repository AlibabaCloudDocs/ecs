---
keyword: [Alibaba Cloud, back up, back up data, roll back, disaster recovery]
---

# Snapshot overview

The Alibaba Cloud snapshot service allows you to create crash-consistent snapshots for all disk categories. Crash-consistent snapshots are an effective solution to disaster recovery and are used to back up data, create custom images, and implement disaster recovery for applications.

## Scenarios

You can use snapshots for the following scenarios:

-   Disaster recovery and backup: You can create a snapshot for a disk and then use the snapshot to create another disk to implement zone- or geo-disaster recovery.
-   Environment clone: You can use a system disk snapshot to create a custom image and then use the custom image to create ECS instances with identical environments.
-   Data development: Snapshots can provide near-real-time production data for applications such as data mining, report queries, and development and testing.
-   Enhancement of fault tolerance: You can roll a disk back to a previous point in time by using a snapshot to reduce the risk of data loss caused by incorrect operations. Snapshots are suitable for the following scenarios:
    -   Create snapshots on a regular basis to prevent losses caused by incorrect operations. Incorrect operations include: writing incorrect data to disks, accidentally releasing ECS instances, data errors caused by application errors, and data loss due to hacking.
    -   Create snapshots before you perform high-risk O&M operations, such as replacing operating systems, upgrading applications, and migrating data.

## Snapshot classification

Snapshots are classified into normal and local snapshots based on how they are stored. The following table describes the classification of snapshots based on different standards.

|Classification standard|Type|Description|Scenario|
|-----------------------|----|-----------|--------|
|Storage method|Normal snapshot|A snapshot is stored in an OSS bucket within the same region as the source disk. You can create normal snapshots for disks. Normal snapshots can be created for system disks and data disks.

|Normal snapshots are ideal for scenarios that require high disaster recovery capabilities. However, it takes an extended period of time to create normal snapshots.|
|Local snapshot|A local snapshot is stored in the same storage cluster as the source disk and can be used to perform data backup and disk rollback within seconds. Local snapshots can be created only for enhanced SSDs \(ESSDs\).

|-   You can use local snapshots to quickly back up key business systems that contain a large amount of data, such as databases, containers, and SAP High-performance Analytic Appliance \(SAP HANA\).
-   You can also use local snapshots to back up data before you perform high-risk operations to reduce backup time. High-risk operations include replacing system disks, resizing disks, and updating system patches.
-   You can use local snapshots in DevOps applications to accelerate the creation of custom images and the startup of ECS instances. |
|Creation method|Manual snapshot|A manual snapshot is a snapshot that you manually create.

|You can create manual snapshots before you perform high-risk operations to enhance fault tolerance.|
|[Automatic snapshot](/intl.en-US/Snapshots/Automatic snapshot policies/Overview.md)|An automatic snapshot is a snapshot that is created based on an automatic snapshot policy. After you create an automatic snapshot policy and apply it to a disk, ECS automatically creates snapshots for the disk at the points in time specified in the policy.

**Note:** All automatic snapshots are normal snapshots.

|You can use automatic snapshots to back up data and improve the security of your business data.|
|Creation order|Full snapshot|A full snapshot is the first snapshot created for a disk. This snapshot contains all the data stored on the disk at the time the snapshot was created.

|N/A.|
|[Incremental snapshots](/intl.en-US/Snapshots/Incremental snapshots.md)|An incremental snapshot is a snapshot created after the full snapshot. Incremental snapshot contains only the data blocks that have been modified since the last snapshot.

|N/A.|
|Encryption|Encrypted snapshot|An encrypted snapshot is a snapshot that was created from an encrypted disk. **Note:** All encrypted snapshots are normal snapshots. For information about the encryption feature, see [Encryption overview](/intl.en-US/Block Storage/Encrypt a disk/Encryption overview.md).

|You can create encrypted snapshots to comply with the security standards required by your business.|
|Unencrypted snapshot|An unencrypted snapshot is a snapshot that was created from an unencrypted disk.|N/A.|

## Pricing

Snapshots are billed based on their sizes. They can be billed on a pay-as-you-go basis. For more information, see [Snapshot](/intl.en-US/Pricing/Billing items/Snapshot billing.md).

**Note:** Local snapshots can be billed only on a pay-as-you-go basis and are not able to have their bills offset by OSS storage plans.

## Limits

For the limits and quotas of snapshots, see the "Snapshot limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).

Local snapshots have the following limits:

-   Local snapshots can be created only for ESSDs.
-   A maximum of 10 local snapshots can be retained for an ESSD.
-   When you use a local snapshot to create a disk, the specified disk size cannot be less than the snapshot size.
-   You cannot use automatic snapshot policies to create local snapshots.
-   Local snapshots cannot be created for encrypted disks or local disks.

## Benefits

The following table describes the benefits of Alibaba Cloud ECS snapshots compared with snapshots in traditional storage services.

|Item|Alibaba Cloud ECS snapshot|Traditional storage service snapshot|
|:---|:-------------------------|:-----------------------------------|
|Capacity|Unlimited capacity for storing large amounts of business data.|Limited capacity, dependent on the capacity of the storage device.|
|Scalability|High scalability allows you to extend storage devices to any size within seconds.|Low scalability, dependent on the storage performance, available capacity, and vendor support.|
|Total cost of ownership \(TCO\)|You only need to pay for the storage space occupied by your snapshots.|High upfront costs for software licenses, reserved storage space, upgrade, and maintenance.|
|Security|Supports data encryption. If you encrypt a disk, all snapshots created for it afterwards are encrypted. Unencrypted snapshots cannot be directly converted to encrypted snapshots, and encrypted snapshots cannot be directly converted to unencrypted snapshots. For more information, see [Encryption overview](/intl.en-US/Block Storage/Encrypt a disk/Encryption overview.md).|Encryption attributes and policies are subject to the underlying storage logic. If the storage architecture has a security flaw, snapshots created based on this architecture may not be secure.|
|Impact on performance|Uses redirect-on-write \(ROW\). -   Impacts on the I/O performance of the source disk are reduced.
-   Snapshots do not affect service availability and can be created at any time without affecting user experience.

|Typically uses copy-on-write \(COW\), but may also use ROW or other methods. COW may affect the data write capabilities of the source system.|

## Operations

-   You can perform the following operations in the ECS console:
    -   [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md)
    -   [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md)
    -   [Roll back a disk by using a snapshot](/intl.en-US/Snapshots/Use snapshots/Roll back a disk by using a snapshot.md)
    -   [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md)
    -   [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md)
-   For information about API operations, see the "Snapshots" section in [List of operations by function](/intl.en-US/API Reference/List of operations by function.md).

