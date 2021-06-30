---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Memory optimized instance families

This topic describes the features of memory optimized instance families and lists the instance types of each family.

-   Recommended instance families
    -   [r7a, memory optimized instance family](#r7a)
    -   [r7, memory optimized instance family](#r7)
    -   [r7t, security-enhanced memory optimized instance family](#section_kni_2nn_01u)
    -   [re6p, persistent memory optimized instance family](#section_k8y_u9u_vax)
    -   [r6a, memory optimized instance family](#section_zx4_s2u_rlk)
    -   [r6e, memory optimized instance family with enhanced performance](#section_6x3_goi_4ou)
    -   [r6, memory optimized instance family](#section_qcw_6gn_p4u)
    -   [re6, high memory instance family](#section_c9u_7hq_srd)
    -   [r5, memory optimized instance family](#section_5vq_ldx_j20)
-   Other available instance families
    -   [re4, high memory instance family](#section_i3s_oh8_6q4)
    -   [re4e, high memory instance family](#section_6zy_cbu_zum)
    -   [se1ne, memory optimized instance family with enhanced network performance](#section_k1p_8hm_72f)
    -   [se1, memory optimized instance family](#section_s5w_lh9_07j)

## r7a, memory optimized instance family

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Uses the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8.
    -   Uses 2.55 GHz AMD EPYCTM MILAN processors that deliver a maximum single-core turbo frequency of 3.5 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs \(ESSDs\), standard SSDs, and ultra disks.
    -   Provides disk burstable IOPS and bandwidth capabilities for low-specification instances.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides burstable bandwidth capabilities for low-specification instances.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   High-performance and in-memory databases
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise applications
    -   Blockchain applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Disk baseline/burst IOPS|Disk baseline/burst bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|-----------------------------------|:-----------------------------|-----------|----------|:---|------------------------|----------------------------------------|
|ecs.r7a.large|2|16|1/burstable up to 10|900,000|Up to 250,000|2|3|12,500/burstable up to 110,000|1/burstable up to 6|
|ecs.r7a.xlarge|4|32|1.5/burstable up to 10|1,000,000|Up to 250,000|4|4|20,000/burstable up to 110,000|1.5/burstable up to 6|
|ecs.r7a.2xlarge|8|64|2.5/burstable up to 10|1,600,000|Up to 250,000|8|4|30,000/burstable up to 110,000|2/burstable up to 6|
|ecs.r7a.4xlarge|16|128|5/burstable up to 10|2,000,000|300,000|8|8|60,000/burstable up to 110,000|3/burstable up to 6|
|ecs.r7a.8xlarge|32|256|8/burstable up to 10|3,000,000|600,000|16|7|75,000/burstable up to 110,000|4/burstable up to 6|
|ecs.r7a.16xlarge|64|512|16/none|6,000,000|1,000,000|32|7|150,000/none|8/none|
|ecs.r7a.32xlarge|128|1024|32/none|12,000,000|2,000,000|32|15|300,000/none|16/none|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

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
    -   Supports only ESSDs.
    -   Provides burstable storage I/O capabilities for low-specification instances.
    -   Provides high storage I/O performance based on large computing capacity.
-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides burstable bandwidth capabilities for low-specification instances.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   High-performance and in-memory databases
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise-level applications
    -   Scenarios that require secure and trusted computing

Instance types

|Instance type|vCPU|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk baseline/burst IOPS|Disk baseline/burst bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|-----------------------------------|:-----------------------------|------------|-----------|----------|:---|----------------------------|------------------------|----------------------------------------|
|ecs.r7.large|2|16|2/burstable up to 10|900,000|Yes|Up to 250,000|2|3|6|20,000/burstable up to 110,000|1.5/burstable up to 6|
|ecs.r7.xlarge|4|32|3/burstable up to 10|1,000,000|Yes|Up to 250,000|4|4|15|40,000/burstable up to 110,000|2/burstable up to 6|
|ecs.r7.2xlarge|8|64|5/burstable up to 10|1,600,000|Yes|Up to 250,000|8|4|15|50,000/burstable up to 110,000|3/burstable up to 6|
|ecs.r7.3xlarge|12|96|8/burstable up to 10|2,400,000|Yes|Up to 250,000|8|8|15|70,000/burstable up to 110,000|4/burstable up to 6|
|ecs.r7.4xlarge|16|128|10/burstable up to 25|3,000,000|Yes|300,000|8|8|30|80,000/burstable up to 110,000|5/burstable up to 6|
|ecs.r7.6xlarge|24|192|12/burstable up to 25|4,500,000|Yes|450,000|12|8|30|110,000/none|6/none|
|ecs.r7.8xlarge|32|256|16/burstable up to 25|6,000,000|Yes|600,000|16|8|30|150,000/none|8/none|
|ecs.r7.16xlarge|64|512|32/none|12,000,000|Yes|1,200,000|32|8|30|300,000/none|16/none|
|ecs.r7.32xlarge|128|1024|64/none|24,000,000|Yes|2,400,000|32|15|30|600,000/none|32/none|

**Note:**

-   If you use Virtual Network Computing \(VNC\) to log on to a Windows instance, two cursors may appear. For information about how to fix this issue, see the “Why do two cursors appear after I use VNC to log on to a Windows instance?” section in [Instance FAQ](/intl.en-US/Instance/Instance FAQ.mdsection_jma_ml8_us3).
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

## r7t, security-enhanced memory optimized instance family

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Supports up to 512 GiB encrypted memory and encrypted computing based on Intel® Software Guard Extensions \(SGX\) to protect the confidentiality and integrity of essential code and data from malware attacks.
-   Supports SGX technology applicable to virtual machines and allows you to select instance types that suit your needs.
-   Implements trusted boots based on TCM or TPM chips. During a trusted boot, all modules in the boot chain from the underlying server hardware to the guest OS are measured and verified.
-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:8. About 50% of memory is encrypted.
    -   Uses the third-generation Intel® Xeon® Scalable processors \(Ice Lake\) that deliver a base frequency of 2.7 GHz and an all-core turbo frequency of 3.5 GHz for consistent computing performance.
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

|Instance type|vCPU|Memory \(GiB\)|Encrypted portion of memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk baseline/burst IOPS|Disk baseline/burst bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|-----------------------------------|-----------------------------------|:-----------------------------|------------|-----------|----------|:---|----------------------------|------------------------|----------------------------------------|
|ecs.r7t.large|2|16|8|2/burstable up to 10|900,000|Yes|Up to 250,000|2|3|6|20,000/burstable up to 110,000|1.5/burstable up to 6|
|ecs.r7t.xlarge|4|32|16|3/burstable up to 10|1,000,000|Yes|Up to 250,000|4|4|15|40,000/burstable up to 110,000|2/burstable up to 6|
|ecs.r7t.2xlarge|8|64|32|5/burstable up to 10|1,600,000|Yes|Up to 250,000|8|4|15|50,000/burstable up to 110,000|3/burstable up to 6|
|ecs.r7t.3xlarge|12|96|48|8/burstable up to 10|2,400,000|Yes|Up to 250,000|8|8|15|70,000/burstable up to 110,000|4/burstable up to 6|
|ecs.r7t.4xlarge|16|128|64|10/burstable up to 25|3,000,000|Yes|300,000|8|8|30|80,000/burstable up to 110,000|5/burstable up to 6|
|ecs.r7t.6xlarge|24|192|96|12/burstable up to 25|4,500,000|Yes|450,000|12|8|30|110,000/none|6/none|
|ecs.r7t.8xlarge|32|256|128|16/burstable up to 25|6,000,000|Yes|600,000|16|8|30|150,000/none|8/none|
|ecs.r7t.16xlarge|64|512|256|32/none|12,000,000|Yes|1,200,000|32|8|30|300,000/none|16/none|
|ecs.r7t.32xlarge|128|1024|512|64/none|24,000,000|Yes|2,400,000|32|15|30|600,000/none|32/none|

**Note:**

-   The instance family is in invitational preview. Resources are limited. No service level agreement \(SLA\) compliance is ensured. To use this instance family, submit an application based on your minimum business requirements.
-   Intel Ice Lake supports only remote attestation based on Intel SGX DCAP, and does not support remote attestation based on Intel EPID. You must adapt applications before you can use the remote attestation feature. For more information about remote attestation, see [attestation-service](https://software.intel.com/content/www/us/en/develop/topics/software-guard-extensions/attestation-services.html).
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

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

|Instance type|vCPU|Memory \(GiB\)|Persistent memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|-------------------------|-----------------------------------|:-----------------------------|-----------|----------|:---|---------|-------------------------|
|ecs.re6p.large|2|8|31.5|1/3|300,000|Up to 250,000|2|2|10,000|1|
|ecs.re6p.xlarge|4|16|63|1.5/5|500,000|Up to 250,000|4|3|20,000|1.5|
|ecs.re6p.2xlarge|8|32|126|2.5/10|800,000|Up to 250,000|8|4|25,000|2|
|ecs.re6p.13xlarge|52|192|756|12.5/none|3,000,000|900,000|32|7|100,000|8|
|ecs.re6p.26xlarge|104|384|1512|25/none|6,000,000|1,800,000|32|15|200,000|16,0|
|ecs.re6p-redis.large|2|8|31.5|1/3|300,000|Up to 250,000|2|2|10,000|1|
|ecs.re6p-redis.xlarge|4|16|63|1.5/5|500,000|Up to 250,000|4|3|20,000|1.5|
|ecs.re6p-redis.2xlarge|8|32|126|2.5/10|800,000|Up to 250,000|8|4|25,000|2|
|ecs.re6p-redis.13xlarge|52|192|756|12.5/none|3,000,000|900,000|32|7|100,000|8|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

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

|Instance type|vCPU|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|ENIs|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|-----------------------------------|:-----------------------------|:---|---------|-------------------------|
|ecs.r6a.large|2|16|1/10|900,000|2|12,500|1|
|ecs.r6a.xlarge|4|32|1.5/10|1,000,000|3|20,000|1.5|
|ecs.r6a.2xlarge|8|64|2.5/10|1,600,000|4|30,000|2|
|ecs.r6a.4xlarge|16|128|5/10|2,000,000|8|60,000|3|
|ecs.r6a.8xlarge|32|256|8/10|3,000,000|7|75,000|4,0|
|ecs.r6a.16xlarge|64|512|16/none|6,000,000|8|150,000|8|
|ecs.r6a.32xlarge|128|1024|32/none|12,000,000|15|300,000|16|
|ecs.r6a.64xlarge|256|2048|64/none|24,000,000|15|600,000|32|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

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
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise-level applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|-----------------------------------|:-----------------------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.r6e.large|2|16|1.2/burstable up to 10|900,000|Up to 250,000|2|3|6|20,000|1|
|ecs.r6e.xlarge|4|32|2/burstable up to 10|1,000,000|Up to 250,000|4|4|15|40,000|1.5|
|ecs.r6e.2xlarge|8|64|3/burstable up to 10|1,600,000|Up to 250,000|8|4|15|50,000|2|
|ecs.r6e.4xlarge|16|128|3/burstable up to 10|3,000,000|300,000|8|8|30|80,000|3|
|ecs.r6e.8xlarge|32|256|10/none|6,000,000|600,000|16|8|30|150,000|5|
|ecs.r6e.13xlarge|52|384|16/none|9,000,000|900,000|32|7|30|240,000|8|
|ecs.r6e.26xlarge|104|768|32/none|24,000,000|1,800,000|32|15|30|480,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other network metrics.

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
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise-level applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:----------------------------------|:-----------------------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.r6.large|2|16|1/3|300,000|Up to 250,000|2|2|6|10,000|1|
|ecs.r6.xlarge|4|32|1.5/5|500,000|Up to 250,000|4|3|10|20,000|1.5|
|ecs.r6.2xlarge|8|64|2.5/8|800,000|Up to 250,000|8|4|10|25,000|2|
|ecs.r6.3xlarge|12|96|4/10|900,000|Up to 250,000|8|6|10|30,000|2.5|
|ecs.r6.4xlarge|16|128|5/10|1,000,000|300,000|8|8|20|40,000|3|
|ecs.r6.6xlarge|24|192|7.5/10|1,500,000|450,000|12|8|20|50,000|4|
|ecs.r6.8xlarge|32|256|10/none|2,000,000|600,000|16|8|20|60,000|5|
|ecs.r6.13xlarge|52|384|12.5/none|3,000,000|900,000|32|7|20|100,000|8|
|ecs.r6.26xlarge|104|768|25/none|6,000,000|1,800,000|32|15|20|200,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

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
    -   Memory intensive applications
    -   Big data processing engines such as Apache Spark and Presto

Instance types

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.re6.13xlarge|52|768|10|1,800,000|16|7|20|50,000|4|
|ecs.re6.26xlarge|104|1536|16|3,000,000|32|7|20|100,000|8|
|ecs.re6.52xlarge|208|3072|32|6,000,000|32|15|20|200,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

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
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise-level applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.r5.large|2|16|1|300,000|2|2|6|
|ecs.r5.xlarge|4|32|1.5|500,000|2|3|10|
|ecs.r5.2xlarge|8|64|2.5|800,000|2|4|10|
|ecs.r5.3xlarge|12|96|4|900,000|4|6|10|
|ecs.r5.4xlarge|16|128|5|1,000,000|4|8|20|
|ecs.r5.6xlarge|24|192|7.5|1,500,000|6|8|20|
|ecs.r5.8xlarge|32|256|10|2,000,000|8|8|20|
|ecs.r5.16xlarge|64|512|20|4,000,000|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

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
    -   Memory intensive applications
    -   Big data processing engines such as Apache Spark and Presto

Instance types

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.re4.10xlarge|40|480|8|1,000,000|8|4|10|
|ecs.re4.20xlarge|80|960|15|2,000,000|16|8|20|
|ecs.re4.40xlarge|160|1920|30|4,500,000|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

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
    -   Memory intensive applications
    -   Big data processing engines such as Apache Spark and Presto

Instance types

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.re4e.40xlarge|160|3840|30|4,500,000|16|15|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

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
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise-level applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.se1ne.large|2|16|1|300,000|2|2|6|
|ecs.se1ne.xlarge|4|32|1.5|500,000|2|3|10|
|ecs.se1ne.2xlarge|8|64|2|1,000,000|4|4|10|
|ecs.se1ne.3xlarge|12|96|2.5|1,300,000|4|6|10|
|ecs.se1ne.4xlarge|16|128|3|1,600,000|4|8|20|
|ecs.se1ne.6xlarge|24|192|4.5|2,000,000|6|8|20|
|ecs.se1ne.8xlarge|32|256|6|2,500,000|8|8|20|
|ecs.se1ne.14xlarge|56|480|10|4,500,000|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

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
    -   High-performance and in-memory databases
    -   Data analysis, data mining, and distributed memory caching
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise-level applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.se1.large|2|16|0.5|100,000|1|2|6|
|ecs.se1.xlarge|4|32|0.8|200,000|1|3|10|
|ecs.se1.2xlarge|8|64|1.5|400,000|1|4|10|
|ecs.se1.4xlarge|16|128|3|500,000|2|8|20|
|ecs.se1.8xlarge|32|256|6|800,000|3|8|20|
|ecs.se1.14xlarge|56|480|10|1,200,000|4|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance family.md).

## References

-   [Instance family](/intl.en-US/Instance/Instance family.md)
-   [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md)

