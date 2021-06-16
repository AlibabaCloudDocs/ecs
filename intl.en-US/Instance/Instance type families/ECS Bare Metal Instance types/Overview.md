---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Overview

This topic describes the features of Elastic Compute Service \(ECS\) Bare Metal Instance families and lists the instance types of each family.

-   Recommended instance families
    -   General purpose instance families:
        -   [ebmg6a, general purpose ECS Bare Metal Instance family](#section_vk4_ake_dah)
        -   [ebmg6e, general purpose ECS Bare Metal Instance family with enhanced performance](#section_69g_hx0_psw)
        -   [ebmg6, general purpose ECS Bare Metal Instance family](#section_qkb_ez6_9c5)
    -   Compute optimized instance families:
        -   [ebmc6me, compute optimized ECS Bare Metal Instance family](#ebmc6me)
        -   [ebmc6a, compute optimized ECS Bare Metal Instance family](#section_m8p_b2e_yqq)
        -   [ebmc6e, compute optimized ECS Bare Metal Instance family with enhanced performance](#section_mdc_24m_q3e)
        -   [ebmc6, compute optimized ECS Bare Metal Instance family](#section_zec_q52_xn9)
    -   Memory optimized instance families:
        -   [ebmr6a, memory optimized ECS Bare Metal Instance family](#section_qwd_bje_kuu)
        -   [ebmr6e, memory optimized ECS Bare Metal Instance family with enhanced performance](#section_ltv_trm_b0o)
        -   [ebmr6, memory optimized ECS Bare Metal Instance family](#section_yv1_t65_log)
        -   [ebmre6p, persistent memory optimized ECS Bare Metal Instance family with enhanced performance](#section_xli_oah_7tq)
        -   [ebmre6-6t, memory optimized ECS Bare Metal Instance family with enhanced performance](#section_6kk_g42_kgh)
    -   Instance families with high clock speeds:
        -   [ebmhfg7, general purpose ECS Bare Metal Instance family with high clock speeds](#section_w8p_4nu_o5m)
        -   [ebmhfc7, compute optimized ECS Bare Metal Instance family with high clock speeds](#section_44h_4rq_5bd)
        -   [ebmhfr7, memory optimized ECS Bare Metal Instance family with high clock speeds](#section_1ja_58l_yiv)
        -   [ebmhfg6, general purpose ECS Bare Metal Instance family with high clock speeds](#section_czp_w4q_mb8)
        -   [ebmhfc6, compute optimized ECS Bare Metal Instance family with high clock speeds](#section_s0v_ihb_z5x)
        -   [ebmhfr6, memory optimized ECS Bare Metal Instance family with high clock speeds](#section_sns_ot8_a1r)
    -   GPU-accelerated compute optimized instance families:
        -   [ebmgn7, GPU-accelerated compute optimized ECS Bare Metal Instance family](#section_71m_cxy_5ct)
        -   [ebmgn6e, GPU-accelerated compute optimized ECS Bare Metal Instance family](#section_xyl_5bo_wez)
        -   [ebmgn6v, GPU-accelerated compute optimized ECS Bare Metal Instance family](#section_lke_80h_kzu)
        -   [ebmgn6i, GPU-accelerated compute optimized ECS Bare Metal Instance family](#section_slz_oyd_k1t)
-   Other available instance families
    -   [ebmg5s, general purpose ECS Bare Metal Instance family with enhanced network performance](#section_qiz_xda_sce)
    -   [ebmg5, general purpose ECS Bare Metal Instance family](#section_nii_o5k_4t2)
    -   [ebmc5s, compute optimized ECS Bare Metal Instance family with enhanced network performance](#section_pnq_v2c_u07)
    -   [ebmc4, compute optimized ECS Bare Metal Instance family](#section_8xi_1ce_45q)
    -   [ebmr5s, memory optimized ECS Bare Metal Instance family with enhanced network performance](#section_v7p_ot4_f4n)
    -   [ebmhfg5, ECS Bare Metal Instance family with high clock speeds](#section_69a_h1f_n9m)

## Introduction

ECS Bare Metal Instance is a compute service that combines the elasticity of virtual machines and the performance and features of physical machines. ECS Bare Metal Instance is designed based on the state-of-the-art virtualization 2.0 technology developed by Alibaba Cloud. The virtualization 2.0 technology used by ECS Bare Metal Instance is optimized to support common ECS instances and nested virtualization. It maintains the elasticity of ECS instances and the performance and features of physical machines.

ECS Bare Metal Instance combines the strengths of both physical machines and ECS instances to deliver powerful and robust computing capabilities. ECS Bare Metal Instance uses virtualization 2.0 to provide your business applications with direct access to the processor and memory resources of the underlying servers without virtualization overheads. ECS Bare Metal Instance retains the hardware feature sets \(such as Intel® VT-x\) and resource isolation capabilities of physical machines, which is ideal for applications that need to run in non-virtualization environments.

ECS Bare Metal Instance integrates features from both physical and virtual machines based on the proprietary chips, hypervisor system software, and a redefined server hardware architecture. ECS Bare Metal Instance can seamlessly connect with other Alibaba Cloud services for storage, networking, and database tasks. ECS Bare Metal Instance is fully compatible with ECS images. These properties allow you to build resources to suit your business requirements.

When you use ECS Bare Metal Instance, take note of the following items:

-   ECS Bare Metal Instance does not support instance type changes.
-   If the physical machine that hosts an ECS bare metal instance fails, the system fails the instance over to another physical machine. Data is retained in the data disks of the instance.

## Benefits

ECS Bare Metal Instance provides the following benefits based on technological innovations:

-   Exclusive computing resources

    ECS Bare Metal Instance is a cloud-based elastic computing service that provides the same performance and resource isolation capabilities as physical machines. It can ensure the exclusivity of computing resources without virtualization overheads or feature loss. ECS Bare Metal Instance supports high clock speeds and 8, 32, 80, 96, and 104 vCPUs. An ECS bare metal instance that has eight vCPUs can have a maximum clock speed of 3.7 GHz to 4.1 GHz and provide better performance and faster response for gaming and finance business than peer services.

-   Chip-level security

    In addition to physical isolation, ECS Bare Metal Instance uses a chip-level trusted execution environment of Intel® Software Guard Extensions \(SGX\) to ensure that encrypted data can be computed only in a secure and trusted environment. This chip-level hardware security protection provides a safe box for your data in the cloud and allows you to control all data encryption and key protection processes. For more information, see [Install SGX](/intl.en-US/Instance/Instance type families/ECS Bare Metal Instance types/Install SGX.md).

-   Compatibility with multiple private clouds

    ECS Bare Metal Instance can address the needs of high-performance computing and help you build new hybrid clouds. Thanks to the flexibility, elasticity, and other strengths inherited from the mix of physical and virtual machines, ECS Bare Metal Instance can implement re-virtualization. Offline private cloud business can be seamlessly migrated to Alibaba Cloud without performance overheads arising from nested virtualization. This provides you a new method to move business to the cloud.

-   Support for heterogeneous instruction set processors

    ECS Bare Metal Instance uses virtualization 2.0 developed by Alibaba Cloud and supports instruction set processors such as Advanced RISC Machine \(ARM\) at no additional costs.


## Comparison of ECS bare metal instances, physical machines, and virtual machines

An ECS bare metal instance delivers better performance than a physical machine that has the same configurations. During Double 11, ECS bare metal instances delivered robust computing capabilities with millions of vCPUs to handle traffic spikes.

The following table compares the features of ECS bare metal instances, physical machines, and virtual machines. In this table, Y means supported, N means not supported, and N/A means not applicable.

|Feature type|Feature|ECS bare metal instance|Physical machine|Virtual machine|
|:-----------|:------|:----------------------|:---------------|:--------------|
|Automated O&M|Delivery within minutes|Y|N|Y|
|Compute|Zero performance loss|Y|Y|N|
|Zero feature loss|Y|Y|N|
|Zero resource contention|Y|Y|N|
|Storage|Compatibility with ECS disks|Y|N|Y|
|Startup from system disks|Y|N|Y|
|Quick reset of system disks|Y|N|Y|
|Use of ECS images|Y|N|Y|
|Cold migration between physical and virtual machines|Y|N|Y|
|No need to install the operating system|Y|N|Y|
|No need of local RAIDs and better protection of data in disks|Y|N|Y|
|Networking|Compatibility with virtual private clouds \(VPCs\)|Y|N|Y|
|Compatibility with the classic network|Y|N|Y|
|No communication bottlenecks between physical and virtual machine clusters in VPCs|Y|N|Y|
|Management|Compatibility with existing ECS management systems|Y|N|Y|
|Consistent user experience on features such as Virtual Network Computing \(VNC\) with that on virtual machines|Y|N|Y|
|Out-of-band \(OOB\) network security|Y|N|N/A|

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

## ebmc6me, compute optimized ECS Bare Metal Instance family

Features

-   Provides dedicated hardware resources and physical isolation.
-   Offers a CPU-to-memory ratio of 1:3.
-   Uses 2.3 GHz Intel® Xeon® Gold 5218 \(Cascade Lake\) processors that deliver a turbo frequency of 3.9 GHz.
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
    -   Frontend servers of massively multiplayer online \(MMO\) games
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|-----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmc6me.16xlarge|64|192.0|32.0|6,000,000|1,800,000|32|10|200,000|16.0|

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
    -   Frontend servers of MMO games
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
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise-level applications

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

To use ebmre6p, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

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

|Instance type|vCPUs|Memory \(GiB\)|Persistent memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|-------------------------|:-------------------|:-----------------------------|:---|----------------------------|---------|-------------------------|
|ecs.ebmre6p.26xlarge|104|384.0|1536.0|32.0|6,000,000|32|10|200,000|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmre6-6t, memory optimized ECS Bare Metal Instance family with enhanced performance

To use ebmre6-6t, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

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
    -   High-performance databases and in-memory databases such as SAP HANA
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
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise-level applications

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
    -   Hadoop clusters, Spark clusters, and other memory-intensive enterprise-level applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|Connections|ENIs|Private IP addresses per ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:----|:-------------|:-------------------|:-----------------------------|:----------|:---|----------------------------|---------|-------------------------|
|ecs.ebmhfr6.20xlarge|80|768.0|32.0|6,000,000|1,800,000|32|10|200,000|16.0|

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
    -   Deep learning applications, such as training applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications that have high GPU workloads, such as computational fluid dynamics, computational finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPU|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|---|:-------------------|:-----------------------------|:---------|:---|----------------------------|
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
    -   32 GB HBM2 memory per GPU \(900 GB/s bandwidth\)
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
    -   Deep learning applications, such as training and inference applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications such as fluid dynamics, finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPU|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|---|----------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.ebmgn6e.24xlarge|96|768.0|NVIDIA V100 × 8|32GB × 8|32.0|4,800,000|16|15|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmgn6v, GPU-accelerated compute optimized ECS Bare Metal Instance family

Features

-   Provides flexible and powerful software-defined compute based on the SHENLONG architecture.
-   Uses NVIDIA V100 GPUs.
-   Uses NVIDIA V100 GPUs \(SXM2-based\) that have the following features:
    -   Innovative Volta architecture
    -   16 GB HBM2 memory per GPU \(900 GB/s bandwidth\)
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
    -   Deep learning applications, such as training and inference applications of AI algorithms used in image classification, autonomous vehicles, and speech recognition
    -   Scientific computing applications such as fluid dynamics, finance, molecular dynamics, and environmental analysis

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPU|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|---|----------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.ebmgn6v.24xlarge|96|384.0|NVIDIA V100 × 8|16GB × 8|30.0|4,500,000|8|32|10|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## ebmgn6i, GPU-accelerated compute optimized ECS Bare Metal Instance family

Features

-   Provides flexible and powerful software-defined compute based on the SHENLONG architecture.
-   Uses NVIDIA T4 GPUs that have the following features:
    -   Innovative NVIDIA Turing architecture
    -   16 GB memory per GPU \(320 GB/s bandwidth\)
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

|Instance type|vCPUs|Memory \(GiB\)|GPU|GPU memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(pps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|---|------------------|:-------------------|:-----------------------------|:---------|:---|----------------------------|
|ecs.ebmgn6i.24xlarge|96|384.0|NVIDIA T4 × 4|16GB × 4|30.0|4,500,000|8|32|10|

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

## Billing methods

ECS Bare Metal Instance supports pay-as-you-go and subscription billing methods. For more information, see [Billing method overview](/intl.en-US/Pricing/Billing methods/Billing method overview.md).

