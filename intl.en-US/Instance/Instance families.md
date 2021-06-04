---
keyword: [ECS instance families, instance families]
---

# Instance families

An Elastic Compute Service \(ECS\) instance is the smallest unit that can provide compute capabilities and services for your business. Compute capabilities vary based on instance types. This topic describes available ECS instance families, including their features, specifications, and application scenarios.

ECS instances are categorized into different instance families based on their usage scenarios. Each instance family is divided into different instance types based on their CPU and memory specifications. ECS instance type defines the basic properties of an ECS instance, such as CPU, clock speed, and memory. In addition to the instance type, you must also configure the Elastic Block Storage \(EBS\) devices, image, and network type when you create an ECS instance.

**Note:** The available instance families and types vary based on regions. You can visit the [ECS Instance Types Available for Each Region](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) page to view the available instance types in each region.

Enterprise scenarios have high requirements for business stability. Alibaba Cloud ECS instance families are divided into enterprise-level and shared instance families based on whether the instance families are suitable for enterprise scenarios. Enterprise-level instance families offer consistent performance and dedicated resources. Each vCPU in an enterprise-level instance family corresponds to a hyperthread of the Intel® Xeon® core. For more information about the differences between enterprise-level and shared instance families, see [Instance FAQ](/intl.en-US/Instance/Instance FAQ.md).

You can upgrade or downgrade instance types within an instance family or across different instance families. For more information, see [Instance families that support instance type changes](/intl.en-US/Instance/Change configurations/Instance families that support instance type changes.md).

For information about how to choose instance families based on scenarios, see [Best practices for instance type selection](/intl.en-US/Best Practices/Best practices for instance type selection.md).

Alibaba Cloud ECS instance families are divided into the following categories based on the system architecture and usage scenarios.

