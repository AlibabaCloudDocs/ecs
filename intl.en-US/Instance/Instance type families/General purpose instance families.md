---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# General purpose instance families

This topic describes the features of general purpose instance families of Elastic Compute Service \(ECS\) and lists the instance types of each family.

-   Recommended instance families
    -   [g7a, general purpose instance family](#g7a)
    -   [g7, general purpose instance family](#g7)
    -   [g7t, security-enhanced general purpose instance family](#section_bew_6jv_c0k)
    -   [g7ne, general purpose instance family with enhanced network performance](#section_srt_k9b_at3)
    -   [g6se, storage enhanced instance family](#section_aky_rag_mve)
    -   [g6a, general purpose instance family](#section_jtr_8p8_3y8)
    -   [g6t, security-enhanced general purpose instance family](#section_2dm_67f_8cm)
    -   [g6e, general purpose instance family with enhanced performance](#section_8u6_czr_21b)
    -   [g6, general purpose instance family](#section_gck_bi6_q6l)
    -   [g5, general purpose instance family](#section_kwi_d9k_sbx)
    -   [g5ne, general purpose instance family with enhanced network performance](#section_ijd_dkf_hht)
-   Other available instance families

    [sn2ne, general purpose instance family with enhanced network performance](#section_1ki_kxs_w47)


## g7a, general purpose instance family

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Uses the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.55 GHz AMD EPYCTM MILAN processors that deliver a maximum single-core turbo frequency of 3.5 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs \(ESSDs\), standard SSDs, and ultra disks.
    -   Provides disk burstable IOPS and bandwidth performance for low-specification instances.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the next-generation enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides burstable network bandwidth performance for low-specification instances.
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

|Instance type|vCPUs|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Disk baseline/burst IOPS|Disk baseline/burst bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------------|:-----------------------------|-----------|----------|:---|------------------------|----------------------------------------|
|ecs.g7a.large|2|8|1/burstable up to 10|900,000|Up to 250,000|2|3|12,500/burstable up to 110,000|1/burstable up to 6|
|ecs.g7a.xlarge|4|16|1.5/burstable up to 10|1,000,000|Up to 250,000|4|4|20,000/burstable up to 110,000|1.5/burstable up to 6|
|ecs.g7a.2xlarge|8|32|2.5/burstable up to 10|1,600,000|Up to 250,000|8|4|30,000/burstable up to 110,000|2/burstable up to 6|
|ecs.g7a.4xlarge|16|64|5/burstable up to 10|2,000,000|300,000|8|8|60,000/burstable up to 110,000|3/burstable up to 6|
|ecs.g7a.8xlarge|32|128|8/burstable up to 10|3,000,000|600,000|16|7|75,000/burstable up to 110,000|4/burstable up to 6|
|ecs.g7a.16xlarge|64|256|16/none|6,000,000|1,000,000|32|7|150,000/none|8/none|
|ecs.g7a.32xlarge|128|512|32/none|12,000,000|2,000,000|32|15|300,000/none|16/none|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## g7, general purpose instance family

Features

-   Uses the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Supports the virtual Trusted Platform Module \(vTPM\) feature and implements trusted boots based on Trusted Cryptography Module \(TCM\) or Trusted Platform Module \(TPM\) chips. During a trusted boot, all modules in the boot chain from the underlying hardware to the guest OS are measured and verified.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses the third-generation Intel® Xeon® scalable processors \(Ice Lake\) that deliver a base frequency of 2.7 GHz and an all-core turbo frequency of 3.5 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only ESSDs.
    -   Provides burstable storage I/O performance for low-specification instances.
    -   Provides high storage I/O performance based on large computing capacity.
-   Network:
    -   Supports IPv6.
    -   Provides ultra-high packet forwarding rates.
    -   Provides burstable network performance for low-specification instances.
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

|Instance type|vCPUs|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk baseline/burst IOPS|Disk baseline/burst bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------------|:-----------------------------|------------|-----------|----------|:---|----------------------------|------------------------|----------------------------------------|
|ecs.g7.large|2|8|2/burstable up to 10|900,000|Yes|Up to 250,000|2|3|6|20,000/burstable up to 110,000|1.5/burstable up to 6|
|ecs.g7.xlarge|4|16|3/burstable up to 10|1,000,000|Yes|Up to 250,000|4|4|15|40,000/burstable up to 110,000|2/burstable up to 6|
|ecs.g7.2xlarge|8|32|5/burstable up to 10|1,600,000|Yes|Up to 250,000|8|4|15|50,000/burstable up to 110,000|3/burstable up to 6|
|ecs.g7.3xlarge|12|48|8/burstable up to 10|2,400,000|Yes|Up to 250,000|8|8|15|70,000/burstable up to 110,000|4/burstable up to 6|
|ecs.g7.4xlarge|16|64|10/burstable up to 25|3,000,000|Yes|300,000|8|8|30|80,000/burstable up to 110,000|5/burstable up to 6|
|ecs.g7.6xlarge|24|96|12/burstable up to 25|4,500,000|Yes|450,000|12|8|30|110,000/none|6/none|
|ecs.g7.8xlarge|32|128|16/burstable up to 25|6,000,000|Yes|600,000|16|8|30|150,000/none|8/none|
|ecs.g7.16xlarge|64|256|32/none|12,000,000|Yes|1,200,000|32|8|30|300,000/none|16/none|
|ecs.g7.32xlarge|128|512|64/none|24,000,000|Yes|2,400,000|32|15|30|600,000/none|32/none|

**Note:**

-   If you use Virtual Network Computing \(VNC\) to log on to a Windows instance, two cursors may appear. For information about how to fix this issue, see the “Why do two cursors appear after I use VNC to log on to a Windows instance?” section in [Instance FAQ](/intl.en-US/Instance/Instance FAQ.md).
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## g7t, security-enhanced general purpose instance family

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Supports encrypted computing based on Intel® Software Guard Extensions \(SGX\) and up to 256 GiB encrypted memory to protect the confidentiality and integrity of essential code and data from malware attacks.
-   Supports SGX technology applicable to virtual machines and allows you to select instance types that suit your needs.
-   Implements trusted boot based on TCM or TPM chips. During a trusted boot, all modules in the boot chain from the underlying hardware to the guest OS are measured and verified.
-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1: 4. About 50% of memory is encrypted.
    -   Uses the third-generation Intel® Xeon® scalable processors \(Ice Lake\) that deliver a base frequency of 2.7 GHz and an all-core turbo frequency of 3.5 GHz for consistent computing performance.
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
    -   Scenarios that require high security and enhanced trust, such as services for financial organizations, public service sectors, and enterprises
    -   Enterprise-level applications of various types and sizes

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Encrypted portion of memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk baseline/burst IOPS|Disk baseline/burst bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------------|-----------------------------------|:-----------------------------|------------|-----------|----------|:---|----------------------------|------------------------|----------------------------------------|
|ecs.g7t.large|2|8|4|2/burstable up to 10|900,000|Yes|Up to 250,000|2|3|6|20,000/burstable up to 110,000|1.5/burstable up to 6|
|ecs.g7t.xlarge|4|16|8|3/burstable up to 10|1,000,000|Yes|Up to 250,000|4|4|15|40,000/burstable up to 110,000|2/burstable up to 6|
|ecs.g7t.2xlarge|8|32|16|5/burstable up to 10|1,600,000|Yes|Up to 250,000|8|4|15|50,000/burstable up to 110,000|3/burstable up to 6|
|ecs.g7t.3xlarge|12|48|24|8/burstable up to 10|2,400,000|Yes|Up to 250,000|8|8|15|70,000/burstable up to 110,000|4/burstable up to 6|
|ecs.g7t.4xlarge|16|64|32|10/burstable up to 25|3,000,000|Yes|300,000|8|8|30|80,000/burstable up to 110,000|5/burstable up to 6|
|ecs.g7t.6xlarge|24|96|48|12/burstable up to 25|4,500,000|Yes|450,000|12|8|30|110,000/none|6/none|
|ecs.g7t.8xlarge|32|128|64|16/burstable up to 25|6,000,000|Yes|600,000|16|8|30|150,000/none|8/none|
|ecs.g7t.16xlarge|64|256|128|32/none|12,000,000|Yes|1,200,000|32|8|30|300,000/none|16/none|
|ecs.g7t.32xlarge|128|512|256|64/none|24,000,000|Yes|2,400,000|32|15|30|600,000/none|32/none|

**Note:**

-   The instance family is in invitational preview. Resources are limited. No service level agreement \(SLA\) compliance is ensured. To use this instance family, submit an application based on your minimum business requirements.
-   Intel Ice Lake supports only remote attestation based on Intel SGX DCAP, and does not support remote attestation based on Intel EPID. You must adapt applications before you can use the remote attestation feature. For more information about remote attestation, see [attestation-service](https://software.intel.com/content/www/us/en/develop/topics/software-guard-extensions/attestation-services.html).
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

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

|Instance type|vCPUs|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------------|:-----------------------------|-----------|----------|:---|----------------------------|---------|-------------------------|
|ecs.g7ne.large|2|8|1.5/10|900,000|450,000|2|3|10|10,000|0.75|
|ecs.g7ne.xlarge|4|16|3/10|1,000,000|900,000|4|4|15|20,000|1|
|ecs.g7ne.2xlarge|8|32|6/15|1,500,000|1,750,000|8|6|15|25,000|1.2|
|ecs.g7ne.4xlarge|16|64|12/25|3,000,000|3,500,000|16|8|30|40,000|2|
|ecs.g7ne.8xlarge|32|128|25/none|6,000,000|6,000,000|16|8|30|75,000|5|
|ecs.g7ne.12xlarge|48|192|40/none|12,000,000|8,000,000|32|8|30|100,000|8|
|ecs.g7ne.16xlarge|64|256|50/none|16,000,000|14,000,000|32|8|30|150,000|8|
|ecs.g7ne.24xlarge|96|384|80/none|24,000,000|16,000,000|32|15|50|240,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

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
    -   I/O-intensive scenarios such as large and medium-sized Online Transaction Processing \(OLTP\) core databases
    -   Large and medium-sized NoSQL databases
    -   Search and real-time log analytics
    -   Traditional large enterprise-level commercial software, such as SAP

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------------|:-----------------------------|----------|:---|----------------------------|---------|-------------------------|
|ecs.g6se.large|2|8|0.7/2|300,000|2|2|6|30,000|1.5|
|ecs.g6se.xlarge|4|16|1/3|500,000|4|3|10|60,000|2|
|ecs.g6se.2xlarge|8|32|1.5/5|800,000|8|4|10|90,000|3|
|ecs.g6se.4xlarge|16|64|3/6|1,000,000|8|8|20|150,000|5|
|ecs.g6se.8xlarge|32|128|6/none|2,000,000|16|8|20|300,000|10|
|ecs.g6se.13xlarge|52|192|8/none|3,000,000|32|7|20|500,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

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

|Instance type|vCPUs|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|ENIs|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------------|:-----------------------------|:---|---------|-------------------------|
|ecs.g6a.large|2|8|1/10|900,000|2|12,500|1|
|ecs.g6a.xlarge|4|16|1.5/10|1,000,000|3|20,000|1.5|
|ecs.g6a.2xlarge|8|32|2.5/10|1,600,000|4|30,000|2|
|ecs.g6a.4xlarge|16|64|5/10|2,000,000|8|60,000|3|
|ecs.g6a.8xlarge|32|128|8/10|3,000,000|7|75,000|4|
|ecs.g6a.16xlarge|64|256|16/none|6,000,000|8|150,000|8|
|ecs.g6a.32xlarge|128|512|32/none|12,000,000|15|300,000|16|
|ecs.g6a.64xlarge|256|1024|64/none|24,000,000|15|600,000|32|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## g6t, security-enhanced general purpose instance family

Features

-   Implements trusted boot based on TCM or TPM chips. During a trusted boot, all modules in the boot chain from the underlying hardware to the guest OS are measured and verified.
-   Provides vTPMs that deliver a full set of trusted capabilities at the IaaS layer based on integrity monitoring.
-   Supports the Enclave feature and provides a trusted isolation space inside ECS instances to encapsulate the security operations of legitimate software within an enclave. This ensures the confidentiality and integrity of your code and data against malware attacks.
-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
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
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios that require high security and enhanced trust, such as services for financial organizations, public service sectors, and enterprises
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-level applications of various types and sizes
    -   Websites and application servers
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Computing clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|vTPM support|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:----------------------------------|:-----------------------------|------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.g6t.large|2|8|1.2/burstable up to 10|900,000|Yes|Up to 250,000|2|3|6|20,000|1|
|ecs.g6t.xlarge|4|16|2/burstable up to 10|1,000,000|Yes|Up to 250,000|4|4|15|40,000|1.5|
|ecs.g6t.2xlarge|8|32|3/burstable up to 10|1,600,000|Yes|Up to 250,000|8|4|15|50,000|2|
|ecs.g6t.4xlarge|16|64|6/burstable up to 10|3,000,000|Yes|300,000|8|8|30|80,000|3|
|ecs.g6t.8xlarge|32|128|10/none|6,000,000|Yes|600,000|16|8|30|150,000|5|
|ecs.g6t.13xlarge|52|192|16/none|9,000,000|Yes|900,000|32|7|30|240,000|8|
|ecs.g6t.26xlarge|104|384|32/none|24,000,000|Yes|1,800,000|32|15|30|480,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
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
    -   Computing clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-----------------------------------|:-----------------------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.g6e.large|2|8|1.2/burstable up to 10|900,000|Up to 250,000|2|3|6|20,000|1|
|ecs.g6e.xlarge|4|16|2/burstable up to 10|1,000,000|Up to 250,000|4|4|15|40,000|1.5|
|ecs.g6e.2xlarge|8|32|3/burstable up to 10|1,600,000|Up to 250,000|8|4|15|50,000|2|
|ecs.g6e.4xlarge|16|64|6/burstable up to 10|3,000,000|300,000|8|8|30|80,000|3|
|ecs.g6e.8xlarge|32|128|10/none|6,000,000|600,000|16|8|30|150,000|5|
|ecs.g6e.13xlarge|52|192|16/none|9,000,000|900,000|32|7|30|240,000|8|
|ecs.g6e.26xlarge|104|384|32/none|24,000,000|1,800,000|32|15|30|480,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other network metrics.

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
    -   Computing clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline/burst bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:----------------------------------|:-----------------------------|-----------|:---------|:---|----------------------------|---------|-------------------------|
|ecs.g6.large|2|8|1/3|300,000|Up to 250,000|2|2|6|10,000|1|
|ecs.g6.xlarge|4|16|1.5/5|500,000|Up to 250,000|4|3|10|20,000|1.5|
|ecs.g6.2xlarge|8|32|2.5/8|800,000|Up to 250,000|8|4|10|25,000|2|
|ecs.g6.3xlarge|12|48|4/10|900,000|Up to 250,000|8|6|10|30,000|2.5|
|ecs.g6.4xlarge|16|64|5/10|1,000,000|300,000|8|8|20|40,000|3|
|ecs.g6.6xlarge|24|96|7.5/10|1,500,000|450,000|12|8|20|50,000|4|
|ecs.g6.8xlarge|32|128|10/none|2,000,000|600,000|16|8|20|60,000|5|
|ecs.g6.13xlarge|52|192|12.5/none|3,000,000|900,000|32|7|20|100,000|8|
|ecs.g6.26xlarge|104|384|25/none|6,000,000|1,800,000|32|15|20|200,000|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

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
    -   Computing clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.g5.large|2|8|1|300,000|2|2|6|
|ecs.g5.xlarge|4|16|1.5|500,000|2|3|10|
|ecs.g5.2xlarge|8|32|2.5|800,000|2|4|10|
|ecs.g5.3xlarge|12|48|4|900,000|4|6|10|
|ecs.g5.4xlarge|16|64|5|1,000,000|4|8|20|
|ecs.g5.6xlarge|24|96|7.5|1,500,000|6|8|20|
|ecs.g5.8xlarge|32|128|10|2,000,000|8|8|20|
|ecs.g5.16xlarge|64|256|20|4,000,000|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

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
|ecs.g5ne.large|2|8|1|400,000|450,000|2|3|10|10,000|1|
|ecs.g5ne.xlarge|4|16|2|750,000|900,000|4|4|15|15,000|1|
|ecs.g5ne.2xlarge|8|32|3.5|1,500,000|1,750,000|8|6|15|30,000|1|
|ecs.g5ne.4xlarge|16|64|7|3,000,000|3,500,000|16|8|30|60,000|2|
|ecs.g5ne.8xlarge|32|128|15|6,000,000|7,000,000|32|8|30|120,000|4|
|ecs.g5ne.16xlarge|64|256|30|12,000,000|14,000,000|32|8|30|240,000|8|
|ecs.g5ne.18xlarge|72|288|33|13,500,000|16,000,000|32|15|50|270,000|9|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

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
    -   Computing clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.sn2ne.large|2|8|1|300,000|2|2|6|
|ecs.sn2ne.xlarge|4|16|1.5|500,000|2|3|10|
|ecs.sn2ne.2xlarge|8|32|2|1,000,000|4|4|10|
|ecs.sn2ne.3xlarge|12|48|2.5|1,300,000|4|6|10|
|ecs.sn2ne.4xlarge|16|64|3|1,600,000|4|8|20|
|ecs.sn2ne.6xlarge|24|96|4.5|2,000,000|6|8|20|
|ecs.sn2ne.8xlarge|32|128|6|2,500,000|8|8|20|
|ecs.sn2ne.14xlarge|56|224|10|4,500,000|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## References

-   [Instance families](/intl.en-US/Instance/Instance families.md)
-   [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md)

