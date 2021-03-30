---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# General purpose instance families

This topic describes the features of general purpose instance families of ECS and lists the instance types of each family.

-   Recommended instance families
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


## g7t, security-enhanced general purpose instance family

g7t is in invitational preview. To use g7t, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

-   Supports confidential computing based on Intel® SGX and up to 256 GiB encrypted memory to protect the confidentiality and integrity of key codes and data from malware attacks.
-   Supports SGX technology applicable to virtual machines and allows you to select instance types based on your needs.
-   Implements trusted boot based on Trusted Cryptography Module \(TCM\) or Trusted Platform Module \(TPM\) chips. During a trusted boot, all modules in the boot chain from the underlying hardware to the guest OS are measured and verified.
-   Uses the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory-to-encrypted memory ratio of 1:2:2.
    -   Uses the third-generation Intel® Xeon® scalable processors \(Ice Lake\) that deliver an all-core turbo frequency of 3.5 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs \(ESSDs\) only.
    -   Provides high storage I/O performance based on large computing capacity.
-   Network:
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

|Instance type|vCPUs|Memory \(GiB\)|Encrypted memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|vTPM support|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|------------------------|:--------------------|-----------------------------------|:---------------------------------------------|------------|:-----------|----------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.g7t.large|2|4.0|4.0|None|Burstable up to 10.0|900|Yes|Yes|2|3|6|Burstable up to 100|Burstable up to 6.0|
|ecs.g7t.xlarge|4|8.0|8.0|None|Burstable up to 10.0|1,000|Yes|Yes|4|4|15|Burstable up to 100|Burstable up to 6.0|
|ecs.g7t.2xlarge|8|16.0|16.0|None|Burstable up to 10.0|1,600|Yes|Yes|8|4|15|Burstable up to 100|Burstable up to 6.0|
|ecs.g7t.3xlarge|12|24.0|24.0|None|Burstable up to 10.0|2,400|Yes|Yes|8|8|15|Burstable up to 100|Burstable up to 6.0|
|ecs.g7t.4xlarge|16|32.0|32.0|None|Burstable up to 25.0|3,000|Yes|Yes|8|8|30|Burstable up to 100|Burstable up to 6.0|
|ecs.g7t.6xlarge|24|48.0|48.0|None|Burstable up to 25.0|4,500|Yes|Yes|12|8|30|100|6.0|
|ecs.g7t.8xlarge|32|64.0|64.0|None|Burstable up to 25.0|6,000|Yes|Yes|16|8|30|150|8.0|
|ecs.g7t.16xlarge|64|128.0|128.0|None|32.0|12,000|Yes|Yes|32|8|30|300|16.0|
|ecs.g7t.32xlarge|128|256.0|256.0|None|64.0|24,000|Yes|Yes|32|15|30|600|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## g7ne, general purpose instance family with enhanced network performance

g7ne is in invitational preview. To use g7ne, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

-   Improves the network bandwidth and packet forwarding rate of a single instance.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses Intel® Xeon® Platinum 8369HB \(Cooper Lake\) or Intel® Xeon® Platinum 8369HC \(Cooper Lake\) processors that deliver a maximum turbo frequency of 3.8 GHz and a minimum clock speed of 3.3 GHz for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs only and provides ultra-high I/O performance.
-   Network:
    -   Provides ultra-high network performance with a packet forwarding rate of up to 24,000 Kpps per instance.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Network intensive scenarios such as NFV or SD-WAN, mobile Internet, on-screen video comments, and telecom data forwarding
    -   Small and medium-sized database systems, caches, and search clusters
    -   Enterprise-level applications of various types and sizes
    -   Big data analysis and machine learning

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:--------------------|--------------------------------------------|---------------------------------------------|:---------------------------------------------|:-----------|-----------------|----------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.g7ne.large|2|8.0|None|1.5|25.0|900|Yes|450|2|3|10|10|0.75|
|ecs.g7ne.xlarge|4|16.0|None|3.0|25.0|1,000|Yes|900|4|4|15|20|1.0|
|ecs.g7ne.2xlarge|8|32.0|None|6.0|25.0|1,500|Yes|1,750|8|6|15|25|1.5|
|ecs.g7ne.4xlarge|16|64.0|None|12.5|25.0|3,000|Yes|3,500|16|8|30|40|2.5|
|ecs.g7ne.8xlarge|32|128.0|None|25.0|None|6,000|Yes|7,000|16|8|30|75|5.0|
|ecs.g7ne.12xlarge|48|192.0|None|40.0|None|12,000|Yes|8,000|32|8|30|100|8.0|
|ecs.g7ne.16xlarge|64|256.0|None|50.0|None|16,000|Yes|14,000|32|8|30|150|8.0|
|ecs.g7ne.24xlarge|96|384.0|None|80.0|None|24,000|Yes|16,000|32|15|50|240|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## g6se, storage enhanced instance family

