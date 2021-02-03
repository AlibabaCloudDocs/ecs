---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Instance types with local SSDs

This topic describes the features of ECS instance families with local SSDs and lists the instance types of each family.

-   Recommended instance families
    -   [i3, instance family with local SSDs](#section_ogb_jlc_y4v)
    -   [i2, instance family with local SSDs](#section_y55_6f0_568)
    -   [i2g, instance family with local SSDs](#section_0xx_a83_xv8)
    -   [i2ne, instance family with local SSDs](#section_yum_us8_tq0)
    -   [i2gne, instance family with local SSDs](#section_lze_1l0_mtl)
-   Other available instance families

    [i1, instance family with local SSDs](#section_buh_5lq_frq)


## Overview

Instances with local SSDs provide high I/O performance. They are suitable for scenarios that impose high demands on storage I/O performance and high availability architecture at the application level. For example, they are suitable for NoSQL databases, massively parallel processing \(MPP\) data warehouses, and distributed file systems.

Instances with local SSDs are suitable for enterprises that provide online services such as online gaming, e-commerce, live video streaming, and media. Instances with local SSDs can satisfy the high requirements of I/O-intensive applications for low latency and high I/O performance of Elastic Block Storage \(EBS\) devices.

Instances with local SSDs have the following features:

-   Provide up to hundreds of thousands of low latency random read/write IOPS for large databases.
-   Offer a maximum throughput of several gibibytes per second for sequential read/write operations in big data, parallel computing, and other large dataset scenarios.
-   Use local NVMe SSDs to deliver hundreds of thousands of random read/write IOPS with only several microseconds of latency.

When you use instances with local SSDs, take note of the following items:

-   Instances with local SSDs do not support changes in instance types, bandwidth, and billing methods, and do not support failover.
-   The number and capacity of local disks of an instance vary with the instance type. Instances with local SSDs are bound to their local disks. You cannot attach additional local disks to these instances or detach local disks from these instances and attach the disks to other instances.
-   You cannot create snapshots for local disks. If you want to create an image for the system disk and data disks of an instance with local SSDs, we recommend that you create an image by using the snapshots of both the system disk and data disks \(data disks must be non-local disks\).
-   You cannot create images that contain system disks and data disks based on instance IDs.
-   You can attach a standard SSD to an instance with local SSDs. The capacity of the standard SSD is scalable.
-   Local disks are attached to a single physical server, which increases the risks of single points of failure \(SPOFs\). The durability of data stored on local disks is based on the reliability of the physical server.

    **Warning:** For example, data stored on local disks may be lost when hardware failures occur. We recommend that you store only temporary data on local disks.

    -   To ensure data availability, we recommend that you implement data redundancy at the application layer. You can use deployment sets to distribute ECS instances across multiple physical servers to achieve high availability and disaster recovery. For more information, see [Create a deployment set](/intl.en-US/Elasticity/Deployment sets/Create a deployment set.md).
    -   If your applications do not have data reliability architectures, we recommend that you use cloud disks or the backup service in your ECS instances for data reliability. For more information, see [Cloud disks](/intl.en-US/Block Storage/Block Storage overview/Cloud disks.md) or [What is Hybrid Backup Recovery?](/intl.en-US/Product Introduction/What is Hybrid Backup Recovery?.md).
-   Operations on an instance with local SSDs may affect the data stored on the local SSDs. For more information, see [Impacts of instance operations on data stored on local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i3, instance family with local SSDs

Features

-   Uses 2.5 GHz Intel ® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency, and allows damaged disks to be isolated online.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs only.
-   Provides high network performance based on large computing capacity.
-   Suits to the following scenarios:
    -   Online transaction processing \(OLTP\) and high-performance relational databases
    -   NoSQL databases such as Cassandra and MongoDB
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Total inbound and outbound base bandwidth \(Gbit/s\)|Total inbound and outbound burstable bandwidth \(Gbit/s\)|Total inbound and outbound packet forwarding rate \(Kpps\)|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:---------------------------------------------------|---------------------------------------------------------|:---------------------------------------------------------|:-----------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.i3.xlarge|4|32.0|1 \* 894|1.5|10|1,000|Yes|250|4|4|15|40|1.5|
|ecs.i3.2xlarge|8|64.0|1 \* 1788|2.5|10|1,600|Yes|250|8|4|15|50|2.0|
|ecs.i3.4xlarge|16|128.0|2 \* 1788|5.0|10|3,000|Yes|300|8|8|30|80|3.0|
|ecs.i3.8xlarge|32|256.0|4 \* 1788|10.0|None|6,000|Yes|600|16|8|30|150|5.0|
|ecs.i3.13xlarge|52|384.0|6 \* 1788|16.0|None|9,000|Yes|900|32|7|30|240|8.0|
|ecs.i3.26xlarge|104|768.0|12 \* 1788|32.0|None|24,000|Yes|1,800|32|15|30|480|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i2, instance family with local SSDs

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency.
-   Offers a CPU-to-memory ratio of 1:8, which is designed for high-performance databases.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors.
-   Provides high network performance based on large computing capacity.
-   Suits to the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases such as Cassandra, MongoDB, and HBase
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Total inbound and outbound bandwidth \(Gbit/s\)|Total inbound and outbound packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:----------------------------------------------|:---------------------------------------------------------|:-----------|:---------|:---------------------------------|----------------------------|-------------------------|
|ecs.i2.xlarge|4|32.0|1 \* 894|1.0|500|Yes|2|3|10|Up to 16|
|ecs.i2.2xlarge|8|64.0|1 \* 1788|2.0|1,000|Yes|2|4|10|Up to 16|
|ecs.i2.4xlarge|16|128.0|2 \* 1788|3.0|1,500|Yes|4|8|20|Up to 16|
|ecs.i2.8xlarge|32|256.0|4 \* 1788|6.0|2,000|Yes|8|8|20|Up to 16|
|ecs.i2.16xlarge|64|512.0|8 \* 1788|10.0|4,000|Yes|16|8|20|Up to 16|
|ecs.i2d.21xlarge|84|712.0|4 \* 3570|25.0|4,000|Yes|32|16|20|Up to 16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i2g, instance family with local SSDs

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency.
-   Offers a CPU-to-memory ratio of 1:4, which is designed for high-performance databases.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors.
-   Provides high network performance based on large computing capacity.
-   Suits to the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases such as Cassandra, MongoDB, and HBase
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Total inbound and outbound bandwidth \(Gbit/s\)|Total inbound and outbound packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:----------------------------------------------|:---------------------------------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.i2g.2xlarge|8|32.0|1 \* 894|2.0|1,000|No|2|4|10|
|ecs.i2g.4xlarge|16|64.0|1 \* 1788|3.0|1,500|No|4|8|20|
|ecs.i2g.8xlarge|32|128.0|2 \* 1788|6.0|2,000|No|8|8|20|
|ecs.i2g.16xlarge|64|256.0|4 \* 1788|10.0|4,000|No|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i2ne, instance family with local SSDs

i2ne is in invitational preview. To use i2ne,[submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency.
-   Provides a bandwidth of up to 20 Gbit/s.
-   Offers a CPU-to-memory ratio of 1:8, which is designed for high-performance databases.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors.
-   Provides high network performance based on large computing capacity.
-   Suits to the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases such as Cassandra, MongoDB, and HBase
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Total inbound and outbound bandwidth \(Gbit/s\)|Total inbound and outbound packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:----------------------------------------------|:---------------------------------------------------------|:-----------|:---------|:---------------------------------|----------------------------|-------------------------|
|ecs.i2ne.xlarge|4|32.0|1 \* 894|1.5|500|Yes|2|3|10|Up to 16|
|ecs.i2ne.2xlarge|8|64.0|1 \* 1788|2.5|1,000|Yes|2|4|10|Up to 16|
|ecs.i2ne.4xlarge|16|128.0|2 \* 1788|5.0|1,500|Yes|4|8|20|Up to 16|
|ecs.i2ne.8xlarge|32|256.0|4 \* 1788|10.0|2,000|Yes|8|8|20|Up to 16|
|ecs.i2ne.16xlarge|64|512.0|8 \* 1788|20.0|4,000|Yes|16|8|20|Up to 16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i2gne, instance family with local SSDs

i2gne is in invitational preview. To use i2gne,[submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency.
-   Provides a bandwidth of up to 20 Gbit/s.
-   Offers a CPU-to-memory ratio of 1:4, which is designed for high-performance databases.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors.
-   Provides high network performance based on large computing capacity.
-   Suits to the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases such as Cassandra, MongoDB, and HBase
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Total inbound and outbound bandwidth \(Gbit/s\)|Total inbound and outbound packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:----------------------------------------------|:---------------------------------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.i2gne.2xlarge|8|32.0|1 \* 894|2.5|1,000|No|2|4|10|
|ecs.i2gne.4xlarge|16|64.0|1 \* 1788|5.0|1,500|No|4|8|20|
|ecs.i2gne.8xlarge|32|128.0|2 \* 1788|10.0|2,000|No|8|8|20|
|ecs.i2gne.16xlarge|64|256.0|4 \* 1788|20.0|4,000|No|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about the specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i1, instance family with local SSDs

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency.
-   Offers a CPU-to-memory ratio of 1:4, which is designed for high-performance databases.
-   Uses 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) processors.
-   Provides high network performance based on large computing capacity.
-   Suits to the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases such as Cassandra and MongoDB
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Total inbound and outbound bandwidth \(Gbit/s\)|Total inbound and outbound packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:----------------------------------------------|:---------------------------------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.i1.xlarge|4|16.0|2 \* 104|0.8|200|No|1|3|10|
|ecs.i1.2xlarge|8|32.0|2 \* 208|1.5|400|No|1|4|10|
|ecs.i1.3xlarge|12|48.0|2 \* 312|2.0|400|No|1|6|10|
|ecs.i1.4xlarge|16|64.0|2 \* 416|3.0|500|No|2|8|20|
|ecs.i1-c5d1.4xlarge|16|64.0|2 \* 1456|3.0|400|No|2|8|20|
|ecs.i1.6xlarge|24|96.0|2 \* 624|4.5|600|No|2|8|20|
|ecs.i1.8xlarge|32|128.0|2 \* 832|6.0|800|No|3|8|20|
|ecs.i1-c10d1.8xlarge|32|128.0|2 \* 1456|6.0|800|No|3|8|20|
|ecs.i1.14xlarge|56|224.0|2 \* 1456|10.0|1,200|No|4|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

