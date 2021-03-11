---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Compute optimized instance families

This topic describes the features of compute optimized instance families of ECS and lists the instance types of each family.

-   Recommended instance families
    -   [c6a, compute optimized instance family](#section_i7i_zsw_bde)
    -   [c6t, security-enhanced compute optimized instance family](#section_c0u_8gn_bry)
    -   [c6e, compute optimized instance family with enhanced performance](#section_wiv_kqq_u7o)
    -   [c6, compute optimized instance family](#section_0yl_3wv_ims)
    -   [c5, compute optimized instance family](#section_1zf_ox2_m08)
    -   [ic5, compute intensive instance family](#section_5hn_iox_k41)
-   Other available instance families

    [sn1ne, compute optimized instance family with enhanced network performance](#section_2mi_djo_dff)


## c6a, compute optimized instance family

Features

-   Uses the SHENLONG architecture to provide predictable and consistent high performance and reduce virtualization overheads.
-   Compute:
    -   Uses 2.6 GHz AMD EPYC TM ROME processors that deliver a maximum turbo frequency of 3.3 GHz for consistent computing performance.
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Allows you to enable or disable hyper-threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports enhanced SSDs \(ESSDs\), standard SSDs, and ultra disks.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Provides an ultra high packet forwarding rate.
    -   Provides high network performance based on large computing capacity.
-   Scenarios:
    -   Video encoding and decoding
    -   Scenarios where large volumes of packets are received and transmitted
    -   Web frontend servers
    -   Frontend servers of massively multiplayer online \(MMO\) games
    -   Test and development, such as DevOps

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|ENIs \(including one primary ENI\)|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|--------------------------------------------|---------------------------------------------|:---------------------------------------------|:-----------|:---------------------------------|---------------|-------------------------|
|ecs.c6a.large|2|4.0|None|1.0|10.0|900|Yes|2|12.5|1.0|
|ecs.c6a.xlarge|4|8.0|None|1.5|10.0|1,000|Yes|3|20|1.5|
|ecs.c6a.2xlarge|8|16.0|None|2.5|10.0|1,600|Yes|4|30|2.0|
|ecs.c6a.4xlarge|16|32.0|None|5.0|10.0|2,000|Yes|8|60|3.0|
|ecs.c6a.8xlarge|32|64.0|None|8.0|10.0|3,000|Yes|7|75|4,0|
|ecs.c6a.16xlarge|64|128.0|None|16.0|None|6,000|Yes|8|150|8.0|
|ecs.c6a.32xlarge|128|256.0|None|32.0|None|12,000|Yes|15|300|16.0|
|ecs.c6a.64xlarge|256|512.0|None|64.0|None|24,000|Yes|15|600|32.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## c6t, security-enhanced compute optimized instance family

Features

-   Implements trusted boot based on the Trusted Platform Module \(TPM\) chip. During a trusted boot, each module in the boot chain from the underlying hardware to the guest OS is measured and verified.
-   Supports comprehensive monitoring on the IaaS layer and provides trusted capabilities of the whole IaaS layer.
-   Supports the Enclave feature and provides a trusted isolation space inside ECS instances to encapsulate security operations of legitimate software in an enclave.
-   Uses the third-generation SHENLONG architecture to provide predictable and consistent high performance and reduce virtualization overheads. c6t improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of SHENLONG chips.
-   Compute:
    -   Uses 2.5 GHz Intel ® Xeon ® Platinum 8269 \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
    -   Offers a CPU-to-memory ratio of 1:2.
    -   Allows you to enable or disable hyper-threading.

        **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Storage:
    -   Is an instance family in which all instances are I/O optimized.
    -   Supports ESSDs only.
    -   Provides high storage I/O performance based on large computing capacity.

        **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Network:
    -   Provides an ultra high packet forwarding rate.
    -   Provides high network performance based on large computing capacity.
-   Scenarios:
    -   Scenarios that require high security and enhanced trust, such as financial services, government affairs, and enterprise services
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and re-transmission of telecommunication information
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|TPM support|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|-----------------------------------|:---------------------------------------------|-----------|:-----------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.c6t.large|2|4.0|None|A burstable bandwidth of up to 10.0|900|Yes|Yes|Up to 250|2|3|6|20|1.0|
|ecs.c6t.xlarge|4|8.0|None|A burstable bandwidth of up to 10.0|1,000|Yes|Yes|Up to 250|4|4|15|40|1.5|
|ecs.c6t.2xlarge|8|16.0|None|A burstable bandwidth of up to 10.0|1,600|Yes|Yes|Up to 250|8|4|15|50|2.0|
|ecs.c6t.4xlarge|16|32.0|None|A burstable bandwidth of up to 10.0|3,000|Yes|Yes|300|8|8|30|80|3.0|
|ecs.c6t.8xlarge|32|64.0|None|10.0|6,000|Yes|Yes|600|16|8|30|150|5.0|
|ecs.c6t.13xlarge|52|96.0|None|16.0|9,000|Yes|Yes|900|32|7|30|240|8.0|
|ecs.c6t.26xlarge|104|192.0|None|32.0|24,000|Yes|Yes|1,800|32|15|30|480|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other metrics of the network.

## c6e, compute optimized instance family with enhanced performance

Features

-   Uses the third-generation SHENLONG architecture to provide predictable and consistent high performance and reduce virtualization overheads. c6e improves storage performance, network performance, and computing stability by an order of magnitude by using fast path acceleration of SHENLONG chips.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs only.
-   Provides high network and storage I/O performance based on large computing capacity.

    **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Provides an ultra-high packet forwarding rate.

    **Note:** The maximum network performance varies with instance families. For higher concurrent connection capabilities, we recommend that you use g5ne.

-   Offers a CPU-to-memory ratio of 1:2.
-   Uses 2.5 GHz Intel ® Xeon ® Platinum 8269 \(Cascade\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
-   Allows you to enable or disable hyper-threading.

    **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and re-transmission of telecommunication information
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|-----------------------------------|:---------------------------------------------|:-----------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.c6e.large|2|4.0|None|A burstable bandwidth of up to 10.0|900|Yes|Up to 250|2|3|6|20|1.0|
|ecs.c6e.xlarge|4|8.0|None|A burstable bandwidth of up to 10.0|1,000|Yes|Up to 250|4|4|15|40|1.5|
|ecs.c6e.2xlarge|8|16.0|None|A burstable bandwidth of up to 10.0|1,600|Yes|Up to 250|8|4|15|50|2.0|
|ecs.c6e.4xlarge|16|32.0|None|A burstable bandwidth of up to 10.0|3,000|Yes|300|8|8|30|80|3.0|
|ecs.c6e.8xlarge|32|64.0|None|10.0|6,000|Yes|600|16|8|30|150|5.0|
|ecs.c6e.13xlarge|52|96.0|None|16.0|9,000|Yes|900|32|7|30|240|8.0|
|ecs.c6e.26xlarge|104|192.0|None|32.0|24,000|Yes|1,800|32|15|30|480|16.0|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).
-   The results for network capabilities are the maximum values obtained from single item tests. For example, when network bandwidth is tested, no stress tests are performed on the packet forwarding rate or other specifications.

## c6, compute optimized instance family

Features

-   Uses the SHENLONG architecture to provide predictable and consistent high performance and reduce virtualization overheads.
-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.

    **Note:** The maximum performance of disks varies with instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

-   Provides high storage I/O performance based on large compute capacity.

    **Note:** For more information about the storage I/O performance of the new generation of enterprise-level instance families, see [Storage I/O performance](/intl.en-US/Block Storage/Performance/Storage I/O performance.md).

-   Allows you to enable or disable hyper-threading.

    **Note:** By default, Hyper-Threading is enabled on ECS instances. For more information, see [Customize CPU options](/intl.en-US/Instance/Manage instances/Customize CPU options.md).

-   Offers a CPU-to-memory ratio of 1:2.
-   Provides an ultra-high packet forwarding rate.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8269CY \(Cascade Lake\) processors that deliver a maximum turbo frequency of 3.2 GHz for consistent computing performance.
-   Provides high network performance based on large computing capacity.
-   Supports instance type changes to g6 or r6.
-   Scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and re-transmission of telecommunication information
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance science and engineering applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Baseline bandwidth \(bidirectional\), Gbit/s|Burstable bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|Connections \(K\)|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|Disk IOPS \(K\)|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:-------------------------------------------|---------------------------------------------|:---------------------------------------------|:-----------|-----------------|:---------|:---------------------------------|----------------------------|---------------|-------------------------|
|ecs.c6.large|2|4.0|None|1.0|3.0|300|Yes|Up to 250|2|2|6|10|1|
|ecs.c6.xlarge|4|8.0|None|1.5|5.0|500|Yes|Up to 250|4|3|10|20|1.5|
|ecs.c6.2xlarge|8|16.0|None|2.5|8.0|800|Yes|Up to 250|8|4|10|25|2|
|ecs.c6.3xlarge|12|24.0|None|4.0|10.0|900|Yes|Up to 250|8|6|10|30|2.5|
|ecs.c6.4xlarge|16|32.0|None|5.0|10.0|1,000|Yes|300|8|8|20|40|3|
|ecs.c6.6xlarge|24|48.0|None|7.5|10.0|1,500|Yes|450|12|8|20|50|4|
|ecs.c6.8xlarge|32|64.0|None|10.0|None|2,000|Yes|600|16|8|20|60|5|
|ecs.c6.13xlarge|52|96.0|None|12.5|None|3,000|Yes|900|32|7|20|100|8|
|ecs.c6.26xlarge|104|192.0|None|25.0|None|6,000|Yes|1,800|32|15|20|200|16|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## c5, compute optimized instance family

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.

    **Note:** The maximum performance of disks varies with instance families. A single instance of this instance family can deliver up to 200,000 IOPS. For higher storage I/O performance, we recommend that you use g6se.

-   Offers a CPU-to-memory ratio of 1:2.
-   Provides an ultra-high packet forwarding rate.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) or 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Provides high network performance based on large computing capacity.
-   Scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and re-transmission of telecommunication information
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.c5.large|2|4.0|None|1.0|300|Yes|2|2|6|
|ecs.c5.xlarge|4|8.0|None|1.5|500|Yes|2|3|10|
|ecs.c5.2xlarge|8|16.0|None|2.5|800|Yes|2|4|10|
|ecs.c5.3xlarge|12|24.0|None|4.0|900|Yes|4|6|10|
|ecs.c5.4xlarge|16|32.0|None|5.0|1,000|Yes|4|8|20|
|ecs.c5.6xlarge|24|48.0|None|7.5|1,500|Yes|6|8|20|
|ecs.c5.8xlarge|32|64.0|None|10.0|2,000|Yes|8|8|20|
|ecs.c5.16xlarge|64|128.0|None|20.0|4,000|Yes|16|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## ic5, compute intensive instance family

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports ESSDs, standard SSDs, and ultra disks.
-   Offers a CPU-to-memory ratio of 1:1.
-   Provides an ultra-high packet forwarding rate.
-   Uses 2.5 GHz Intel® Xeon® Platinum 8163 \(Skylake\) or 8269CY \(Cascade Lake\) processors for consistent computing performance.
-   Provides high network performance based on large computing capacity.
-   Scenarios:
    -   Web frontend servers
    -   Data analysis, batch processing, and video encoding
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and re-transmission of telecommunication information
    -   Frontend servers of MMO games

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.ic5.large|2|2.0|None|1.0|300|No|2|2|6|
|ecs.ic5.xlarge|4|4.0|None|1.5|500|No|2|3|10|
|ecs.ic5.2xlarge|8|8.0|None|2.5|800|No|2|4|10|
|ecs.ic5.3xlarge|12|12.0|None|4.0|900|No|4|6|10|
|ecs.ic5.4xlarge|16|16.0|None|5.0|1,000|No|4|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## sn1ne, compute optimized instance family with enhanced network performance

Features

-   Is an instance family in which all instances are I/O optimized.
-   Supports standard SSDs and ultra disks only.
-   Offers a CPU-to-memory ratio of 1:2.
-   Provides an ultra-high packet forwarding rate.
-   Uses 2.5 GHz Intel® Xeon® E5-2682 v4 \(Broadwell\) or Platinum 8163 \(Skylake\) processors for consistent computing performance.
-   Provides high network performance based on large computing capacity.
-   Scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as on-screen video comments and re-transmission of telecommunication information
    -   Web frontend servers
    -   Frontend servers of MMO games
    -   Data analysis, batch processing, and video encoding
    -   High-performance scientific and engineering applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(bidirectional\), Gbit/s|Packet forwarding rate \(bidirectional\), Kpps|IPv6 support|NIC queues|ENIs \(including one primary ENI\)|Private IP addresses per ENI|
|:------------|:---|:-------------|:--------------------|:----------------------------------|:---------------------------------------------|:-----------|:---------|:---------------------------------|----------------------------|
|ecs.sn1ne.large|2|4.0|None|1.0|300|Yes|2|2|6|
|ecs.sn1ne.xlarge|4|8.0|None|1.5|500|Yes|2|3|10|
|ecs.sn1ne.2xlarge|8|16.0|None|2.0|1,000|Yes|4|4|10|
|ecs.sn1ne.3xlarge|12|24.0|None|2.5|1,300|Yes|4|6|10|
|ecs.sn1ne.4xlarge|16|32.0|None|3.0|1,600|Yes|4|8|20|
|ecs.sn1ne.6xlarge|24|48.0|None|4.5|2,000|Yes|6|8|20|
|ecs.sn1ne.8xlarge|32|64.0|None|6.0|2,500|Yes|8|8|20|

**Note:**

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.mdsection_e9r_xkf_z15).

## References

-   [Instance families](/intl.en-US/Instance/Instance families.md)
-   [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md)

