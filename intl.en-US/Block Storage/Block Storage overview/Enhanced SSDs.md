---
keyword: [select an ESSD, select ESSDs, commercially available ESSD, high-performance database disk]
---

# Enhanced SSDs

This topic provides general information about Alibaba Cloud enhanced SSDs \(ESSDs\), such as performance levels \(PLs\), usage scenarios, and performance specifications. ESSDs integrate 25 Gigabit Ethernet and remote direct memory access \(RDMA\) technologies to reduce latency and deliver up to 1 million random IOPS.

## Specifications

**Note:** PL0 ESSDs have been put into public preview since August 27, 2020. You cannot modify the PL of PL0 ESSDs when the disks are in public preview.

The API parameter value cloud\_essd indicates ESSDs. ESSDs are divided into four PLs based on the maximum performance per disk.

|ESSD attribute|PL|
|PL3|PL2|PL1|PL0|
|:-------------|:-|
|:--|:--|:--|:--|
|Performance description|Ultra-high maximum concurrent I/O performance and ultra-low I/O latency|High maximum concurrent I/O performance and low I/O latency|Moderate maximum concurrent I/O performance and low I/O latency|Moderate maximum concurrent I/O performance and low I/O latency|
|Capacity range \(GiB\)|1,261~32,768|461~32,768|20~32,768|40~32,768|
|Data durability|99.9999999%|99.9999999%|99.9999999%|99.9999999%|
|Maximum IOPS per disk|1,000,000|100,000|50,000|10,000|
|Maximum throughput per disk \(MB/s\)|4,000|750|350|180|
|Formula for calculating the IOPS per disk|min\{1,800 + 50 × Capacity, 1,000,000\}|min\{1,800 + 50 × Capacity, 100,000\}|min\{1,800 + 50 × Capacity, 50,000\}|min\{1,800 + 12 × Capacity, 10,000\}|
|Formula for calculating the throughput per disk \(MB/s\)|min\{120 + 0.5 × Capacity, 4,000\}|min\{120 + 0.5 × Capacity, 750\}|min\{120 + 0.5 × Capacity, 350\}|min\{100 + 0.25 × Capacity, 180\}|
|Example scenario|Large and medium-sized relational databases for core business and NoSQL databases, and large SAP and Oracle databases|Medium-sized relational databases and NoSQL databases, medium-sized ELK log clusters, and enterprise-level commercial software such as SAP and Oracle|Small and medium-sized MySQL and SQL Server databases, small and medium-sized ELK log clusters, enterprise-level commercial software such as SAP and Oracle, and container applications|Small and medium-sized MySQL and SQL Server databases, small and medium-sized ELK log clusters, enterprise-level commercial software such as SAP and Oracle, and container applications|
|Recommended system or data disks to be replaced with ESSDs in recommended business scenarios|Data disks of instance families that are equipped with local SSDs and have 16 or more vCPUs \(i1, i2, and i2g\)|Data disks of instance families that are equipped with local SSDs \(i1, i2, and i2g\)|Standard SSDs|System disk|

For information about how to perform stress testing on ESSDs, see [Test the IOPS performance of an enhanced SSD](/intl.en-US/Block Storage/Performance/Test the IOPS performance of an enhanced SSD.md).

## Billing methods

ESSDs support pay-as-you-go and subscription billing methods. For more information, see [Create a disk](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a pay-as-you-go disk.md) and [Create a subscription disk]().

For information about the pricing of ESSDs at different PLs, see the Pricing tab on the [Elastic Compute Service](https://www.alibabacloud.com/product/ecs#pricing).

## Scenarios

ESSDs are suitable for the following latency-sensitive applications or I/O intensive business scenarios:

-   Large online transaction processing \(OLTP\) databases: relational databases such as MySQL, PostgreSQL, Oracle, and SQL Server
-   NoSQL databases: non-relational databases such as MongoDB, HBase, and Cassandra databases
-   Elasticsearch distributed logs: Elasticsearch, Logstash, and Kibana \(ELK\) log analysis

## Capacity and PLs of ESSDs

The performance of a storage device is closely related to the capacity of the device. A storage device with larger capacity provides higher data processing capabilities. All ESSDs have the same I/O performance per unit capacity. However, the performance of ESSDs increases linearly together with its capacity until the maximum performance per disk at the PL is reached.

|PL|ESSD capacity range \(GiB\)|Maximum IOPS|Maximum throughput \(MB/s\)|
|--|---------------------------|------------|---------------------------|
|PL0|40~32,768|10,000|180|
|PL1|20~32,768|50,000|350|
|PL2|461~32,768|100,000|750|
|PL3|1,261~32,768|1,000,000|4,000|

-   Example 1: If Alex selects 20 GiB of storage capacity when Alex creates an ESSD in the ECS console, PL1 is the only available option. PL1 ESSDs have a maximum IOPS of 50,000.

    ![Create an ESSD in the ECS console](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1672909951/p49959.png)

-   Example 2: If Alex selects 32,000 GiB of storage capacity when Alex creates an ESSD in the ECS console, all PLs are available. The maximum IOPS is 10,000 for PL0, 50,000 for PL1, 100,000 for PL2, and 1,000,000 for PL3.

    ![Create an ESSD in the ECS console](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1672909951/p129355.png)


## Storage I/O performance of instance types

The storage I/O performance of some new-generation instance families is proportional to the specifications of instance types. For example, in the g6se storage enhanced instance family, the higher the specifications an instance type has, the higher storage IOPS and throughput it can deliver. For more information, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

The following section describes the relationship between instance types and ESSDs in terms of performance:

-   If the total storage performance of ESSDs of an instance does not exceed the maximum storage performance that the instance type can deliver, the instance delivers the total storage performance of the ESSDs.
-   If the total storage performance of ESSDs of an instance exceeds the maximum storage performance that the instance type can deliver, the storage performance of the instance is limited to the maximum storage performance that the instance type can deliver.

The actual storage performance differs among instances of different instance types that have ESSDs at different PLs attached. g6se is used in the following examples:

-   Example 1: Alex creates a 16 GiB instance of the ecs.g6se.xlarge instance type. The maximum IOPS of this instance type is 60,000. Alex then attaches a PL2 ESSD to the instance. The ESSD has a capacity of 2,000 GiB and a maximum IOPS of 100,000. The maximum IOPS of the instance is limited by the maximum IOPS of the instance type to 60,000.
-   Example 2: Alex creates a 64 GiB instance of the ecs.g6se.4xlarge instance type. The maximum IOPS of this instance type is 150,000. Alex then attaches three PL2 ESSDs to the instance. Each ESSD has a capacity of 2,000 GiB and a maximum IOPS of 100,000. The total maximum IOPS of these ESSDs is 300,000. The maximum IOPS of the instance is limited by the maximum IOPS of the instance type to 150,000.
-   Example 3: Alex creates a 64 GiB instance of the ecs.g6se.4xlarge instance type. The maximum IOPS of this instance type is 150,000. Alex then attaches a PL3 ESSD to the instance. The ESSD has a capacity of 2,000 GiB and a maximum IOPS of 101,800. The maximum IOPS of the instance is no longer limited by the maximum IOPS of the instance type, but is limited by the maximum IOPS of the ESSD to 101,800.

## Instance families supported by ESSDs

For information about instance families supported by ESSDs at PL0, PL1, PL2, and PL3, see [Instance families](/intl.en-US/Instance/Instance families.md).

