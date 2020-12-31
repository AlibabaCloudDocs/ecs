---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Memory optimized instance families

This topic describes the features of memory optimized instance families and lists the instance types of each family.

-   Recommended instance families
    -   [re6p, persistent memory optimized instance family](#section_k8y_u9u_vax)
    -   [r6a, memory optimized instance family](#section_zx4_s2u_rlk)
    -   [r6e, memory optimized instance family with enhanced performance](#section_6x3_goi_4ou)
    -   [r6, memory optimized instance family](#section_qcw_6gn_p4u)
    -   [re6, memory optimized instance family with enhanced performance](#section_c9u_7hq_srd)
    -   [r5, memory optimized instance family](#section_5vq_ldx_j20)
-   Other available instance families
    -   [re4, memory optimized instance family with enhanced performance](#section_i3s_oh8_6q4)
    -   [re4e, memory optimized instance family with enhanced performance](#section_6zy_cbu_zum)
    -   [se1ne, memory optimized instance family with enhanced network performance](#section_k1p_8hm_72f)
    -   [se1, memory optimized instance family](#section_s5w_lh9_07j)

## re6p, persistent memory optimized instance family

Features

-   Uses Intel ®OptaneTM persistent memory.

    **Note:** The reliability of data stored in persistent memory depends on the reliability of persistent memory devices and the physical servers to which these devices are attached. This increases risks of single points of failure. To ensure the reliability of application data, we recommend that you implement data redundancy at the application layer and use cloud disks for long-term data storage.

-   Supports configuring different usage modes of persistent memory on some instance types. You can use the persistent memory as memory or local SSDs.

    **Note:** For more information, see [Configure the usage mode of persistent memory](/intl.en-US/Instance/Instance type families/Memory optimized instance families/Configure the usage mode of persistent memory.md).

-   Provides the ecs.re6p-redis.<nx\>large instances types for Redis applications.

    **Note:** ecs.re6p-redis.<nx\>large instance types are exclusively provided for Redis applications. By default, the persistent memory of the dedicated instance type is used as memory. You cannot re-configure the persistent memory of a dedicated instance type as a local SSD disk. For more information about how to deploy an Redis application, see [Deploy Redis applications on re6p instances](/intl.en-US/Instance/Instance type families/Memory optimized instance families/Deploy Redis applications on re6p instances.md).

-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8269CY \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
-   Is an instance family in which all instances are I/O optimized.
-   Supports enhanced SSDs \(ESSDs\), standard SSDs, and ultra disks.
-   Supports VPCs only.
-   Applies to the following scenarios:
    -   Redis and other NoSQL databases such as Cassandra and MongoDB
    -   Structured databases such as MySQL
    -   I/O intensive applications such as e-commerce, online games, and media applications
    -   Elasticsearch
    -   Live video streaming, instant messaging, and room-based online games
    -   High-performance relational databases and online transaction processing \(OLTP\) systems

Instance types

|Instance type|vCPU|DRAM \(GiB\)|AEP memory \(GiB\)|Local storage \(GiB\)|Base bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-----------|------------------|---------------------|-------------------------|------------------------------|:------------------------------|------------|-----------------|----------|:---------------------------------|----------|-------------------------|
|ecs.re6p.large|2|8.0|31.5|None|1.0|3.0|300|Yes|Up to 250|2|2|10|1.0|
|ecs.re6p.xlarge|4|16.0|63.0|None|1.5|5.0|500|Yes|Up to 250|4|3|20|1.5|
|ecs.re6p.2xlarge|8|32.0|126.0|None|2.5|10.0|800|Yes|Up to 250|8|4|25|2.0|
|ecs.re6p.13xlarge|52|192.0|756.0|None|12.5|None|3,000|Yes|900|32|7|100|8.0|
|ecs.re6p.26xlarge|104|384.0|1512.0|None|25.0|None|600|Yes|1,800|32|15|200|16,0|
|ecs.re6p-redis.large|2|8.0|31.5|None|1.0|3.0|300|Yes|Up to 250|2|2|10|1.0|
|ecs.re6p-redis.xlarge|4|16.0|63.0|None|1.5|5.0|500|Yes|Up to 250|4|3|20|1.5|
|ecs.re6p-redis.2xlarge|8|32.0|126.0|None|2.5|10.0|800|Yes|Up to 250|8|4|25|2.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
-   For answers to commonly asked questions about persistent memory optimized instances, see [ECS instance FAQ](/intl.en-US/Instance/Instance FAQ.md).

## r6a, memory optimized instance family

r6a is in invitational preview. To use r6a,[submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Uses the SHENLONG architecture to provide predictable and consistent high performance and reduce virtualization overheads.
-   Compute:
    -   Uses 2.6 GHz AMD EPYC TM ROME processors that deliver a maximum turbo frequency of 3.3 GHz for consistent computing performance.
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Allows you to enable or disable hyper-threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Provides an ultra-high packet forwarding rate.
    -   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Video encoding and decoding
    -   Scenarios where large volumes of packets are received and transmitted
    -   In-memory databases
    -   Hadoop clusters, Spark clusters, and other memory intensive enterprise applications
    -   Test and development, such as DevOps

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Base bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|ENIs \(including one primary ENI\)|IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|-------------------------|------------------------------|:------------------------------|:-----------|:---------------------------------|----------|-------------------------|
|ecs.r6a.large|2|16.0|None|1.0|10.0|900|Yes|2|12.5|1.0|
|ecs.r6a.xlarge|4|32.0|None|1.5|10.0|1,000|Yes|3|20|1.5|
|ecs.r6a.2xlarge|8|64.0|None|2.5|10.0|1,600|Yes|4|30|2.0|
|ecs.r6a.4xlarge|16|128.0|None|5.0|10.0|2,000|Yes|8|60|3.0|
|ecs.r6a.8xlarge|32|256.0|None|8.0|10.0|3,000|Yes|7|75|4,0|
|ecs.r6a.16xlarge|64|512.0|None|16.0|None|6,000|Yes|8|150|8.0|
|ecs.r6a.32xlarge|128|1024.0|None|32.0|None|12,000|Yes|15|300|16.0|
|ecs.r6a.64xlarge|256|2048.0|None|64.0|None|24,000|Yes|15|600|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## r6e, memory optimized instance family with enhanced performance

Features

-   Uses the SHENLONG architecture to provide predictable and consistent high performance and reduce virtualization overheads. In addition, improves storage performance, network performance, and computing stability by an order of magnitude through fast path acceleration of chips.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs only.
-   Provides high network and storage I/O performance based on large computing capacity.

    **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Provides an ultra-high packet forwarding rate.

    **Note:** The maximum network performance varies with instance families. For higher concurrent connection capabilities, we recommend that you use g5ne.

-   Offers a CPU-to-memory ratio of 1:8.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8269 processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
-   Allows you to enable or disable hyper-threading.

    **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Applies to the following scenarios:
    -   Scenarios such as on-screen video comments and telecom data forwarding where large volumes of packets are received and transmitted
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory intensive enterprise applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|--------------------|:------------------------------|:-----------|-----------------|:---------|:---------------------------------|----------------------------|----------|-------------------------|
|ecs.r6e.large|2|16.0|None|A burstable bandwidth of up to 10.0|900|Yes|Up to 250|2|3|6|20|1.0|
|ecs.r6e.xlarge|4|32.0|None|A burstable bandwidth of up to 10.0|1,000|Yes|Up to 250|4|4|15|40|1.5|
|ecs.r6e.2xlarge|8|64.0|None|A burstable bandwidth of up to 10.0|1,600|Yes|Up to 250|8|4|15|50|2.0|
|ecs.r6e.4xlarge|16|128.0|None|A burstable bandwidth of up to 10.0|3,000|Yes|300|8|8|30|80|3.0|
|ecs.r6e.8xlarge|32|256.0|None|10.0|6,000|Yes|600|16|8|30|150|5.0|
|ecs.r6e.13xlarge|52|384.0|None|16.0|9,000|Yes|900|32|7|30|240|8.0|
|ecs.r6e.26xlarge|104|768.0|None|32.0|24,000|Yes|1,800|32|15|30|480|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other metrics of the network.

## r6, memory optimized instance family

Features

-   Uses the SHENLONG architecture to provide predictable and consistent high performance and reduce virtualization overheads.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.

    **Note:** The maximum performance of disks varies with instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

-   Provides high storage I/O performance based on large compute capacity.

    **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Provides an ultra-high packet forwarding rate.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8269CY \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
-   Offers a CPU-to-memory ratio of 1:8.
-   Allows you to enable or disable hyper-threading.

    **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Provides high network performance based on large computing capacity.
-   Supports changes to g6 or c6 instance families.
-   Applies to the following scenarios:
    -   Scenarios such as on-screen video comments and telecom data forwarding where large volumes of packets are received and transmitted
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory intensive enterprise applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Base bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:------------------------|------------------------------|:------------------------------|:-----------|-----------------|:---------|:---------------------------------|----------------------------|----------|-------------------------|
|ecs.r6.large|2|16.0|None|1.0|3.0|300|Yes|Up to 250|2|2|6|10|1|
|ecs.r6.xlarge|4|32.0|None|1.5|5.0|500|Yes|Up to 250|4|3|10|20|1.5|
|ecs.r6.2xlarge|8|64.0|None|2.5|8.0|800|Yes|Up to 250|8|4|10|25|2|
|ecs.r6.3xlarge|12|96.0|None|4.0|10.0|900|Yes|Up to 250|8|6|10|30|2.5|
|ecs.r6.4xlarge|16|128.0|None|5.0|10.0|1,000|Yes|300|8|8|20|40|3|
|ecs.r6.6xlarge|24|192.0|None|7.5|10.0|1,500|Yes|450|12|8|20|50|4|
|ecs.r6.8xlarge|32|256.0|None|10.0|None|2,000|Yes|600|16|8|20|60|5|
|ecs.r6.13xlarge|52|384.0|None|12.5|None|3,000|Yes|900|32|7|20|100|8|
|ecs.r6.26xlarge|104|768.0|None|25.0|None|6,000|Yes|1,800|32|15|20|200|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## re6, memory optimized instance family with enhanced performance

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Optimized for high-performance databases, in-memory databases, and other memory intensive enterprise applications.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8269CY \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
-   Offers a CPU-to-memory ratio of 1:15 and up to 3 TiB memory.
-   Applies to the following scenarios:
    -   High-performance databases and in-memory databases such as SAP HANA
    -   Memory intensive applications
    -   Big data processing engines such as Apache Spark and Presto

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|----------|-------------------------|
|ecs.re6.13xlarge|52|768.0|None|10.0|1,800|Yes|16|7|20|50|4|
|ecs.re6.26xlarge|104|1536.0|None|16.0|3,000|Yes|32|7|20|100|8|
|ecs.re6.52xlarge|208|3072.0|None|32.0|6,000|Yes|32|15|20|200|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## r5, memory optimized instance family

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.

    **Note:** The maximum performance of disks varies with instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

-   Provides an ultra-high packet forwarding rate.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) or Intel ® Xeon ® Paltinum 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Offers a CPU-to-memory ratio of 1:8.
-   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Scenarios such as on-screen video comments and telecom data forwarding where large volumes of packets are received and transmitted
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory intensive enterprise applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.r5.large|2|16.0|None|1.0|300|Yes|2|2|6|
|ecs.r5.xlarge|4|32.0|None|1.5|500|Yes|2|3|10|
|ecs.r5.2xlarge|8|64.0|None|2.5|800|Yes|2|4|10|
|ecs.r5.3xlarge|12|96.0|None|4.0|900|Yes|4|6|10|
|ecs.r5.4xlarge|16|128.0|None|5.0|1,000|Yes|4|8|20|
|ecs.r5.6xlarge|24|192.0|None|7.5|1,500|Yes|6|8|20|
|ecs.r5.8xlarge|32|256.0|None|10.0|2,000|Yes|8|8|20|
|ecs.r5.16xlarge|64|512.0|None|20.0|4,000|Yes|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## re4, memory optimized instance family with enhanced performance

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Optimized for high-performance databases, in-memory databases, and other memory intensive enterprise applications.
-   Uses 2.2 GHz Intel ® Xeon ® E7 8880 v4\(Broadwell\) processors that deliver a maximum turbo frequency of 2.4 GHz for consistent computing performance.
-   Offers a CPU-to-memory ratio of 1:12 and up to 1,920 GiB memory.
-   The ecs.re4.20xlarge and ecs.re4.40xlarge instance types are SAP HANA-certified.
-   Applies to the following scenarios:
    -   High-performance databases and in-memory databases such as SAP HANA
    -   Memory intensive applications
    -   Big data processing engines such as Apache Spark and Presto

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.re4.20xlarge|80|960.0|None|15.0|2,000|Yes|16|8|20|
|ecs.re4.40xlarge|160|1920.0|None|30.0|4,500|Yes|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## re4e, memory optimized instance family with enhanced performance

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Optimized for high-performance databases, in-memory databases, and other memory intensive enterprise applications.
-   Uses 2.2 GHz Intel ® Xeon ® E7 8880 v4\(Broadwell\) processors that deliver a maximum turbo frequency of 2.4 GHz for consistent computing performance.
-   Offers a CPU-to-memory ratio of 1:24 and up to 3,840 GiB memory.
-   Applies to the following scenarios:
    -   High-performance databases and in-memory databases such as SAP HANA
    -   Memory intensive applications
    -   Big data processing engines such as Apache Spark and Presto

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.re4e.40xlarge|160|3840.0|None|30.0|4,500|Yes|16|15|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## se1ne, memory optimized instance family with enhanced network performance

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Offers a CPU-to-memory ratio of 1:8.
-   Provides an ultra-high packet forwarding rate.
-   Uses 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) or Intel ® Xeon ® Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Scenarios such as on-screen video comments and telecom data forwarding where large volumes of packets are received and transmitted
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory intensive enterprise applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.se1ne.large|2|16.0|None|1.0|300|Yes|2|2|6|
|ecs.se1ne.xlarge|4|32.0|None|1.5|500|Yes|2|3|10|
|ecs.se1ne.2xlarge|8|64.0|None|2.0|1,000|Yes|4|4|10|
|ecs.se1ne.3xlarge|12|96.0|None|2.5|1,300|Yes|4|6|10|
|ecs.se1ne.4xlarge|16|128.0|None|3.0|1,600|Yes|4|8|20|
|ecs.se1ne.6xlarge|24|192.0|None|4.5|2,000|Yes|6|8|20|
|ecs.se1ne.8xlarge|32|256.0|None|6.0|2,500|Yes|8|8|20|
|ecs.se1ne.14xlarge|56|480.0|None|10.0|4,500|Yes|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## se1, memory optimized instance family

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Offers a CPU-to-memory ratio of 1:8.
-   Uses 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) processors for consistent computing performance.
-   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory intensive enterprise applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.se1.large|2|16.0|None|0.5|100|No|1|2|6|
|ecs.se1.xlarge|4|32.0|None|0.8|200|No|1|3|10|
|ecs.se1.2xlarge|8|64.0|None|1.5|400|No|1|4|10|
|ecs.se1.4xlarge|16|128.0|None|3.0|500|No|2|8|20|
|ecs.se1.8xlarge|32|256.0|None|6.0|800|No|3|8|20|
|ecs.se1.14xlarge|56|480.0|None|10.0|1,200|No|4|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## References

-   [Instance families](/intl.en-US/Instance/Instance families.md)
-   [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md)

