---
keyword: [cloud disk performance, EBS performance, ESSD performance, performance metric, IOPS, capacity, throughput, throughput]
---

# EBS performance

This topic describes the performance metrics and specifications of various Elastic Block Storage \(EBS\) devices, such as cloud disks and local disks.

## Performance metrics

The key metrics used to measure EBS performance include input/output operations per second \(IOPS\), throughput, and latency. Some EBS devices also have capacity requirements. For example, enhanced SSDs \(ESSDs\) at different performance levels \(PLs\) have different capacity ranges.

-   IOPS

    The IOPS metric measures the number of read/write operations that can be performed per second. This metric indicates the performance of transaction-intensive applications such as databases. A standard SSD can implement the committed IOPS performance only when it is attached to an I/O optimized instance. For more information about I/O optimized instances, see [Instance families](/intl.en-US/Instance/Instance families.md). Common IOPS performance metrics that are measured include sequential and random operations. The following table describes these performance metrics.

    |Metric|Description|Data access method|
    |:-----|:----------|:-----------------|
    |Total IOPS|The total number of I/O operations per second.|Randomly and sequentially access locations in storage devices.|
    |Random read IOPS|The average number of random read I/O operations per second.|Randomly access locations in storage devices.|
    |Random write IOPS|The average number of random write I/O operations per second.|
    |Sequential read IOPS|The average number of sequential read I/O operations per second.|Sequentially access locations in storage devices.|
    |Sequential write IOPS|The average number of sequential write I/O operations per second.|

-   Throughput

    The throughput metric measures the amount of data transferred per second. Unit: MB/s. This metric indicates the performance of applications such as Hadoop offline computing applications that require a large number of sequential read/write operations.

-   Latency

    Latency is the amount of time required for an EBS device to process an I/O request. Unit: s, ms, or μs. High latency may cause performance degradation or errors in applications that require low latency.

    -   For latency-sensitive applications such as databases, we recommend that you use ESSDs, standard SSDs, or local SSDs.
    -   For applications such as Hadoop offline computing applications that need high throughput but not low latency, we recommend that you use Elastic Compute Service \(ECS\) instances of the d1 or d1ne instance family that are attached with local SATA HDDs.
-   Capacity

    Capacity is the size of storage space. Unit: TiB, GiB, MiB, or KiB. EBS capacity is measured in binary units. For example, 1 GiB equals 1,024 MiB.

    You cannot use the capacity as a metric to measure the performance of EBS devices. However, the performance of EBS devices varies based on capacity. The larger the capacity of an EBS device is, the stronger its processing capabilities are. EBS devices of the same type have the same I/O performance per unit capacity. However, the performance of each disk increases based on capacity until it reaches the upper limit performance for that single disk. ESSDs of different capacity ranges have different PLs.


For more information about how to test the performance of different types of EBS devices, see [Test the performance of Elastic Block Storage devices](/intl.en-US/Block Storage/Performance/Test the performance of Elastic Block Storage devices.md) or [Test the IOPS performance of an enhanced SSD](/intl.en-US/Block Storage/Performance/Test the IOPS performance of an enhanced SSD.md).

## Disk performance

The following table describes the performance and typical scenarios of different categories of disks.

|Performance category|ESSD|Standard SSD|Ultra disk|Basic disk 3|
|:-------------------|:---|:-----------|:---------|------------|
|PL|PL3|PL2|PL1|PL0|None|None|None|
|Maximum capacity of a single disk \(GiB\)|1261~32768|461~32768|20~32768|40~32768|32768|32768|2000|
|Maximum IOPS|1000000|100000|50000|10000|25,000 1|5000|Several hundreds|
|Maximum throughput \(Mbit/s\)|4000|750|350|180|300 1|140|30~40|
|Formula to calculate the IOPS of a single disk 2|min\{1800 + 50 × Capacity, 1000000\}|min\{1800 + 50 × Capacity, 100000\}|min\{1800 + 50 × Capacity, 50000\}|min\{1800 + 12 × Capacity, 10000\}|min\{1800 + 30 × Capacity, 25000\}|min\{1800 + 8 × Capacity, 5000\}|None|
|Formula to calculate the throughput of a single disk \(MB/s\) 2|min\{120 + 0.5 × Capacity, 4000\}|min\{120 + 0.5 × Capacity, 750\}|min\{120 + 0.5 × Capacity, 350\}|min\{100 + 0.25 × Capacity, 180\}|min\{120 + 0.5 × Capacity, 300\}|min\{100 + 0.15 × Capacity, 140\}|None|
|Data durability|99.9999999%|99.9999999%|99.9999999%|99.9999999%|99.9999999%|99.9999999%|99.9999999%|
|Average single-channel random write latency in milliseconds \(block size = 4 KB\)|0.2|0.3~0.5|0.5~2|1~3|5~10|
|API parameter value|cloud\_essd|cloud\_ssd|cloud\_efficiency|cloud|
|Scenario|-   Large online transaction processing \(OLTP\) databases: relational databases such as MySQL, PostgreSQL, Oracle, and SQL Server databases
-   NoSQL databases: non-relational databases such as MongoDB, HBase, and Cassandra databases
-   Elasticsearch distributed logs: Elasticsearch, Logstash, and Kibana \(ELK\) log analysis

|-   I/O intensive applications
-   Small and medium-sized relational databases
-   NoSQL databases

|-   Development and test business
-   System disks

|-   Applications that are not frequently accessed or have low I/O loads
-   Applications that require low costs and random I/O operations |

1 The performance of standard SSDs varies based on the sizes of data blocks. Smaller data blocks result in lower throughput and higher IOPS, as described in the following table.

|Data block size \(KiB\)|Maximum IOPS|Throughput \(MB/s\)|
|:----------------------|:-----------|:------------------|
|4|Approximately 25,000|Approximately 100|
|16|Approximately 17,200|Approximately 260|
|32|Approximately 9,600|Approximately 300|
|64|Approximately 4,800|Approximately 300|

2 In the following examples, a standard SSD is used to describe how to calculate the performance of a single disk:

-   Maximum IOPS: The baseline IOPS is 1,800. The performance increases by 30 IOPS per additional GiB of storage. The maximum IOPS is 25,000.
-   Maximum throughput: The baseline throughput is 120 MB/s. The performance increases by 0.5 MB/s per additional GiB of storage. The maximum throughput is 300 MB/s.

3 Basic disks are part of a previous generation of disks and are no longer available for purchase.

## Performance of local disks

For more information about the performance of local NVMe SSDs and SATA HDDs, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).