g6se is in invitational preview. To use g6se, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Delivers a sequential read/write performance of up to 32 Gbit/s per instance.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs only and provides ultra-high I/O performance.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   I/O-intensive scenarios such as large and medium-sized OLTP core databases
    -   Large and medium-sized NoSQL databases
    -   Search and real-time log analytics
    -   Traditional large enterprise-level commercial software, such as SAP

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:--------------------|--------------------------------------------|---------------------------------------------|:---------------------------------------------|:-----------|----------|:---------------------------------|----------------------------|---------------|-------------------------|
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

Features

-   Uses the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
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
    -   Provides ultra-high packet forwarding rates.
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Video encoding and decoding
    -   Scenarios where large volumes of packets are received and transmitted
    -   Websites and application servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Game servers
    -   Test and development, such as DevOps
    -   Other general-purpose enterprise-level applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|ENIs \(including one primary ENI\)|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:--------------------|--------------------------------------------|---------------------------------------------|:---------------------------------------------|:-----------|:---------------------------------|---------------|-------------------------|
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

Features

-   Implements trusted boot based on TCM or TPM chips. During a trusted boot, all modules in the boot chain from the underlying hardware to the guest OS are measured and verified.
-   Provides vTPMs that deliver a full set of trusted capabilities at the IaaS layer based on integrity monitoring.
-   Supports the Enclave feature and provides a trusted isolation space inside ECS instances to encapsulate security operations of legitimate software in an enclave. This ensures the confidentiality and integrity of your code and data against malware attacks.
-   Uses the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269 \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs only.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
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

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|vTPM support|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|------------|------------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.g6t.large|2|8.0|None|Burstable up to 10.0|900|Yes|Yes|Up to 250|2|3|6|20|1.0|
|ecs.g6t.xlarge|4|16.0|None|Burstable up to 10.0|1,000|Yes|Yes|Up to 250|4|4|15|40|1.5|
|ecs.g6t.2xlarge|8|32.0|None|Burstable up to 10.0|1,600|Yes|Yes|Up to 250|8|4|15|50|2.0|
|ecs.g6t.4xlarge|16|64.0|None|Burstable up to 10.0|3,000|Yes|Yes|300|8|8|30|80|3.0|
|ecs.g6t.8xlarge|32|128.0|None|10.0|6,000|Yes|Yes|600|16|8|30|150|5.0|
|ecs.g6t.13xlarge|52|192.0|None|16.0|9,000|Yes|Yes|900|32|7|30|240|8.0|
|ecs.g6t.26xlarge|104|384.0|None|32.0|24,000|Yes|Yes|1,800|32|15|30|480|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other network metrics.

## g6e, general purpose instance family with enhanced performance

Features

