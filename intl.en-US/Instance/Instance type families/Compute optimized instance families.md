---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Compute optimized instance families

This topic describes the features of compute optimized instance families of Elastic Compute Service \(ECS\) and lists the instance types of each family.

-   Recommended instance families
    -   [c7, compute optimized instance family](#c7)
    -   [c7t, security-enhanced compute optimized instance family](#section_m7c_byy_0ye)
    -   [c6a, compute optimized instance family](#section_i7i_zsw_bde)
    -   [c6t, security-enhanced compute optimized instance family](#section_c0u_8gn_bry)
    -   [c6e, compute optimized instance family with enhanced performance](#section_wiv_kqq_u7o)
    -   [c6, compute optimized instance family](#section_0yl_3wv_ims)
    -   [c5, compute optimized instance family](#section_1zf_ox2_m08)
    -   [ic5, compute intensive instance family](#section_5hn_iox_k41)
-   Other available instance families

    [sn1ne, compute optimized instance family with enhanced network performance](#section_2mi_djo_dff)


## c7, compute optimized instance family

Features

-   Uses the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Supports the vTPM feature and implements trusted boots based on Trusted Cryptography Module \(TCM\) or Trusted Platform Module \(TPM\) chips to provide ultra-high security capabilities. During a trusted boot, all modules in the boot chain from the underlying server to the ECS instance are measured and verified.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses the third-generation Intel® Xeon® Scalable processors \(Ice Lake\) that deliver an all-core turbo frequency of 3.5 GHz for consistent computing performance.
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

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|vTPM support|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|--------------------|:------------------------------|------------|----------|:---|----------------------------|---------------|-------------------------|
|ecs.c7.large|2|4.0|Burstable up to 10.0|900|Yes|2|3|6|Burstable up to 100|Burstable up to 6.0|
|ecs.c7.xlarge|4|8.0|Burstable up to 100|1,000|Yes|4|4|15|Burstable up to 100|Burstable up to 6.0|
|ecs.c7.2xlarge|8|16.0|Burstable up to 100|1,600|Yes|8|4|15|Burstable up to 100|Burstable up to 6.0|
|ecs.c7.3xlarge|12|24.0|Burstable up to 100|2,400|Yes|8|8|15|Burstable up to 100|Burstable up to 6.0|
|ecs.c7.4xlarge|16|32.0|Burstable up to 25.0|3,000|Yes|8|8|30|Burstable up to 100|Burstable up to 6.0|
|ecs.c7.6xlarge|24|48.0|Burstable up to 25.0|4,500|Yes|12|8|30|100|6.0|
|ecs.c7.8xlarge|32|64.0|Burstable up to 25.0|6,000|Yes|16|8|30|150|8.0|
|ecs.c7.16xlarge|64|128.0|32.0|12,000|Yes|32|8|30|300|16.0|
|ecs.c7.32xlarge|128|256.0|64.0|24,000|Yes|32|15|30|600|32.0|

**Note:**

-   If you use Virtual Network Computing \(VNC\) to log on to a Windows instance, two cursors may appear. For information about how to fix this issue, see the [Why do two cursors appear after I use VNC to log on to a Windows instance?](/intl.en-US/Instance/Instance FAQ.md) section in Instance FAQ.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## c7t, security-enhanced compute optimized instance family

This instance family is in invitational preview. To use this instance family, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

Features

-   Supports up to 128 GiB encrypted memory and encrypted computing based on Intel® Software Guard Extensions \(SGX\) to protect the confidentiality and integrity of key code and data from malicious attacks.
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

|Instance type|vCPU|Memory \(GiB\)|Encrypted memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|vTPM support|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|------------------------|--------------------|:------------------------------|------------|----------|:---|----------------------------|---------------|-------------------------|
|ecs.c7t.large|2|4.0|2.0|Burstable up to 10.0|900|Yes|2|3|6|Burstable up to 100|Burstable up to 6.0|
|ecs.c7t.xlarge|4|8.0|4.0|Burstable up to 100|1,000|Yes|4|4|15|Burstable up to 100|Burstable up to 6.0|
|ecs.c7t.2xlarge|8|16.0|8.0|Burstable up to 100|1,600|Yes|8|4|15|Burstable up to 100|Burstable up to 6.0|
|ecs.c7t.3xlarge|12|24.0|12.0|Burstable up to 100|2,400|Yes|8|8|15|Burstable up to 100|Burstable up to 6.0|
|ecs.c7t.4xlarge|16|32.0|16.0|Burstable up to 25.0|3,000|Yes|8|8|30|Burstable up to 100|Burstable up to 6.0|
|ecs.c7t.6xlarge|24|48.0|24.0|Burstable up to 25.0|4,500|Yes|12|8|30|100|6.0|
|ecs.c7t.8xlarge|32|64.0|32.0|Burstable up to 25.0|6,000|Yes|16|8|30|150|8.0|
|ecs.c7t.16xlarge|64|128.0|64.0|32.0|12,000|Yes|32|8|30|300|16.0|
|ecs.c7t.32xlarge|128|256.0|128.0|64.0|24,000|Yes|32|15|30|600|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## c6a, compute optimized instance family

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses 2.6 GHz AMD EPYCTM ROME processors that deliver a turbo frequency of 3.3 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

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

|Instance type|vCPU|Memory \(GiB\)|Baseline bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|ENIs|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|-----------------------------|------------------------------|:------------------------------|:---|---------------|-------------------------|
|ecs.c6a.large|2|4.0|1.0|10.0|900|2|12.5|1.0|
|ecs.c6a.xlarge|4|8.0|1.5|10.0|1,000|3|20|1.5|
|ecs.c6a.2xlarge|8|16.0|2.5|10.0|1,600|4|30|2.0|
|ecs.c6a.4xlarge|16|32.0|5.0|10.0|2,000|8|60|3.0|
|ecs.c6a.8xlarge|32|64.0|8.0|10.0|3,000|7|75|4,0|
|ecs.c6a.16xlarge|64|128.0|16.0|None|6,000|8|150|8.0|
|ecs.c6a.32xlarge|128|256.0|32.0|None|12,000|15|300|16.0|
|ecs.c6a.64xlarge|256|512.0|64.0|None|24,000|15|600|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

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

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

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

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|vTPM support|Connections \(K\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|--------------------|:------------------------------|------------|-----------------|:---------|:---|----------------------------|---------------|-------------------------|
|ecs.c6t.large|2|4.0|Burstable up to 10.0|900|Yes|Up to 250|2|3|6|20|1.0|
|ecs.c6t.xlarge|4|8.0|Burstable up to 100|1,000|Yes|Up to 250|4|4|15|40|1.5|
|ecs.c6t.2xlarge|8|16.0|Burstable up to 100|1,600|Yes|Up to 250|8|4|15|50|2.0|
|ecs.c6t.4xlarge|16|32.0|Burstable up to 100|3,000|Yes|300|8|8|30|80|3.0|
|ecs.c6t.8xlarge|32|64.0|10.0|6,000|Yes|600|16|8|30|150|5.0|
|ecs.c6t.13xlarge|52|96.0|16.0|9,000|Yes|900|32|7|30|240|8.0|
|ecs.c6t.26xlarge|104|192.0|32.0|24,000|Yes|1,800|32|15|30|480|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other network metrics.

## c6e, compute optimized instance family with enhanced performance

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads. This instance family improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of chips.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269 \(Cascade\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

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

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|Connections \(K\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|--------------------|:------------------------------|-----------------|:---------|:---|----------------------------|---------------|-------------------------|
|ecs.c6e.large|2|4.0|Burstable up to 10.0|900|Up to 250|2|3|6|20|1.0|
|ecs.c6e.xlarge|4|8.0|Burstable up to 100|1,000|Up to 250|4|4|15|40|1.5|
|ecs.c6e.2xlarge|8|16.0|Burstable up to 100|1,600|Up to 250|8|4|15|50|2.0|
|ecs.c6e.4xlarge|16|32.0|Burstable up to 100|3,000|300|8|8|30|80|3.0|
|ecs.c6e.8xlarge|32|64.0|10.0|6,000|600|16|8|30|150|5.0|
|ecs.c6e.13xlarge|52|96.0|16.0|9,000|900|32|7|30|240|8.0|
|ecs.c6e.26xlarge|104|192.0|32.0|24,000|1,800|32|15|30|480|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other network metrics.

## c6, compute optimized instance family

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

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

|Instance type|vCPU|Memory \(GiB\)|Baseline bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|Connections \(K\)|NIC queues|ENIs|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:----------------------------|------------------------------|:------------------------------|-----------------|:---------|:---|----------------------------|---------------|-------------------------|
|ecs.c6.large|2|4.0|1.0|3.0|300|Up to 250|2|2|6|10|1|
|ecs.c6.xlarge|4|8.0|1.5|5.0|500|Up to 250|4|3|10|20|1.5|
|ecs.c6.2xlarge|8|16.0|2.5|8.0|800|Up to 250|8|4|10|25|2|
|ecs.c6.3xlarge|12|24.0|4.0|10.0|900|Up to 250|8|6|10|30|2.5|
|ecs.c6.4xlarge|16|32.0|5.0|10.0|1,000|300|8|8|20|40|3|
|ecs.c6.6xlarge|24|48.0|7.5|10.0|1,500|450|12|8|20|50|4|
|ecs.c6.8xlarge|32|64.0|10.0|None|2,000|600|16|8|20|60|5|
|ecs.c6.13xlarge|52|96.0|12.5|None|3,000|900|32|7|20|100|8|
|ecs.c6.26xlarge|104|192.0|25.0|None|6,000|1,800|32|15|20|200|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

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

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.c5.large|2|4.0|1.0|300|2|2|6|
|ecs.c5.xlarge|4|8.0|1.5|500|2|3|10|
|ecs.c5.2xlarge|8|16.0|2.5|800|2|4|10|
|ecs.c5.3xlarge|12|24.0|4.0|900|4|6|10|
|ecs.c5.4xlarge|16|32.0|5.0|1,000|4|8|20|
|ecs.c5.6xlarge|24|48.0|7.5|1,500|6|8|20|
|ecs.c5.8xlarge|32|64.0|10.0|2,000|8|8|20|
|ecs.c5.16xlarge|64|128.0|20.0|4,000|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

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

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.ic5.large|2|2.0|1.0|300|2|2|6|
|ecs.ic5.xlarge|4|4.0|1.5|500|2|3|10|
|ecs.ic5.2xlarge|8|8.0|2.5|800|2|4|10|
|ecs.ic5.3xlarge|12|12.0|4.0|900|4|6|10|
|ecs.ic5.4xlarge|16|16.0|5.0|1,000|4|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

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

|Instance type|vCPU|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:---|:-------------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.sn1ne.large|2|4.0|1.0|300|2|2|6|
|ecs.sn1ne.xlarge|4|8.0|1.5|500|2|3|10|
|ecs.sn1ne.2xlarge|8|16.0|2.0|1,000|4|4|10|
|ecs.sn1ne.3xlarge|12|24.0|2.5|1,300|4|6|10|
|ecs.sn1ne.4xlarge|16|32.0|3.0|1,600|4|8|20|
|ecs.sn1ne.6xlarge|24|48.0|4.5|2,000|6|8|20|
|ecs.sn1ne.8xlarge|32|64.0|6.0|2,500|8|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## References

-   [Instance families](/intl.en-US/Instance/Instance families.md)
-   [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md)

