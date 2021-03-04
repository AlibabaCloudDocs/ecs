---
keyword: [local disk, local storage, local disk breakdown, low latency, NoSQL, Hadoop, SATA HDD]
---

# Local disks

Local disks are physically located on the same physical server as the ECS instance to which the disks are attached. Local disks provide local storage and access for ECS instances. Local disks are cost-effective and provide high random IOPS, high throughput, and low latency.

## Disk categories

**Note:** This topic provides information about the local disks that are sold together with ECS instances. For more information about the performance of instance families that are equipped with local SSDs and big data instance families, see [Instance families](/intl.en-US/Instance/Instance families.md).

Local disks are suited for business scenarios that require high storage I/O performance, mass storage, and high cost performance. Alibaba Cloud provides two categories of local disks. The following table describes the categories.

|Category|Instance family|Scenario|
|--------|---------------|--------|
|Local NVMe SSD|Instances of the following instance families are equipped with local NVMe SSDs:

-   Instance families equipped with local SSDs: i3, i2, i2g, i2ne, i2gne, and i1
-   GPU-accelerated compute optimized instance family: gn5

|Instance families equipped with local NVMe SSDs are suited for the following scenarios:

-   Services such as online gaming, e-commerce, live streaming, and media that run I/O-intensive applications and require high I/O performance and low latency.
-   Services such as NoSQL databases \(including Cassandra, MongoDB, and HBase\), MPP data warehouses, and distributed file systems that require high storage I/O performance and a high availability architecture at the application layer. |
|Local SATA HDD|Instances of the d1ne and d1 instance families are equipped with local SATA HDDs.

|Local SATA HDDs are the preferred storage media for industries such as Internet and finance that have high requirements for big data computing, storage, and analysis. These disks are suited for business scenarios that require mass storage and offline computing. They are applicable to distributed computing services such as Hadoop that have high requirements for storage performance, storage capacity, and internal bandwidth. |

## Local NVMe SSDs

**Note:** You can test the bandwidth, IOPS, and latency of local NVMe SSDs to obtain the standard performance data and measure the Quality of Service \(QoS\) of Alibaba Cloud local disks. For more information, see [Commands used to test the performance of local disks](/intl.en-US/Block Storage/Performance/Test the performance of Elastic Block Storage devices.md).

-   The following table describes the performance metrics of local NVMe SSDs that the i2 and i2g instance families use.

    |Performance metric|Single disk performance|Overall instance performance①|
|ecs.i2.xlarge and ecs.i2g.2xlarge|Other i2 and i2g instance types|
    |:-----------------|:----------------------|-----------------------------|
    |:--------------------------------|:------------------------------|
    |Maximum capacity \(GiB\)|894|1,788|8 × 1,788|
    |Maximum read IOPS|150,000|300,000|1,500,000|
    |Maximum read throughput \(GB/s\)|1|2|16|
    |Maximum write throughput \(GB/s\)|0.5|1|8|
    |Access latency|Within microseconds|

    ① Overall instance performance data in the preceding table applies only to ecs.i2.16xlarge, and represents the highest performance levels of local storage in the i2 instance family.

-   The following table describes the performance metrics of local NVMe SSDs that the i2ne and i2gne instance families use.

    |Performance metric|ecs.i2ne.xlarge and ecs.i2gne.2xlarge|ecs.i2ne.2xlarge and ecs.i2gne.4xlarge|ecs.i2ne.4xlarge and ecs.i2gne.8xlarge|ecs.i2ne.8xlarge and ecs.i2gne.16xlarge|ecs.i2ne.16xlarge|
    |------------------|-------------------------------------|--------------------------------------|--------------------------------------|---------------------------------------|-----------------|
    |Maximum capacity \(GiB\)|894|1,788|2 × 1,788|4 × 1,788|8 × 1,788|
    |Maximum read IOPS|250,000|500,000|1,000,000|2,000,000|4,000,000|
    |Maximum read throughput \(GB/s\)|1.5|3|6|12|24|
    |Maximum write throughput \(GB/s\)|1|2|4|8|16|
    |Access latency|Within microseconds|

    **Note:** To obtain the maximum throughput performance of disks for Linux instances, we recommend that you use the latest versions of Alibaba Cloud Linux 2 images. Otherwise, Linux instances may not be able to deliver their maximum IOPS.