|Enterprise-level computing instance families based on the x86 architecture|
|--------------------------------------------------------------------------|
|Recommended instance families|Other available instance families|
|-   [g7, general purpose instance family](#g7)
-   [g7t, security-enhanced general purpose instance family](#g7t)
-   [g7ne, network enhanced instance family](#g7ne)
-   [g6, general purpose instance family](#g6)
-   [g6se, storage enhanced instance family](#g6se)
-   [g6a, general purpose instance family](#g6a)
-   [g6t, security-enhanced general purpose instance family](#g6t)
-   [g6e, general purpose instance family with enhanced performance](#g6e)
-   [g5, general purpose instance family](#g5)
-   [g5se, storage enhanced instance family](#g5se)
-   [g5ne, network enhanced instance family](#g5ne)
-   [c7, compute optimized instance family](#c7)
-   [c7t, security-enhanced compute optimized instance family](#c7t)
-   [c6, compute optimized instance family](#c6)
-   [c6a, compute optimized instance family](#c6a)
-   [c6t, security-enhanced compute optimized instance family](#c6t)
-   [c6e, compute optimized instance family with enhanced performance](#c6e)
-   [c5, compute optimized instance family](#c5)
-   [ic5, compute intensive instance family](#ic5)
-   [r7, memory optimized instance family](#r7)
-   [r7t, security-enhanced memory optimized instance family](#r7t)
-   [r6, memory optimized instance family](#r6)
-   [re6p, persistent memory optimized instance family](#re6p)
-   [r6a, memory optimized instance family](#r6a)
-   [r6e, memory optimized instance family with enhanced performance](#r6e)
-   [re6, high memory instance family](#re6)
-   [r5, memory optimized instance family](#r5)
-   [d2c, compute intensive big data instance family](#d2c)
-   [d2s, storage intensive big data instance family](#d2s)
-   [d1ne, big data instance family with enhanced network performance](#d1ne)
-   [i3g, instance family with local SSDs](#i3g)
-   [i3, instance family with local SSDs](#i3)
-   [i2, instance family with local SSDs](#i2)
-   [i2g, instance family with local SSDs](#i2g)
-   [i2ne, instance family with local SSDs](#i2ne)
-   [i2gne, instance family with local SSDs](#i2gne)
-   [hfc7, compute optimized instance family with high clock speeds](#hfc7)
-   [hfc6, compute optimized instance family with high clock speeds](#hfc6)
-   [hfg7, general purpose instance family with high clock speeds](#hfg7)
-   [hfg6, general purpose instance family with high clock speeds](#hfg6)
-   [hfr7, memory optimized instance family with high clock speeds](#hfr7)
-   [hfr6, memory optimized instance family with high clock speeds](#hfr6)

|-   [sn2ne, general purpose instance family with enhanced network performance](#sn2ne)
-   [sn1ne, compute optimized instance family with enhanced network performance](#sn1ne)
-   [re4, high memory instance family](#re4)
-   [re4e, high memory instance family](#re4e)
-   [se1ne, memory optimized instance family with enhanced network performance](#se1ne)
-   [se1, memory optimized instance family](#se1)
-   [d1, big data instance family](#d1)
-   [i1, instance family with local SSDs](#i1)
-   [hfc5, compute optimized instance family with high clock speeds](#hfc5)
-   [hfg5, general purpose instance family with high clock speeds](#hfg5) |

|Enterprise-level heterogeneous computing instance families|
|----------------------------------------------------------|
|Recommended instance families|Other available instance families|
|-   [gn7, GPU-accelerated compute optimized instance family](#gn7)
-   [vgn6i, lightweight GPU-accelerated compute optimized instance family](#vgn6i)
-   [gn6i, GPU-accelerated compute optimized instance family](#gn6i)
-   [gn6e, GPU-accelerated compute optimized instance family](#gn6e)
-   [gn6v, GPU-accelerated compute optimized instance family](#gn6v)
-   [f3, FPGA-accelerated compute optimized instance family](#f3)

|-   [vgn5i, lightweight GPU-accelerated compute optimized instance family](#vgn5i)
-   [gn5, GPU-accelerated compute optimized instance family](#gn5)
-   [gn5i, GPU-accelerated compute optimized instance family](#gn5i)
-   [f1, FPGA-accelerated compute optimized instance family](#f1) |

|ECS Bare Metal Instance families and Super Computing Cluster \(SCC\) instance families|
|--------------------------------------------------------------------------------------|
|Recommended instance families|Other available instance families|
|-   [ebmgn7, GPU-accelerated compute optimized ECS Bare Metal Instance family](#ebmgn7)
-   [ebmgn6e, GPU-accelerated compute optimized ECS Bare Metal Instance family](#ebmgn6e)
-   [ebmgn6v, GPU-accelerated compute optimized ECS Bare Metal Instance family](#ebmgn6v)
-   [ebmgn6i, GPU-accelerated compute optimized ECS Bare Metal Instance family](#ebmgn6i)
-   [ebmc6a, compute optimized ECS Bare Metal Instance family](#ebmc6a)
-   [ebmc6e, compute optimized ECS Bare Metal Instance family with enhanced performance](#ebmc6e)
-   [ebmc6, compute optimized ECS Bare Metal Instance family](#ebmc6)
-   [ebmg6a, general purpose ECS Bare Metal Instance family](#ebmg6a)
-   [ebmg6e, general purpose ECS Bare Metal Instance family with enhanced performance](#ebmg6e)
-   [ebmg6, general purpose ECS Bare Metal Instance family](#ebmg6)
-   [ebmr6a, memory optimized ECS Bare Metal Instance family](#ebmr6a)
-   [ebmr6e, memory optimized ECS Bare Metal Instance family with enhanced performance](#ebmr6e)
-   [ebmr6, memory optimized ECS Bare Metal Instance family](#ebmr6)
-   [ebmre6p, persistent memory optimized ECS Bare Metal Instance family with enhanced performance](#ebmre6p)
-   [ebmre6-6t, memory optimized ECS Bare Metal Instance family with enhanced performance](#ebmre6-6t)
-   [ebmhfg7, general purpose ECS Bare Metal Instance family with high clock speeds](#ebmhfg7)
-   [ebmhfc7, compute optimized ECS Bare Metal Instance family with high clock speeds](#ebmhfc7)
-   [ebmhfr7, memory optimized ECS Bare Metal Instance family with high clock speeds](#ebmhfr7)
-   [ebmhfg6, general purpose ECS Bare Metal Instance family with high clock speeds](#ebmhfg6)
-   [ebmhfc6, compute optimized ECS Bare Metal Instance family with high clock speeds](#ebmhfc6)
-   [ebmhfr6, memory optimized ECS Bare Metal Instance family with high clock speeds](#ebmhfr6)
-   [scchfc6, compute optimized SCC instance family with high clock speeds](#scchfc6)
-   [scchfg6, general purpose SCC instance family with high clock speeds](#scchfg6)
-   [scchfr6, memory optimized SCC instance family with high clock speeds](#scchfr6)
-   [scch5, SCC instance family with high clock speeds](#scch5)
-   [sccg5, general purpose SCC instance family](#sccg5)
-   [sccgn6e, GPU-accelerated compute optimized SCC instance family](#sccgn6e)
-   [sccgn6, GPU-accelerated compute optimized SCC instance family](#sccgn6)

|-   [ebmc5s, compute optimized ECS Bare Metal Instance family with enhanced network performance](#ebmc5s)
-   [ebmg5s, general purpose ECS Bare Metal Instance family with enhanced network performance](#ebmg5s)
-   [ebmr5s, memory optimized ECS Bare Metal Instance family with enhanced network performance](#ebmr5s)
-   [ebmg5, general purpose ECS Bare Metal Instance family](#ebmg5)
-   [ebmhfg5, ECS Bare Metal Instance family with high clock speeds](#ebmhfg5)
-   [ebmc4, compute optimized ECS Bare Metal Instance family](#ebmc4) |

|Shared computing instance families based on the x86 architecture|
|----------------------------------------------------------------|
|Recommended instance families|Other available instance families|
|-   [t6, burstable instance family](#t6)

|-   [t5, burstable instance family](#t5)
-   [v5, CPU overprovisioned instance family](#v5)
-   [xn4, n4, mn4, and e4, previous-generation shared instance families](#xn4-n4-mn4-e4) |

For information about retired instance families, see [Retired instance types](/intl.en-US/Instance/Instance type families/Retired instance types.md).

## g7, general purpose instance family

Features

-   Uses the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Supports the virtual Trusted Platform Module \(vTPM\) feature and implements trusted boots based on Trusted Cryptography Module \(TCM\) or Trusted Platform Module \(TPM\) chips. During a trusted boot, all modules in the boot chain from the underlying hardware to the guest OS are measured and verified.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses the third-generation Intel® Xeon® Scalable processors \(Ice Lake\) that deliver a base frequency of 2.7 GHz and an all-core turbo frequency of 3.5 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only enhanced SSDs \(ESSDs\).
    -   Provides burstable storage I/O performance on low-specification instances.
    -   Provides high storage I/O performance based on large computing capacity.
-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides burstable network performance on low-specification instances.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Enterprise-level applications of various types and sizes
    -   Websites and application servers
    -   Data analysis and computing
    -   Scenarios that require secure and trusted computing
    -   Blockchain scenarios

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|--------------------|:-----------------------------|------------|----------|:---|----------------------------|---------|-------------------------|
|ecs.g7.large|2|8.0|Burstable up to 10.0|900,000|Yes|2|3|6|Burstable up to 100,000|Burstable up to 6.0|
|ecs.g7.xlarge|4|16.0|Burstable up to 10.0|1,000,000|Yes|4|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.g7.2xlarge|8|32.0|Burstable up to 10.0|1,600,000|Yes|8|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.g7.3xlarge|12|48.0|Burstable up to 10.0|2,400,000|Yes|8|8|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.g7.4xlarge|16|64.0|Burstable up to 25.0|3,000,000|Yes|8|8|30|Burstable up to 100,000|Burstable up to 6.0|
|ecs.g7.6xlarge|24|96.0|Burstable up to 25.0|4,500,000|Yes|12|8|30|100,000|6.0|
|ecs.g7.8xlarge|32|128.0|Burstable up to 25.0|6,000,000|Yes|16|8|30|150,000|8.0|
|ecs.g7.16xlarge|64|256.0|32.0|12,000,000|Yes|32|8|30|300,000|16.0|
|ecs.g7.32xlarge|128|512.0|64.0|24,000,000|Yes|32|15|30|600,000|32.0|

**Note:**

-   If you use Virtual Network Computing \(VNC\) to log on to a Windows instance, two cursors may appear. For information about how to fix this issue, see the “Why do two cursors appear after I use VNC to log on to a Windows instance?” section in [Instance FAQ](/intl.en-US/Instance/Instance FAQ.mdsection_jma_ml8_us3).
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## g7t, security-enhanced general purpose instance family

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Supports encrypted computing based on Intel® Software Guard Extensions \(SGX\) and up to 256 GiB encrypted memory to protect the confidentiality and integrity of key code and data from malware attacks.
-   Supports SGX technology applicable to virtual machines and allows you to select instance types that suit your needs.
-   Implements trusted boots based on TCM or TPM chips. During a trusted boot, all modules in the boot chain from the underlying server hardware to the guest OS are measured and verified.
-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1: 4. About 50% of memory is encrypted.
    -   Uses the third-generation Intel® Xeon® Scalable processors for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs.
    -   Provides high storage I/O performance based on large computing capacity.
-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios that involve sensitive information such as personal identity information, healthcare information, financial information, and intellectual property data
    -   Scenarios where confidential data is shared among multiple parties
    -   Blockchain scenarios
    -   Confidential machine learning
    -   Scenarios that require high security and enhanced trust, such as finance, government, and enterprise services
    -   Enterprise-level applications of various types and sizes

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Encrypted portion of memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------------|--------------------|:-----------------------------|------------|----------|:---|----------------------------|---------|-------------------------|
|ecs.g7t.large|2|8.0|4.0|Burstable up to 10.0|900,000|Yes|2|3|6|Burstable up to 100,000|Burstable up to 6.0|
|ecs.g7t.xlarge|4|16.0|8.0|Burstable up to 10.0|1,000,000|Yes|4|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.g7t.2xlarge|8|32.0|16.0|Burstable up to 10.0|1,600,000|Yes|8|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.g7t.3xlarge|12|48.0|24.0|Burstable up to 10.0|2,400,000|Yes|8|8|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.g7t.4xlarge|16|64.0|32.0|Burstable up to 25.0|3,000,000|Yes|8|8|30|Burstable up to 100,000|Burstable up to 6.0|
|ecs.g7t.6xlarge|24|96.0|48.0|Burstable up to 25.0|4,500,000|Yes|12|8|30|100,000|6.0|
|ecs.g7t.8xlarge|32|128.0|64.0|Burstable up to 25.0|6,000,000|Yes|16|8|30|150,000|8.0|
|ecs.g7t.16xlarge|64|256.0|128.0|32.0|12,000,000|Yes|32|8|30|300,000|16.0|
|ecs.g7t.32xlarge|128|512.0|256.0|64.0|24,000,000|Yes|32|15|30|600,000|32.0|

**Note:**

-   The instance family is in invitational preview. Resources are limited. No service level agreement \(SLA\) compliance is ensured. To use this instance family, submit an application based on your minimum business requirements.
-   Intel Ice Lake supports only remote attestation based on Intel SGX DCAP, and does not support remote attestation based on Intel EPID. You must adapt applications before you can use the remote attestation feature. For more information about remote attestation, see [attestation-service](https://software.intel.com/content/www/us/en/develop/topics/software-guard-extensions/attestation-services.html).
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## g7ne, general purpose instance family with enhanced network performance

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Significantly improves the network throughput and packet forwarding rate per instance. A single instance can deliver a packet forwarding rate of up to 24,000,000 pps.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses Intel ® Xeon ® Platinum 8369HB \(Cooper Lake\) or Intel ® Xeon® Platinum 8369HC \(Cooper Lake\) processors that deliver a turbo frequency of 3.8 GHz and a minimum clock speed of 3.3 GHz for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs and provides ultra-high I/O performance.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Network-intensive scenarios such as Network Functions Virtualization \(NFV\) or Software-defined Wide Area Network \(SD-WAN\), mobile Internet, on-screen video comments, and telecom data forwarding
    -   Small and medium-sized database systems, caches, and search clusters
    -   Enterprise-level applications of various types and sizes
    -   Big data analysis and machine learning

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------|------------------------------|:-----------------------------|-----------|----------|:---|----------------------------|---------|-------------------------|
|ecs.g7ne.large|2|8.0|1.5|10.0|900,000|450,000|2|3|10|10,000|0.75|
|ecs.g7ne.xlarge|4|16.0|3.0|10.0|1,000,000|900,000|4|4|15|20,000|1.0|
|ecs.g7ne.2xlarge|8|32.0|6.0|15.0|1,500,000|1,750,000|8|6|15|25,000|1.2|
|ecs.g7ne.4xlarge|16|64.0|12.5|25.0|3,000,000|3,500,000|16|8|30|40,000|2.0|
|ecs.g7ne.8xlarge|32|128.0|25.0|None|6,000,000|6,000,000|16|8|30|75,000|5.0|
|ecs.g7ne.12xlarge|48|192.0|40.0|None|12,000,000|8,000,000|32|8|30|100,000|8.0|
|ecs.g7ne.16xlarge|64|256.0|50.0|None|16,000,000|14,000,000|32|8|30|150,000|8.0|
|ecs.g7ne.24xlarge|96|384.0|80.0|None|24,000,000|16,000,000|32|15|50|240,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## g6, general purpose instance family

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.

        **Note:** The maximum performance of disks varies based on instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.

        **Note:** The network performance varies based on instance families. For higher concurrent connection and network packet forwarding capabilities, we recommend that you use g7ne.

    -   Provides high network performance based on large computing capacity.
-   Supports changes to instance types in the c6 or r6 instance family.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-level applications of various types and sizes
    -   Websites and application servers
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:----------------------------|------------------------------|:-----------------------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.g6.large|2|8.0|1.0|3.0|300,000|Up to 250,000|2|2|6|10,000|1|
|ecs.g6.xlarge|4|16.0|1.5|5.0|500,000|Up to 250,000|4|3|10|20,000|1.5|
|ecs.g6.2xlarge|8|32.0|2.5|8.0|800,000|Up to 250,000|8|4|10|25,000|2|
|ecs.g6.3xlarge|12|48.0|4.0|10.0|900,000|Up to 250,000|8|6|10|30,000|2.5|
|ecs.g6.4xlarge|16|64.0|5.0|10.0|1,000,000|300,000|8|8|20|40,000|3|
|ecs.g6.6xlarge|24|96.0|7.5|10.0|1,500,000|450,000|12|8|20|50,000|4|
|ecs.g6.8xlarge|32|128.0|10.0|None|2,000,000|600,000|16|8|20|60,000|5|
|ecs.g6.13xlarge|52|192.0|12.5|None|3,000,000|900,000|32|7|20|100,000|8|
|ecs.g6.26xlarge|104|384.0|25.0|None|6,000,000|1,800,000|32|15|20|200,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## g6se, storage enhanced instance family

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Delivers a sequential read/write performance of up to 32 Gbit/s per instance.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs and provides ultra-high I/O performance.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   I/O-intensive scenarios such as large and medium-sized online transactional processing \(OLTP\) core databases
    -   Large and medium-sized NoSQL databases
    -   Search and real-time log analytics
    -   Traditional large enterprise-level commercial software, such as SAP

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------|------------------------------|:-----------------------------|----------|:---|----------------------------|---------|-------------------------|
|ecs.g6se.large|2|8.0|0.7|2.0|300,000|2|2|6|30,000|1.5|
|ecs.g6se.xlarge|4|16.0|1.0|3.0|500,000|4|3|10|60,000|2.0|
|ecs.g6se.2xlarge|8|32.0|1.5|5.0|800,000|8|4|10|90,000|3.0|
|ecs.g6se.4xlarge|16|64.0|3.0|6.0|1,000,000|8|8|20|150,000|5.0|
|ecs.g6se.8xlarge|32|128.0|6.0|None|2,000,000|16|8|20|300,000|10.0|
|ecs.g6se.13xlarge|52|192.0|8.0|None|3,000,000|32|7|20|500,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## g6a, general purpose instance family

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.6 GHz AMD EPYCTM ROME processors that deliver a turbo frequency of 3.3 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Video encoding and decoding
    -   Scenarios where large volumes of packets are received and transmitted
    -   Websites and application servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Game servers
    -   Scenarios where applications such as DevOps applications are developed and tested
    -   Other general-purpose enterprise-level applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|ENIs|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------|------------------------------|:-----------------------------|:---|---------|-------------------------|
|ecs.g6a.large|2|8.0|1.0|10.0|900,000|2|12,500|1.0|
|ecs.g6a.xlarge|4|16.0|1.5|10.0|1,000,000|3|20,000|1.5|
|ecs.g6a.2xlarge|8|32.0|2.5|10.0|1,600,000|4|30,000|2.0|
|ecs.g6a.4xlarge|16|64.0|5.0|10.0|2,000,000|8|60,000|3.0|
|ecs.g6a.8xlarge|32|128.0|8.0|10.0|3,000,000|7|75,000|4.0|
|ecs.g6a.16xlarge|64|256.0|16.0|None|6,000,000|8|150,000|8.0|
|ecs.g6a.32xlarge|128|512.0|32.0|None|12,000,000|15|300,000|16.0|
|ecs.g6a.64xlarge|256|1024.0|64.0|None|24,000,000|15|600,000|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## g6t, security-enhanced general purpose instance family

Features

-   Implements trusted boots based on TCM or TPM chips. During a trusted boot, all modules in the boot chain from the underlying server hardware to the guest OS are measured and verified.
-   Provides vTPMs that deliver a full set of trusted capabilities at the IaaS layer based on integrity monitoring.
-   Supports the Enclave feature and provides a trusted isolation space inside ECS instances to encapsulate the security operations of legitimate software within an enclave. This ensures the confidentiality and integrity of your code and data against malware attacks.
-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
    -   Allows you to enable or disable hyper-threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios that require high security and enhanced trust, such as finance, government, and enterprise services
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-level applications of various types and sizes
    -   Websites and application servers
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.g6t.large|2|8.0|Burstable up to 10.0|900,000|Yes|Up to 250,000|2|3|6|20,000|1.0|
|ecs.g6t.xlarge|4|16.0|Burstable up to 10.0|1,000,000|Yes|Up to 250,000|4|4|15|40,000|1.5|
|ecs.g6t.2xlarge|8|32.0|Burstable up to 10.0|1,600,000|Yes|Up to 250,000|8|4|15|50,000|2.0|
|ecs.g6t.4xlarge|16|64.0|Burstable up to 10.0|3,000,000|Yes|300,000|8|8|30|80,000|3.0|
|ecs.g6t.8xlarge|32|128.0|10.0|6,000,000|Yes|600,000|16|8|30|150,000|5.0|
|ecs.g6t.13xlarge|52|192.0|16.0|9,000,000|Yes|900,000|32|7|30|240,000|8.0|
|ecs.g6t.26xlarge|104|384.0|32.0|24,000,000|Yes|1,800,000|32|15|30|480,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other network metrics.

## g6e, general purpose instance family with enhanced performance

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269 \(Cascade\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.

        **Note:** The network performance varies based on instance families. For higher concurrent connection and network packet forwarding capabilities, we recommend that you use g7ne.

    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-level applications of various types and sizes
    -   Websites and application servers
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|--------------------|:-----------------------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.g6e.large|2|8.0|Burstable up to 10.0|900,000|Up to 250,000|2|3|6|20,000|1.0|
|ecs.g6e.xlarge|4|16.0|Burstable up to 10.0|1,000,000|Up to 250,000|4|4|15|40,000|1.5|
|ecs.g6e.2xlarge|8|32.0|Burstable up to 10.0|1,600,000|Up to 250,000|8|4|15|50,000|2.0|
|ecs.g6e.4xlarge|16|64.0|Burstable up to 10.0|3,000,000|300,000|8|8|30|80,000|3.0|
|ecs.g6e.8xlarge|32|128.0|10.0|6,000,000|600,000|16|8|30|150,000|5.0|
|ecs.g6e.13xlarge|52|192.0|16.0|9,000,000|900,000|32|7|30|240,000|8.0|
|ecs.g6e.26xlarge|104|384.0|32.0|24,000,000|1,800,000|32|15|30|480,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other network metrics.

## g5, general purpose instance family

Features

-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) or 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.

        **Note:** The maximum performance of disks varies based on instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.

        **Note:** The network performance varies based on instance families. For higher concurrent connection and network packet forwarding capabilities, we recommend that you use g7ne.

    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-level applications of various types and sizes
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.g5.large|2|8.0|1.0|300,000|2|2|6|
|ecs.g5.xlarge|4|16.0|1.5|500,000|2|3|10|
|ecs.g5.2xlarge|8|32.0|2.5|800,000|2|4|10|
|ecs.g5.3xlarge|12|48.0|4.0|900,000|4|6|10|
|ecs.g5.4xlarge|16|64.0|5.0|1,000,000|4|8|20|
|ecs.g5.6xlarge|24|96.0|7.5|1,500,000|6|8|20|
|ecs.g5.8xlarge|32|128.0|10.0|2,000,000|8|8|20|
|ecs.g5.16xlarge|64|256.0|20.0|4,000,000|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## g5se, storage enhanced instance family

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   You can create g5se instances only on dedicated hosts.

    **Note:** For more information about other types of instances that can be created on dedicated hosts, see [Dedicated host types](/intl.en-US/Product Introduction/Dedicated host types.md).

-   A single g5se instance attached with enhanced SSDs \(ESSDs\) can deliver a random input/output operations per second \(IOPS\) of up to 1,000,000 and a sequential read and write performance of up to 32 Gbit/s.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
-   Suits the following scenarios:
    -   I/O-intensive scenarios such as large and medium-sized online transactional processing \(OLTP\) core databases
    -   Large and medium-sized NoSQL databases
    -   Search and real-time log analytics
    -   Traditional large enterprise-level commercial software, such as SAP

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|---------------|-------------------------|
|ecs.g5se.large|2|8.0|1.0|300|2|2|6|30|1.5|
|ecs.g5se.xlarge|4|16.0|1.5|500|2|3|6|60|2|
|ecs.g5se.2xlarge|8|32.0|2.0|800|2|4|8|85|3|
|ecs.g5se.4xlarge|16|64.0|4.0|1,000|4|8|10|150|5|
|ecs.g5se.8xlarge|32|128.0|7.0|2,000|8|8|10|300|10|
|ecs.g5se.16xlarge|64|256.0|14.0|3,000|16|7|10|750|25|
|ecs.g5se.18xlarge|70|336.0|16.0|4,000|16|15|10|1,000|32|

**Note:** For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## g5ne, general purpose instance family with enhanced network performance

Features

-   Significantly improves the network throughput and packet forwarding rate per instance. A single instance can deliver a packet forwarding rate of up to 10,000,000 pps.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) or 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.

        **Note:** We recommend that you select instance types of the g5ne instance family to deploy Data Plane Development Kit \(DPDK\) applications.

-   Suits the following scenarios:
    -   DPDK applications
    -   Network-intensive scenarios such as NFV or SD-WAN, mobile Internet, on-screen video comments, and telecom data forwarding
    -   Small and medium-sized database systems, caches, and search clusters
    -   Enterprise-level applications of various types and sizes
    -   Big data analysis and machine learning

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.g5ne.large|2|8.0|1.0|400,000|450,000|2|3|10|10,000|1|
|ecs.g5ne.xlarge|4|16.0|2.0|750,000|900,000|4|4|15|15,000|1|
|ecs.g5ne.2xlarge|8|32.0|3.5|1,500,000|1,750,000|8|6|15|30,000|1|
|ecs.g5ne.4xlarge|16|64.0|7.0|3,000,000|3,500,000|16|8|30|60,000|2|
|ecs.g5ne.8xlarge|32|128.0|15.0|6,000,000|7,000,000|32|8|30|120,000|4|
|ecs.g5ne.16xlarge|64|256.0|30.0|12,000,000|14,000,000|32|8|30|240,000|8|
|ecs.g5ne.18xlarge|72|288.0|33.0|13,500,000|16,000,000|32|15|50|270,000|9|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## c7, compute optimized instance family

Features

-   Uses the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Supports the virtual Trusted Platform Module \(vTPM\) feature and implements trusted boots based on Trusted Cryptography Module \(TCM\) or Trusted Platform Module \(TPM\) chips to provide ultra-high security capabilities. During a trusted boot, all modules in the boot chain from the underlying server to the ECS instance are measured and verified.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses the third-generation Intel® Xeon® Scalable processors \(Ice Lake\) that deliver a base frequency of 2.7 GHz and an all-core turbo frequency of 3.5 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only enhanced SSDs \(ESSDs\).
    -   Provides burstable storage I/O performance for low-specification instances.
    -   Provides high storage I/O performance based on large compute capacity.
-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides burstable network performance for low-specification instances.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Frontend servers of massively multiplayer online \(MMO\) games
    -   Web frontend servers
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications
    -   Scenarios that require secure and trusted computing
    -   Enterprise-level applications of various types and sizes
    -   Blockchain scenarios

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|--------------------|:-----------------------------|------------|----------|:---|----------------------------|---------|-------------------------|
|ecs.c7.large|2|4.0|Burstable up to 10.0|900,000|Yes|2|3|6|Burstable up to 100,000|Burstable up to 6.0|
|ecs.c7.xlarge|4|8.0|Burstable up to 10.0|1,000,000|Yes|4|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.c7.2xlarge|8|16.0|Burstable up to 10.0|1,600,000|Yes|8|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.c7.3xlarge|12|24.0|Burstable up to 10.0|2,400,000|Yes|8|8|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.c7.4xlarge|16|32.0|Burstable up to 25.0|3,000,000|Yes|8|8|30|Burstable up to 100,000|Burstable up to 6.0|
|ecs.c7.6xlarge|24|48.0|Burstable up to 25.0|4,500,000|Yes|12|8|30|100,000|6.0|
|ecs.c7.8xlarge|32|64.0|Burstable up to 25.0|6,000,000|Yes|16|8|30|150,000|8.0|
|ecs.c7.16xlarge|64|128.0|32.0|12,000,000|Yes|32|8|30|300,000|16.0|
|ecs.c7.32xlarge|128|256.0|64.0|24,000,000|Yes|32|15|30|600,000|32.0|

**Note:**

-   If you use Virtual Network Computing \(VNC\) to log on to a Windows instance, two cursors may appear. For information about how to fix this issue, see the “Why do two cursors appear after I use VNC to log on to a Windows instance?” section in [Instance FAQ](/intl.en-US/Instance/Instance FAQ.mdsection_jma_ml8_us3).
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## c7t, security-enhanced compute optimized instance family

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Supports up to 128 GiB encrypted memory and encrypted computing based on Intel® Software Guard Extensions \(SGX\) to protect the confidentiality and integrity of key code and data from malware attacks.
-   Supports SGX technology applicable to virtual machines and allows you to choose instance types based on your needs.
-   Implements trusted boots based on TCM or TPM chips. During a trusted boot, each module in the boot chain from the underlying hardware to the guest OS is measured and verified.
-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2, where the encrypted memory occupies about 50% of the total memory.
    -   Uses the third-generation Intel® Xeon® Scalable processors for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs.
    -   Provides high storage I/O performance based on large compute capacity.
-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios that involve sensitive information such as personal identity information, healthcare information, financial information, and intellectual property data
    -   Scenarios where confidential data is shared among multiple parties
    -   Blockchain scenarios
    -   Confidential machine learning
    -   Scenarios that require high security and enhanced trust, such as finance, government, and enterprise services
    -   Enterprise-level applications of various types and sizes

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Encrypted memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|------------------------|--------------------|:-----------------------------|------------|----------|:---|----------------------------|---------|-------------------------|
|ecs.c7t.large|2|4.0|2.0|Burstable up to 10.0|900,000|Yes|2|3|6|Burstable up to 100,000|Burstable up to 6.0|
|ecs.c7t.xlarge|4|8.0|4.0|Burstable up to 10.0|1,000,000|Yes|4|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.c7t.2xlarge|8|16.0|8.0|Burstable up to 10.0|1,600,000|Yes|8|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.c7t.3xlarge|12|24.0|12.0|Burstable up to 10.0|2,400,000|Yes|8|8|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.c7t.4xlarge|16|32.0|16.0|Burstable up to 25.0|3,000,000|Yes|8|8|30|Burstable up to 100,000|Burstable up to 6.0|
|ecs.c7t.6xlarge|24|48.0|24.0|Burstable up to 25.0|4,500,000|Yes|12|8|30|100,000|6.0|
|ecs.c7t.8xlarge|32|64.0|32.0|Burstable up to 25.0|6,000,000|Yes|16|8|30|150,000|8.0|
|ecs.c7t.16xlarge|64|128.0|64.0|32.0|12,000,000|Yes|32|8|30|300,000|16.0|
|ecs.c7t.32xlarge|128|256.0|128.0|64.0|24,000,000|Yes|32|15|30|600,000|32.0|

**Note:**

-   The instance family is in invitational preview. Resources are limited. No service level agreement \(SLA\) compliance is ensured. To use this instance family, submit an application based on your minimum business requirements.
-   Intel Ice Lake supports only remote attestation based on Intel SGX DCAP, and does not support remote attestation based on Intel EPID. You must adapt applications before you can use the remote attestation feature. For more information about remote attestation, see [attestation-service](https://software.intel.com/content/www/us/en/develop/topics/software-guard-extensions/attestation-services.html).
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## c6, compute optimized instance family

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.

        **Note:** The maximum performance of disks varies based on instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

    -   Provides high storage I/O performance based on large compute capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Supports changes to instance types in the g6 or r6 instance family.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:----------------------------|------------------------------|:-----------------------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.c6.large|2|4.0|1.0|3.0|300,000|Up to 250,000|2|2|6|10,000|1|
|ecs.c6.xlarge|4|8.0|1.5|5.0|500,000|Up to 250,000|4|3|10|20,000|1.5|
|ecs.c6.2xlarge|8|16.0|2.5|8.0|800,000|Up to 250,000|8|4|10|25,000|2|
|ecs.c6.3xlarge|12|24.0|4.0|10.0|900,000|Up to 250,000|8|6|10|30,000|2.5|
|ecs.c6.4xlarge|16|32.0|5.0|10.0|1,000,000|300,000|8|8|20|40,000|3|
|ecs.c6.6xlarge|24|48.0|7.5|10.0|1,500,000|450,000|12|8|20|50,000|4|
|ecs.c6.8xlarge|32|64.0|10.0|None|2,000,000|600,000|16|8|20|60,000|5|
|ecs.c6.13xlarge|52|96.0|12.5|None|3,000,000|900,000|32|7|20|100,000|8|
|ecs.c6.26xlarge|104|192.0|25.0|None|6,000,000|1,800,000|32|15|20|200,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## c6a, compute optimized instance family

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses 2.6 GHz AMD EPYCTM ROME processors that deliver a turbo frequency of 3.3 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
    -   Provides high storage I/O performance based on large compute capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Video encoding and decoding
    -   Scenarios where large volumes of packets are received and transmitted
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Scenarios where applications such as DevOps applications are developed and tested

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|ENIs|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------|------------------------------|:-----------------------------|:---|---------|-------------------------|
|ecs.c6a.large|2|4.0|1.0|10.0|900,000|2|12,500|1.0|
|ecs.c6a.xlarge|4|8.0|1.5|10.0|1,000,000|3|20,000|1.5|
|ecs.c6a.2xlarge|8|16.0|2.5|10.0|1,600,000|4|30,000|2.0|
|ecs.c6a.4xlarge|16|32.0|5.0|10.0|2,000,000|8|60,000|3.0|
|ecs.c6a.8xlarge|32|64.0|8.0|10.0|3,000,000|7|75,000|4,0|
|ecs.c6a.16xlarge|64|128.0|16.0|None|6,000,000|8|150,000|8.0|
|ecs.c6a.32xlarge|128|256.0|32.0|None|12,000,000|15|300,000|16.0|
|ecs.c6a.64xlarge|256|512.0|64.0|None|24,000,000|15|600,000|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## c6t, security-enhanced compute optimized instance family

Features

-   Implements trusted boots based on TPM chips. During a trusted boot, each module in the boot chain from the underlying hardware to the guest OS is measured and verified.
-   Supports comprehensive monitoring at the IaaS layer and provides trusted capabilities of the whole IaaS layer.
-   Supports the Enclave feature and provides a trusted isolation space inside ECS instances to encapsulate security operations of legitimate software in an enclave. This ensures the confidentiality and integrity of your code and data against malware attacks.
-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs.
    -   Provides high storage I/O performance based on large compute capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios that require high security and enhanced trust, such as finance, government, and enterprise services
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|--------------------|:-----------------------------|------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.c6t.large|2|4.0|Burstable up to 10.0|900,000|Yes|Up to 250,000|2|3|6|20,000|1.0|
|ecs.c6t.xlarge|4|8.0|Burstable up to 10.0|1,000,000|Yes|Up to 250,000|4|4|15|40,000|1.5|
|ecs.c6t.2xlarge|8|16.0|Burstable up to 10.0|1,600,000|Yes|Up to 250,000|8|4|15|50,000|2.0|
|ecs.c6t.4xlarge|16|32.0|Burstable up to 10.0|3,000,000|Yes|300,000|8|8|30|80,000|3.0|
|ecs.c6t.8xlarge|32|64.0|10.0|6,000,000|Yes|600,000|16|8|30|150,000|5.0|
|ecs.c6t.13xlarge|52|96.0|16.0|9,000,000|Yes|900,000|32|7|30|240,000|8.0|
|ecs.c6t.26xlarge|104|192.0|32.0|24,000,000|Yes|1,800,000|32|15|30|480,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other network metrics.

## c6e, compute optimized instance family with enhanced performance

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269 \(Cascade\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs.
    -   Provides high storage I/O performance based on large compute capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.

        **Note:** The network performance varies based on instance families. For higher concurrent connection and network packet forwarding capabilities, we recommend that you use g7ne.

    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|--------------------|:-----------------------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.c6e.large|2|4.0|Burstable up to 10.0|900,000|Up to 250,000|2|3|6|20,000|1.0|
|ecs.c6e.xlarge|4|8.0|Burstable up to 10.0|1,000,000|Up to 250,000|4|4|15|40,000|1.5|
|ecs.c6e.2xlarge|8|16.0|Burstable up to 10.0|1,600,000|Up to 250,000|8|4|15|50,000|2.0|
|ecs.c6e.4xlarge|16|32.0|Burstable up to 10.0|3,000,000|300,000|8|8|30|80,000|3.0|
|ecs.c6e.8xlarge|32|64.0|10.0|6,000,000|600,000|16|8|30|150,000|5.0|
|ecs.c6e.13xlarge|52|96.0|16.0|9,000,000|900,000|32|7|30|240,000|8.0|
|ecs.c6e.26xlarge|104|192.0|32.0|24,000,000|1,800,000|32|15|30|480,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other network metrics.

## c5, compute optimized instance family

Features

-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) or 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.

        **Note:** The maximum performance of disks varies based on instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.c5.large|2|4.0|1.0|300,000|2|2|6|
|ecs.c5.xlarge|4|8.0|1.5|500,000|2|3|10|
|ecs.c5.2xlarge|8|16.0|2.5|800,000|2|4|10|
|ecs.c5.3xlarge|12|24.0|4.0|900,000|4|6|10|
|ecs.c5.4xlarge|16|32.0|5.0|1,000,000|4|8|20|
|ecs.c5.6xlarge|24|48.0|7.5|1,500,000|6|8|20|
|ecs.c5.8xlarge|32|64.0|10.0|2,000,000|8|8|20|
|ecs.c5.16xlarge|64|128.0|20.0|4,000,000|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ic5, compute intensive instance family

Features

-   Compute:
    -   Offers a CPU-to-memory ratio of 1:1.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) or 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
-   Network:
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Web frontend servers
    -   Data analysis, batch processing, and video encoding
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Frontend servers of MMO games

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.ic5.large|2|2.0|1.0|300,000|2|2|6|
|ecs.ic5.xlarge|4|4.0|1.5|500,000|2|3|10|
|ecs.ic5.2xlarge|8|8.0|2.5|800,000|2|4|10|
|ecs.ic5.3xlarge|12|12.0|4.0|900,000|4|6|10|
|ecs.ic5.4xlarge|16|16.0|5.0|1,000,000|4|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## r7, memory optimized instance family

Features

-   Uses the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Supports the virtual Trusted Platform Module \(vTPM\) feature and implements trusted boots based on Trusted Cryptography Module \(TCM\) or Trusted Platform Module \(TPM\) chips to provide ultra-high security capabilities. During a trusted boot, all modules in the boot chain from the underlying server to the ECS instance are measured and verified.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses the third-generation Intel® Xeon® Scalable processors \(Ice Lake\) that deliver a base frequency of 2.7 GHz and an all-core turbo frequency of 3.5 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only enhanced SSDs \(ESSDs\).
    -   Provides burstable storage I/O performance for low-specification instances.
    -   Provides high storage I/O performance based on large computing capacity.
-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides burstable network performance for low-specification instances.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   High-performance databases and in-memory databases
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications
    -   Scenarios that require secure and trusted computing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|--------------------|:-----------------------------|------------|----------|:---|----------------------------|---------|-------------------------|
|ecs.r7.large|2|16.0|Burstable up to 10.0|900,000|Yes|2|3|6|Burstable up to 100,000|Burstable up to 6.0|
|ecs.r7.xlarge|4|32.0|Burstable up to 10.0|1,000,000|Yes|4|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.r7.2xlarge|8|64.0|Burstable up to 10.0|1,600,000|Yes|8|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.r7.3xlarge|12|96.0|Burstable up to 10.0|2,400,000|Yes|8|8|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.r7.4xlarge|16|128.0|Burstable up to 25.0|3,000,000|Yes|8|8|30|Burstable up to 100,000|Burstable up to 6.0|
|ecs.r7.6xlarge|24|192.0|Burstable up to 25.0|4,500,000|Yes|12|8|30|100,000|6.0|
|ecs.r7.8xlarge|32|256.0|Burstable up to 25.0|6,000,000|Yes|16|8|30|150,000|8.0|
|ecs.r7.16xlarge|64|512.0|32.0|12,000,000|Yes|32|8|30|300,000|16.0|
|ecs.r7.32xlarge|128|1024.0|64.0|24,000,000|Yes|32|15|30|600,000|32.0|

**Note:**

-   If you use Virtual Network Computing \(VNC\) to log on to a Windows instance, two cursors may appear. For information about how to fix this issue, see the “Why do two cursors appear after I use VNC to log on to a Windows instance?” section in [Instance FAQ](/intl.en-US/Instance/Instance FAQ.mdsection_jma_ml8_us3).
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## r7t, security-enhanced memory optimized instance family

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Supports up to 512 GiB encrypted memory and encrypted computing based on Intel® Software Guard Extensions \(SGX\) to protect the confidentiality and integrity of essential code and data from malware attacks.
-   Supports SGX technology applicable to virtual machines and allows you to select instance types that suit your needs.
-   Implements trusted boots based on TCM or TPM chips. During a trusted boot, all modules in the boot chain from the underlying server hardware to the guest OS are measured and verified.
-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8. About 50% of memory is encrypted.
    -   Uses the third-generation Intel® Xeon® Scalable processors for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs.
    -   Provides high storage I/O performance based on large computing capacity.
-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Encrypted computing applications for databases
    -   Scenarios that involve sensitive information such as personal identity information, healthcare information, financial information, and intellectual property data
    -   Scenarios where confidential data is shared among multiple parties
    -   Blockchain scenarios
    -   Confidential machine learning
    -   Scenarios that require high security and enhanced trust, such as finance, government, and enterprise services
    -   Enterprise-level applications of various types and sizes

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Encrypted portion of memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------------|--------------------|:-----------------------------|------------|----------|:---|----------------------------|---------|-------------------------|
|ecs.r7t.large|2|16.0|8.0|Burstable up to 10.0|900,000|Yes|2|3|6|Burstable up to 100,000|Burstable up to 6.0|
|ecs.r7t.xlarge|4|32.0|16.0|Burstable up to 10.0|1,000,000|Yes|4|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.r7t.2xlarge|8|64.0|32.0|Burstable up to 10.0|1,600,000|Yes|8|4|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.r7t.3xlarge|12|96.0|48.0|Burstable up to 10.0|2,400,000|Yes|8|8|15|Burstable up to 100,000|Burstable up to 6.0|
|ecs.r7t.4xlarge|16|128.0|64.0|Burstable up to 25.0|3,000,000|Yes|8|8|30|Burstable up to 100,000|Burstable up to 6.0|
|ecs.r7t.6xlarge|24|192.0|96.0|Burstable up to 25.0|4,500,000|Yes|12|8|30|100,000|6.0|
|ecs.r7t.8xlarge|32|256.0|128.0|Burstable up to 25.0|6,000,000|Yes|16|8|30|150,000|8.0|
|ecs.r7t.16xlarge|64|512.0|256.0|32.0|12,000,000|Yes|32|8|30|300,000|16.0|
|ecs.r7t.32xlarge|128|1024.0|512.0|64.0|24,000,000|Yes|32|15|30|600,000|32.0|

**Note:**

-   The instance family is in invitational preview. Resources are limited. No service level agreement \(SLA\) compliance is ensured. To use this instance family, submit an application based on your minimum business requirements.
-   Intel Ice Lake supports only remote attestation based on Intel SGX DCAP, and does not support remote attestation based on Intel EPID. You must adapt applications before you can use the remote attestation feature. For more information about remote attestation, see [attestation-service](https://software.intel.com/content/www/us/en/develop/topics/software-guard-extensions/attestation-services.html).
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## r6, memory optimized instance family

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.

        **Note:** The maximum performance of disks varies based on instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Supports changes to instance types in the g6 or c6 instance family.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   High-performance databases and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:----------------------------|------------------------------|:-----------------------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.r6.large|2|16.0|1.0|3.0|300,000|Up to 250,000|2|2|6|10,000|1|
|ecs.r6.xlarge|4|32.0|1.5|5.0|500,000|Up to 250,000|4|3|10|20,000|1.5|
|ecs.r6.2xlarge|8|64.0|2.5|8.0|800,000|Up to 250,000|8|4|10|25,000|2|
|ecs.r6.3xlarge|12|96.0|4.0|10.0|900,000|Up to 250,000|8|6|10|30,000|2.5|
|ecs.r6.4xlarge|16|128.0|5.0|10.0|1,000,000|300,000|8|8|20|40,000|3|
|ecs.r6.6xlarge|24|192.0|7.5|10.0|1,500,000|450,000|12|8|20|50,000|4|
|ecs.r6.8xlarge|32|256.0|10.0|None|2,000,000|600,000|16|8|20|60,000|5|
|ecs.r6.13xlarge|52|384.0|12.5|None|3,000,000|900,000|32|7|20|100,000|8|
|ecs.r6.26xlarge|104|768.0|25.0|None|6,000,000|1,800,000|32|15|20|200,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## re6p, persistent memory optimized instance family

For information about frequently asked questions about persistent memory optimized instances, see [Instance FAQ](/intl.en-US/Instance/Instance FAQ.md).

Features

-   Uses Intel® OptaneTM persistent memory.

    **Note:** The reliability of data stored in persistent memory depends on the reliability of persistent memory devices and the physical servers to which these devices are attached. This may cause risks of single points of failure. To ensure the reliability of application data, we recommend that you implement data redundancy at the application layer and use cloud disks for long-term data storage.

-   Allows persistent memory to be used as memory or as local SSDs on instances of some instance types.

    **Note:** For more information, see [Configure the usage mode of persistent memory](/intl.en-US/Instance/Instance type families/Memory optimized instance families/Configure the usage mode of persistent memory.md).

-   Exclusively provides the ecs.re6p-redis.<nx\>large instances types for Redis applications.

    **Note:** ecs.re6p-redis.<nx\>large instance types are exclusively provided for Redis applications. The persistent memory on instances of these instance types is used as memory by default and cannot be re-configured as local SSDs. For more information about how to deploy an Redis application, see [Deploy Redis applications on re6p instances](/intl.en-US/Instance/Instance type families/Memory optimized instance families/Deploy Redis applications on re6p instances.md).

-   Compute:
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Supports only virtual private clouds \(VPCs\).
-   Suits the following scenarios:
    -   Redis and other NoSQL databases such as Cassandra and MongoDB
    -   Structured databases such as MySQL
    -   I/O-intensive applications such as e-commerce, online games, and media applications
    -   Elasticsearch
    -   Live video streaming, instant messaging, and room-based online games that require persistent connections
    -   High-performance relational databases and online transaction processing \(OLTP\) systems

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Persistent memory \(GiB\)|Baseline bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-------------------------|-----------------------------|------------------------------|:-----------------------------|-----------|----------|:---|---------|-------------------------|
|ecs.re6p.large|2|8.0|31.5|1.0|3.0|300,000|Up to 250,000|2|2|10,000|1.0|
|ecs.re6p.xlarge|4|16.0|63.0|1.5|5.0|500,000|Up to 250,000|4|3|20,000|1.5|
|ecs.re6p.2xlarge|8|32.0|126.0|2.5|10.0|800,000|Up to 250,000|8|4|25,000|2.0|
|ecs.re6p.13xlarge|52|192.0|756.0|12.5|None|3,000,000|900,000|32|7|100,000|8.0|
|ecs.re6p.26xlarge|104|384.0|1512.0|25.0|None|6,000,000|1,800,000|32|15|200,000|16,0|
|ecs.re6p-redis.large|2|8.0|31.5|1.0|3.0|300,000|Up to 250,000|2|2|10,000|1.0|
|ecs.re6p-redis.xlarge|4|16.0|63.0|1.5|5.0|500,000|Up to 250,000|4|3|20,000|1.5|
|ecs.re6p-redis.2xlarge|8|32.0|126.0|2.5|10.0|800,000|Up to 250,000|8|4|25,000|2.0|
|ecs.re6p-redis.13xlarge|52|192.0|756.0|12.5|None|3,000,000|900,000|32|7|100,000|8.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## r6a, memory optimized instance family

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses 2.6 GHz AMD EPYCTM ROME processors that deliver a turbo frequency of 3.3 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Video encoding and decoding
    -   Scenarios where large volumes of packets are received and transmitted
    -   In-memory databases
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications
    -   Scenarios where applications such as DevOps applications are developed and tested

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|ENIs|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------|------------------------------|:-----------------------------|:---|---------|-------------------------|
|ecs.r6a.large|2|16.0|1.0|10.0|900,000|2|12,500|1.0|
|ecs.r6a.xlarge|4|32.0|1.5|10.0|1,000,000|3|20,000|1.5|
|ecs.r6a.2xlarge|8|64.0|2.5|10.0|1,600,000|4|30,000|2.0|
|ecs.r6a.4xlarge|16|128.0|5.0|10.0|2,000,000|8|60,000|3.0|
|ecs.r6a.8xlarge|32|256.0|8.0|10.0|3,000,000|7|75,000|4,0|
|ecs.r6a.16xlarge|64|512.0|16.0|None|6,000,000|8|150,000|8.0|
|ecs.r6a.32xlarge|128|1024.0|32.0|None|12,000,000|15|300,000|16.0|
|ecs.r6a.64xlarge|256|2048.0|64.0|None|24,000,000|15|600,000|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## r6e, memory optimized instance family with enhanced performance

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269 processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs.
    -   Provides high network and storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.

        **Note:** The network performance varies based on instance families. For higher concurrent connection and network packet forwarding capabilities, we recommend that you use g7ne.

-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   High-performance databases and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|--------------------|:-----------------------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.r6e.large|2|16.0|Burstable up to 10.0|900,000|Up to 250,000|2|3|6|20,000|1.0|
|ecs.r6e.xlarge|4|32.0|Burstable up to 10.0|1,000,000|Up to 250,000|4|4|15|40,000|1.5|
|ecs.r6e.2xlarge|8|64.0|Burstable up to 10.0|1,600,000|Up to 250,000|8|4|15|50,000|2.0|
|ecs.r6e.4xlarge|16|128.0|Burstable up to 10.0|3,000,000|300,000|8|8|30|80,000|3.0|
|ecs.r6e.8xlarge|32|256.0|10.0|6,000,000|600,000|16|8|30|150,000|5.0|
|ecs.r6e.13xlarge|52|384.0|16.0|9,000,000|900,000|32|7|30|240,000|8.0|
|ecs.r6e.26xlarge|104|768.0|32.0|24,000,000|1,800,000|32|15|30|480,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other network metrics.

## re6, high memory instance family

Features

-   Is optimized for high-performance databases, in-memory databases, and other memory-intensive enterprise applications.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:15 and up to 3 TiB memory.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6.
-   Suits the following scenarios:
    -   High-performance databases and in-memory databases such as SAP HANA
    -   Memory-intensive applications
    -   Big data processing engines such as Apache Spark and Presto

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.re6.13xlarge|52|768.0|10.0|1,800,000|16|7|20|50,000|4|
|ecs.re6.26xlarge|104|1536.0|16.0|3,000,000|32|7|20|100,000|8|
|ecs.re6.52xlarge|208|3072.0|32.0|6,000,000|32|15|20|200,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## r5, memory optimized instance family

Features

-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) or Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.

        **Note:** The maximum performance of disks varies based on instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   High-performance databases and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.r5.large|2|16.0|1.0|300,000|2|2|6|
|ecs.r5.xlarge|4|32.0|1.5|500,000|2|3|10|
|ecs.r5.2xlarge|8|64.0|2.5|800,000|2|4|10|
|ecs.r5.3xlarge|12|96.0|4.0|900,000|4|6|10|
|ecs.r5.4xlarge|16|128.0|5.0|1,000,000|4|8|20|
|ecs.r5.6xlarge|24|192.0|7.5|1,500,000|6|8|20|
|ecs.r5.8xlarge|32|256.0|10.0|2,000,000|8|8|20|
|ecs.r5.16xlarge|64|512.0|20.0|4,000,000|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

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

## hfc7, compute optimized instance family with high clock speeds

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses Intel® Xeon® Cooper Lake processors that deliver an all-core turbo frequency of 3.8 GHz and have a minimum clock speed of 3.3 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only enhanced SSDs \(ESSDs\) and provides ultra-high I/O performance.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   High-performance frontend server clusters
    -   Frontend servers of massive multiplayer online \(MMO\) games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------------------------------|---------------------------------------------|:---------------------------------------------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.hfc7.large|2|4.0|1.2|10.0|900|250|2|2|6|20|1.0|
|ecs.hfc7.xlarge|4|8.0|2.0|10.0|1,000|250|4|3|15|30|1.5|
|ecs.hfc7.2xlarge|8|16.0|3.0|10.0|1,600|250|8|4|15|45|2.0|
|ecs.hfc7.3xlarge|12|24.0|4.5|10.0|2,000|250|8|6|15|60|2.5|
|ecs.hfc7.4xlarge|16|32.0|6.0|10.0|2,500|300|8|8|300|75|3.0|
|ecs.hfc7.6xlarge|24|48.0|8.0|10.0|3,000|450|12|8|300|90|4.0|
|ecs.hfc7.8xlarge|32|64.0|10.0|None|4,000|600|16|8|300|105|5.0|
|ecs.hfc7.12xlarge|48|96.0|16.0|None|6,000|1,000|24|8|300|150|8.0|
|ecs.hfc7.24xlarge|96|192.0|32.0|None|12,000|1,800|32|15|300|300|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## hfc6, compute optimized instance family with high clock speeds

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses 3.1 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver a turbo frequency of 3.5 GHz for consistent computing performance.

        **Note:** The CPUs used by this instance family have a clock speed of 3.1 GHz. The Intel System Studio \(ISS\) feature may cause a lower clock speed to be displayed. Alibaba Cloud is working on this issue. This issue does not affect the actual clock speeds of your instances.

        You can separately run the following commands and use the turbostat tool to view the actual clock speeds:

        ```
        yum install kernel-tools
        ```

        ```
        turbostat
        ```

    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs, standard SSDs, and ultra disks.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------------------------------|---------------------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.hfc6.large|2|4.0|1.0|3.0|300|2|2|6|10|1.0|
|ecs.hfc6.xlarge|4|8.0|1.5|5.0|500|4|3|10|20|1.5|
|ecs.hfc6.2xlarge|8|16.0|2.5|8.0|800|8|4|10|25|2.0|
|ecs.hfc6.3xlarge|12|24.0|4.0|10.0|900|8|6|10|30|2.5|
|ecs.hfc6.4xlarge|16|32.0|5.0|10.0|1,000|8|8|20|40|3.0|
|ecs.hfc6.6xlarge|24|48.0|75|10.0|1,500|12|8|20|50|4.0|
|ecs.hfc6.8xlarge|32|64.0|10.0|None|2,000|16|8|20|60|5.0|
|ecs.hfc6.10xlarge|40|96.0|12.5|None|3,000|32|7|20|100|8.0|
|ecs.hfc6.16xlarge|64|128.0|20.0|None|4,000|32|8|20|120|10.0|
|ecs.hfc6.20xlarge|80|192.0|25.0|None|6,000|32|15|20|200|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## hfg7, general purpose instance family with high clock speeds

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses Intel® Xeon® Cooper Lake processors that deliver an all-core turbo frequency of 3.8 GHz and have a minimum clock speed of 3.3 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs and provides ultra-high I/O performance.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-grade applications of various types and sizes
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   High-performance scientific computing
    -   Video encoding applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------------------------------|---------------------------------------------|:---------------------------------------------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.hfg7.large|2|8.0|1.2|10.0|900|250|2|2|6|20|1.0|
|ecs.hfg7.xlarge|4|16.0|2.0|10.0|1,000|250|4|3|15|30|1.5|
|ecs.hfg7.2xlarge|8|32.0|3.0|10.0|1,600|250|8|4|15|45|2.0|
|ecs.hfg7.3xlarge|12|48.0|4.5|10.0|2,000|250|8|6|15|60|2.5|
|ecs.hfg7.4xlarge|16|64.0|6.0|10.0|2,500|300|8|8|300|75|3.0|
|ecs.hfg7.6xlarge|24|96.0|8.0|10.0|3,000|450|12|8|300|90|4.0|
|ecs.hfg7.8xlarge|32|128.0|10.0|None|4,000|600|16|8|300|105|5.0|
|ecs.hfg7.12xlarge|48|192.0|16.0|None|6,000|1,000|24|8|300|150|8.0|
|ecs.hfg7.24xlarge|96|384.0|32.0|None|12,000|1,800|32|15|300|300|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## hfg6, general purpose instance family with high clock speeds

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 3.1 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver a turbo frequency of 3.5 GHz for consistent computing performance.

        **Note:** The CPUs used by this instance family have a clock speed of 3.1 GHz. The Intel System Studio \(ISS\) feature may cause a lower clock speed to be displayed. Alibaba Cloud is working on this issue. This issue does not affect the actual clock speeds of your instances.

        You can separately run the following commands and use the turbostat tool to view the actual clock speeds:

        ```
        yum install kernel-tools
        ```

        ```
        turbostat
        ```

    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs, standard SSDs, and ultra disks.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-grade applications of various types and sizes
    -   Websites and application servers
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------------------------------|---------------------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.hfg6.large|2|8.0|1.0|3.0|300|2|2|6|10|1.0|
|ecs.hfg6.xlarge|4|16.0|1.5|5.0|500|4|3|10|20|1.5|
|ecs.hfg6.2xlarge|8|32.0|2.5|8.0|800|8|4|10|25|2.0|
|ecs.hfg6.3xlarge|12|48.0|4.0|10.0|900|8|6|10|30|2.5|
|ecs.hfg6.4xlarge|16|64.0|5.0|10.0|1,000|8|8|20|40|3.0|
|ecs.hfg6.6xlarge|24|96.0|7.5|10.0|1,500|12|8|20|50|4.0|
|ecs.hfg6.8xlarge|32|128.0|10.0|None|2,000|16|8|20|60|5.0|
|ecs.hfg6.10xlarge|40|192.0|12.5|None|3,000|32|7|20|100|8.0|
|ecs.hfg6.16xlarge|64|256.0|20.0|None|4,000|32|8|20|120|10.0|
|ecs.hfg6.20xlarge|80|384.0|25.0|None|6,000|32|15|20|200|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## hfr7, memory optimized instance family with high clock speeds

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses Intel® Xeon® Cooper Lake processors that deliver an all-core turbo frequency of 3.8 GHz and have a minimum clock speed of 3.3 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs and provides ultra-high I/O performance.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------------------------------|---------------------------------------------|:---------------------------------------------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.hfr7.large|2|16.0|1.2|10.0|900|250|2|2|6|20|1.0|
|ecs.hfr7.xlarge|4|32.0|2.0|10.0|1,000|250|4|3|15|30|1.5|
|ecs.hfr7.2xlarge|8|64.0|3.0|10.0|1,600|250|8|4|15|45|2.0|
|ecs.hfr7.3xlarge|12|96.0|4.5|10.0|2,000|250|8|6|15|60|2.5|
|ecs.hfr7.4xlarge|16|128.0|6.0|10.0|2,500|300|8|8|300|75|3.0|
|ecs.hfr7.6xlarge|24|192.0|8.0|10.0|3,000|450|12|8|300|90|4.0|
|ecs.hfr7.8xlarge|32|256.0|10.0|None|4,000|600|16|8|300|105|5.0|
|ecs.hfr7.12xlarge|48|384.0|16.0|None|6,000|1,000|24|8|300|150|8.0|
|ecs.hfr7.24xlarge|96|768.0|32.0|None|12,000|1,800|32|15|300|300|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## hfr6, memory optimized instance family with high clock speeds

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses 3.1 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver a turbo frequency of 3.5 GHz for consistent computing performance.

        **Note:** The CPUs used by this instance family have a clock speed of 3.1 GHz. The Intel System Studio \(ISS\) feature may cause a lower clock speed to be displayed. Alibaba Cloud is working on this issue. This issue does not affect the actual clock speeds of your instances.

        You can separately run the following commands and use the turbostat tool to view the actual clock speeds:

        ```
        yum install kernel-tools
        ```

        ```
        turbostat
        ```

    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs, standard SSDs, and ultra disks.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------------------------------|---------------------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.hfr6.large|2|16.0|1.0|3.0|300|2|2|6|10|1.0|
|ecs.hfr6.xlarge|4|32.0|1.5|5.0|500|4|3|10|20|1.5|
|ecs.hfr6.2xlarge|8|64.0|2.5|8.0|800|8|4|10|25|2.0|
|ecs.hfr6.3xlarge|12|96.0|4.0|10.0|900|8|6|10|30|2.5|
|ecs.hfr6.4xlarge|16|128.0|5.0|10.0|1,000|8|8|20|40|3.0|
|ecs.hfr6.6xlarge|24|192.0|7.5|10.0|1,500|12|8|20|50|4.0|
|ecs.hfr6.8xlarge|32|256.0|10.0|None|2,000|16|8|20|60|5.0|
|ecs.hfr6.10xlarge|40|384.0|12.5|None|3,000|32|7|20|100|8.0|
|ecs.hfr6.16xlarge|64|512.0|20.0|None|4,000|32|8|20|120|10.0|
|ecs.hfr6.20xlarge|80|768.0|25.0|None|6,000|32|15|20|200|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## sn2ne, general purpose instance family with enhanced network performance

Features

-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) or Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-level applications of various types and sizes
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.sn2ne.large|2|8.0|1.0|300,000|2|2|6|
|ecs.sn2ne.xlarge|4|16.0|1.5|500,000|2|3|10|
|ecs.sn2ne.2xlarge|8|32.0|2.0|1,000,000|4|4|10|
|ecs.sn2ne.3xlarge|12|48.0|2.5|1,300,000|4|6|10|
|ecs.sn2ne.4xlarge|16|64.0|3.0|1,600,000|4|8|20|
|ecs.sn2ne.6xlarge|24|96.0|4.5|2,000,000|6|8|20|
|ecs.sn2ne.8xlarge|32|128.0|6.0|2,500,000|8|8|20|
|ecs.sn2ne.14xlarge|56|224.0|10.0|4,500,000|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## sn1ne, compute optimized instance family with enhanced network performance

Features

-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) or Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.sn1ne.large|2|4.0|1.0|300,000|2|2|6|
|ecs.sn1ne.xlarge|4|8.0|1.5|500,000|2|3|10|
|ecs.sn1ne.2xlarge|8|16.0|2.0|1,000,000|4|4|10|
|ecs.sn1ne.3xlarge|12|24.0|2.5|1,300,000|4|6|10|
|ecs.sn1ne.4xlarge|16|32.0|3.0|1,600,000|4|8|20|
|ecs.sn1ne.6xlarge|24|48.0|4.5|2,000,000|6|8|20|
|ecs.sn1ne.8xlarge|32|64.0|6.0|2,500,000|8|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## re4, high memory instance family

Features

-   Is optimized for high-performance databases, in-memory databases, and other memory-intensive enterprise applications.
-   The ecs.re4.20xlarge and ecs.re4.40xlarge instance types are SAP HANA-certified.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:12 and up to 1,920 GiB memory.
    -   Uses 2.2 GHz Intel® Xeon® E7 8880 v4 \(Broadwell\) processors that deliver a maximum turbo frequency of 2.4 GHz for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
-   Suits the following scenarios:
    -   High-performance databases and in-memory databases such as SAP HANA
    -   Memory-intensive applications
    -   Big data processing engines such as Apache Spark and Presto

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.re4.10xlarge|40|480.0|8.0|1,000,000|8|4|10|
|ecs.re4.20xlarge|80|960.0|15.0|2,000,000|16|8|20|
|ecs.re4.40xlarge|160|1920.0|30.0|4,500,000|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## re4e, high memory instance family

Features

-   Is optimized for high-performance databases, in-memory databases, and other memory-intensive enterprise applications.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:24 and up to 3,840 GiB memory.
    -   Uses 2.2 GHz Intel® Xeon® E7 8880 v4 \(Broadwell\) processors that deliver a maximum turbo frequency of 2.4 GHz for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
-   Suits the following scenarios:
    -   High-performance databases and in-memory databases such as SAP HANA
    -   Memory-intensive applications
    -   Big data processing engines such as Apache Spark and Presto

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.re4e.40xlarge|160|3840.0|30.0|4,500,000|16|15|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## se1ne, memory optimized instance family with enhanced network performance

Features

-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) or Intel® Xeon® Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   High-performance databases and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.se1ne.large|2|16.0|1.0|300,000|2|2|6|
|ecs.se1ne.xlarge|4|32.0|1.5|500,000|2|3|10|
|ecs.se1ne.2xlarge|8|64.0|2.0|1,000,000|4|4|10|
|ecs.se1ne.3xlarge|12|96.0|2.5|1,300,000|4|6|10|
|ecs.se1ne.4xlarge|16|128.0|3.0|1,600,000|4|8|20|
|ecs.se1ne.6xlarge|24|192.0|4.5|2,000,000|6|8|20|
|ecs.se1ne.8xlarge|32|256.0|6.0|2,500,000|8|8|20|
|ecs.se1ne.14xlarge|56|480.0|10.0|4,500,000|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## se1, memory optimized instance family

Features

-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   High-performance databases and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.se1.large|2|16.0|0.5|100,000|1|2|6|
|ecs.se1.xlarge|4|32.0|0.8|200,000|1|3|10|
|ecs.se1.2xlarge|8|64.0|1.5|400,000|1|4|10|
|ecs.se1.4xlarge|16|128.0|3.0|500,000|2|8|20|
|ecs.se1.8xlarge|32|256.0|6.0|800,000|3|8|20|
|ecs.se1.14xlarge|56|480.0|10.0|1,200,000|4|8|20|

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

## hfc5, compute optimized instance family with high clock speeds

Features

-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses 3.1 GHz Intel® Xeon® Gold 6149 \(Skylake\) processors.
    -   Provides consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   High-performance web frontend servers
    -   High-performance scientific and engineering applications
    -   MMO gaming and video encoding

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.hfc5.large|2|4.0|1.0|300|2|2|6|
|ecs.hfc5.xlarge|4|8.0|1.5|500|2|3|10|
|ecs.hfc5.2xlarge|8|16.0|2.0|1,000|2|4|10|
|ecs.hfc5.3xlarge|12|24.0|2.5|1,300|4|6|10|
|ecs.hfc5.4xlarge|16|32.0|3.0|1,600|4|8|20|
|ecs.hfc5.6xlarge|24|48.0|4.5|2,000|6|8|20|
|ecs.hfc5.8xlarge|32|64.0|6.0|2,500|8|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## hfg5, general purpose instance family with high clock speeds

Features

-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4 \(excluding the instance type that has 56 vCPUs\).
    -   Uses 3.1 GHz Intel® Xeon® Gold 6149 \(Skylake\) processors.
    -   Provides consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   High-performance web frontend servers
    -   High-performance scientific and engineering applications
    -   MMO gaming and video encoding

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.hfg5.large|2|8.0|1.0|300|2|2|6|
|ecs.hfg5.xlarge|4|16.0|1.5|500|2|3|10|
|ecs.hfg5.2xlarge|8|32.0|2.0|1,000|2|4|10|
|ecs.hfg5.3xlarge|12|48.0|2.5|1,300|4|6|10|
|ecs.hfg5.4xlarge|16|64.0|3.0|1,600|4|8|20|
|ecs.hfg5.6xlarge|24|96.0|4.5|2,000|6|8|20|
|ecs.hfg5.8xlarge|32|128.0|6.0|2,500|8|8|20|
|ecs.hfg5.14xlarge|56|160.0|10.0|4,000|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn7, GPU-accelerated compute optimized instance family

This instance family is in invitational preview and unavailable for sale.

Features

-   Compute:
    -   Uses NVIDIA A100 GPUs. NVSwitches are used to establish connections between NVIDIA A100 GPUs.
        -   New Ampere architecture
        -   40 GB HBM2 memory per GPU
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs \(ESSDs\), standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6 addresses.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning applications such as training applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications that have high GPU workloads such as computational fluid dynamics, computational finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPU|Memory \(GiB\)|GPU|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|
|:------------|:---|:-------------|:--|:---------|--------------------|:------------------------------|:---------|:---|
|ecs.gn7-c12g1.3xlarge|12|95.0|NVIDIA A100 \* 1|40GB \* 1|4.0|2,500|4|8|
|ecs.gn7-c13g1.13xlarge|52|380.0|NVIDIA A100 \* 4|40GB \* 4|15.0|9,000|16|8|
|ecs.gn7-c13g1.26xlarge|104|760.0|NVIDIA A100 \* 8|40GB \* 8|30.0|18,000|16|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## vgn6i, lightweight GPU-accelerated compute optimized instance family

Features

-   If you want your vgn6i instance to support graphics features such as Open Graphics Library \(OpenGL\), you must purchase a GRID license from [NVIDIA](https://www.nvidia.com/object/nvidia-enterprise-account.html). Then, you must create an instance and manually install a GRID driver and activate the license after the instance is created.
-   Compute:
    -   Uses NVIDIA T4 GPU computing accelerators.
    -   Contains virtual GPUs generated from GPU slice virtualization.
        -   Supports the 1/4 and 1/2 computing capacity of NVIDIA Tesla T4 GPUs.
        -   Supports 4 GB and 8 GB of GPU video memory.
    -   Offers a CPU-to-memory ratio of 1:5.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports standard SSDs and ultra disks only.
-   Network:
    -   Supports IPv6 addresses.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Real-time rendering for cloud games
    -   Real-time rendering for AR and VR applications
    -   AI \(deep learning and machine learning\) inference for elastic Internet service deployment
    -   Educational environment of deep learning
    -   Modeling experiment environment of deep learning

Instance types

|Instance type|vCPU|Memory \(GiB\)|GPU|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:--|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.vgn6i-m4.xlarge|4|23.0|NVIDIA T4 \* 1/4|16GB \* 1/4|3.0|500|2|4|10|
|ecs.vgn6i-m8.2xlarge|10|46.0|NVIDIA T4 \* 1/2|16GB \* 1/2|4.0|800|4|5|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn6i, GPU-accelerated compute optimized instance family

Features

-   Compute:
    -   Uses NVIDIA T4 GPUs that feature:
        -   New NVIDIA Turing architecture
        -   16 GB memory per GPU \(320 GB/s bandwidth\)
        -   2,560 CUDA cores per GPU
        -   Up to 320 Turing Tensor cores per GPU
        -   Mixed-precision Tensor cores that support 65 FP16 TFLOPS, 130 INT8 TOPS, and 260 INT4 TOPS
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports standard SSDs, ultra disks, and ESSDs that deliver millions of input/output operations per second \(IOPS\).
-   Network:
    -   Supports IPv6 addresses.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   AI \(deep learning and machine learning\) inference for computer vision, speech recognition, speech synthesis, natural language processing \(NLP\), machine translation, and recommendation systems
    -   Real-time rendering for cloud games
    -   Real-time rendering for AR and VR applications
    -   Graphics workstations or overloaded graphics computing
    -   GPU-accelerated databases
    -   High-performance computing

Instance types

|Instance type|vCPU|Memory \(GiB\)|GPU|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:--|:---------|--------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.gn6i-c4g1.xlarge|4|15.0|NVIDIA T4 \* 1|16GB \* 1|4.0|500|2|2|10|
|ecs.gn6i-c8g1.2xlarge|8|31.0|NVIDIA T4 \* 1|16GB \* 1|5.0|800|2|2|10|
|ecs.gn6i-c16g1.4xlarge|16|62.0|NVIDIA T4 \* 1|16GB \* 1|6.0|1,000|4|3|10|
|ecs.gn6i-c24g1.6xlarge|24|93.0|NVIDIA T4 \* 1|16GB \* 1|7.5|1,200|6|4|10|
|ecs.gn6i-c24g1.12xlarge|48|186.0|NVIDIA T4 \* 2|16GB \* 2|15.0|2,400|12|6|10|
|ecs.gn6i-c24g1.24xlarge|96|372.0|NVIDIA T4 \* 4|16GB \* 4|30.0|4,800|24|8|10|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn6e, GPU-accelerated compute optimized instance family

Features

-   Compute:
    -   Uses NVIDIA V100 \(32 GB NVLink\) GPU processors.
    -   Uses NVIDIA V100 GPUs \(SXM2-based\) that feature:
        -   New Volta architecture
        -   32 GB HBM2 memory \(900 GB/s bandwidth\) per GPU
        -   5,120 CUDA cores per GPU
        -   640 Tensor cores per GPU
        -   Up to six NVLink connections and a total bandwidth of 300 Gbit/s \(25 Gbit/s per connection\)
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6 addresses.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning applications such as training and inference applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications such as fluid dynamics, finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPU|Memory \(GiB\)|GPU|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:--|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.gn6e-c12g1.3xlarge|12|92.0|NVIDIA V100 \* 1|32GB \* 1|5.0|800|8|6|10|
|ecs.gn6e-c12g1.12xlarge|48|368.0|NVIDIA V100 \* 4|32GB \* 4|16.0|2,400|8|8|20|
|ecs.gn6e-c12g1.24xlarge|96|736.0|NVIDIA V100 \* 8|32GB \* 8|32.0|4,800|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn6v, GPU-accelerated compute optimized instance family

Features

-   Compute:
    -   Uses NVIDIA V100 GPUs.
    -   Uses NVIDIA V100 GPUs \(SXM2-based\) that feature:
        -   New Volta architecture
        -   16 GB HBM2 memory per GPU \(900 Gbit/s bandwidth\)
        -   5,120 CUDA cores per GPU
        -   640 Tensor cores per GPU
        -   Up to six NVLink connections and a total bandwidth of 300 Gbit/s \(25 Gbit/s per connection\)
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6 addresses.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning applications such as training and inference applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications such as fluid dynamics, finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPU|Memory \(GiB\)|GPU|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:--|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.gn6v-c8g1.2xlarge|8|32.0|NVIDIA V100 \* 1|16GB \* 1|2.5|800|4|4|10|
|ecs.gn6v-c8g1.8xlarge|32|128.0|NVIDIA V100 \* 4|16GB \* 4|10.0|2,000|8|8|20|
|ecs.gn6v-c8g1.16xlarge|64|256.0|NVIDIA V100 \* 8|16GB \* 8|20.0|2,500|16|8|20|
|ecs.gn6v-c10g1.20xlarge|82|336.0|NVIDIA V100 \* 8|16GB \* 8|32.0|4,500|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## f3, FPGA-accelerated compute optimized instance family

Features

-   Uses Xilinx 16nm Virtex UltraScale+ VU9P FPGAs.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning and inference
    -   Genomics research
    -   Database acceleration
    -   Image transcoding such as conversion of JPEG images to WebP images
    -   Real-time video processing such as H.265 video compression

Instance types

|Instance type|vCPUs|Memory \(GiB\)|FPGAs|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:----|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.f3-c4f1.xlarge|4|16.0|1 × Xilinx VU9P|1.5|300|2|3|10|
|ecs.f3-c8f1.2xlarge|8|32.0|1 × Xilinx VU9P|2.5|500|4|4|10|
|ecs.f3-c16f1.4xlarge|16|64.0|1 × Xilinx VU9P|5.0|1,000|4|8|20|
|ecs.f3-c16f1.8xlarge|32|128.0|2 × Xilinx VU9P|10.0|2,000|8|8|20|
|ecs.f3-c16f1.16xlarge|64|256.0|4 × Xilinx VU9P|20.0|2,500|16|8|20|
|ecs.f3-c22f1.22xlarge|88|336.0|4 × Xilinx VU9P|30.0|4,500|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## vgn5i, lightweight GPU-accelerated compute optimized instance family

Features

-   If you want your vgn5i instance to support graphics features such as Open Graphics Library \(OpenGL\), you must purchase a GRID license from [NVIDIA](https://www.nvidia.com/object/nvidia-enterprise-account.html). Then, you must create an instance and manually install a GRID driver and activate the license after the instance is created.
-   Compute:
    -   Uses NVIDIA P4 GPU computing accelerators.
    -   Contains virtual GPUs generated from GPU slice virtualization.
        -   Supports the 1/8, 1/4, 1/2, and 1/1 computing capacity of NVIDIA Tesla P4 GPUs.
        -   Supports 1 GB, 2 GB, 4 GB, and 8 GB of GPU memory.
    -   Offers a CPU-to-memory ratio of 1:3.
    -   Uses 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports standard SSDs and ultra disks only.
-   Network:
    -   Supports IPv6 addresses.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Real-time rendering for cloud games
    -   Real-time rendering for AR and VR applications
    -   AI \(deep learning and machine learning\) inference for elastic Internet service deployment
    -   Educational environment of deep learning
    -   Modeling experiment environment of deep learning

Instance types

|Instance type|vCPU|Memory \(GiB\)|GPU|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:--|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.vgn5i-m1.large|2|6.0|NVIDIA P4 \* 1/8|8GB \* 1/8|1.0|300|2|2|6|
|ecs.vgn5i-m2.xlarge|4|12.0|NVIDIA P4 \* 1/4|8GB \* 1/4|2.0|500|2|3|10|
|ecs.vgn5i-m4.2xlarge|8|24.0|NVIDIA P4 \* 1/2|8GB \* 1/2|3.0|800|2|4|10|
|ecs.vgn5i-m8.4xlarge|16|48.0|NVIDIA P4 \* 1|8GB \* 1|5.0|1,000|4|5|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn5, GPU-accelerated compute optimized instance family

Features

-   Compute:
    -   Uses NVIDIA P100 GPU processors.
    -   Offers multiple CPU-to-memory ratios.
    -   Uses 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) processors.
-   Storage:
    -   Supports high-performance local NVMe SSDs.
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports standard SSDs and ultra disks only.
-   Network:
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning
    -   Scientific computing applications, such as fluid dynamics, finance, genomics, and environmental analysis
    -   Server-side GPU compute workloads such as high-performance computing, rendering, and multi-media encoding and decoding

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|GPU|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:--|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.gn5-c4g1.xlarge|4|30.0|440|NVIDIA P100 \* 1|16GB \* 1|3.0|300|1|3|10|
|ecs.gn5-c8g1.2xlarge|8|60.0|440|NVIDIA P100 \* 1|16GB \* 1|3.0|400|1|4|10|
|ecs.gn5-c4g1.2xlarge|8|60.0|880|NVIDIA P100 \* 2|16GB \* 2|5.0|1,000|2|4|10|
|ecs.gn5-c8g1.4xlarge|16|120.0|880|NVIDIA P100 \* 2|16GB \* 2|5.0|1,000|4|8|20|
|ecs.gn5-c28g1.7xlarge|28|112.0|440|NVIDIA P100 \* 1|16GB \* 1|5.0|1,000|8|8|20|
|ecs.gn5-c8g1.8xlarge|32|240.0|1760|NVIDIA P100 \* 4|16GB \* 4|10.0|2,000|8|8|20|
|ecs.gn5-c28g1.14xlarge|56|224.0|880|NVIDIA P100 \* 2|16GB \* 2|10.0|2,000|14|8|20|
|ecs.gn5-c8g1.14xlarge|54|480.0|3520|NVIDIA P100 \* 8|16GB \* 8|25.0|4,000|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## gn5i, GPU-accelerated compute optimized instance family

Features

-   Compute:
    -   Uses NVIDIA P4 GPUs.
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports standard SSDs and ultra disks only.
-   Network:
    -   Supports IPv6 addresses.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning inference
    -   Server-side GPU compute workloads such as multi-media encoding and decoding

Instance types

|Instance type|vCPU|Memory \(GiB\)|GPU|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:--|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.gn5i-c2g1.large|2|8.0|NVIDIA P4 \* 1|8GB \* 1|1.0|100|2|2|6|
|ecs.gn5i-c4g1.xlarge|4|16.0|NVIDIA P4 \* 1|8GB \* 1|1.5|200|2|3|10|
|ecs.gn5i-c8g1.2xlarge|8|32.0|NVIDIA P4 \* 1|8GB \* 1|2.0|400|4|4|10|
|ecs.gn5i-c16g1.4xlarge|16|64.0|NVIDIA P4 \* 1|8GB \* 1|3.0|800|4|8|20|
|ecs.gn5i-c16g1.8xlarge|32|128.0|NVIDIA P4 \* 2|8GB \* 2|6.0|1,200|8|8|20|
|ecs.gn5i-c28g1.14xlarge|56|224.0|NVIDIA P4 \* 2|8GB \* 2|10.0|2,000|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## f1, FPGA-accelerated compute optimized instance family

Features

-   Uses Intel® Arria® 10 GX 1150 FPGAs
-   Compute:
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
    -   Offers a CPU-to-memory ratio of 1:7.5.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning and inference
    -   Genomics research
    -   Financial analysis
    -   Image transcoding
    -   Computational workloads such as real-time video processing and security management

Instance types

|Instance type|vCPUs|Memory \(GiB\)|FPGAs|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:----|:----------------------------------|:---------------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.f1-c8f1.2xlarge|8|60.0|Intel ARRIA 10 GX 1150|3.0|400|4|4|10|
|ecs.f1-c8f1.4xlarge|16|120.0|2 × Intel ARRIA 10 GX 1150|5.0|1,000|4|8|20|
|ecs.f1-c28f1.7xlarge|28|112.0|Intel ARRIA 10 GX 1150|5.0|2,000|8|8|20|
|ecs.f1-c28f1.14xlarge|56|224.0|2 × Intel ARRIA 10 GX 1150|10.0|2,000|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmgn7, GPU-accelerated compute optimized ECS Bare Metal Instance family

Features

-   Provides flexible and powerful software-defined compute based on the SHENLONG architecture.
-   Uses NVIDIA A100 GPUs. NVSwitches are used to establish connections between NVIDIA A100 GPUs. The GPUs have the following features:
    -   Innovative Ampere architecture
    -   40 GB HBM2 memory per GPU
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8269CY \(Cascade Lake\) processors.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning applications such as training applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications that have high GPU workloads, such as computational fluid dynamics, computational finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|----|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.ebmgn7.26xlarge|104|768.0|NVIDIA A100 × 8|30.0|18,000,000|16|15|10|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmgn6e, GPU-accelerated compute optimized ECS Bare Metal Instance family

Features

-   Provides flexible and powerful software-defined compute based on the SHENLONG architecture.
-   Uses NVIDIA V100 \(32 GB NVLink\) GPUs.
-   Uses NVIDIA V100 GPUs \(SXM2-based\) that have the following features:
    -   Innovative Volta architecture
    -   32 GB HBM2 memory \(900 GB/s bandwidth\) per GPU
    -   5,120 CUDA cores per GPU
    -   640 Tensor cores per GPU
    -   Support for up to six NVLink connections for a total bandwidth of 300 GB/s per GPU \(25 GB/s per connection\)
-   Offers a CPU-to-memory ratio of 1:8.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning applications such as training and inference applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications such as computational fluid dynamics, computational finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory \(GB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|----|-----------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.ebmgn6e.24xlarge|96|768.0|NVIDIA V100 × 8|32 GB × 8|32.0|4,800,000|16|15|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmgn6v, GPU-accelerated compute optimized ECS Bare Metal Instance family

Features

-   Provides flexible and powerful software-defined compute based on the SHENLONG architecture.
-   Uses NVIDIA V100 GPUs.
-   Uses NVIDIA V100 GPUs \(SXM2-based\) that have the following features:
    -   Innovative Volta architecture
    -   16 GB HBM2 memory \(900 GB/s bandwidth\) per GPU
    -   5,120 CUDA cores per GPU
    -   640 Tensor cores per GPU
    -   Support for up to six NVLink connections for a total bandwidth of 300 GB/s per GPU \(25 GB/s per connection\)
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning applications such as training and inference applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications such as computational fluid dynamics, computational finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory \(GB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|----|-----------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.ebmgn6v.24xlarge|96|384.0|NVIDIA V100 × 8|16GB × 8|30.0|4,500,000|8|32|10|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmgn6i, GPU-accelerated compute optimized ECS Bare Metal Instance family

Features

-   Provides flexible and powerful software-defined compute based on the SHENLONG architecture.
-   Uses NVIDIA T4 GPUs that have the following features:
    -   Innovative NVIDIA Turing architecture
    -   16 GB memory \(320 GB/s bandwidth\) per GPU
    -   2,560 CUDA cores per GPU
    -   Up to 320 Turing Tensor cores per GPU
    -   Mixed-precision Tensor cores that support 65 FP16 TFLOPS, 130 INT8 TOPS, and 260 INT4 TOPS
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs, ultra disks, and ESSDs that deliver millions of IOPS.
-   Supports IPv6.
-   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   AI \(deep learning and machine learning\) inference for computer vision, speech recognition, speech synthesis, natural language processing \(NLP\), machine translation, and recommendation systems
    -   Real-time rendering for cloud gaming
    -   Real-time rendering for AR and VR applications
    -   Graphics workstations or overloaded graphics computing
    -   GPU-accelerated databases
    -   High-performance computing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory \(GB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|----|-----------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.ebmgn6i.24xlarge|96|384.0|NVIDIA T4 × 4|16GB × 4|30.0|4,500,000|8|32|10|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmc6a, compute optimized ECS Bare Metal Instance family

The instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Uses the fast path acceleration feature of chips to provide predictable and consistent ultra-high computing, storage, and network performance based on the third-generation SHENLONG architecture.
-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:2.
-   Uses 2.6 GHz AMD EPYCTM ROME processors that deliver a turbo frequency of 3.3 GHz for consistent computing performance.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides ultra-high network performance with a packet forwarding rate of 24,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Video encoding, decoding, and rendering
    -   Data analysis and computing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|--------------------|:-----------------------------|----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmc6a.64xlarge|256|512.0|64.0|24,000,000|32|31|10|600,000|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmc6e, compute optimized ECS Bare Metal Instance family with enhanced performance

Features

-   Uses the fast path acceleration feature of chips to provide predictable and consistent ultra-high computing, storage, and network performance based on the third-generation SHENLONG architecture.
-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:2.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver an all-core turbo frequency of 3.2 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports only ESSDs and provides ultra-high I/O performance.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides ultra-high network performance with a packet forwarding rate of 24,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Web frontend servers
    -   Frontend servers of massively multiplayer online \(MMO\) games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|-----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmc6e.26xlarge|104|192.0|32.0|24,000,000|1,800,000|32|10|480,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmc6, compute optimized ECS Bare Metal Instance family

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:2.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver an all-core turbo frequency of 3.2 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 6,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Video encoding, decoding, and rendering
    -   Frontend servers of MMO games
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|-----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmc6.26xlarge|104|192.0|32.0|6,000,000|1,800,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmg6a, general purpose ECS Bare Metal Instance family

The instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Uses the fast path acceleration feature of chips to provide predictable and consistent ultra-high computing, storage, and network performance based on the third-generation SHENLONG architecture.
-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.6 GHz AMD EPYCTM ROME processors that deliver a turbo frequency of 3.3 GHz for consistent computing performance.
-   Is an instance family in which all instances are I/O optimized.
-   Supports enhanced SSDs \(ESSDs\), standard SSDs, and ultra disks.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides ultra-high network performance with a packet forwarding rate of 24,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Video encoding, decoding, and rendering
    -   Compute clusters and memory-intensive data processing
    -   Data analysis and computing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|--------------------|:-----------------------------|----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmg6a.64xlarge|256|1024.0|64.0|24,000,000|32|31|10|600,000|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmg6e, general purpose ECS Bare Metal Instance family with enhanced performance

Features

-   Uses the fast path acceleration feature of chips to provide predictable and consistent ultra-high computing, storage, and network performance based on the third-generation SHENLONG architecture.
-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver an all-core turbo frequency of 3.2 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports only ESSDs and provides ultra-high I/O performance.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides ultra-high network performance with a packet forwarding rate of 24,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-level applications of various types and sizes
    -   Websites and application servers
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|-----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmg6e.26xlarge|104|384.0|32.0|24,000,000|1,800,000|32|10|480,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmg6, general purpose ECS Bare Metal Instance family

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver an all-core turbo frequency of 3.2 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 6,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Video encoding, decoding, and rendering
    -   Enterprise-level applications such as large and medium-sized databases
    -   Compute clusters and memory-intensive data processing
    -   Data analysis and computing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|-----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmg6.26xlarge|104|384.0|32.0|6,000,000|1,800,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmr6a, memory optimized ECS Bare Metal Instance family

The instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Uses the fast path acceleration feature of chips to provide predictable and consistent ultra-high computing, storage, and network performance based on the third-generation SHENLONG architecture.
-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:8.
-   Uses 2.6 GHz AMD EPYCTM ROME processors that deliver a turbo frequency of 3.3 GHz for consistent computing performance.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides ultra-high network performance with a packet forwarding rate of 24,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   In-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|--------------------|:-----------------------------|----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmr6a.64xlarge|256|2048.0|64.0|24,000,000|32|31|10|600,000|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmr6e, memory optimized ECS Bare Metal Instance family with enhanced performance

Features

-   Uses the fast path acceleration feature of chips to provide predictable and consistent ultra-high computing, storage, and network performance based on the third-generation SHENLONG architecture.
-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:8.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver an all-core turbo frequency of 3.2 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports only ESSDs and provides ultra-high I/O performance.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides ultra-high network performance with a packet forwarding rate of 24,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   High-performance databases and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|-----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmr6e.26xlarge|104|768.0|32.0|24,000,000|1,800,000|32|10|480,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmr6, memory optimized ECS Bare Metal Instance family

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:8.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver an all-core turbo frequency of 3.2 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 6,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   High-performance databases and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|-----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmr6.26xlarge|104|768.0|32.0|6,000,000|1,800,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmre6p, persistent memory optimized ECS Bare Metal Instance family with enhanced performance

To use ebmre6p,[submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Provides dedicated hardware resources and physical isolation.
-   Uses the Intel ® OptaneTM persistent memory and is tuned for Redis applications in an end-to-end manner to provide cost-effectiveness.
-   Supports a maximum of 1,920 GiB memory \(384 GiB DRAM + 1,536 GiB Intel® OptaneTM persistent memory\), offers a CPU-to-memory ratio of 1:20, and can meet the needs of memory-intensive applications.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver an all-core turbo frequency of 3.2 GHz for consistent computing performance.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 6,000,000 pps.
-   Suits the following scenarios:
    -   In-memory databases such as Redis
    -   High-performance databases such as SAP HANA
    -   Other memory-intensive applications such as AI applications and smart search applications

Instance types

|Instance type|vCPUs|DRAM \(GiB\)|Persistent memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-----------|-------------------------|:-------------------|:-----------------------------|:---|----------------------------|---------|-------------------------|
|ecs.ebmre6p.26xlarge|104|384.0|1536.0|32.0|6,000,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmre6-6t, memory optimized ECS Bare Metal Instance family with enhanced performance

To use ebmre6-6t,[submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:30.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver an all-core turbo frequency of 3.2 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 6,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   High-performance and in-memory databases such as SAP HANA databases
    -   Memory-intensive applications
    -   Big data processing engines such as Apache Spark and Presto

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|-----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmre6-6t.52xlarge|208|6144.0|32.0|6,000,000|1,800,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmhfg7, general purpose ECS Bare Metal Instance family with high clock speeds

Features

-   Uses the fast path acceleration feature of chips to provide predictable and consistent ultra-high computing, storage, and network performance based on the third-generation SHENLONG architecture.
-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses the third-generation Intel® Xeon® Scalable processors \(Cooper Lake\) that deliver a base frequency of not lower than 3.3 GHz and an all-core turbo frequency of 3.8 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports only ESSDs and provides ultra-high I/O performance.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides ultra-high network performance with a packet forwarding rate of 24,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-level applications of various types and sizes
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   High-performance scientific computing
    -   Video encoding applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.ebmhfg7.48xlarge|192|768.0|64.0|24,000,000|32|31|10|600,000|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmhfc7, compute optimized ECS Bare Metal Instance family with high clock speeds

Features

-   Uses the fast path acceleration feature of chips to provide predictable and consistent ultra-high computing, storage, and network performance based on the third-generation SHENLONG architecture.
-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:2.
-   Uses the third-generation Intel® Xeon® Scalable processors \(Cooper Lake\) that deliver a base frequency of not lower than 3.3 GHz and an all-core turbo frequency of 3.8 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports only ESSDs and provides ultra-high I/O performance.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides ultra-high network performance with a packet forwarding rate of 24,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   High-performance frontend server clusters
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.ebmhfc7.48xlarge|192|384.0|64.0|24,000,000|32|31|10|600,000|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmhfr7, memory optimized ECS Bare Metal Instance family with high clock speeds

Features

-   Uses the fast path acceleration feature of chips to provide predictable and consistent ultra-high computing, storage, and network performance based on the third-generation SHENLONG architecture.
-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:8.
-   Uses the third-generation Intel® Xeon® Scalable processors \(Cooper Lake\) that deliver a base frequency of not lower than 3.3 GHz and an all-core turbo frequency of 3.8 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports only ESSDs and provides ultra-high I/O performance.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides ultra-high network performance with a packet forwarding rate of 24,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   High-performance databases and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.ebmhfr7.48xlarge|192|1536.0|64.0|24,000,000|32|31|10|600,000|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmhfg6, general purpose ECS Bare Metal Instance family with high clock speeds

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:4.8.
-   Uses 3.1 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver an all-core turbo frequency of 3.5 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 6,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Enterprise-level applications such as large and medium-sized databases
    -   Video encoding, decoding, and rendering

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|-----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmhfg6.20xlarge|80|384.0|32.0|6,000,000|1,800,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmhfc6, compute optimized ECS Bare Metal Instance family with high clock speeds

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:2.4.
-   Uses 3.1 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver an all-core turbo frequency of 3.5 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 6,000,000 pps.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Video encoding, decoding, and rendering

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmhfc6.20xlarge|80|192.0|32.0|6,000,000|1,800,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmhfr6, memory optimized ECS Bare Metal Instance family with high clock speeds

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:9.6.
-   Uses 3.1 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver an all-core turbo frequency of 3.5 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports IPv6.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 6,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   High-performance databases and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmhfr6.20xlarge|80|768.0|32.0|6,000,000|1,800,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## scchfc6, compute optimized SCC instance family with high clock speeds

To use scchfc6, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Provides all features of ECS Bare Metal Instance.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.4.
    -   Uses 3.1 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.5 GHz.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs \(ESSDs\), standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Supports both RoCE networks and VPCs. RoCE networks are dedicated to RDMA communication.
-   Suits the following scenarios:
    -   Large-scale machine learning training
    -   Large-scale high-performance scientific computing and simulations
    -   Large-scale data analysis, batch processing, and video encoding

Instance types

|Instance type|vCPUs|Physical cores|Memory \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|RoCE bandwidth \(bidirectional\), Gbit/s|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|--------------|:----------------------------------|:---------------------------------------------|:---------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.scchfc6.20xlarge|80|40|192.0|30.0|6,000|50|8|32|10|

**Note:**

-   ecs.scchfc6.20xlarge provides 80 logical processors on 40 physical cores.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## scchfg6, general purpose SCC instance family with high clock speeds

To use scchfg6, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Provides all features of ECS Bare Metal Instance.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.8.
    -   Uses 3.1 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.5 GHz.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Supports both RoCE networks and VPCs. RoCE networks are dedicated to RDMA communication.
-   Suits the following scenarios:
    -   Large-scale machine learning training
    -   Large-scale high-performance scientific computing and simulations
    -   Large-scale data analysis, batch processing, and video encoding

Instance types

|Instance type|vCPUs|Physical cores|Memory \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|RoCE bandwidth \(bidirectional\), Gbit/s|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|--------------|:----------------------------------|:---------------------------------------------|:---------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.scchfg6.20xlarge|80|40|384.0|30.0|6,000|50|8|32|10|

**Note:**

-   ecs.scchfg6.20xlarge provides 80 logical processors on 40 physical cores.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## scchfr6, memory optimized SCC instance family with high clock speeds

To use scchfr6, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Provides all features of ECS Bare Metal Instance.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:9.6.
    -   Uses 3.1 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.5 GHz.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6.
    -   Supports both RoCE networks and VPCs. RoCE networks are dedicated to RDMA communication.
-   Suits the following scenarios:
    -   Large-scale machine learning training
    -   Large-scale high-performance scientific computing and simulations
    -   Large-scale data analysis, batch processing, and video encoding

Instance types

|Instance type|vCPUs|Physical cores|Memory \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|RoCE bandwidth \(bidirectional\), Gbit/s|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|--------------|:----------------------------------|:---------------------------------------------|:---------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.scchfr6.20xlarge|80|40|768.0|30.0|6,000|50|8|32|10|

**Note:**

-   ecs.scchfr6.20xlarge provides 80 logical processors on 40 physical cores.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## scch5, SCC instance family with high clock speeds

Features

-   Provides all features of ECS Bare Metal Instance.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:3.
    -   Uses 3.1 GHz Intel® Xeon® Gold 6149 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports standard SSDs and ultra disks.
-   Network:
    -   Supports both RoCE networks and VPCs. RoCE networks are dedicated to RDMA communication.
-   Suits the following scenarios:
    -   Large-scale machine learning training
    -   Large-scale high-performance scientific computing and simulations
    -   Large-scale data analysis, batch processing, and video encoding

Instance types

|Instance type|vCPUs|Physical cores|Memory \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|RoCE bandwidth \(bidirectional\), Gbit/s|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|--------------|:----------------------------------|:---------------------------------------------|:---------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.scch5.16xlarge|64|32|192.0|10.0|4,500|25 × 2|8|32|10|

**Note:**

-   ecs.scch5.16xlarge provides 64 logical processors on 32 physical cores.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## sccg5, general purpose SCC instance family

Features

-   Provides all features of ECS Bare Metal Instance.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports standard SSDs and ultra disks.
-   Network:
    -   Supports both RoCE networks and VPCs. RoCE networks are dedicated to RDMA communication.
-   Suits the following scenarios:
    -   Large-scale machine learning training
    -   Large-scale high-performance scientific computing and simulations
    -   Large-scale data analysis, batch processing, and video encoding

Instance types

|Instance type|vCPUs|Physical cores|Memory \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|RoCE bandwidth \(bidirectional\), Gbit/s|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|--------------|:----------------------------------|:---------------------------------------------|:---------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.sccg5.24xlarge|96|48|384.0|10.0|4,500|25 × 2|8|32|10|

**Note:**

-   ecs.sccg5.24xlarge provides 96 logical processors on 48 physical cores.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## sccgn6, GPU-accelerated compute optimized SCC instance family

Features

-   Provides all features of ECS Bare Metal Instance.
-   Compute:
    -   Uses NVIDIA V100 GPUs \(SXM2-based\) that feature:
        -   Innovative Volta architecture
        -   Up to 16 GB HBM2 GPU memory
        -   5,120 CUDA Cores
        -   640 Tensor Cores
        -   GPU memory bandwidth of up to 900 Gbit/s
        -   Support for up to six NVLink connections and total bandwidth of 300 GB/s \(25 GB/s per connection\)
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
    -   Supports high-performance CPFS.
-   Network:
    -   Supports IPv6.
    -   Supports VPCs.
    -   Supports RoCE v2 networks, which are dedicated to low-latency RDMA communication.
-   Suits the following scenarios:
    -   Ultra-large-scale training for machine learning on a distributed GPU cluster
    -   Large-scale high-performance scientific computing and simulations
    -   Large-scale data analysis, batch processing, and video encoding

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|RoCE bandwidth \(bidirectional\), Gbit/s|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:---|:----------------------------------|:---------------------------------------------|----------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.sccgn6.24xlarge|96|384.0|NVIDIA V100 × 8|30.0|4,500|25 × 2|8|32|10|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## sccgn6e, GPU-accelerated compute optimized SCC instance family

To use sccgn6e, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Provides all features of ECS Bare Metal Instance.
-   Compute:
    -   Uses NVIDIA V100 GPUs \(SXM2-based\) that feature:
        -   Innovative Volta architecture
        -   32 GB HBM2 GPU memory
        -   5,120 CUDA Cores
        -   640 Tensor Cores
        -   GPU memory bandwidth of up to 900 Gbit/s
        -   Support for up to six NVLink connections and total bandwidth of 300 GB/s \(25 GB/s per connection\)
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
    -   Supports high-performance Cloud Paralleled File System \(CPFS\).
-   Network:
    -   Supports IPv6.
    -   Supports VPCs.
    -   Supports RoCE v2 networks, which are dedicated to low-latency RDMA communication.
-   Suits the following scenarios:
    -   Ultra-large-scale training for machine learning on a distributed GPU cluster
    -   Large-scale high-performance scientific computing and simulations
    -   Large-scale data analysis, batch processing, and video encoding

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory \(GB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|RoCE bandwidth \(bidirectional\), Gbit/s|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:---|-----------------|:----------------------------------|:---------------------------------------------|----------------------------------------|:---------|:---------------------------------|----------------------------|
|ecs.sccgn6e.24xlarge|96|768.0|NVIDIA V100 × 8|32 GB × 8|32.0|4,800|25 × 2|8|32|10|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmc5s, compute optimized ECS Bare Metal Instance family with enhanced network performance

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:2.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors that deliver an all-core turbo frequency of 2.7 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 4,500,000 pps.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Video encoding, decoding, and rendering

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmc5s.24xlarge|96|192.0|32.0|4,500,000|1,800,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmg5s, general purpose ECS Bare Metal Instance family with enhanced network performance

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors that deliver an all-core turbo frequency of 2.7 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 4,500,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Enterprise-level applications such as large and medium-sized databases
    -   Video encoding

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmg5s.24xlarge|96|384.0|32.0|4,500,000|1,800,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmr5s, memory optimized ECS Bare Metal Instance family with enhanced network performance

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:8.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors that deliver an all-core turbo frequency of 2.7 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 4,500,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   High-performance databases and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmr5s.24xlarge|96|768.0|32.0|4,500,000|1,800,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmg5, general purpose ECS Bare Metal Instance family

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors that deliver an all-core turbo frequency of 2.7 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports only standard SSDs and ultra disks.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 4,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Enterprise-level applications such as large and medium-sized databases
    -   Video encoding

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---|----------------------------|
|ecs.ebmg5.24xlarge|96|384.0|10.0|4,000,000|32|10|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmhfg5, ECS Bare Metal Instance family with high clock speeds

Features

-   Provides dedicated hardware resources and physical isolation.
-   Supports encrypted computing based on Intel® SGX.
-   Has failover disabled by default.

    You can call the [ModifyInstanceMaintenanceAttributes](/intl.en-US/API Reference/Operations and monitoring/ModifyInstanceMaintenanceAttributes.md) operation to modify the maintenance action. Set ActionOnMaintenance to AutoRedeploy to enable failover.

-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 3.7 GHz Intel® Xeon® E3-1240v6 \(Skylake\) processors that deliver a turbo frequency of 4.1 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports only standard SSDs and ultra disks.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 2,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Gaming and finance applications that require high performance
    -   High-performance web servers
    -   Enterprise-level applications such as high-performance databases

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---|----------------------------|
|ecs.ebmhfg5.2xlarge|8|32.0|6.0|2,000,000|6|8|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmc4, compute optimized ECS Bare Metal Instance family

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:2.
-   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors that deliver a turbo frequency of 3.0 GHz.
-   Is an instance family in which all instances are I/O optimized.
-   Supports only standard SSDs and ultra disks.
-   Supports only VPCs.
-   Provides high network performance with a packet forwarding rate of 4,000,000 pps.
-   Suits the following scenarios:
    -   Workloads that require direct access to physical resources or that require a license to be bound to the hardware
    -   Scenarios that require compatibility with third-party hypervisors to implement hybrid-cloud and multi-cloud deployments
    -   Containers including Docker, Clear Containers, and Pouch
    -   Enterprise-level applications such as large and medium-sized databases
    -   Video encoding

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---|----------------------------|
|ecs.ebmc4.8xlarge|32|64.0|10.0|4,000,000|12|10|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## t6, burstable instance family

Features

-   Provides baseline CPU performance and is burstable but limited by accrued CPU credits.
-   Is more cost-effective when compared with the t5 burstable instance family.
-   Compute:
    -   Uses 2.5 GHz Intel® Xeon® Cascade Lake processors that deliver a turbo frequency of 3.2 GHz.
    -   Uses the DDR4 memory.
-   Storage:
    -   Supports enhanced SSDs \(ESSD\), standard SSDs, and ultra disks.

        **Note:** PL2 and PL3 ESSDs cannot provide maximum performance due to the specification limits of burstable instances. We recommend that you use enterprise-level instances or ESSDs that are at lower performance levels.

-   Network:
    -   Supports IPv6.
    -   Supports only VPCs.
    -   Delivers a bandwidth of up to 4 Gbit/s.
-   Suits the following scenarios:
    -   Web application servers
    -   Lightweight applications and microservices
    -   Development and testing environments

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline CPU computing performance|CPU credits per hour|Max CPU credit balance|Base bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|--------------|:---------------------------------|:-------------------|:---------------------|-------------------------|-------------------------------|----------|:---|----------------------------|
|ecs.t6-c4m1.large|2|0.5|5%|6|144|0.08|40|1|2|2|
|ecs.t6-c2m1.large|2|1.0|10%|12|288|0.08|60|1|2|2|
|ecs.t6-c1m1.large|2|2.0|20%|24|576|0.08|100|1|2|2|
|ecs.t6-c1m2.large|2|4.0|20%|24|576|0.08|100|1|2|2|
|ecs.t6-c1m4.large|2|8.0|30%|36|864|0.08|100|1|2|2|
|ecs.t6-c1m4.xlarge|4|16.0|40%|96|2,304|0.16|200|1|2|6|
|ecs.t6-c1m4.2xlarge|8|32.0|40%|192|4,608|0.32|400|1|2|6|

**Note:**

-   When you bind elastic network interfaces \(ENIs\) to or unbind ENIs from instances of the following instance types, the instances must be in the Stopped state: ecs.t6-c1m1.large, ecs.t6-c1m2.large, ecs.t6-c1m4.large, ecs.t6-c2m1.large, and ecs.t6-c4m1.large.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## t5, burstable instance family

Features

-   Provides baseline CPU performance and is burstable but limited by accrued CPU credits.
-   Offers a balance between compute, memory, and network resources.
-   Compute:
    -   Offers multiple CPU-to-memory ratios.
    -   Uses 2.5 GHz Intel® Xeon® processors.
    -   Uses the DDR4 memory.
-   Network:
    -   Supports IPv6.
    -   Supports only VPCs.
-   Suits the following scenarios:
    -   Web application servers
    -   Lightweight applications and microservices
    -   Development and testing environments

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline CPU computing performance|CPU credits per hour|Max CPU credit balance|Disk bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|--------------|:---------------------------------|:-------------------|:---------------------|-------------------------|-------------------------------|----------|:---|----------------------------|
|ecs.t5-lc2m1.nano|1|0.5|20%|12|288|0.1|40|1|2|2|
|ecs.t5-lc1m1.small|1|1.0|20%|12|288|0.2|60|1|2|2|
|ecs.t5-lc1m2.small|1|2.0|20%|12|288|0.2|60|1|2|2|
|ecs.t5-lc1m2.large|2|4.0|20%|24|576|0.4|100|1|2|2|
|ecs.t5-lc1m4.large|2|8.0|20%|24|576|0.4|100|1|2|2|
|ecs.t5-c1m1.large|2|2.0|25%|30|720|0.5|100|1|2|2|
|ecs.t5-c1m2.large|2|4.0|25%|30|720|0.5|100|1|2|2|
|ecs.t5-c1m4.large|2|8.0|25%|30|720|0.5|100|1|2|2|
|ecs.t5-c1m1.xlarge|4|4.0|25%|60|1440|0.8|200|1|2|6|
|ecs.t5-c1m2.xlarge|4|8.0|25%|60|1440|0.8|200|1|2|6|
|ecs.t5-c1m4.xlarge|4|16.0|25%|60|1440|0.8|200|1|2|6|
|ecs.t5-c1m1.2xlarge|8|8.0|25%|120|2,880|1.2|400|1|2|6|
|ecs.t5-c1m2.2xlarge|8|16.0|25%|120|2,880|1.2|400|1|2|6|
|ecs.t5-c1m4.2xlarge|8|32.0|25%|120|2,880|1.2|400|1|2|6|
|ecs.t5-c1m1.4xlarge|16|16.0|25%|240|5,760|1.2|600|1|2|6|
|ecs.t5-c1m2.4xlarge|16|32.0|25%|240|5,760|1.2|600|1|2|6|

**Note:**

-   When you bind ENIs to or unbind ENIs from instances of the following instance types, the instances must be in the Stopped state: ecs.t5-lc2m1.nano, ecs.t5-c1m1.large, ecs.t5-c1m2.large, ecs.t5-c1m4.large, ecs.t5-lc1m1.small, ecs.t5-lc1m2.large, ecs.t5-lc1m2.small, and ecs.t5-lc1m4.large.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## v5, CPU overprovisioned instance family

Features

-   You can create v5 instances only on dedicated hosts.

    **Note:** For more information about other types of instances that can be created on dedicated hosts, see [Dedicated host types](/intl.en-US/Product Introduction/Dedicated host types.md).

-   Compute:
    -   Supports multiple CPU-to-memory ratios such as 1:1, 1:2, 1:4, and 1:8.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
-   Network:
    -   Supports IPv6.
-   Suits the following scenarios:
    -   Migration from offline virtualization environments to Alibaba Cloud
    -   Services that generate low, medium, or burstable CPU loads

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|-------------|-----|--------------|--------------------|-------------------------------|----------|----|----------------------------|
|ecs.v5-c1m1.large|2|2.0|2.0|300|2|2|2|
|ecs.v5-c1m1.xlarge|4|4.0|2.0|300|2|2|6|
|ecs.v5-c1m1.2xlarge|8|8.0|3.0|400|2|3|6|
|ecs.v5-c1m1.3xlarge|12|12.0|3.0|400|4|3|6|
|ecs.v5-c1m1.4xlarge|16|16.0|4.0|500|4|4|6|
|ecs.v5-c1m1.8xlarge|32|32.0|4.0|500|8|4|6|
|ecs.v5-c1m2.large|2|4.0|2.0|300|2|2|2|
|ecs.v5-c1m2.xlarge|4|8.0|2.0|300|2|2|6|
|ecs.v5-c1m2.2xlarge|8|16.0|3.0|400|2|3|6|
|ecs.v5-c1m2.3xlarge|12|24.0|3.0|400|4|3|6|
|ecs.v5-c1m2.4xlarge|16|32.0|4.0|500|4|4|6|
|ecs.v5-c1m2.8xlarge|32|64.0|4.0|500|8|4|6|
|ecs.v5-c1m4.large|2|8.0|2.0|300|2|2|2|
|ecs.v5-c1m4.xlarge|4|16.0|2.0|300|2|2|6|
|ecs.v5-c1m4.2xlarge|8|32.0|3.0|400|2|3|6|
|ecs.v5-c1m4.3xlarge|12|48.0|3.0|400|4|3|6|
|ecs.v5-c1m4.4xlarge|16|64.0|4.0|500|4|4|6|
|ecs.v5-c1m4.8xlarge|32|128.0|4.0|500|8|4|6|
|ecs.v5-c1m8.large|2|16.0|2.0|300|2|2|2|
|ecs.v5-c1m8.xlarge|4|32.0|2.0|300|2|2|6|
|ecs.v5-c1m8.2xlarge|8|64.0|3.0|400|2|3|6|
|ecs.v5-c1m8.3xlarge|12|96.0|3.0|400|4|3|6|
|ecs.v5-c1m8.4xlarge|16|128.0|4.0|500|4|4|6|
|ecs.v5-c1m8.8xlarge|32|256.0|4.0|500|8|4|6|

**Note:** For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## Previous-generation shared instance families xn4, n4, mn4, and e4

Features

-   Offers multiple CPU-to-memory ratios.
-   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
-   Uses the DDR4 memory.

|Instance family|Description|vCPU-to-memory ratio|Scenario|
|:--------------|:----------|:-------------------|:-------|
|xn4|Compact type|1:1|-   Frontend web applications
-   Lightweight applications and microservices
-   Development and testing environments |
|n4|Shared compute type|1:2|-   Websites and web applications
-   Development environments, servers, code repositories, microservices, and testing and staging environments
-   Lightweight enterprise applications |
|mn4|Shared balanced type|1:4|-   Websites and web applications
-   Lightweight databases and caches
-   Integrated applications and lightweight enterprise services |
|e4|Shared memory type|1:8|-   Applications that require a large memory
-   Lightweight databases and caches |

xn4

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.xn4.small|1|1.0|0.5|50|1|2|2|

**Note:**

-   When you bind an elastic network interface \(ENI\) to or unbind an ENI from an instance of the ecs.xn4.small instance type, the instance must be in the Stopped state.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

n4

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.n4.small|1|2.0|0.5|50|1|2|2|
|ecs.n4.large|2|4.0|0.5|100|1|2|2|
|ecs.n4.xlarge|4|8.0|0.8|150|1|2|6|
|ecs.n4.2xlarge|8|16.0|1.2|300|1|2|6|
|ecs.n4.4xlarge|16|32.0|2.5|400|1|2|6|
|ecs.n4.8xlarge|32|64.0|5.0|500|1|2|6|

**Note:**

-   When you bind an ENI to or unbind an ENI from an instance of the ecs.n4.small or ecs.n4.large instance type, the instance must be in the Stopped state.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

mn4

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.mn4.small|1|4.0|0.5|50|1|2|2|
|ecs.mn4.large|2|8.0|0.5|100|1|2|2|
|ecs.mn4.xlarge|4|16.0|0.8|150|1|2|6|
|ecs.mn4.2xlarge|8|32.0|1.2|300|1|2|6|
|ecs.mn4.4xlarge|16|64.0|2.5|400|1|2|6|
|ecs.mn4.8xlarge|32|128.0|5|500|2|8|6|

**Note:**

-   When you bind an ENI to or unbind an ENI from an instance of the ecs.mn4.small or ecs.mn4.large instance type, the instance must be in the Stopped state.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

e4

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.e4.small|1|8.0|0.5|50|1|2|2|
|ecs.e4.large|2|16.0|0.5|100|1|2|2|
|ecs.e4.xlarge|4|32.0|0.8|150|1|2|6|
|ecs.e4.2xlarge|8|64.0|1.2|300|1|3|6|
|ecs.e4.4xlarge|16|128.0|2.5|400|1|8|6|

**Note:**

-   When you bind an ENI to or unbind an ENI from an instance of the ecs.e4.small or ecs.e4.large instance type, the instance must be in the Stopped state.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## Description of instance specifications

|Specification|Description|
|-------------|-----------|
|local storage|Local storage \(also called cache disks or local disks\) refers to the disks attached to the physical servers where ECS instances are hosted. Local storage provides temporary block storage for instances. Local storage capacity is measured in GiB. Data stored on local disks may be lost when the computing resources of an instance are released or when an instance is failed over to a normal physical server. Computing resources include vCPUs and memory. For more information, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).|
|bandwidth|The maximum sum of inbound and outbound bandwidth values. **Note:** Each instance specification is verified and obtained in a test environment. In actual scenarios, the performance of an instance may vary based on other factors, such as instance load and networking model. We recommend that you perform business stress tests on instances to select appropriate instance types. |
|packet forwarding rate|The maximum sum of inbound and outbound packet forwarding rates. For information about how to test the packet forwarding rate, see [Test network performance](https://www.alibabacloud.com/help/faq-detail/55757.htm). **Note:** Each instance specification is verified and obtained in a test environment. In actual scenarios, the performance of an instance may vary based on other factors, such as instance load, image version, and networking model. We recommend that you perform business stress tests on instances to select appropriate instance types. |
|connections|Connections, also called sessions, are the process of establishing connections and transferring data between a client and a server. A connection is uniquely defined by the network communication quintuple that consists of a source IP address, a destination IP address, a source port, a destination port, and a protocol. Connections of an ECS instance include TCP, UDP, and Internet Control Message Protocol \(ICMP\) connections.|
|NIC queues|The maximum number of network interface controller \(NIC\) queues supported by the primary NIC of an instance. If your instance type is not a member of an ECS Bare Metal Instance family, the maximum number of NIC queues supported by a secondary NIC is the same as that supported by the primary NIC.|
|ENIs|The total number of elastic network interfaces \(ENIs\) that include one primary ENI.|

