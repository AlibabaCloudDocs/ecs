# Retired instance types

This topic describes all retired instance types on the China site \(aliyun.com\). However, instance types sn1, sn2, n1, n2, and e3 are still available for purchase on the International site \(alibabacloud.com\).

## Instance type change

For more information about the configuration changes between instance types, see [Instance families that support instance type changes](/intl.en-US/Instance/Change configurations/Instance families that support instance type changes.md).

## sn2, general purpose instance family

Features

-   Offers a CPU-to-memory ratio of 1:4.
-   Uses 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) or E5-2680 v3 \(Haswell\) processors for consistent computing performance.
-   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Enterprise-level applications of various types and sizes
    -   Small and medium-sized database systems, caches, and search clusters
    -   Data analysis and computing

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|
|-------------|-----|--------------|--------------------|-------------------------------|----------|----|
|ecs.sn2.medium|2|8.0|0.5|100|1|2|
|ecs.sn2.large|4|16.0|0.8|200|1|3|
|ecs.sn2.xlarge|8|32.0|1.5|400|1|4|
|ecs.sn2.3xlarge|16|64.0|3.0|500|2|8|
|ecs.sn2.7xlarge|32|128.0|6.0|800|3|8|
|ecs.sn2.13xlarge|56|224.0|10.0|1,200|4|8|

## sn1, compute optimized instance family

Features

-   Offers a CPU-to-memory ratio of 1:2.
-   Uses 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) or E5-2680 v3 \(Haswell\) processors for consistent computing performance.
-   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Web frontend servers
    -   Frontends of massively multiplayer online \(MMO\) games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|
|-------------|-----|--------------|--------------------|-------------------------------|----------|----|
|ecs.sn1.medium|2|4.0|0.5|100|1|2|
|ecs.sn1.large|4|8.0|0.8|200|1|3|
|ecs.sn1.xlarge|8|16.0|1.5|400|1|4|
|ecs.sn1.3xlarge|16|32.0|3.0|500|2|8|
|ecs.sn1.7xlarge|32|64.0|6.0|800|3|8|

## c4, ce4, and cm4, compute optimized instance families with high clock speeds

Features

-   Uses 3.2 GHz Intel Xeon E5-2667 v4 \(Broadwell\) processors.
-   Provides consistent computing performance.
-   Is an instance family in which all instances are I/O optimized.
-   Supports only standard SSDs and ultra disks.
-   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   High-performance web frontend servers
    -   High-performance scientific and engineering applications
    -   MMO gaming and video encoding

c4

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|
|-------------|-----|--------------|--------------------|-------------------------------|----------|----|
|ecs.c4.xlarge|4|8.0|1.5|200|1|3|
|ecs.c4.2xlarge|8|16.0|3.0|400|1|4|
|ecs.c4.3xlarge|12|24.0|4.5|600|2|6|
|ecs.c4.4xlarge|16|32.0|6.0|800|2|8|

ce4

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|
|-------------|-----|--------------|--------------------|-------------------------------|----------|----|
|ecs.ce4.xlarge|4|32.0|1.5|200|1|3|
|ecs.ce4.2xlarge|8|64.0|3.0|400|1|3|

cm4

|Instance type|vCPUs|Memory \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|
|-------------|-----|--------------|--------------------|-------------------------------|----------|----|
|ecs.cm4.xlarge|4|16.0|1.5|200|1|3|
|ecs.cm4.2xlarge|8|32.0|3.0|400|1|4|
|ecs.cm4.3xlarge|12|48.0|4.5|600|2|6|
|ecs.cm4.4xlarge|16|64.0|6.0|800|2|8|
|ecs.cm4.6xlarge|24|96.0|10.0|1,200|4|8|

## gn4, GPU-accelerated compute optimized instance family

Features

-   Uses NVIDIA M40 GPUs.
-   Compute:
    -   Offers multiple CPU-to-memory ratios.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Deep learning
    -   Scientific computing applications such as fluid dynamics, finance, genomics, and environmental analysis
    -   Server-side GPU compute workloads such as high-performance computing, rendering, and multi-media encoding and decoding

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:---|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.gn4-c4g1.xlarge|4|30.0|NVIDIA M40 × 1|12 GB × 1|3.0|300|1|3|10|
|ecs.gn4-c8g1.2xlarge|8|30.0|NVIDIA M40 × 1|12 GB × 1|3.0|400|1|4|10|
|ecs.gn4.8xlarge|32|48.0|NVIDIA M40 × 1|12 GB × 1|6.0|800|3|8|20|
|ecs.gn4-c4g1.2xlarge|8|60.0|NVIDIA M40 × 2|12 GB × 2|5.0|500|1|4|10|
|ecs.gn4-c8g1.4xlarge|16|60.0|NVIDIA M40 × 2|12 GB × 2|5.0|500|1|8|20|
|ecs.gn4.14xlarge|56|96.0|NVIDIA M40 × 2|12GB × 2|10.0|1,200|4|8|20|

