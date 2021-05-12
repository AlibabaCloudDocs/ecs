---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Instance families with local SSDs

This topic describes the features of Elastic Compute Service \(ECS\) instance families with local SSDs and lists the instance types of each family.

-   Recommended instance families
    -   [i3g, instance family with local SSDs](#section_o4u_ofu_2f5)
    -   [i3, instance family with local SSDs](#section_ogb_jlc_y4v)
    -   [i2, instance family with local SSDs](#section_y55_6f0_568)
    -   [i2g, instance family with local SSDs](#section_0xx_a83_xv8)
    -   [i2ne, instance family with local SSDs](#section_yum_us8_tq0)
    -   [i2gne, instance family with local SSDs](#section_lze_1l0_mtl)
-   Other available instance families

    [i1, instance family with local SSDs](#section_buh_5lq_frq)


## Overview

Instances with local SSDs provide high I/O performance. They are suitable for scenarios that place high demands on storage I/O performance and require a high availability architecture at the application layer. For example, they are suitable for NoSQL databases, massively parallel processing \(MPP\) data warehouses, and distributed file systems.

Instances with local SSDs are suitable for enterprises that provide online services such as online gaming, e-commerce, live video streaming, and media. These instances can satisfy the requirements that I/O-intensive applications have for low latency and high I/O performance of Elastic Block Storage \(EBS\) devices.

Instances with local SSDs have the following features:

-   Deliver up to hundreds of thousands of low-latency random read/write IOPS for large databases.
-   Offer a maximum sequential read/write throughput of several gibibytes per second in big data, parallel computing, and other large dataset scenarios.
-   Use local NVMe SSDs to deliver hundreds of thousands of random read/write IOPS with single-digit microsecond latency.

When you use instances with local SSDs, take note of the following items:

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

## i3g, instance family with local SSDs

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4, which is designed for high-performance databases.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only enhanced SSDs \(ESSDs\).
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Online transaction processing \(OLTP\) and high-performance relational databases
    -   NoSQL databases such as Cassandra, MongoDB, and HBase
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:--------------------|:-------------------------------------------|---------------------------------------------|:---------------------------------------------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.i3g.2xlarge|8|32.0|1 × 447|3.0|10|1,750|250|8|4|15|52.5|2.0|
|ecs.i3g.4xlarge|16|64.0|1 × 894|5.0|10|3,500|300|8|8|15|84.0|3.0|
|ecs.i3g.8xlarge|32|128.0|2 × 894|12.0|None|7,000|600|8|8|300|157.5|5.0|
|ecs.i3g.13xlarge|52|192.0|3 × 894|16.0|None|12,000|900|16|8|300|252.0|8.0|
|ecs.i3g.26xlarge|104|384.0|6 × 894|32.0|None|24,000|1,800|32|15|300|500.0|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i3, instance family with local SSDs

The instance family is in invitational preview.

Features

-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency, and allows damaged disks to be isolated online.
-   Compute:
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases such as Cassandra and MongoDB
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:--------------------|:-------------------------------------------|---------------------------------------------|:---------------------------------------------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.i3.xlarge|4|32.0|1 × 894|1.5|10|1,000|250|4|4|15|40|1.5|
|ecs.i3.2xlarge|8|64.0|1 × 1,788|2.5|10|1,600|250|8|4|15|50|2.0|
|ecs.i3.4xlarge|16|128.0|2 × 1,788|5.0|10|3,000|300|8|8|300|80|3.0|
|ecs.i3.8xlarge|32|256.0|4 × 1,788|10.0|None|6,000|600|16|8|300|150|5.0|
|ecs.i3.13xlarge|52|384.0|6 × 1,788|16.0|None|9,000|900|32|7|300|240|8.0|
|ecs.i3.26xlarge|104|768.0|12 × 1,788|32.0|None|24,000|1,800|32|15|300|480|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i2, instance family with local SSDs

Features

-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8, which is designed for high-performance databases.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases such as Cassandra, MongoDB, and HBase
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|-------------------------|
|ecs.i2.xlarge|4|32.0|1 × 894|1.0|500|2|3|10|Up to 16|
|ecs.i2.2xlarge|8|64.0|1 × 1,788|2.0|1,000|2|4|10|Up to 16|
|ecs.i2.4xlarge|16|128.0|2 × 1,788|3.0|1,500|4|8|20|Up to 16|
|ecs.i2.8xlarge|32|256.0|4 × 1,788|6.0|2,000|8|8|20|Up to 16|
|ecs.i2.16xlarge|64|512.0|8 × 1,788|10.0|4,000|16|8|20|Up to 16|
|ecs.i2d.21xlarge|84|712.0|4 × 3,570|25.0|4,000|32|16|20|Up to 16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i2g, instance family with local SSDs

Features

-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4, which is designed for high-performance databases.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases such as Cassandra, MongoDB, and HBase
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.i2g.2xlarge|8|32.0|1 × 894|2.0|1,000|2|4|10|
|ecs.i2g.4xlarge|16|64.0|1 × 1,788|3.0|1,500|4|8|20|
|ecs.i2g.8xlarge|32|128.0|2 × 1,788|6.0|2,000|8|8|20|
|ecs.i2g.16xlarge|64|256.0|4 × 1,788|10.0|4,000|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i2ne, instance family with local SSDs

Features

-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8, which is designed for high-performance databases.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
    -   Provides a bandwidth of up to 20 Gbit/s.
-   Suits the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases such as Cassandra, MongoDB, and HBase
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|-------------------------|
|ecs.i2ne.xlarge|4|32.0|1 × 894|1.5|500|2|3|10|Up to 16|
|ecs.i2ne.2xlarge|8|64.0|1 × 1,788|2.5|1,000|2|4|10|Up to 16|
|ecs.i2ne.4xlarge|16|128.0|2 × 1,788|5.0|1,500|4|8|20|Up to 16|
|ecs.i2ne.8xlarge|32|256.0|4 × 1,788|10.0|2,000|8|8|20|Up to 16|
|ecs.i2ne.16xlarge|64|512.0|8 × 1,788|20.0|4,000|16|8|20|Up to 16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i2gne, instance family with local SSDs

Features

-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4, which is designed for high-performance databases.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Provides high network performance based on large computing capacity.
    -   Provides a bandwidth of up to 20 Gbit/s.
-   Suits the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases such as Cassandra, MongoDB, and HBase
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.i2gne.2xlarge|8|32.0|1 × 894|2.5|1,000|2|4|10|
|ecs.i2gne.4xlarge|16|64.0|1 × 1,788|5.0|1,500|4|8|20|
|ecs.i2gne.8xlarge|32|128.0|2 × 1,788|10.0|2,000|8|8|20|
|ecs.i2gne.16xlarge|64|256.0|4 × 1,788|20.0|4,000|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

## i1, instance family with local SSDs

Features

-   Is attached with high-performance local NVMe SSDs that deliver high IOPS, high I/O throughput, and low latency.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4, which is designed for high-performance databases.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases such as Cassandra and MongoDB
    -   Search scenarios that use solutions such as Elasticsearch

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.i1.xlarge|4|16.0|2 × 104|0.8|200|1|3|10|
|ecs.i1.2xlarge|8|32.0|2 × 208|1.5|400|1|4|10|
|ecs.i1.3xlarge|12|48.0|2 × 312|2.0|400|1|6|10|
|ecs.i1.4xlarge|16|64.0|2 × 416|3.0|500|2|8|20|
|ecs.i1-c5d1.4xlarge|16|64.0|2 × 1,456|3.0|400|2|8|20|
|ecs.i1.6xlarge|24|96.0|2 × 624|4.5|600|2|8|20|
|ecs.i1.8xlarge|32|128.0|2 × 832|6.0|800|3|8|20|
|ecs.i1-c10d1.8xlarge|32|128.0|2 × 1,456|6.0|800|3|8|20|
|ecs.i1.14xlarge|56|224.0|2 × 1,456|10.0|1,200|4|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   For more information about the performance metrics of local SSDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

