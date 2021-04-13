# What is Asynchronous Block Storage Replication?

Asynchronous Block Storage Replication \(ABSR\) is a block-level feature for asynchronous replication of cloud disks. It asynchronously replicates data on a cloud disk within one region to a cloud disk within another region. ABSR protects data and resumes services when an exception occurs on a primary disk. This reduces or prevents data loss and ensures service continuity for key data.

## Overview

ABSR allows you to replicate cloud disks to other regions to implement geo-disaster recovery of data. After a replication relationship is created and activated, data on the associated primary disk is asynchronously replicated to the associated secondary disk on a regular basis. When you asynchronously replicate data on a cloud disk, you do not need to create snapshots. For example, when you replicate data of a cloud disk within one region to a cloud disk within another region, you need only to create a destination disk in the ECS console and establish a replication relationship between the disks.

![Asynchronous replication](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3997746161/p247233.png)

After a replication relationship is created, the full amount of disk data is synchronized when the data of a disk is synchronized for the first time. The amount of time it takes to synchronize disk data depends on the amount of data. The larger the amount of disk data, the longer it takes to synchronize data. Subsequent synchronization operations are incremental, which synchronize only the changed disk data.

ABSR is supported between the following regions:

-   Mutual replication is supported between the following regions:
    -   China \(Beijing\): Zone F and Zone G
    -   China \(Shanghai\): Zone B and Zone F
    -   China \(Heyuan\): Zone A and Zone B
-   Mutual replication is supported between the following regions:
    -   US \(Silicon Valley\): Zone A and Zone B
    -   US \(Virginia\): Zone A and Zone B

## Terms

The following terms are used in ABSR:

-   Asynchronous replication: Data on a cloud disk within one Alibaba Cloud region is asynchronously replicated to a cloud disk within another region on a regular basis.
-   Primary disk: the cloud disk whose data is to be replicated. The primary disk is also called the source disk.
-   Secondary disk: the destination disk to which data is replicated.
-   Recovery point objective \(RPO\): the amount of data that may be lost due to a failure. RPO is measured by time. For example, if the RPO is 1 hour, all the data written to the cloud disk within the last hour is lost when the disk becomes unavailable.
-   Recovery time objective \(RTO\): the duration of time within which a business system is restored after a disaster. For example, if the RTO is 1 hour, the service is restored within 1 hour after a disk becomes unavailable.
-   Replication relationship: the replication relationship established between the primary disk, secondary disk, and replication configurations.

## Usage specifications

|Specification|Description|
|-------------|-----------|
|The maximum number of replication relationships that can be created for an account within a single zone|16|
|The number of replication relationships that can be created for a cloud disk|1|
|Minimum replication cycle|15 minutes \(replication is automatically performed every 15 minutes\)|
|Primary disk category|Data disks that have the enhanced SSD \(ESSD\) category and use the pay-as-you-go billing method|
|Secondary disk category|Cloud disks that have the same category and capacity as the primary disk|

After an replication relationship is created for a cloud disk, some features of the cloud disk are limited. The following table describes these limits.

|Item|Support for the primary disk|Support for the secondary disk|
|----|----------------------------|------------------------------|
|Read and write operations|Yes|No|
|Deletion|No\*|No\*|
|Re-initialization|No|No|
|Resizing|No|No|
|Attachment|Yes|No\*|
|Snapshot creation|Yes|No\*|
|Performance type modification|No|No|
|Encryption|No|No|

**Note:** \*: The operation is supported after the replication relationship is deleted.