## ga1, GPU-accelerated compute optimized instance family

Features

-   Uses AMD S7150 GPUs.
-   Supports high-performance local NVMe SSDs.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.5.
    -   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports only standard SSDs and ultra disks.
-   Network:
    -   Provides high network performance based on large computing capacity.
-   Suits the following scenarios:
    -   Rendering and multimedia encoding and decoding
    -   Machine learning, high-performance computing, and high-performance databases
    -   Server-side workloads that require powerful concurrent floating-point computing capacity

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|GPUs|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:---|:---------|:-------------------|:------------------------------|:---------|:---|----------------------------|
|ecs.ga1.xlarge|4|10.0|1 × 87|AMD S7150 × 1/4|8 GB × 1/4|1.0|200|1|3|10|
|ecs.ga1.2xlarge|8|20.0|1 × 175|AMD S7150 × 1/2|8 GB × 1/2|1.5|300|1|4|10|
|ecs.ga1.4xlarge|16|40.0|1 × 350|AMD S7150 × 1|8 GB × 1|3.0|500|2|8|20|
|ecs.ga1.8xlarge|32|80.0|1 × 700|AMD S7150 × 2|8 GB × 2|6.0|800|3|8|20|
|ecs.ga1.14xlarge|56|160.0|1 × 1400|AMD S7150 × 4|8 GB × 4|10.0|1,200|4|8|20|

## sccgn6ne, GPU-accelerated compute optimized SCC instance family

Features

-   Provides all features of ECS Bare Metal Instance.
-   Compute:
    -   Uses NVIDIA V100 GPUs \(SXM2-based\) that feature:
        -   Innovative Volta architecture
        -   32 GB HBM2 GPU memory
        -   CUDA Cores 5120
        -   Tensor Cores 640
        -   GPU memory bandwidth of up to 900 Gbit/s
        -   Support for up to six NVLink connections and total bandwidth of 300 Gbit/s \(25 Gbit/s per connection\)
    -   Offers a CPU-to-memory ratio of 1:4.
    -   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs, standard SSDs, and ultra disks.
    -   Supports high performance CPFSs.
-   Network:
    -   Supports IPv6.
    -   Supports VPCs.
    -   Supports RoCE v2 networks, which are dedicated to low-latency RDMA communication.
-   Suits the following scenarios:
    -   Ultra-large-scale training for machine learning on a distributed GPU cluster
    -   Large-scale high performance scientific computing and simulations
    -   Large-scale data analysis, batch processing, and video encoding

Instance types

