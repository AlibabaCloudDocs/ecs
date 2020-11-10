---
keyword: [local disk, local storage, local disk breakdown, low latency, NoSQL, Hadoop, SATA HDD]
---

# Local disks

Local disks are attached to the same physical server as the ECS instance to which the disks are attached. Local disks provide local storage and access for ECS instances. Local disks are cost-effective and provide high random IOPS, high throughput, and low latency.

## Disk categories

**Note:** This topic provides information about the local disks that are sold together with ECS instances. For more information about the performance of instance families that are equipped with local SSDs and big data instance families, see [Instance families](/intl.en-US/Instance/Instance families.md).

Local disks are suitable for business scenarios that require high storage I/O performance, mass storage, and high cost performance. Alibaba Cloud provides the following two categories of local disks:

-   NVMe SSDs

    Instances of the following instance families are equipped with NVMe SSDs:

    -   Instance families equipped with local SSDs: i3, i2, i2g, i2ne, i2gne, and i1
    -   GPU-accelerated compute optimized instance family: gn5
    For example, instance families with local NVMe SSDs are suitable for the following scenarios:

    -   Services such as online games, e-commerce, live streaming, and media services that run I/O intensive applications and require high I/O performance and low latency.
    -   Services that require high storage I/O performance and a high availability architecture at the application layer, such as NoSQL databases \(including Cassandra, MongoDB, and HBase\), MPP data warehouses, and distributed file systems.
-   SATA HDDs

    Instances of the d1ne and d1 instance families are equipped with SATA HDDs. These disks are the preferred storage media for industries that have high requirements for big data computing, storage, and analysis, such as the Internet and financial industries. The disks are suitable for business scenarios that require mass storage and offline computing. These disks can fulfill the requirements of distributed computing services such as Hadoop, which have high requirements for storage performance, storage capacity, and internal bandwidth.


## NVMe SSDs