-   Uses the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269 \(Cascade\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
-   Allows you to enable or disable Hyper-Threading.

    **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs only.
-   Provides high network and storage I/O performance based on large computing capacity.

    **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Provides ultra-high packet forwarding rates.

    **Note:** The maximum network performance varies with instance families. For higher concurrent connection capabilities, we recommend that you use g5ne.

-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-level applications of various types and sizes
    -   Websites and application servers
    -   Game servers
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:--------------------|-----------------------------------|:---------------------------------------------|:-----------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.g6e.large|2|8.0|None|Burstable up to 10.0|900|Yes|Up to 250|2|3|6|20|1.0|
|ecs.g6e.xlarge|4|16.0|None|Burstable up to 10.0|1,000|Yes|Up to 250|4|4|15|40|1.5|
|ecs.g6e.2xlarge|8|32.0|None|Burstable up to 10.0|1,600|Yes|Up to 250|8|4|15|50|2.0|
|ecs.g6e.4xlarge|16|64.0|None|Burstable up to 10.0|3,000|Yes|300|8|8|30|80|3.0|
|ecs.g6e.8xlarge|32|128.0|None|10.0|6,000|Yes|600|16|8|30|150|5.0|
|ecs.g6e.13xlarge|52|192.0|None|16.0|9,000|Yes|900|32|7|30|240|8.0|
|ecs.g6e.26xlarge|104|384.0|None|32.0|24,000|Yes|1,800|32|15|30|480|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other network metrics.

## g6, general purpose instance family

Features

-   Uses the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a turbo frequency of 3.2 GHz for consistent computing performance.
-   Allows you to enable or disable Hyper-Threading.

    **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.

    **Note:** The maximum performance of disks varies with instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

-   Provides high storage I/O performance based on large compute capacity.

    **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Provides ultra-high packet forwarding rates.

    **Note:** The maximum network performance varies with instance families. For higher concurrent connection capabilities, we recommend that you use g5ne.

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

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:--------------------|:-------------------------------------------|---------------------------------------------|:---------------------------------------------|:-----------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.g6.large|2|8.0|None|1.0|3.0|300|Yes|Up to 250|2|2|6|10|1|
|ecs.g6.xlarge|4|16.0|None|1.5|5.0|500|Yes|Up to 250|4|3|10|20|1.5|
|ecs.g6.2xlarge|8|32.0|None|2.5|8.0|800|Yes|Up to 250|8|4|10|25|2|
|ecs.g6.3xlarge|12|48.0|None|4.0|10.0|900|Yes|Up to 250|8|6|10|30|2.5|
|ecs.g6.4xlarge|16|64.0|None|5.0|10.0|1,000|Yes|300|8|8|20|40|3|
|ecs.g6.6xlarge|24|96.0|None|7.5|10.0|1,500|Yes|450|12|8|20|50|4|
|ecs.g6.8xlarge|32|128.0|None|10.0|None|2,000|Yes|600|16|8|20|60|5|
|ecs.g6.13xlarge|52|192.0|None|12.5|None|3,000|Yes|900|32|7|20|100|8|
|ecs.g6.26xlarge|104|384.0|None|25.0|None|6,000|Yes|1,800|32|15|20|200|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## g5, general purpose instance family

Features

-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) or 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.

    **Note:** The maximum performance of disks varies with instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

-   Provides ultra-high packet forwarding rates.

    **Note:** The maximum network performance varies with instance families. For higher concurrent connection capabilities, we recommend that you use g5ne.

-   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-level applications of various types and sizes
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
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

## g5ne, general purpose instance family with enhanced network performance

Features

-   Significantly improves the network throughput and packet forwarding rate per instance. A single instance can deliver a packet forwarding rate of up to 10,000 Kpps.
-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) or 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks.
-   Provides high network performance based on large computing capacity.

    **Note:** We recommend that you select instance types of the g5ne instance family to deploy Data Plane Development Kit \(DPDK\) applications.

-   Suits the following scenarios:
    -   DPDK applications
    -   Network intensive scenarios such as NFV or SD-WAN, mobile Internet, on-screen video comments, and telecom data forwarding
    -   Small and medium-sized database systems, caches, and search clusters
    -   Enterprise-level applications of various types and sizes
    -   Big data analysis and machine learning

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|------------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.g5ne.large|2|8.0|None|1.0|400|Yes|450|2|3|10|10|1|
|ecs.g5ne.xlarge|4|16.0|None|2.0|750|Yes|900|4|4|15|15|1|
|ecs.g5ne.2xlarge|8|32.0|None|3.5|1,500|Yes|1750|8|6|15|30|1|
|ecs.g5ne.4xlarge|16|64.0|None|7.0|3,000|Yes|3,500|16|8|30|60|2|
|ecs.g5ne.8xlarge|32|128.0|None|15.0|6,000|Yes|7,000|32|8|30|120|4|
|ecs.g5ne.16xlarge|64|256.0|None|30.0|12,000|Yes|14,000|32|8|30|240|8|
|ecs.g5ne.18xlarge|72|288.0|None|33.0|13,500|Yes|16,000|32|15|50|270|9|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## sn2ne, general purpose instance family with enhanced network performance

Features

-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) or Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Provides ultra-high packet forwarding rates.
-   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and telecom data forwarding
    -   Enterprise-level applications of various types and sizes
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing
    -   Compute clusters and memory-intensive data processing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
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

