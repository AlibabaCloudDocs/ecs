---
keyword: [disk performance, Elastic Block Storage performance, performance, I/O, ECS]
---

# Storage I/O performance

Storage I/O performance, also known as storage read/write performance, is the performance that can be delivered when disks are attached to instances of different ECS instance types. Metrics of storage I/O performance include IOPS and throughput.

## I/O size

I/O \(Input/Output or Read/Write\) is random or sequential data requests initiated by an application. The volume of I/O requests is also known as the I/O size in KiB, such as 4 KiB, 256 KiB, and 1,024 KiB.

When you design the underlying storage architecture or select an instance type, you must consider metrics such as IOPS, I/O size, and throughput. You can use the following formula to calculate throughput based on the I/O size and IOPS: IOPS × I/O size = Throughput. You can select different Elastic Block Storage devices and instance types based on the I/O request features of applications to achieve the best results.

-   For the applications such as offline analysis and data warehousing applications that require a large I/O size, we recommend that you select the big data instance families that deliver high throughput.
-   For the applications such as OLTP databases and enterprise-level applications like SAP that require low-latency, random, and small-sized I/O, we recommend that you select enhanced SSDs \(ESSDs\) and standard SSDs that deliver high IOPS.

For more information about IOPS and throughput, see [EBS performance](/intl.en-US/Block Storage/Performance/EBS performance.md).

## Storage I/O performance of instances

