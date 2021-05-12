---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Overview

This topic describes the features of Super Computing Cluster \(SCC\) instance families and lists the instance types of each family.

-   [scchfc6, compute optimized SCC instance family with high clock speeds](#section_pn1_b80_0du)
-   [scchfg6, general purpose SCC instance family with high clock speeds](#section_7hn_bci_mdv)
-   [scchfr6, memory optimized SCC instance family with high clock speeds](#section_bl1_dyi_mil)
-   [scch5, SCC instance family with high clock speeds](#section_o3g_ifk_1fs)
-   [sccg5, general purpose SCC instance family](#section_rcg_pie_45u)
-   [sccgn6e, GPU-accelerated compute optimized SCC instance family](#section_0ql_a2s_pga)
-   [sccgn6, GPU-accelerated compute optimized SCC instance family](#section_qo6_ux9_4ar)

## Introduction

SCC is based on ECS Bare Metal Instance and significantly improves the network performance and acceleration ratio of large-scale clusters by using the high-speed Remote Direct Memory Access \(RDMA\) based interconnects. SCC has all the benefits of ECS Bare Metal Instance and can provide high-quality network performance that features high bandwidth and low latency.

SCC is used in scenarios such as high performance computing, artificial intelligence, machine learning, scientific and engineering computing, data analysis, and audio and video processing. In SCCs, nodes are connected over RDMA networks that feature high bandwidth and low latency. This ensures the parallel efficiency of applications in areas such as high performance computing, artificial intelligence, and machine learning. RDMA over Converged Ethernet \(RoCE\) networks rival InfiniBand networks in terms of connection speed and can support more Ethernet-based applications.

SCC can be used in conjunction with other Alibaba Cloud computing services such as Elastic Compute Service \(ECS\) and Elastic GPU Service to provide ultimate high-performance parallel computing resources for [Elastic High Performance Computing \(E-HPC\)](https://www.alibabacloud.com/help/doc-detail/57677.htm) and make cloud-based super computing possible.

## Comparison of SCCs, physical machines, and virtual machines

The following table compares the features of SCCs, physical machines, and virtual machines. In this table, Y means supported, N means not supported, and N/A means not applicable.

|Feature type|Feature|SCC|Physical machine|Virtual machine|
|:-----------|:------|:--|:---------------|:--------------|
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
|No need of local redundant arrays of independent disks \(RAIDs\) and better protection of data in disks|Y|N|Y|
|Networks|Compatibility with virtual private clouds \(VPCs\)|Y|N|Y|
|Compatibility with the classic network|Y|N|Y|
|No communication bottlenecks between physical and virtual machine clusters in VPCs|Y|N|Y|
|Management|Compatibility with existing ECS management systems|Y|N|Y|
|Consistent user experience on features such as VNC with that on virtual machines|Y|N|Y|
|Out-of-band \(OOB\) network security|Y|N|N/A|

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

## Billing

SCCs support pay-as-you-go and subscription billing methods. For more information, see [Billing method overview](/intl.en-US/Pricing/Billing methods/Billing method overview.md).