|Instance type|vCPUs|Memory \(GiB\)|GPUs|GPU memory|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|RoCE \(Gbit/s\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|:-------------|:---|----------|:-------------------|:------------------------------|---------------|:---------|:---|----------------------------|
|ecs.sccgn6ne.24xlarge|96|768.0|NVIDIA V100 × 8|32 GB× 8|32.0|4,800|100|16|8|20|

## n1, n2, and e3, shared instance families

Features

-   Uses 2.5 GHz Intel Xeon E5-2680 v3 \(Haswell\) processors.
-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks.
-   Provides high network performance based on large computing capacity.

|Instance family|Description|CPU-to-memory ratio|Scenario|
|---------------|-----------|-------------------|--------|
|n1|Shared compute optimized instance family|1:2|-   Small and medium-sized web servers
-   Batch processing
-   Distributed analysis.
-   Advertisement services |
|n2|Shared general purpose instance family|1:4|-   Medium-sized web servers
-   Batch processing
-   Distributed analysis.
-   Advertisement services
-   Hadoop clusters |
|e3|Shared memory optimized instance family|1:8|-   Cache/Redis
-   Search applications
-   Memory databases
-   Databases with high I/O requirements, such as Oracle and MongoDB
-   Hadoop clusters
-   Large-volume data processing |

n1

|Instance type|vCPUs|Memory \(GiB\)|ENIs|
|-------------|-----|--------------|----|
|ecs.n1.tiny|1|1.0|1|
|ecs.n1.small|1|2.0|1|
|ecs.n1.medium|2|4.0|1|
|ecs.n1.large|4|8.0|2|
|ecs.n1.xlarge|8|16.0|2|
|ecs.n1.3xlarge|16|32.0|2|
|ecs.n1.7xlarge|32|64.0|2|

n2

|Instance type|vCPUs|Memory \(GiB\)|ENIs|
|-------------|-----|--------------|----|
|ecs.n2.small|1|4.0|1|
|ecs.n2.medium|2|8.0|1|
|ecs.n2.large|4|16.0|2|
|ecs.n2.xlarge|8|32.0|2|
|ecs.n2.3xlarge|16|64.0|2|
|ecs.n2.7xlarge|32|128.0|2|

e3

|Instance type|vCPUs|Memory \(GiB\)|ENIs|
|-------------|-----|--------------|----|
|ecs.e3.small|1|8.0|1|
|ecs.e3.medium|2|16.0|1|
|ecs.e3.large|4|32.0|2|
|ecs.e3.xlarge|8|64.0|2|
|ecs.e3.3xlarge|16|128.0|2|

## Generation I instance families

Generation I instance families include t1, s1, s2, s3, m1, m2, c1, and c2. All these instance families are legacy shared instance families. They are categorized based on the number of cores such as 1, 2, 4, 8, or 16 cores.

Features

-   Uses Intel Xeon E5-2420 processors with clock speeds of no less than 1.9 GHz.
-   Uses the latest DDR3 memory.
-   Is an instance family in which instances can be I/O optimized or non-I/O optimized.

I/O optimized instances support standard SSDs and ultra disks. The following table describes the instance types and their specifications.

|Category|Instance type|vCPUs|Memory \(GiB\)|
|--------|-------------|-----|--------------|
|Standard|ecs.s2.large|2|4|
|ecs.s2.xlarge|2|8|
|ecs.s2.2xlarge|2|16|
|ecs.s3.medium|4|4|
|ecs.s3.large|4|8|
|High Memory|ecs.m1.medium|4|16|
|ecs.m2.medium|4|32|
|ecs.m1.xlarge|8|32|
|High CPU|ecs.c1.small|8|8|
|ecs.c1.large|8|16|
|ecs.c2.medium|16|16|
|ecs.c2.large|16|32|
|ecs.c2.xlarge|16|64|

Non-I/O optimized instances support only basic disks. The following table describes the instance types and their specifications.

|Category|Instance type|vCPUs|Memory \(GiB\)|
|--------|-------------|-----|--------------|
|Tiny|ecs.t1.small|1|1|
|Standard|ecs.s1.small|1|2|
|ecs.s1.medium|1|4|
|ecs.s1.large|1|8|
|ecs.s2.small|2|2|
|ecs.s2.large|2|4|
|ecs.s2.xlarge|2|8|
|ecs.s2.2xlarge|2|16|
|ecs.s3.medium|4|4|
|ecs.s3.large|4|8|
|High Memory|ecs.m1.medium|4|16|
|ecs.m2.medium|4|32|
|ecs.m1.xlarge|8|32|
|High CPU|ecs.c1.small|8|8|
|ecs.c1.large|8|16|
|ecs.c2.medium|16|16|
|ecs.c2.large|16|32|
|ecs.c2.xlarge|16|64|

## Description of instance specifications

|Specification|Description|
|-------------|-----------|
|local storage|Local storage, also called cache disks or local disks, refers to the disks attached to the physical servers where ECS instances are hosted. Local storage provides temporary block storage for instances. Local storage capacity is measured in GiB. Data stored on local disks may be lost when the computing resources of an instance are released or when an instance is failed over to a normal physical server. Computing resources include vCPUs and memory. For more information, see [Local disks](/intl.en-US/Block Storage/Block Storage overview/Local disks.md).|
|bandwidth|The maximum sum of inbound and outbound bandwidth values. **Note:** Each instance specification is verified and obtained in a test environment. In actual scenarios, the performance of an instance may vary based on other factors such as the instance load and networking model. We recommend that you perform business stress tests on instances to choose appropriate instance types. |
|packet forwarding rate|The maximum sum of inbound and outbound packet forwarding rates. For information about how to test the packet forwarding rate, see [Test network performance](https://www.alibabacloud.com/help/faq-detail/55757.htm). **Note:** Each instance specification is verified and obtained in a test environment. In actual scenarios, the performance of an instance may vary based on other factors such as the instance load, image version, and networking model. We recommend that you perform business stress tests on instances to choose appropriate instance types. |
|connections|Connections, also called sessions, are the process of establishing connections and transferring data between a client and a server. A connection is uniquely defined by the network communication quintuple that consists of a source IP address, a destination IP address, a source port, a destination port, and a protocol. Connections of an ECS instance include TCP, UDP, and ICMP connections.|
|NIC queues|The maximum number of NIC queues supported by the primary NIC of an instance. If your instance type is not a member of an ECS Bare Metal Instance family, the maximum number of NIC queues supported by a secondary NIC is the same as that supported by the primary NIC.|

