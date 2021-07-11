---
keyword: [Alibaba Cloud, back up, back up data, roll back, disaster recovery]
---

# Snapshot overview

The Alibaba Cloud snapshot service is an agentless backup service that allows you to create crash-consistent snapshots for all disk categories to back up or restore an entire disk. Crash-consistent snapshots are an effective solution to disaster recovery and can be used to back up data, create images, and implement disaster recovery for applications.

## Introduction

A snapshot is a point-in-time backup of a disk. The first snapshot of a disk is a full snapshot that does not contain the copies of empty data blocks. Subsequent snapshots are incremental snapshots that store only changed data blocks. For more information, see [Incremental snapshots](/intl.en-US/Snapshots/Incremental snapshots.md).

The following figure shows common operations on a snapshot. ![Scenarios](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8723484161/p207220.png)



|Operation|Description|References|
|---------|-----------|----------|
|Create a snapshot|You can use the following methods to create snapshots:-   You can manually create snapshots. Manually created snapshots are called manual snapshots. You can create manual snapshots before you perform high-risk operations to improve fault tolerance.
-   You can create automatic snapshot policies to create snapshots. Snapshots created based on these policies are called automatic snapshots. After you create an automatic snapshot policy and apply it to a disk, the system creates snapshots for the disk at the points in time specified in the policy. You can use automatic snapshots to back up data and improve the security of your business data.

|-   [Create a snapshot for a disk](/intl.en-US/Snapshots/Use snapshots/Create a snapshot for a disk.md)
-   [Overview](/intl.en-US/Snapshots/Automatic snapshot policies/Overview.md) |
|Roll back a disk|When the system is unresponsive or when accidental changes are made, you can roll back a disk to a previous version by using one of its snapshots.|[Roll back a disk by using a snapshot](/intl.en-US/Snapshots/Use snapshots/Roll back a disk by using a snapshot.md)|
|Create an image from a system disk snapshot|You can create a custom image from a snapshot that contains the operating system and data of an Elastic Compute Service \(ECS\) instance. Then, you can use the custom image to create multiple instances that have identical application environments.|[Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md)|
|Create a disk from a snapshot|A single snapshot can be used to create multiple identical disks.|[Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md)|
|Copy a snapshot from other regions|When a snapshot is copied from one region to another, a copy of the snapshot is created in the destination region.|[Copy a snapshot](/intl.en-US/Snapshots/Use snapshots/Copy a snapshot.md)|

In addition, the snapshot service provides advanced features such as instant access. For more information, see [Enable or disable the instant access feature](/intl.en-US/Snapshots/Use snapshots/Enable or disable the instant access feature.md).

## Billing methods

Snapshots are billed based on their size and use the pay-as-you-go billing method. For more information, see [Snapshots](/intl.en-US/Pricing/Billing items/Snapshots.md).

**Note:** Pay-as-you-go bills of snapshots can be offset by storage capacity units \(SCUs\).

## Limits

For the limits and quotas of snapshots, see the "Snapshot limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).

## Scenarios

You can use snapshots for the following scenarios:

-   Disaster recovery and backup: You can create a snapshot for a disk and then use the snapshot to create another disk to implement zone- or geo-disaster recovery.
-   Environment clone: You can use a system disk snapshot to create a custom image and then use the custom image to create ECS instances that have identical environments.
-   Improvement of fault tolerance: You can reduce the risk of data loss caused by accidental changes by using a snapshot to roll a disk back to a previous version. Snapshots are suitable for the following scenarios:
    -   Create snapshots on a regular basis to prevent data loss caused by accidental changes or external attacks. For example, data may be lost due to the fact that invalid data is written to disks, ECS instances are accidentally released, data errors arise from application errors, or hackers exploit application vulnerabilities to delete business data.
    -   Create snapshots before you perform high-risk O&M operations, such as replacing operating systems, upgrading applications, and migrating data.

## Benefits

The following table describes the benefits of Alibaba Cloud ECS snapshots compared with snapshots in traditional storage services.

|Item|Alibaba Cloud ECS snapshot|Traditional storage service snapshot|
|:---|:-------------------------|:-----------------------------------|
|Capacity|Unlimited capacity for storing large amounts of business data.|Limited capacity, dependent on the capacity of the storage device.|
|Scalability|High scalability allows you to extend storage devices to any sizes within seconds.|Low scalability, dependent on the storage performance, available capacity, and vendor support.|
|Total cost of ownership \(TCO\)|You need only to pay for the amount of storage space that your snapshots occupy.|High upfront costs for software licenses, reserved storage space, upgrade, and maintenance.|
|Security|Supports data encryption. After you encrypt a disk, all snapshots that are created for it are also encrypted. Unencrypted snapshots cannot be converted to or from encrypted snapshots. For more information, see [Encryption overview](/intl.en-US/Block Storage/Encrypt a disk/Encryption overview.md).|Encryption attributes and policies are subject to the underlying storage logic. If the storage architecture has security flaws, snapshots created based on this architecture may be insecure.|
|Impact on performance|Uses redirect-on-write \(ROW\). -   Impacts on the I/O performance of the source disk are reduced.
-   Snapshots do not affect service availability and can be created at any time without affecting user experience.

|Typically uses copy-on-write \(COW\), but may also use ROW or other methods. COW may affect the data write capabilities of the source system.|

