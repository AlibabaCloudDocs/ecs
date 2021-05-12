---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Big data instance families

This topic describes the features of big data instance families and lists the instance types of each family.

-   Recommended instance families
    -   [d2c, compute-intensive big data instance family](#section_g5o_ipf_viq)
    -   [d2s, storage-intensive big data instance family](#section_eum_nil_2ui)
    -   [d1ne, big data instance family with enhanced network performance](#section_0yv_1sx_xyf)
-   Other available instance families
    -   [d1, big data instance family](#section_cfw_1il_9ai)

## Description

Big data instance families are designed to deliver cloud computing and storage for large amounts of data to support the needs of big data-oriented businesses. These instance families are suitable for scenarios that require offline computing and storage of large amounts of data, such as Hadoop distributed computing, extensive log processing, and large-scale data warehousing. Big data instance families are suitable for businesses that use distributed networks and have high requirements on storage, capacity, and internal bandwidth.

These instance families are suitable for customers in industries such as Internet and finance that need to compute, store, and analyze big data. Big data instance families use local storage to ensure large amounts of storage space and high storage performance.

Big data instances have the following benefits:

-   Enterprise-level computing power ensures efficient and stable data processing.
-   Enhanced network performance including higher maximum internal bandwidth per instance and higher maximum packet forwarding rates satisfies demands for data transfer such as shuffling in Hadoop MapReduce at peak times.
-   When instances are created for the first time, their disks must warm up before the disks can achieve optimal performance. Each disk delivers sequential read and write performance of up to 190 MB/s, and each instance offers a maximum storage throughput of 5 GB/s. This can reduce the amount of time required to read data from and write data to Hadoop Distributed File System \(HDFS\) files.
-   The cost of local storage is 97% lower than that of standard SSDs. This significantly reduces the cost to build Hadoop clusters.

When you use big data instances, take note of the following items:

-   Instances with local SSDs do not support instance configuration changes or failover.
-   The number and capacity of local disks on an instance vary based on the instance type. The local disks with which instances are equipped are tied to the instances. You cannot separately purchase local disks, or detach local disks from the associated instances and then attach the disks to other instances.
-   You cannot create snapshots for local disks. If you want to create an image from the system disk and data disks of an instance with local SSDs, we recommend that you create an image by combining the snapshots of both the system disk and data disks. In this case the data disks must be cloud disks.
-   You cannot create images that contain snapshots of system disks and data disks based on instance IDs.
-   You can attach a standard SSD to an instance with local SSDs, and extend the capacity of the standard SSD.
-   Local disks are physically located on a single physical server, which increases the risks of single points of failure \(SPOFs\). The durability of data stored on local disks is determined by the reliability of the associated physical server.

    **Warning:** For example, data stored on local disks may be lost when hardware failures occur. We recommend that you store only temporary data on local disks.

    -   To ensure data availability, we recommend that you implement data redundancy at the application layer. You can use deployment sets to distribute ECS instances across multiple physical servers to implement high availability and disaster recovery. For more information, see [Create a deployment set](/intl.en-US/Elasticity/Deployment sets/Create a deployment set.md).
    -   If your applications do not have data reliability architectures, we recommend that you use cloud disks or the backup service in your ECS instances for data reliability. For more information, see [Cloud disks](/intl.en-US/Block Storage/Block Storage overview/Cloud disks.md) or [What is Hybrid Backup Recovery?](/intl.en-US/Product Introduction/What is Hybrid Backup Recovery?.md).
-   Operations on an instance with local SSDs may affect the data stored on the local SSDs. For more information, see [Impacts of instance operations on data stored on local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## Best practices for mounting a file system to a big data instance

You must initialize the inode table when you mount a file system such as ext4 for the first time. By default, the lazyinit feature is enabled in Linux kernel V2.6.37 and later. In this case, the inode table is not initialized until the file system is mounted. In addition, local disks require a large amount of throughput \(such as 600 MB/s for 30 local disks\) when they are being initialized and may affect service stability. The concurrency of lazyinit in Linux kernel V4.x is improved to resolve this problem. For more information, visit [index: kernel/git/stable/linux.git](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/commit/?id=e22834f0248d0fa841ead6436d6c19f65539dc9c). We recommend that you use the following best practices to initialize the inode table at your earliest convenience:

1.  Obtain a list of all local serial advanced technology attachment \(SATA\) hard disk drives \(HDDs\).
2.  Run the following command to initialize each local disk separately.

    In this example, an ext4 file system is created on a local disk whose device name is /dev/vdb.

    ```
    mkfs.ext4 -E lazy_itable_init=0,lazy_journal_init=0 /dev/vdb &
    ```

3.  After all local disks are initialized, run the iostat -x 5 command until the I/O activities of all local disks are displayed as 0.
4.  Batch run the mount command.

## d2c, compute-intensive big data instance family

Features

-   Is attached with high-capacity and high-throughput local SATA HDDs and provides a maximum bandwidth of 35 Gbit/s among instances.
-   Supports online replacement and hot swapping of damaged disks to avoid instance shutdown.

    If a local disk fails, you receive a notification about the system event. You can respond to the system event by initiating the process of fixing the damaged disk. For more information, see [Overview of system events on ECS instances equipped with local disks](/intl.en-US/Deployment & Maintenance/System events/System events on ECS instances equipped with local disks/Overview of system events on ECS instances equipped with local disks.md).

    -   If a backup disk is available on the physical machine, Alibaba Cloud online replaces the damaged disk with the backup disk.
    -   If no backup disks are available on the physical machine, the disk hardware must be manually replaced before Alibaba Cloud can replace the damaged disk.
    **Note:** After you initiate the process of fixing the damaged disk, data in the damaged disk cannot be recovered.

-   Compute:
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs \(ESSDs\), standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Big data computing and storage business scenarios where services such as Hadoop MapReduce, HDFS, Hive, and HBase are used
    -   Scenarios in which EMR JindoFS and Operation Orchestration Service \(OOS\) are used in combination to store hot and cold data separately and decouple storage and computing
    -   Machine learning scenarios such as Spark in-memory computing and MLlib
    -   Search and log data processing scenarios where solutions such as Elasticsearch and Kafka are used

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.d2c.6xlarge|24|88.0|3 × 4,000|12.0|1,600|8|8|20|
|ecs.d2c.12xlarge|48|176.0|6 × 4,000|20.0|2,000|16|8|20|
|ecs.d2c.24xlarge|96|352.0|12 × 4,000|35.0|4,500|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## d2s, storage-intensive big data instance family

Features

-   Is attached with high-capacity and high-throughput local SATA HDDs and provides a maximum bandwidth of 35 Gbit/s among instances.
-   Supports online replacement and hot swapping of damaged disks to avoid instance shutdown.

    If a local disk fails, you receive a notification about the system event. You can respond to the system event by initiating the process of fixing the damaged disk. For more information, see [Overview of system events on ECS instances equipped with local disks](/intl.en-US/Deployment & Maintenance/System events/System events on ECS instances equipped with local disks/Overview of system events on ECS instances equipped with local disks.md).

    -   If a backup disk is available on the physical machine, Alibaba Cloud online replaces the damaged disk with the backup disk.
    -   If no backup disks are available on the physical machine, the disk hardware must be manually replaced before Alibaba Cloud can replace the damaged disk.
    **Note:** After you initiate the process of fixing the damaged disk, data in the damaged disk cannot be recovered.

-   Compute:
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Big data computing and storage business scenarios where services such as Hadoop MapReduce, HDFS, Hive, and HBase are used
    -   Machine learning scenarios such as Spark in-memory computing and MLlib
    -   Search and log data processing scenarios where solutions such as Elasticsearch and Kafka are used

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.d2s.5xlarge|20|88.0|8 × 7,300|12.0|1,600|8|8|20|
|ecs.d2s.10xlarge|40|176.0|15 × 7,300|20.0|2,000|16|8|20|
|ecs.d2s.20xlarge|80|352.0|30 × 7,300|35.0|4,500|32|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## d1ne, big data instance family with enhanced network performance

Features

-   Is attached with high-capacity and high-throughput local SATA HDDs and provides a maximum bandwidth of 35 Gbit/s among instances.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4, which is designed for big data scenarios.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where services such as Hadoop MapReduce, HDFS, Hive, and HBase are used
    -   Machine learning scenarios such as Spark in-memory computing and MLlib
    -   Search and log data processing scenarios where solutions such as Elasticsearch are used

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.d1ne.2xlarge|8|32.0|4 × 5,500|6.0|1,000|4|4|10|
|ecs.d1ne.4xlarge|16|64.0|8 × 5,500|12.0|1,600|4|8|20|
|ecs.d1ne.6xlarge|24|96.0|12 × 5,500|16.0|2,000|6|8|20|
|ecs.d1ne-c8d3.8xlarge|32|128.0|12 × 5,500|20.0|2,000|6|8|20|
|ecs.d1ne.8xlarge|32|128.0|16 × 5,500|20.0|2,500|8|8|20|
|ecs.d1ne-c14d3.14xlarge|56|160.0|12 × 5,500|35.0|4,500|14|8|20|
|ecs.d1ne.14xlarge|56|224.0|28 × 5,500|35.0|4,500|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## d1, big data instance family

Features

-   Is attached with high-capacity and high-throughput local SATA HDDs and provides a maximum bandwidth of 17 Gbit/s among instances.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4, which is designed for big data scenarios.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where services such as Hadoop MapReduce, HDFS, Hive, and HBase are used
    -   Machine learning scenarios such as Spark in-memory computing and MLlib
    -   Suitable for customers in industries such as Internet and finance that need to compute, store, and analyze big data
    -   Search and log data processing scenarios where solutions such as Elasticsearch are used

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.d1.2xlarge|8|32.0|4 × 5,500|3.0|300|1|4|10|
|ecs.d1.3xlarge|12|48.0|6 × 5,500|4.0|400|1|6|10|
|ecs.d1.4xlarge|16|64.0|8 × 5,500|6.0|600|2|8|20|
|ecs.d1.6xlarge|24|96.0|12 × 5,500|8.0|800|2|8|20|
|ecs.d1-c8d3.8xlarge|32|128.0|12 × 5,500|10.0|1,000|4|8|20|
|ecs.d1.8xlarge|32|128.0|16 × 5,500|10.0|1,000|4|8|20|
|ecs.d1-c14d3.14xlarge|56|160.0|12 × 5,500|17.0|1,800|6|8|20|
|ecs.d1.14xlarge|56|224.0|28 × 5,500|17.0|1,800|6|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

