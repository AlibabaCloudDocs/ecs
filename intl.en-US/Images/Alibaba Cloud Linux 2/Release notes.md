---
keyword: [release notes, ECS, Alibaba Cloud Linux]
---

# Release notes

This topic describes the updates to Alibaba Cloud Linux 2 images. The release notes are ordered by release date, from the latest to the earliest.

## Background information

-   Unless otherwise stated, the released updates apply to all Alibaba Cloud regions where Elastic Compute Service \(ECS\) is available.
-   Alibaba Cloud Linux 2 images are applicable to most instance families. For more information about the instance families that do not support Alibaba Cloud Linux 2 images and can use only specified public images, see the [Release notes of images that are applicable only to some instance families](#section_zai_t2o_j01) section in this topic.

## Release notes

|Image ID|Release date|Description|
|--------|------------|-----------|
|aliyun\_2\_1903\_x64\_20G\_alibase\_20210325.vhd|2021-03-25|-   The `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image is updated to the latest software version to be compatible with CentOS 7.9. Common vulnerabilities and exposures \(CVEs\) are fixed.
-   The CVE-2021-3156 sudo vulnerability in Linux is fixed. For more information, see [Vulnerability announcement \| Linux sudo permission vulnerability \(CVE-2021-3156\)](/intl.en-US/Announcements & Updates/Security announcement/Vulnerability announcement | Linux sudo permission vulnerability (CVE-2021-3156).md).
-   The default network configuration service is switched to network-scripts.
-   The net.ipv4.tcp\_max\_tw\_buckets value is increased.
-   The NVMe driver is added to initramfs.
-   The kdump service is enabled by default.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-23.al7 version.
    -   Kernel bugs and key security vulnerabilities are fixed.
    -   Intel SGX is supported.
    -   The network diagnosis tool Ping Trace is supported.
    -   Cgroups can be created in a lightweight manner in scenarios in which multiple instances are deployed on a single server. This can effectively reduce the amount of time required to create cgroups.
    -   Intel IceLake MCA is supported. |
|aliyun\_2\_1903\_x64\_20G\_qboot\_alibase\_20210325.vhd|2021-03-25|-   The `Alibaba Cloud Linux 2.1903 64-bit (Quick Start)` image is updated.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20210325.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image.
-   Applicable regions: China \(Hangzhou\), China \(Beijing\), China \(Zhangjiakou\), China \(Shenzhen\), China \(Hong Kong\), Singapore \(Singapore\), Malaysia \(Kuala Lumpur\), and US \(Virginia\). |
|aliyun\_2\_1903\_x64\_20G\_qboot\_alibase\_20210218.vhd|2021-02-18|-   The `Alibaba Cloud Linux 2.1903 64-bit (Quick Start)` image is updated.
-   The default network configuration service is switched to network-scripts.
-   The CVE-2021-3156 sudo vulnerability in Linux is fixed. For more information, see [Vulnerability announcement \| Linux sudo permission vulnerability \(CVE-2021-3156\)](/intl.en-US/Announcements & Updates/Security announcement/Vulnerability announcement | Linux sudo permission vulnerability (CVE-2021-3156).md).
-   Applicable regions: China \(Hangzhou\), China \(Shenzhen\), China \(Beijing\), China \(Zhangjiakou\), China \(Hong Kong\), Singapore \(Singapore\), Malaysia \(Kuala Lumpur\), and US \(Virginia\). |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20210120.vhd|2021-01-20|-   The `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image is updated to the latest software version to be compatible with CentOS 7.9. CVEs are fixed.
-   The update-motd service is released and enabled by default.
-   The rhel-loadmodules service is enabled by default.
-   The vring\_force\_dma\_api startup parameter is added.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-22.2.al7 version.
    -   Kernel bugs and key security vulnerabilities are fixed.
    -   The kernel file system is synchronized with the latest ext4 file system from the Linux community to gain enhanced stability.
    -   Redundant Array of Independent Disks \(RAID\) is supported by default.
    -   The Dragonfly Enclaves feature is supported.
    -   The performance debugging of Intel IceLake PMU Topdown is supported.
    -   The read capability of io\_uring buffer is optimized.
    -   blk-throttle is optimized.
    -   The Chinese cryptographic algorithm SM2 and the standard X509-formatted certificate that uses the SM2-with-SM3 Chinese cryptographic algorithm are supported.
    -   blk-mq batch requests are supported.
    -   The PCIe Error recover feature is supported.
    -   Swap is optimized to significantly improve the memory overselling stability.
    -   The container enhancement technology is supported. |
|aliyun\_2\_1903\_x64\_20G\_qboot\_alibase\_20210120.vhd|2021-01-20|-   The `Alibaba Cloud Linux 2.1903 64-bit (Quick Start)` image is updated.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20210120.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image.
-   Applicable regions: China \(Hangzhou\), China \(Shenzhen\), China \(Beijing\), China \(Zhangjiakou\), China \(Hong Kong\), Singapore \(Singapore\), Malaysia \(Kuala Lumpur\), and US \(Virginia\). |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd|2020-09-04|-   The `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image is updated to the latest software version to be compatible with CentOS 7.8. CVEs are fixed.
-   Information in /etc/redhat-release is changed from Aliyun Linux release 7.2 LTS \(Hunting Beagle\) to Alibaba Cloud Linux \(Aliyun Linux\) release 2.1903 LTS \(Hunting Beagle\).
-   The image type information in /etc/image-id is optimized.
-   The tuned service is enabled by default.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-21.al7 version.
    -   Kernel bugs and security vulnerabilities are fixed.
    -   The io\_uring bug is fixed and new features are added.
    -   Transparent Huge Pages \(THP\) fork optimization is added to accelerate the creation of memory intensive processes.
    -   Secure operations on Apache Pass \(AEP\) devices are supported.
    -   The TCP-RT feature developed by Alibaba Cloud is supported.
    -   The virtio-mem feature is supported.
    -   The PCIe Gen4 feature, RAS feature, and power management of Intel® IceLake processors are enhanced.
    -   The Intel® Speed Select Technology is supported. |
|aliyun\_2\_1903\_x64\_20G\_qboot\_alibase\_20200904.vhd|2020-09-04|-   The `Alibaba Cloud Linux 2.1903 64-bit (Quick Start)` image is updated.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image.
-   Applicable regions: China \(Hangzhou\), China \(Shenzhen\), China \(Zhangjiakou\), and China \(Hong Kong\). |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200529.vhd|2020-05-29|-   The `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image is updated to the latest software version to be compatible with CentOS 7.8. CVEs are fixed.
-   The /etc/image-id file that contains image information such as the image type is added.
-   The tuned service is disabled by default.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-19.1.al7 version.
    -   The kernel interface support provided by the Alibaba Cloud kernel on the statistics of scheduling and memory QoS metrics is open sourced to perform fine-grained monitoring of Service Level Indicators \(SLIs\) related to scheduling and memory.
    -   The kernel interface support provided by the Alibaba Cloud kernel on priority control when a memcg is out of memory \(OOM\) is open sourced to improve protection on important processes during system OOM.
    -   AMD QoS is supported.
    -   The virtio pmem driver is supported.
    -   The free page reporting feature is supported to enhance the awareness of hypervisors about idle memory of a guest OS and manage and utilize physical memory resources in an efficient manner.
    -   Memory compaction is optimized to alleviate memory fragmentation and improve the utilization of system memory.
    -   Kernel bugs and security vulnerabilities are fixed. |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200324.vhd|2020-03-24|-   The `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image is updated to the latest software version to be compatible with CentOS 7.8. CVEs are fixed.
-   The latest fixes for CVEs can be obtained by using YUM.
-   The LTS version of Alibaba Cloud Linux 2 is released and /etc/alinux-release is updated to Aliyun Linux release 2.1903 LTS \(Hunting Beagle\).
-   The tuned service is enabled by default.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-18.al7 version.
    -   NVMe devices are supported.
    -   The THP feature is enabled by default to improve application performance.
    -   io\_uring is added.
    -   Intel\_idle and guest halt polling are enabled to improve the guest CPU performance.
    -   ftrace syscalls is enabled to enhance the performance of the bpftrace tool.
    -   Multiple Alibaba Cloud optimizations and bug fixes to the kernel including subsystems such as schedulers, memory, file systems, and block layers are open sourced.
    -   Kernel security vulnerabilities are fixed. |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200221.vhd|2020-02-21|-   The `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image is updated to the latest software version to be compatible with CentOS 7.8. CVEs are fixed.
-   IPv6 is enabled by default.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.81-17.1.al7 version.
    -   Intel Cooper Lake processors and Ice Lake processors are supported.
    -   The support for the AMD and ARM 64-bit CPU architectures is enhanced.
    -   Persistent memory is supported.
    -   The blk-iocost feature is supported. This feature is based on the cost model and the weight-based throttling feature of blkio cgroup controllers. For more information, see [Configure the weight-based throttling feature of blk-iocost](/intl.en-US/Images/Alibaba Cloud Linux 2/Features and interfaces supported by Alibaba Cloud Linux 2/Configure the weight-based throttling feature of blk-iocost.md).
    -   The Pressure Stall Information \(PSI\) feature implemented based on cgroup v1 interfaces is supported. For more information, see [Enable the PSI feature for cgroup v1](/intl.en-US/Images/Alibaba Cloud Linux 2/Features and interfaces supported by Alibaba Cloud Linux 2/Enable the PSI feature for cgroup v1.md).
    -   Multiple Alibaba Cloud optimizations and bug fixes to the kernel including subsystems such as schedulers, memory, file systems, and block layers are open sourced.
    -   Kernel security vulnerabilities are fixed. |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200114.qboot.vhd|2020-01-14|-   The `Alibaba Cloud Linux 2.1903 64-bit (Quick Start)` image is released.
-   Kernel updates:
    -   The kernel is updated to the 4.19.81-17.al7.x86\_64 version.
    -   Quick boot with qboot is supported.
-   Applicable regions: China \(Beijing\), China \(Hangzhou\), and China \(Hong Kong\). |
|aliyun\_2\_1903\_64\_20G\_alibase\_20190829.vhd|2019-08-29|-   The `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image is updated to the latest software version.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.57-15.1.al7.x86\_64 version.
    -   The Spectre-V1 SWAPGS vulnerability is fixed.
    -   Issues with DM bio splitting code are fixed.
    -   The default TCP congestion control algorithm is set to CUBIC.
    -   The network is configured to 10-eth0.network. |
|aliyun\_2\_1903\_64\_20G\_alibase\_20190619.vhd|2019-06-19|-   The `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image is updated to the latest software version.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.43-13.2.al7.x86\_64 version.
    -   The cgroup writeback feature implemented based on cgroup v1 interfaces is supported.
    -   Policy-based routing is supported.
    -   The INET\_DIAG kernel configuration item is enabled to support the ss command from the iproute2 suite.
    -   The configurable net.ipv4.tcp\_tw\_timeout kernel interface is supported.
    -   The following network-related CVEs are fixed:
        -   CVE-2019-11477
        -   CVE-2019-11478
        -   CVE-2019-11479 |
|aliyun-2.1903-x64-20G-alibase-20190507.vhd|2019-05-07|-   The `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image is updated to the latest software version.
-   The issue of time synchronization latency on instance startup is fixed.
-   The kernel is updated to the kernel-4.19.34-11.al7.x86\_64 version, and other issues are fixed. |
|aliyun-2.1903-x64-20G-alibase-20190327.vhd|2019-03-27|-   The `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image is released.
-   The kernel-4.19.24-9.al7.x86\_64 kernel version is used in the base image. |

## Release notes of images that are applicable only to some instance families

|Image ID|Release date|Applicable instance family|Description|
|--------|------------|--------------------------|-----------|
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20210325.vhd|2021-03-25|Trusted instance families:-   ecs.g6t
-   ecs.c6t

|-   The `Alibaba Cloud Linux 2.1903 64-bit (Trusted)` image is updated.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20210325.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image.
-   Boot mode is changed to the Unified Extensible Firmware Interface \(UEFI\) mode. This is the only supported mode.
-   The kernel is updated to the kernel-kernel-kernel-4.19.91-23.al7 version. |
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20210218.vhd|2021-02-18|Trusted instance families:-   ecs.g6t
-   ecs.c6t

|-   The `Alibaba Cloud Linux 2.1903 64-bit (Trusted)` image is updated.
-   The default network configuration service is switched to network-scripts.
-   The CVE-2021-3156 sudo vulnerability in Linux is fixed. For more information, see [Vulnerability announcement \| Linux sudo permission vulnerability \(CVE-2021-3156\)](/intl.en-US/Announcements & Updates/Security announcement/Vulnerability announcement | Linux sudo permission vulnerability (CVE-2021-3156).md).
-   Boot mode is changed to the UEFI mode. This is the only supported mode.
-   The kernel is updated to the kernel-4.19.91-22.2.al7 version. |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20210218.vhd|2021-02-18|Instance families with AMD processors:-   ecs.ebmg6a
-   ecs.ebmc6a
-   ecs.ebmr6a
-   ecs.ebmg6a-htoff
-   ecs.ebmc6a-htoff
-   ecs.ebmr6a-htoff

|-   The `Alibaba Cloud Linux 2.1903 64-bit (AMD-compatible)` image is updated to the latest software version.
-   The default network configuration service is switched to network-scripts.
-   The CVE-2021-3156 sudo vulnerability in Linux is fixed. For more information, see [Vulnerability announcement \| Linux sudo permission vulnerability \(CVE-2021-3156\)](/intl.en-US/Announcements & Updates/Security announcement/Vulnerability announcement | Linux sudo permission vulnerability (CVE-2021-3156).md).
-   Boot mode is changed to the UEFI mode. This is the only supported mode. |
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20210120.vhd|2021-01-20|Trusted instance families:-   ecs.g6t
-   ecs.c6t

|-   The `Alibaba Cloud Linux 2.1903 64-bit (Trusted)` image is updated.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20210120.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image.
-   Boot mode is changed to the UEFI mode. This is the only supported mode.
-   The kernel is updated to the kernel-4.19.91-22.2.al7 version. |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20210120.vhd|2021-01-20|Instance families with AMD processors:-   ecs.ebmg6a
-   ecs.ebmc6a
-   ecs.ebmr6a
-   ecs.ebmg6a-htoff
-   ecs.ebmc6a-htoff
-   ecs.ebmr6a-htoff

|-   The `Alibaba Cloud Linux 2.1903 64-bit (AMD-compatible)` image is updated to the latest software version.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20210120.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image.
-   Boot mode is changed to the UEFI mode. This is the only supported mode. |
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20200904.vhd|2020-09-04|Trusted instance families:-   ecs.g6t
-   ecs.c6t

|-   The `Alibaba Cloud Linux 2.1903 64-bit (Trusted)` image is updated to the latest software version.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image.
-   Boot mode is changed to the UEFI mode. This is the only supported mode.
-   Trusted features are added. |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20200904.vhd|2020-09-04|Instance families with AMD processors:-   ecs.ebmg6a
-   ecs.ebmc6a
-   ecs.ebmr6a
-   ecs.ebmg6a-htoff
-   ecs.ebmc6a-htoff
-   ecs.ebmr6a-htoff

|-   The `Alibaba Cloud Linux 2.1903 64-bit (AMD-compatible)` image is updated to the latest software version.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image.
-   Boot mode is changed to the UEFI mode. This is the only supported mode. |
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20200622.vhd|2020-06-22|Trusted instance families:-   ecs.g6t
-   ecs.c6t

|-   The `Alibaba Cloud Linux 2.1903 64-bit (Trusted)` image is released.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20200529.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image.
-   Boot mode is changed to the UEFI mode. This is the only supported mode.
-   Trusted features are added.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-19.2.al7 version.
    -   AMD IOMMU is supported. |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20200616.vhd|2020-06-16|Instance families with AMD processors:-   ecs.ebmg6a
-   ecs.ebmc6a
-   ecs.ebmr6a
-   ecs.ebmg6a-htoff
-   ecs.ebmc6a-htoff
-   ecs.ebmr6a-htoff

|-   The `Alibaba Cloud Linux 2.1903 64-bit (AMD-compatible)` image is released.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20200529.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` base image.
-   Boot mode is changed to the UEFI mode. This is the only supported mode.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-19.2.al7 version.
    -   AMD IOMMU is supported. |