**Note:** This section and subsequent sections apply only to the new generation of enterprise-level instance families, including hfg7, hfc7, hfr7, g6e, c6e, r6e, and g5se. For more information, see [Storage I/O performance of the new generation of enterprise-level instance families](#section_9h4_dr9_6nh). These sections are not applicable to local disks.

The new generation of enterprise-level instance families of Alibaba Cloud ECS provides isolation of storage I/O performance. Dedicated storage bandwidths are assigned to ECS instances and disks to avoid storage I/O preemption among ECS instances. The new generation of enterprise-level instance families ensures consistent storage I/O performance of applications even during peak hours.

If your business application is one of the following I/O-sensitive applications that require consistent storage I/O performance, we recommend that you select a new-generation instance family that provides isolation of storage I/O performance:

-   Large and medium-sized databases, such as Oracle, MySQL, SQL Server, PostgreSQL, Cassandra, and MongoDB databases
-   Enterprise-level applications such as ERP and CRM

## Relationship between instance types and storage I/O performance

The storage I/O performance of ECS instances varies based on their instance families, instance types, and attached disks. The storage I/O performance of an instance is subject to the instance type. The higher specifications an instance type has, the higher storage I/O performance \(IOPS and throughput\) it provides.

After you create an ECS instance and attach disks to it, the final storage I/O performance of the ECS instance is determined as described in the following section:

-   Scenario 1: If the total storage performance of the attached disks exceeds the maximum storage I/O performance that the instance type can deliver, the final storage I/O performance of the instance is limited to the maximum storage I/O performance of that instance type.
-   Scenario 2: If the total storage performance of the attached disks does not exceed the maximum storage I/O performance that the instance type can deliver, the final storage I/O performance of the instance is limited to the total storage I/O performance of the disks.

![Instances and their storage I/O performance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2182909951/p73635.png)

For example, the ecs.g6.8xlarge instance type can deliver up to 60,000 IOPS. If a 1,600 GiB PL2 ESSD is attached to an instance of this instance type and the IOPS of the PL2 ESSD is 81,800, the maximum storage IOPS of the instance is still 60,000. For information about the performance levels of ESSDs, see [ESSDs](/intl.en-US/Block Storage/Block Storage overview/ESSDs.md).

When you understand the relationship between instance storage performance and disk storage performance, you can choose instance types and Elastic Block Storage devices based on their performance specifications. This prevents performance bottlenecks caused by improper configurations.

## Storage I/O performance of the new generation of enterprise-level instance families

The following tables list the storage I/O performance of the new generation of enterprise-level instance families. For information about other specifications of the instance families, see [Instance families](/intl.en-US/Instance/Instance families.md).

**Note:** In these tables, the maximum IOPS is measured at an I/O size of 4 KiB and the maximum throughput is measured at an I/O size of 1,024 KiB. For information about test methods, see [Test the performance of Elastic Block Storage devices](/intl.en-US/Block Storage/Performance/Test the performance of Elastic Block Storage devices.md).

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.hfg7.large|20|1.0|125|
|ecs.hfg7.xlarge|30|1.5|187.5|
|ecs.hfg7.2xlarge|45|2.0|250|
|ecs.hfg7.3xlarge|60|2.5|312.5|
|ecs.hfg7.4xlarge|75|3.0|375|
|ecs.hfg7.6xlarge|90|4.0|500|
|ecs.hfg7.8xlarge|105|5.0|625|
|ecs.hfg7.12xlarge|150|8.0|1000|
|ecs.hfg7.24xlarge|300|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.hfc7.large|20|1.0|125|
|ecs.hfc7.xlarge|30|1.5|187.5|
|ecs.hfc7.2xlarge|45|2.0|250|
|ecs.hfc7.3xlarge|60|2.5|312.5|
|ecs.hfc7.4xlarge|75|3.0|375|
|ecs.hfc7.6xlarge|90|4.0|500|
|ecs.hfc7.8xlarge|105|5.0|625|
|ecs.hfc7.12xlarge|150|8.0|1000|
|ecs.hfc7.24xlarge|300|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.hfr7.large|20|1.0|125|
|ecs.hfr7.xlarge|30|1.5|187.5|
|ecs.hfr7.2xlarge|45|2.0|250|
|ecs.hfr7.3xlarge|60|2.5|312.5|
|ecs.hfr7.4xlarge|75|3.0|375|
|ecs.hfr7.6xlarge|90|4.0|500|
|ecs.hfr7.8xlarge|105|5.0|625|
|ecs.hfr7.12xlarge|150|8.0|1000|
|ecs.hfr7.24xlarge|300|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.g6se.large|30|1.5|187.5|
|ecs.g6se.xlarge|60|2.0|250|
|ecs.g6se.2xlarge|90|3.0|375|
|ecs.g6se.4xlarge|150|5.0|625|
|ecs.g6se.8xlarge|300|10.0|1250|
|ecs.g6se.13xlarge|500|16.0|2000|
|ecs.g6se.26xlarge|900|32.0|4000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.g6t.large|20|1.0|125|
|ecs.g6t.xlarge|40|1.5|187.5|
|ecs.g6t.2xlarge|50|2.0|250|
|ecs.g6t.4xlarge|80|3.0|375|
|ecs.g6t.8xlarge|150|5.0|625|
|ecs.g6t.13xlarge|200|8.0|1000|
|ecs.g6t.26xlarge|480|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.c6t.large|20|1.0|125|
|ecs.c6t.xlarge|40|1.5|187.5|
|ecs.c6t.2xlarge|50|2.0|250|
|ecs.c6t.4xlarge|80|3.0|375|
|ecs.c6t.8xlarge|150|5.0|625|
|ecs.c6t.13xlarge|240|8.0|1000|
|ecs.c6t.26xlarge|480|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.g6e.large|20|1.0|125|
|ecs.g6e.xlarge|40|1.5|187.5|
|ecs.g6e.2xlarge|50|2.0|250|
|ecs.g6e.4xlarge|80|3.0|375|
|ecs.g6e.8xlarge|150|5.0|625|
|ecs.g6e.13xlarge|240|8.0|1000|
|ecs.g6e.26xlarge|480|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.c6e.large|20|1.0|125|
|ecs.c6e.xlarge|40|1.5|187.5|
|ecs.c6e.2xlarge|50|2.0|250|
|ecs.c6e.4xlarge|80|3.0|375|
|ecs.c6e.8xlarge|150|5.0|625|
|ecs.c6e.13xlarge|240|8.0|1000|
|ecs.c6e.26xlarge|480|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.r6e.large|20|1.0|125|
|ecs.r6e.xlarge|40|1.5|187.5|
|ecs.r6e.2xlarge|50|2.0|250|
|ecs.r6e.4xlarge|80|3.0|375|
|ecs.r6e.8xlarge|150|5.0|625|
|ecs.r6e.13xlarge|240|8.0|1000|
|ecs.r6e.26xlarge|480|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.g6.large|10|1.0|125|
|ecs.g6.xlarge|20|1.5|187.5|
|ecs.g6.2xlarge|25|2.0|250|
|ecs.g6.3xlarge|30|2.5|312.5|
|ecs.g6.4xlarge|40|3.0|375|
|ecs.g6.6xlarge|50|4.0|500|
|ecs.g6.8xlarge|60|5.0|625|
|ecs.g6.13xlarge|100|8.0|1000|
|ecs.g6.26xlarge|200|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.c6.large|10|1.0|125|
|ecs.c6.xlarge|20|1.5|187.5|
|ecs.c6.2xlarge|25|2.0|250|
|ecs.c6.3xlarge|30|2.5|312.5|
|ecs.c6.4xlarge|40|3.0|375|
|ecs.c6.6xlarge|50|4.0|500|
|ecs.c6.8xlarge|60|5.0|625|
|ecs.c6.13xlarge|100|8.0|1000|
|ecs.c6.26xlarge|200|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.r6.large|10|1.0|125|
|ecs.r6.xlarge|20|1.5|187.5|
|ecs.r6.2xlarge|25|2.0|250|
|ecs.r6.3xlarge|30|2.5|312.5|
|ecs.r6.4xlarge|40|3.0|375|
|ecs.r6.6xlarge|50|4.0|500|
|ecs.r6.8xlarge|60|5.0|625|
|ecs.r6.13xlarge|100|8.0|1000|
|ecs.r6.26xlarge|200|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.hfg6.large|10|1.0|125|
|ecs.hfg6.xlarge|20|1.5|187.5|
|ecs.hfg6.2xlarge|25|2.0|250|
|ecs.hfg6.3xlarge|30|2.5|312.5|
|ecs.hfg6.4xlarge|40|3.0|375|
|ecs.hfg6.6xlarge|50|4.0|500|
|ecs.hfg6.8xlarge|60|5.0|625|
|ecs.hfg6.10xlarge|100|8.0|1000|
|ecs.hfg6.16xlarge|120|10.0|1250|
|ecs.hfg6.20xlarge|200|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.hfc6.large|10|1.0|125|
|ecs.hfc6.xlarge|20|1.5|187.5|
|ecs.hfc6.2xlarge|25|2.0|250|
|ecs.hfc6.3xlarge|30|2.5|312.5|
|ecs.hfc6.4xlarge|40|3.0|375|
|ecs.hfc6.6xlarge|50|4.0|500|
|ecs.hfc6.8xlarge|60|5.0|625|
|ecs.hfc6.10xlarge|100|8.0|1000|
|ecs.hfc6.16xlarge|120|10.0|1250|
|ecs.hfc6.20xlarge|200|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.hfr6.large|10|1.0|125|
|ecs.hfr6.xlarge|20|1.5|187.5|
|ecs.hfr6.2xlarge|25|2.0|250|
|ecs.hfr6.3xlarge|30|2.5|312.5|
|ecs.hfr6.4xlarge|40|3.0|375|
|ecs.hfr6.6xlarge|50|4.0|500|
|ecs.hfr6.8xlarge|60|5.0|625|
|ecs.hfr6.10xlarge|100|8.0|1000|
|ecs.hfr6.16xlarge|120|10.0|1250|
|ecs.hfr6.20xlarge|200|16.0|2000|

|Instance type|Maximum IOPS \(K, 4 KiB I/O\)|Maximum storage bandwidth \(Gbit/s\)|Maximum throughput \(MB/s, 1,024 KiB I/O\)|
|-------------|-----------------------------|------------------------------------|------------------------------------------|
|ecs.g5se.large|30|1.0|125|
|ecs.g5se.xlarge|60|2.0|250|
|ecs.g5se.2xlarge|120|4.0|500|
|ecs.g5se.4xlarge|230|8.0|1000|
|ecs.g5se.6xlarge|340|12.0|1500|
|ecs.g5se.8xlarge|450|15.0|1875|
|ecs.g5se.16xlarge|900|30.0|3750|
|ecs.g5se.18xlarge|1000|32.0|4000|