-   The following table describes the performance metrics of NVMe SSDs that i2 and i2g instance families use.

    |Performance metric|Single disk performance|Overall instance performance[\*](#p_NvmeSsd_appliedCase_i2)|
|ecs.i2.xlarge and ecs.i2g.2xlarge|Other i2 and i2g instance types|
    |:-----------------|:----------------------|-----------------------------------------------------------|
    |:--------------------------------|:------------------------------|
    |Maximum capacity \(GiB\)|894|1,788|8 × 1,788|
    |Maximum read IOPS|150,000|300,000|1,500,000|
    |Maximum read throughput \(GB/s\)|1|2|16|
    |Maximum write throughput \(GB/s\)|0.5|1|8|
    |Access latency|Microsecond \(μs\)|

    \*Overall instance performance in the table applies to only ecs.i2.16xlarge. This performance represents the highest performance level for local storage in the i2 instance family.

-   The following table describes the performance metrics of NVMe SSDs that i2ne and i2gne instance families use.

    |Performance metric|ecs.i2ne.xlarge and ecs.i2gne.2xlarge|ecs.i2ne.2xlarge and ecs.i2gne.4xlarge|ecs.i2ne.4xlarge and ecs.i2gne.8xlarge|ecs.i2ne.8xlarge and ecs.i2gne.16xlarge|ecs.i2ne.16xlarge|
    |------------------|-------------------------------------|--------------------------------------|--------------------------------------|---------------------------------------|-----------------|
    |Maximum capacity \(GiB\)|894|1,788|2 × 1,788|4 × 1,788|8 × 1,788|
    |Maximum read IOPS|250,000|500,000|1,000,000|2,000,000|4,000,000|
    |Maximum read throughput \(GB/s\)|1.5|3|6|12|24|
    |Maximum write throughput \(GB/s\)|1|2|4|8|16|
    |Access latency|Microsecond \(μs\)|

    **Note:** To obtain the maximum throughput performance of disks for Linux instances, we recommend that you use the latest versions of Alibaba Cloud Linux 2 images. Otherwise, the maximum IOPS may not be available for Linux instances.

-   The following table describes the performance metrics of NVMe SSDs that the i1 instance family uses.

    |Performance metric|Single disk performance|Overall instance performance[\*\*\*](#p_NvmeSsd_appliedCase_i1)|
    |:-----------------|:----------------------|:--------------------------------------------------------------|
    |Maximum capacity \(GiB\)|1,456|2,912|
    |Maximum IOPS|240,000|480,000|
    |Write IOPS[\*\*](#singleDisk)|min\{165 × Capacity, 240,000\}|2 × min\{165 × Capacity, 240,000\}|
    |Read IOPS[\*\*](#singleDisk)|
    |Maximum read throughput \(GB/s\)|2|4|
    |Read throughput[\*\*](#singleDisk) \(MB/s\)|min\{1.4 × Capacity, 2,000\}|2 × min\{1.4 × Capacity, 2,000\}|
    |Maximum write throughput \(GB/s\)|1.2|2.4|
    |Write throughput[\*\*](#singleDisk) \(MB/s\)|min\{0.85 × Capacity, 1,200\}|2 × min\{0.85 × Capacity, 1,200\}|
    |Access latency|Microsecond \(μs\)|

    \*\*The following list describes how the performance of a single NVMe SSD is calculated:

    -   Write IOPS: 165 IOPS per GiB, up to 240,000 IOPS
    -   Write throughput: 0.85 MB/s per GiB, up to 1,200 MB/s
    \*\*\*Overall instance performance in the table applies to only ecs.i1.14xlarge. This performance represents the highest performance level for local storage in the i1 instance family.


**Note:** To obtain the standard performance data and measure the Quality of Service \(QoS\) of Alibaba Cloud local disks, you can test the bandwidth, IOPS, and latency of NVMe SSDs. For more information, see [Performance tests on Block Storage](/intl.en-US/Block Storage/Performance/Performance tests on Block Storage.md).

## SATA HDDs

The following table describes the performance metrics of SATA HDDs.

|Performance metric|Single disk performance|Overall instance performance[\*\*\*\*](#p_SataHdd_appliedCase)|
|:-----------------|:----------------------|:-------------------------------------------------------------|
|Maximum capacity \(GiB\)|5,500|154,000|
|Maximum throughput \(MB/s\)|190|5,320|
|Access latency|Millisecond \(ms\)|

\*\*\*\*Overall instance performance in the table applies to only ecs.d1.14xlarge and ecs.d1ne.14xlarge. This performance represents the highest performance level for local storage in the d1 and d1ne instance families.

## Billing methods

Local disks are billed along with the instances to which they are attached. For more information, see [Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md) and [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md).

## Precautions

-   Local disks are attached to a single physical server, which increases risks of single points of failure \(SPOFs\). The reliability of data stored on local disks depends on the reliability of the physical server.

    **Warning:** For example, data stored on local disks may be lost when a hardware failure occurs. We recommend that you store only temporary data on local disks.

    -   To ensure data availability, we recommend that you implement data redundancy at the application layer. You can use deployment sets to distribute ECS instances across multiple physical servers to achieve high availability and disaster recovery. For more information, see [Create a deployment set](/intl.en-US/Elasticity/Deployment sets/Create a deployment set.md).
    -   If your applications do not have data reliability architectures, we recommend that you use cloud disks or the backup service in your ECS instances for data reliability. For more information, see [Disk overview](/intl.en-US/Block Storage/Block Storage overview/Disk overview.md) or [What is Hybrid Backup Recovery?](/intl.en-US/Product Introduction/What is Hybrid Backup Recovery?.md)
-   After you purchase an ECS instance that is attached with a local disk, you must log on to the instance to partition and format the local disk. For more information, see [Partition and format the local disk](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md).
-   The following operations are not supported on a local disk:
    -   Create a separate local disk.
    -   Use a snapshot to create a local disk.
    -   Attach a local disk.
    -   Detach and release a local disk separately.
    -   Resize a local disk.
    -   Re-initialize a local disk.
    -   Create a snapshot for a local disk.
    -   Use a snapshot to roll back a local disk.

## Disk initialization sequence

When you create an ECS instance equipped with local disks, all disks are initialized based on the following rules:

-   Rule 1: If the specified image used to create the instance does not have data disk snapshots, the local disks are initialized prior to the cloud disks that are created together with the ECS instance.
-   Rule 2: If the specified image has data disk snapshots, the initialization sequence of the data disks corresponds to the sequence of data disks retained in the snapshots. The initialization sequence of the remaining disks is subject to Rule 1.

For example, for a Linux image that contains snapshots of two data disks, the disks are initialized in the following sequence:

-   If the original device names of the two data disks are /dev/xvdb and /dev/xvdc, Alibaba Cloud first allocates /dev/xvdb and /dev/xvdc to specified data disks in the image. The system disk is initialized first. Then, the initialization proceeds in the following sequence: data disk 1 specified in the image, data disk 2 specified in the image, local disk 1, local disk 2, cloud disk 1, cloud disk 2, and cloud disk N. This is shown in the following figure.

    ![Rule 2 - Schematic 1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2672909951/p39625.png)

-   If the original device names of the two data disks are /dev/xvdc and /dev/xvdd, Alibaba Cloud first allocates /dev/xvdc and /dev/xvdd to specified data disks in the image. The remaining device names are preferentially allocated to the local disks. The system disk is initialized first. Then, the initialization proceeds in the following sequence: local disk 1, data disk 1 specified in the image, data disk 2 specified in the image, local disk 2, cloud disk 1, cloud disk 2, and cloud disk N. This is shown in the following figure.

    ![Rule 2 - Schematic 2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2672909951/p39626.png)


## Lifecycle

A local disk has the same lifecycle as the instance to which it is attached. For more information, see [ECS instance lifecycle](/intl.en-US/Instance/ECS instance lifecycle.md).

## Impacts of instance operations on the data stored on local disks

The following table describes the impacts of instance operations on the data stored on local disks.

|Instance operation|Data stored on the local disk|Local disk|
|:-----------------|:----------------------------|:---------|
|Restart the operating system, [restart an instance by using the ECS console](/intl.en-US/Instance/Manage instances/Restart an instance.md), or forcibly restart an instance.|Retained×|Retained|
|Shut down the operating system, [stop an instance by using the console](/intl.en-US/Instance/Manage instances/Start ECS instances.md), or forcibly stop an instance.|Retained|Retained|
|[Automatically recover an instance](/intl.en-US/Deployment & Maintenance/System events/Automatic recovery events of instances.md).|Erased|Released|
|[Release an instance](/intl.en-US/Instance/Manage instances/Release an instance.md).|Erased|Released|
|A subscription instance is stopped when it expires or a pay-as-you-go instance is stopped when the account has an overdue payment. However, the instance is not released.|Retained|Retained|
|A subscription instance is stopped when it expires or a pay-as-you-go instance is stopped when the account has an overdue payment. After that, the instance is released.|Erased|Released|
|[Renew](/intl.en-US/Pricing/Renew instances/Manually renew an instance.md) an expired subscription instance.|Retained|Retained|
|[Reactivate](/intl.en-US/Instance/Manage instances/Reactivate an instance.md) a pay-as-you-go instance that is stopped due to an overdue payment.|Retained|Retained|

## References

For information about retired local SSDs, see [Ephemeral SSDs](https://www.alibabacloud.com/help/doc-detail/35241.htm).

