---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Compute optimized instance families with FPGAs

This topic describes the features of compute optimized instance families with Field Programmable Gate Arrays \(FPGAs\) and lists the instance types of each family.

-   Recommended instance families

    [f3, compute optimized instance family with FPGAs](#section_9xy_ea1_wz9)

-   Other available instance families

    [f1, compute optimized instance family with FPGAs](#section_3f4_xet_8t8)


## f3, compute optimized instance family with FPGAs

Features:

-   I/O optimized.
-   Supports standard SSDs and ultra disks.
-   Uses Xilinx 16nm Virtex UltraScale+ VU9P FPGAs.
-   Offers a CPU-to-memory ratio of 1:4.
-   Equipped with 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) processors.
-   Provides a fast and reliable network based on large computing capacity.
-   Suitable for the following scenarios:
    -   Deep learning and inference
    -   Genomics research
    -   Database acceleration
    -   Image transcoding such as conversion of JPEG images to WebP images
    -   Real-time video processing such as H.265 video compression

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|FPGAs|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:----|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.f3-c4f1.xlarge|4|16.0|None|1 × Xilinx VU9P|1.5|300|No|2|3|10|
|ecs.f3-c8f1.2xlarge|8|32.0|None|1 × Xilinx VU9P|2.5|500|No|4|4|10|
|ecs.f3-c16f1.4xlarge|16|64.0|None|1 × Xilinx VU9P|5.0|1,000|No|4|8|20|
|ecs.f3-c16f1.8xlarge|32|128.0|None|2 × Xilinx VU9P|10.0|2,000|No|8|8|20|
|ecs.f3-c16f1.16xlarge|64|256.0|None|4 × Xilinx VU9P|20.0|2,500|No|16|8|20|
|ecs.f3-c22f1.22xlarge|88|336.0|None|4 × Xilinx VU9P|30.0|4,500|No|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## f1, compute optimized instance family with FPGAs

Features:

-   I/O optimized.
-   Supports standard SSDs and ultra disks.
-   Uses Intel® Arria® 10 GX 1150 FPGAs.
-   Offers a CPU-to-memory ratio of 1:7.5.
-   Equipped with 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) processors.
-   Provides a fast and reliable network based on large computing capacity.
-   Suitable for the following scenarios:
    -   Deep learning and inference
    -   Genomics research
    -   Financial analysis
    -   Image transcoding
    -   Computational workloads such as real-time video processing and security management

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Local storage \(GiB\)|FPGAs|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:----|:-------------|:--------------------|:----|:-------------------|:------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.f1-c8f1.2xlarge|8|60.0|None|Intel Arria 10 GX 1150|3.0|400|Yes|4|4|10|
|ecs.f1-c8f1.4xlarge|16|120.0|None|2 × Intel Arria 10 GX 1150|5.0|1,000|Yes|4|8|20|
|ecs.f1-c28f1.7xlarge|28|112.0|None|Intel Arria 10 GX 1150|5.0|2,000|Yes|8|8|20|
|ecs.f1-c28f1.14xlarge|56|224.0|None|2 × Intel Arria 10 GX 1150|10.0|2,000|Yes|14|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

