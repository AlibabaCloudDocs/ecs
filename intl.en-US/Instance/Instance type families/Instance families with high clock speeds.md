---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Instance families with high clock speeds

This topic describes the features of instance families with high clock speeds and lists the instance types of each instance family.

-   Recommended instance families
    -   [hfc7, compute optimized instance family with high clock speeds](#section_hdo_beh_gsf)
    -   [hfc6, compute optimized instance family with high clock speeds](#section_stc_a50_sco)
    -   [hfg7, general purpose instance family with high clock speeds](#section_ms1_d4s_fmi)
    -   [hfg6, general purpose instance family with high clock speeds](#section_xgq_3wb_9ak)
    -   [hfr7, memory optimized instance family with high clock speeds](#section_nzd_6dq_556)
    -   [hfr6, memory optimized instance family with high clock speeds](#section_205_hfc_ekc)
-   Other available instance families
    -   [hfc5, compute optimized instance family with high clock speeds](#section_kkg_4hf_rkf)
    -   [hfg5, general purpose instance family with high clock speeds](#section_rjm_jmo_yll)

## hfc7, compute optimized instance family with high clock speeds

Features

-   Offloads a large number of virtualization features to dedicated hardware with the use of the third-generation SHENLONG architecture to provide predictable and consistent ultra-high performance and reduce virtualization overheads.
-   Compute:
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Uses Intel® Xeon® Cooper Lake processors that deliver an all-core turbo frequency of 3.8 GHz and have a minimum clock speed of 3.3 GHz for consistent computing performance.
    -   Allows you to enable or disable Hyper-Threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

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

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

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

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

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

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

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

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

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

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

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