-   The following table describes the performance metrics of local NVMe SSDs that the i1 instance family uses.

    |Performance metric|Single disk performance|Overall instance performance②|
    |:-----------------|:----------------------|:----------------------------|
    |Maximum capacity \(GiB\)|1,456|2,912|
    |Maximum IOPS|240,000|480,000|
    |Write IOPS①|min\{165 × Capacity, 240,000\}|2 × min\{165 × Capacity, 240,000\}|
    |Read IOPS①|
    |Maximum read throughput \(GB/s\)|2|4|
    |Read throughput \(MB/s\)①|min\{1.4 × Capacity, 2,000\}|2 × min\{1.4 × Capacity, 2,000\}|
    |Maximum write throughput \(GB/s\)|1.2|2.4|
    |Write throughput \(MB/s\)①|min\{0.85 × Capacity, 1,200\}|2 × min\{0.85 × Capacity, 1,200\}|
    |Access latency|Within microseconds|

    ① Items in the formulas used to calculate the performance specifications of a single local NVMe SSD:

    -   In the formula used to calculate the write IOPS, 165 × Capacity indicates the result of 165 IOPS/GiB multiplied by the disk capacity \(GiB\), and 240,000 indicates 240,000 IOPS.
    -   In the formula used to calculate the write throughput, 0.85 × Capacity indicates the result of 0.85 MB/s per GiB multiplied by the disk capacity \(GiB\), and 1,200 indicates 1,200 MB/s.
    ② Overall instance performance data in the preceding table applies only to ecs.i1.14xlarge, and represents the highest performance levels for local storage in the i1 instance family.


## Local SATA HDDs

**Note:** You can test the bandwidth, IOPS, and latency of local NVMe SSDs to obtain the standard performance data and measure the QoS of Alibaba Cloud local disks. For more information, see [Commands used to test the performance of local disks](/intl.en-US/Block Storage/Performance/Test the performance of Elastic Block Storage devices.md).

The following table describes the performance metrics of local SATA HDDs.

|Performance metric|Single disk performance|Overall instance performance①|
|:-----------------|:----------------------|:----------------------------|
|Maximum capacity \(GiB\)|5,500|154,000|
|Maximum throughput \(MB/s\)|190 MB/s|5,320 MB/s|
|Access latency|Within milliseconds|

① Overall instance performance data in the preceding table applies only to ecs.d1.14xlarge and ecs.d1ne.14xlarge, and represents the highest performance levels for local storage in the d1 and d1ne instance families.

## Billing

Local disks are billed along with the instances to which they are attached. For more information, see [Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md) and [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md).

## Limits

-   Local disks are physically located on a single physical server, which increases the risks of single points of failure \(SPOFs\). The durability of data stored on local disks is determined by the reliability of the associated physical server.

    **Warning:** For example, data stored on local disks may be lost when hardware failures occur. We recommend that you store only temporary data on local disks.

    -   To ensure data availability, we recommend that you implement data redundancy at the application layer. You can use deployment sets to distribute ECS instances across multiple physical servers to implement high availability and disaster recovery. For more information, see [Create a deployment set](/intl.en-US/Elasticity/Deployment sets/Create a deployment set.md).
    -   If your applications do not have data reliability architectures, we recommend that you use cloud disks or the backup service in your ECS instances for data reliability. For more information, see [Cloud disks](/intl.en-US/Block Storage/Block Storage overview/Cloud disks.md) or [What is Hybrid Backup Recovery?](/intl.en-US/Product Introduction/What is Hybrid Backup Recovery?.md).
