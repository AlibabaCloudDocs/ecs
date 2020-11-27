---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# General purpose instance families

This topic describes the features of general purpose instance families of ECS and lists the instance types of each family.

-   Recommended instance families
    -   [g6se, storage enhanced instance family](#section_aky_rag_mve)
    -   [g6a, general purpose instance family](#section_jtr_8p8_3y8)
    -   [g6t, security-enhanced general purpose instance family](#section_2dm_67f_8cm)
    -   [g6e, general purpose instance family with enhanced performance](#section_8u6_czr_21b)
    -   [g6, general purpose instance family](#section_gck_bi6_q6l)
    -   [g5, general purpose instance family](#section_kwi_d9k_sbx)
    -   [g5ne, network enhanced instance family](#section_ijd_dkf_hht)
-   Other available instance families

    [sn2ne, general purpose instance family with enhanced network performance](#section_1ki_kxs_w47)


## g6se, storage enhanced instance family

g6se is in invitational preview. To use g6se, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Compute:
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
    -   Offers a CPU-to-memory ratio of 1:4.
-   Storage:
    -   Delivers a sequential read/write performance of up to 32 Gbit/s per instance.
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs \(ESSDs\) only and provides ultra-high I/O performance.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Provides an ultra-high packet forwarding rate.
    -   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   I/O-intensive scenarios, such as medium and large OLTP core databases
    -   Medium and large NoSQL databases
    -   Search and real-time log analytics
    -   Traditional large enterprise-level commercial software, such as SAP

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Base bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|-------------------------|------------------------------|:------------------------------|:-----------|----------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.g6se.large|2|8.0|None|0.7|10.0|300|Yes|2|2|6|30|1.5|
|ecs.g6se.xlarge|4|16.0|None|1.0|10.0|500|Yes|4|3|10|60|2.0|
|ecs.g6se.2xlarge|8|32.0|None|1.5|10.0|800|Yes|8|4|10|90|3.0|
|ecs.g6se.4xlarge|16|64.0|None|3.0|10.0|1,000|Yes|8|8|20|150|5.0|
|ecs.g6se.8xlarge|32|128.0|None|6.0|None|2,000|Yes|16|8|20|300|10.0|
|ecs.g6se.13xlarge|52|192.0|None|8.0|None|3,000|Yes|32|7|20|500|16.0|
|ecs.g6se.26xlarge|104|384.0|None|16.0|None|6,000|Yes|52|15|20|900|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## g6a, general purpose instance family

g6a is in invitational preview. To use g6a, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Provides predictable and consistent ultra-high performance and reduces virtualization overheads based on the X-Dragon architecture.
-   Compute:
    -   Uses 2.6 GHz AMD EPYCTM ROME processors that deliver a maximum turbo frequency of 3.3 GHz for consistent computing performance.
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Allows you to enable or disable Hyper-Threading.

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
    -   Websites and application servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Game servers
    -   Test and development, such as DevOps
    -   Other general purpose enterprise-level applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Base bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|ENIs \(including one primary ENI\)|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|-------------------------|------------------------------|:------------------------------|:-----------|:---------------------------------|---------------|-------------------------|
|ecs.g6a.large|2|8.0|None|1.0|10.0|900|Yes|2|12.5|1.0|
|ecs.g6a.xlarge|4|16.0|None|1.5|10.0|1,000|Yes|3|20|1.5|
|ecs.g6a.2xlarge|8|32.0|None|2.5|10.0|1,600|Yes|4|30|2.0|
|ecs.g6a.4xlarge|16|64.0|None|5.0|10.0|2,000|Yes|8|60|3.0|
|ecs.g6a.8xlarge|32|128.0|None|8.0|10.0|3,000|Yes|7|75|4.0|
|ecs.g6a.16xlarge|64|256.0|None|16.0|None|6,000|Yes|8|150|8.0|
|ecs.g6a.32xlarge|128|512.0|None|32.0|None|12,000|Yes|15|300|16.0|
|ecs.g6a.64xlarge|256|1024.0|None|64.0|None|24,000|Yes|15|600|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## g6t, security-enhanced general purpose instance family

g6t is in invitational preview.

Features

-   Implements trusted boot based on the Trusted Platform Module \(TPM\) chip. During a trusted boot, each module in the boot chain from the underlying hardware to the guest OS is measured and verified.
-   Supports comprehensive monitoring on the IaaS layer and provides trusted capabilities of the whole IaaS layer.
-   Provides predictable and consistent ultra-high performance and reduces virtualization overheads based on the third-generation X-Dragon architecture. g6t improves storage performance, network performance, and computing stability by an order of magnitude through fast path acceleration of X-Dragon chips.
-   Compute:
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Storage:
    -   Supports I/O optimization.
    -   Supports ESSDs only.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Provides an ultra-high packet forwarding rate.
    -   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Scenarios such as financial services, government affairs, and enterprise services that require high security and enhanced trust
    -   Scenarios such as on-screen video comments and telecom data forwarding where large volumes of packets are received and transmitted
    -   Enterprise-level applications of various types and sizes
    -   Websites and application servers
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|TPM support|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|-----------|------------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.g6t.large|2|8.0|None|A burstable bandwidth of up to 10.0|900|Yes|Yes|Up to 250|2|3|6|20|1.0|
|ecs.g6t.xlarge|4|16.0|None|A burstable bandwidth of up to 10.0|1,000|Yes|Yes|Up to 250|4|4|15|40|1.5|
|ecs.g6t.2xlarge|8|32.0|None|A burstable bandwidth of up to 10.0|1,600|Yes|Yes|Up to 250|8|4|15|50|2.0|
|ecs.g6t.4xlarge|16|64.0|None|A burstable bandwidth of up to 10.0|3,000|Yes|Yes|300|8|8|30|80|3.0|
|ecs.g6t.8xlarge|32|128.0|None|10.0|6,000|Yes|Yes|600|16|8|30|150|5.0|
|ecs.g6t.13xlarge|52|192.0|None|16.0|9,000|Yes|Yes|900|32|7|30|240|8.0|
|ecs.g6t.26xlarge|104|384.0|None|32.0|24,000|Yes|Yes|1,800|32|15|30|480|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other metrics of the network.

## g6e, general purpose instance family with enhanced performance

Features

-   Provides predictable and consistent ultra-high performance and reduces virtualization overheads based on the third-generation X-Dragon architecture. g6e improves storage performance, network performance, and computing stability by an order of magnitude through fast path acceleration of X-Dragon chips.
-   Supports I/O optimization.
-   Supports ESSDs only.
-   Provides high network and storage I/O performance based on large computing capacity.

    **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Provides an ultra-high packet forwarding rate.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269 \(Cascade\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
-   Allows you to enable or disable Hyper-Threading.

    **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Applies to the following scenarios:
    -   Scenarios such as on-screen video comments and telecom data forwarding where large volumes of packets are received and transmitted
    -   Enterprise-level applications of various types and sizes
    -   Websites and application servers
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|--------------------|:------------------------------|:-----------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.g6e.large|2|8.0|None|A burstable bandwidth of up to 10.0|900|Yes|Up to 250|2|3|6|20|1.0|
|ecs.g6e.xlarge|4|16.0|None|A burstable bandwidth of up to 10.0|1,000|Yes|Up to 250|4|4|15|40|1.5|
|ecs.g6e.2xlarge|8|32.0|None|A burstable bandwidth of up to 10.0|1,600|Yes|Up to 250|8|4|15|50|2.0|
|ecs.g6e.4xlarge|16|64.0|None|A burstable bandwidth of up to 10.0|3,000|Yes|300|8|8|30|80|3.0|
|ecs.g6e.8xlarge|32|128.0|None|10.0|6,000|Yes|600|16|8|30|150|5.0|
|ecs.g6e.13xlarge|52|192.0|None|16.0|9,000|Yes|900|32|7|30|240|8.0|
|ecs.g6e.26xlarge|104|384.0|None|32.0|24,000|Yes|1,800|32|15|30|480|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other metrics of the network.

## g6, general purpose instance family

Features

-   Provides predictable and consistent ultra-high performance and reduces virtualization overheads based on the X-Dragon architecture.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Provides high storage I/O performance based on large compute capacity.

    **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Offers a CPU-to-memory ratio of 1:4.
-   Allows you to enable or disable Hyper-Threading.

    **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Provides an ultra-high packet forwarding rate.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
-   Provides high network performance based on large computing capacity.
-   Supports instance type changes to c6 or r6.
-   Applies to the following scenarios:
    -   Scenarios such as on-screen video comments and telecom data forwarding where large volumes of packets are received and transmitted
    -   Enterprise-level applications of various types and sizes
    -   Websites and application servers
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Base bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:------------------------|------------------------------|:------------------------------|:-----------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.g6.large|2|8.0|None|1.0|3.0|300|Yes|Up to 250|2|2|6|10|1|
|ecs.g6.xlarge|4|16.0|None|1.5|5.0|500|Yes|Up to 250|4|3|10|20|1.5|
|ecs.g6.2xlarge|8|32.0|None|2.5|8.0|800|Yes|Up to 250|8|4|10|25|2|
|ecs.g6.3xlarge|12|48.0|None|4.0|10.0|900|Yes|Up to 250|8|6|10|30|2.5|
|ecs.g6.4xlarge|16|64.0|None|5.0|10.0|1,000|Yes|300|8|8|20|40|3|
|ecs.g6.6xlarge|24|96.0|None|7.5|10.0|1,500|Yes|450|12|8|20|50|4|
|ecs.g6.8xlarge|32|128.0|None|10.0|None|2,000|Yes|600|16|8|20|60|5|
|ecs.g6.13xlarge|52|192.0|None|12.5|None|3,000|Yes|900|32|7|20|100|8|
|ecs.g6.26xlarge|104|384.0|None|25.0|None|6,000|Yes|1,800|32|15|20|20.0|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## g5, general purpose instance family

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Offers a CPU-to-memory ratio of 1:4.
-   Provides an ultra-high packet forwarding rate.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) or 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Scenarios such as on-screen video comments and telecom data forwarding where large volumes of packets are received and transmitted
    -   Enterprise-level applications of various types and sizes
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.g5.large|2|8.0|None|1.0|300|Yes|2|2|6|
|ecs.g5.xlarge|4|16.0|None|1.5|500|Yes|2|3|10|
|ecs.g5.2xlarge|8|32.0|None|2.5|800|Yes|2|4|10|
|ecs.g5.3xlarge|12|48.0|None|4.0|900|Yes|4|6|10|
|ecs.g5.4xlarge|16|64.0|None|5.0|1,000|Yes|4|8|20|
|ecs.g5.6xlarge|24|96.0|None|7.5|1,500|Yes|6|8|20|
|ecs.g5.8xlarge|32|128.0|None|10.0|2,000|Yes|8|8|20|
|ecs.g5.16xlarge|64|256.0|None|20.0|4,000|Yes|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## g5ne, network enhanced instance family

Features

-   Significantly improves the network throughput and packet forwarding rate per instance. A single instance can deliver a packet forwarding rate of up to 10,000 Kpps.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) or 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Offers a CPU-to-memory ratio of 1:4.
-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks.
-   Provides high network performance based on large computing capacity.

    **Note:** We recommend that you select instance types of the g5ne instance family to deploy Data Plane Development Kit \(DPDK\) applications.

-   Applies to the following scenarios:
    -   DPDK applications
    -   Network intensive scenarios such as NFV or SD-WAN, mobile Internet, on-screen video comments, and telecom data forwarding
    -   Small and medium-sized database systems, caches, and search clusters
    -   Enterprise-level applications of various types and sizes
    -   Big data analysis and machine learning

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|------------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.g5ne.large|2|8.0|None|1.0|400|Yes|450|2|3|10|10|1|
|ecs.g5ne.xlarge|4|16.0|None|2.0|750|Yes|900|4|4|15|15|1|
|ecs.g5ne.2xlarge|8|32.0|None|3.5|1,500|Yes|1,750|8|6|15|30|1|
|ecs.g5ne.4xlarge|16|64.0|None|7.0|3,000|Yes|3,500|16|8|30|60|2|
|ecs.g5ne.8xlarge|32|128.0|None|15.0|6,000|Yes|7,000|32|8|30|120|4|
|ecs.g5ne.16xlarge|64|256.0|None|30.0|12,000|Yes|14,000|32|8|30|240|8|
|ecs.g5ne.18xlarge|72|288.0|None|33.0|13,500|Yes|16,000|32|15|50|270|9|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## sn2ne, general purpose instance family with enhanced network performance

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Offers a CPU-to-memory ratio of 1:4.
-   Provides an ultra-high packet forwarding rate.
-   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) or Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Provides high network performance based on large computing capacity.
-   Applies to the following scenarios:
    -   Scenarios such as on-screen video comments and telecom data forwarding where large volumes of packets are received and transmitted
    -   Enterprise-level applications of various types and sizes
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.sn2ne.large|2|8.0|None|1.0|300|Yes|2|2|6|
|ecs.sn2ne.xlarge|4|16.0|None|1.5|500|Yes|2|3|10|
|ecs.sn2ne.2xlarge|8|32.0|None|2.0|1,000|Yes|4|4|10|
|ecs.sn2ne.3xlarge|12|48.0|None|2.5|1,300|Yes|4|6|10|
|ecs.sn2ne.4xlarge|16|64.0|None|3.0|1,600|Yes|4|8|20|
|ecs.sn2ne.6xlarge|24|96.0|None|4.5|2,000|Yes|6|8|20|
|ecs.sn2ne.8xlarge|32|128.0|None|6.0|2,500|Yes|8|8|20|
|ecs.sn2ne.14xlarge|56|224.0|None|10.0|4,500|Yes|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## References

-   [Instance families](/intl.en-US/Instance/Instance families.md)
-   [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md)

