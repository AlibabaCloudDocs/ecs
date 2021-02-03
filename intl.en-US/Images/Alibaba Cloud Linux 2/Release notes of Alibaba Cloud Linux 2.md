---
keyword: [release notes, ECS, Alibaba Cloud Linux]
---

# Release notes of Alibaba Cloud Linux 2

This topic describes the feature updates of Alibaba Cloud Linux 2 images in the order in which they were released.

## Background information

-   Unless otherwise stated, the released updates apply to all Alibaba Cloud regions where ECS is provided.
-   Alibaba Cloud Linux 2 images are applicable to most instance families. For information about instance families that do not support Alibaba Cloud Linux 2 images and can use only specified public images, see the [Release notes of images that are applicable to only some instance families](#section_zai_t2o_j01) section in this topic.

## Release notes

|Image ID|Release time|Description|
|--------|------------|-----------|
|aliyun\_2\_1903\_x64\_20G\_dengbao\_alibase\_20201231.vhd|2021-01-11|-   This is an updated `Alibaba Cloud Linux 2.1903 LTS 64-bit image that meets the MLPS 2.0 level 3 standards`.
-   The security of the image is hardened based on *GB/T 22239-2019 Information Security Technology - Baseline for Classified Protection of Cybersecurity*. You can use this image to meet the following security compliance requirements without making additional configurations:

    -   Identity authentication
    -   Access control
    -   Security audit
    -   Intrusion prevention
    -   Malicious code prevention
For more information, see [t1961807.md\#]().

-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20201231.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image.
-   Kernel version: kernel-4.19.91-22.al7.
-   Applicable regions: China \(Hangzhou\), China \(Beijing\), China \(Zhangjiakou\), China \(Chengdu\), and China \(Hong Kong\). |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20201231.vhd|2020-12-31|-   This image updates the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image to the latest software version to be compatible with CentOS 7.9. Common vulnerabilities and exposures \(CVEs\) are fixed.
-   The new update-motd service is released and enabled by default.
-   The rhel-loadmodules service is enabled by default.
-   The vring\_force\_dma\_api startup parameter is added.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-22.al7 version.
    -   Kernel bugs and key security vulnerabilities are fixed.
    -   The kernel file system is synchronized with the latest ext4 file system from the Linux community to gain enhanced stability.
    -   RAID support is enabled by default.
    -   The support for the Dragonfly Enclaves feature is added.
    -   The performance debugging support for Intel IceLake PMU Topdown is added.
    -   The read capability of IO\_Uring Buffer is optimized.
    -   blk-throttle is optimized.
    -   The Chinese cryptographic algorithm SM2 and the standard X509-formatted certificate that uses SM2-with-SM3 Chinese cryptographic algorithm are supported.
    -   The support for blk-mq batch request is added.
    -   The support for the PCIe Error recover feature is added.
    -   Swap is optimized to significantly improve the memory overselling stability.
    -   The enhanced technical support for Alibaba Cloud Linux containers is added. |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd|2020-09-04|-   This image updates the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image to the latest software version to be compatible with CentOS 7.8. CVEs are fixed.
-   /etc/redhat-release is changed from Aliyun Linux release 7.2 LTS \(Hunting Beagle\) to Alibaba Cloud Linux \(Aliyun Linux\) release 2.1903 LTS \(Hunting Beagle\).
-   The types of the /etc/image-id image identity are optimized.
-   The tuned service is disabled by default.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-21.al7 version.
    -   Kernel bugs and security vulnerabilities are fixed.
    -   The io\_uring bug is fixed and new features are added.
    -   Transparent Huge Pages \(THP\) fork optimization is added to accelerate the creation of memory intensive processes.
    -   The support for secure operations on Apache Pass \(AEP\) devices is added.
    -   The TCP-RT feature developed by Alibaba Cloud is supported.
    -   The virtio-mem feature is supported.
    -   The PCIe Gen4 feature, RAS feature, and power management of Intel ® IceLake processors are enhanced.
    -   The Intel ® Speed Select Technology is supported. |
|aliyun\_2\_1903\_x64\_20G\_qboot\_alibase\_20200904.vhd|2020-09-04|-   This is an updated `Alibaba Cloud Linux 2.1903 64-bit (Quick Start)` image.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image.
-   Applicable regions: China \(Hangzhou\), China \(Shenzhen\), China \(Zhangjiakou\), and China \(Hong Kong\). |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200529.vhd|2020-05-29|-   This image updates the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image to the latest software version to be compatible with CentOS 7.8. CVEs are fixed.
-   The /etc/image-id image identity is released.
-   The tuned service is disabled by default.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-19.1.al7 version.
    -   The kernel interface support provided by the Alibaba Cloud kernel on the statistics of scheduling and memory QoS metrics is open sourced to perform fine-grained monitoring of Service Level Indicators \(SLIs\) related to scheduling and memory.
    -   The kernel interface support provided by the Alibaba Cloud kernel on priority control when a memcg is out of memory \(OOM\) is open sourced to improve protection on important processes during system OOM.
    -   AMD QoS is supported.
    -   The virtio pmem driver is supported.
    -   The free page reporting feature is supported to enhance the awareness of hypervisors about idle memory of a guest OS and efficiently manage and utilize physical memory resources.
    -   Memory compaction is optimized to alleviate memory fragmentation and improve the utilization of system memory.
    -   Kernel bugs and security vulnerabilities are fixed. |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200324.vhd|2020-03-24|-   This image updates the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image to the latest software version to be compatible with CentOS 7.8. CVEs are fixed.
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
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200221.vhd|2020-02-21|-   This image updates the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image to the latest software version to be compatible with CentOS 7.8. CVEs are fixed.
-   IPv6 is enabled by default.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.81-17.1.al7 version.
    -   Intel Cooper Lake processors and Ice Lake processors are supported.
    -   The support for the AMD and ARM 64-bit CPU architectures is enhanced.
    -   Persistent memory is supported.
    -   The blk-iocost feature is provided. It is based on the cost model and the weight-based throttling function of blkio cgroup controllers. For more information, see [Configure the weight-based throttling feature of blk-iocost](/intl.en-US/Images/Alibaba Cloud Linux 2/Features and interfaces supported by Alibaba Cloud Linux 2/Configure the weight-based throttling feature of blk-iocost.md).
    -   The Pressure Stall Information \(PSI\) feature that is implemented based on cgroup v1 interfaces is supported. For more information, see [Enable the PSI feature for cgroup v1](/intl.en-US/Images/Alibaba Cloud Linux 2/Features and interfaces supported by Alibaba Cloud Linux 2/Enable the PSI feature for cgroup v1.md).
    -   Multiple Alibaba Cloud optimizations and bug fixes to the kernel including subsystems such as schedulers, memory, file systems, and block layers are open sourced.
    -   Kernel security vulnerabilities are fixed. |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200114.qboot.vhd|2020-01-14|-   The new `Alibaba Cloud Linux 2.1903 64-bit (Quick Start)` image is released.
-   Kernel updates:
    -   The kernel is updated to the 4.19.81-17.al7.x86\_64 version.
    -   Quick boot with qboot is supported.
-   Applicable regions: China \(Beijing\), China \(Hangzhou\), and China \(Hong Kong\). |
|aliyun\_2\_1903\_64\_20G\_alibase\_20190829.vhd|2019-08-29|-   This image updates the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image to the latest software version.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.57-15.1.al7.x86\_64 version.
    -   The Spectre-V1 SWAPGS vulnerability is fixed.
    -   Issues with DM bio splitting code are fixed.
    -   The default TCP congestion control algorithm is set to CUBIC.
    -   The network is configured to 10-eth0.network. |
|aliyun\_2\_1903\_64\_20G\_alibase\_20190619.vhd|2019-06-19|-   This image updates the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image to the latest software version.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.43-13.2.al7.x86\_64 version.
    -   The cgroup writeback feature that is implemented based on cgroup v1 interfaces is supported.
    -   Policy-based routing is supported.
    -   The INET\_DIAG kernel configuration item is enabled to support the ss command from the iproute2 suite.
    -   The configurable net.ipv4.tcp\_tw\_timeout kernel interface is supported.
    -   The following network-related CVEs are fixed:
        -   CVE-2019-11477
        -   CVE-2019-11478
        -   CVE-2019-11479 |
|aliyun-2.1903-x64-20G-alibase-20190507.vhd|2019-05-07|-   This image updates the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image to the latest software version.
-   The time synchronization delay that was presented on instance startup is fixed.
-   The kernel is updated to the kernel-4.19.34-11.al7.x86\_64 version and other issues are fixed. |
|aliyun-2.1903-x64-20G-alibase-20190327.vhd|2019-03-27|-   `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image is released.
-   The kernel-4.19.24-9.al7.x86\_64 kernel version is used in the basic image. |

## Release notes of images that are applicable to only some instance families

|Image ID|Release time|Applicable instance family|Description|
|--------|------------|--------------------------|-----------|
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20201231.vhd|2021-01-11|Trusted instance families:-   ecs.g6t
-   ecs.c6t

|-   This is an updated `Alibaba Cloud Linux 2.1903 64-bit (Trusted)` image.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20201231.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image.
-   Boot mode is changed to the Unified Extensible Firmware Interface \(UEFI\) mode. This is the only supported mode.
-   The kernel is updated to the kernel-4.19.91-22.al7 version.
-   Applicable regions: China \(Hangzhou\), China \(Beijing\), China \(Zhangjiakou\), China \(Chengdu\), and China \(Hong Kong\). |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20201231.vhd|2021-01-11|Instance families whose instances are equipped with AMD processors:-   ecs.ebmg6a
-   ecs.ebmc6a
-   ecs.ebmr6a
-   ecs.ebmg6a-htoff
-   ecs.ebmc6a-htoff
-   ecs.ebmr6a-htoff

|-   This image updates the `Alibaba Cloud Linux 2.1903 LTS 64-bit (AMD-compatible)` image to the latest software version.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20201231.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image.
-   Boot mode is changed to the UEFI mode. This is the only supported mode.
-   Applicable regions: China \(Hangzhou\), China \(Beijing\), China \(Zhangjiakou\), China \(Chengdu\), and China \(Hong Kong\). |
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20200904.vhd|2020-09-04|Trusted instance families:-   ecs.g6t
-   ecs.c6t

|-   This image updates the `Alibaba Cloud Linux 2.1903 LTS 64-bit (Trusted)` image to the latest software version.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image.
-   Boot mode is changed to the UEFI mode. This is the only supported mode.
-   Trusted features are added. |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20200904.vhd|2020-09-04|Instance families whose instances are equipped with AMD processors:-   ecs.ebmg6a
-   ecs.ebmc6a
-   ecs.ebmr6a
-   ecs.ebmg6a-htoff
-   ecs.ebmc6a-htoff
-   ecs.ebmr6a-htoff

|-   This image updates the `Alibaba Cloud Linux 2.1903 LTS 64-bit (AMD-compatible)` image to the latest software version.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image.
-   Boot mode is changed to the UEFI mode. This is the only supported mode. |
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20200622.vhd|2020-06-22|Trusted instance families:-   ecs.g6t
-   ecs.c6t

|-   The new `Alibaba Cloud Linux 2.1903 64-bit (Trusted)` image is released.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20200529.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image.
-   Boot mode is changed to the UEFI mode. This is the only supported mode.
-   Trusted features are added.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-19.2.al7 version.
    -   AMD IOMMU is supported. |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20200616.vhd|2020-06-16|Instance families whose instances are equipped with AMD processors:-   ecs.ebmg6a
-   ecs.ebmc6a
-   ecs.ebmr6a
-   ecs.ebmg6a-htoff
-   ecs.ebmc6a-htoff
-   ecs.ebmr6a-htoff

|-   The new `Alibaba Cloud Linux 2.1903 LTS 64-bit (AMD-compatible)` image is released.
-   This image is derived from the aliyun\_2\_1903\_x64\_20G\_alibase\_20200529.vhd version of the `Alibaba Cloud Linux 2.1903 LTS 64-bit` basic image.
-   Boot mode is changed to the UEFI mode. This is the only supported mode.
-   Kernel updates:
    -   The kernel is updated to the kernel-4.19.91-19.2.al7 version.
    -   AMD IOMMU is supported. |