-   After you purchase an ECS instance equipped with local disks, you must log on to the instance to partition and format the local disks. For more information, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md).
-   Local disks do not support the following operations:
    -   Create a separate local disk.
    -   Use a snapshot to create a local disk.
    -   Attach a local disk.
    -   Detach and release a local disk separately.
    -   Resize a local disk.
    -   Re-initialize a local disk.
    -   Create a snapshot for a local disk.
    -   Use a snapshot to roll back a local disk.

## Disk initialization sequence

When you create an ECS instance that has local disks attached, all disks of the created instance are initialized based on the following rules:

-   Rule 1: If the image used to create the instance does not contain data disk snapshots, the local disks are initialized prior to the cloud disks that are created together with the instance.
-   Rule 2: If the image used to create the instance contains data disk snapshots, the data disks created from these snapshots are initialized based on the sequence of the data disks retained in the image. The sequence in which the remaining disks are initialized is subject to Rule 1.

For example, assume that a Linux image which contains the snapshots of two data disks is used to create an instance. The disks on the created instance are initialized in the following sequence:

-   If the original device names of the two data disks retained in the image are /dev/xvdb and /dev/xvdc, Alibaba Cloud first allocates /dev/xvdb and /dev/xvdc to the data disks created from the image. The system disk is initialized first. Then, the data disks are initialized in the following sequence: data disk 1 created from the image, data disk 2 created from the image, local disk 1, local disk 2, cloud disk 1, cloud disk 2, and cloud disk N. The following figure shows the sequence in which the disks are initialized.

    ![Rule 2 - Schematic diagram 1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2672909951/p39625.png)

-   If the device names of the two data disks retained in the image are /dev/xvdc and /dev/xvdd, Alibaba Cloud first allocates /dev/xvdc and /dev/xvdd to the data disks created from the image. The remaining device names are allocated to the local disks first and then to other disks. The system disk is initialized first. Then, the data disks are initialized in the following sequence: local disk 1, data disk 1 created from the image, data disk 2 created from the image, local disk 2, cloud disk 1, cloud disk 2, and cloud disk N. The following figure shows the sequence in which the disks are initialized.

    ![Rule 2 - Schematic diagram 2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2672909951/p39626.png)


## Lifecycle

A local disk has the same lifecycle as the instance to which it is attached. For more information, see [ECS instance lifecycle](/intl.en-US/Instance/ECS instance lifecycle.md).

## Impacts of instance operations on data stored on local disks

The following table describes the impacts of instance operations on the data stored on local disks.

|Instance operation|Data stored on the local disk|Local disk|
|:-----------------|:----------------------------|:---------|
|Restart the operating system, restart an instance by using the ECS console, or forcibly restart an instance.|Retained|Retained|
|Shut down the operating system, stop an instance by using the ECS console, or forcibly stop an instance.|Retained|Retained|
|[Automatically recover an instance](/intl.en-US/Deployment & Maintenance/System events/Automatic recovery events of instances.md).|Erased|Released|
|[Release an instance](/intl.en-US/Instance/Manage instances/Release an instance.md).|Erased|Released|
|When a subscription instance expires or when you have an overdue payment for a pay-as-you-go instance, the system stops the instance without releasing the instance.|Retained|Retained|
|When a subscription instance expires or when you have an overdue payment for a pay-as-you-go instance, the system stops the instance and then releases it.|Erased|Released|
|Renew an expired subscription instance.|Retained|Retained|
|Reactivate a pay-as-you-go instance that was stopped due to overdue payments.|Retained|Retained|

## References

For information about retired local SSDs, see [Ephemeral SSDs](https://www.alibabacloud.com/help/doc-detail/35241.htm).

For information about how to handle system events on ECS instances equipped with local disks, see [Overview of system events on ECS instances equipped with local disks](/intl.en-US/Deployment & Maintenance/System events/System events on ECS instances equipped with local disks/Overview of system events on ECS instances equipped with local disks.md).

