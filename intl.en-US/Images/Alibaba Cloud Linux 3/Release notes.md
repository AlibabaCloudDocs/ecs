# Release notes

This topic describes the updates to Alibaba Cloud Linux 3 images. The release notes are ordered by release date, from the latest to the earliest.

## Background information

-   Unless otherwise stated, the released updates apply to all Alibaba Cloud regions where Elastic Compute Service \(ECS\) is available.
-   Some Alibaba Cloud Linux 3 images are applicable to most instance families, whereas other Alibaba Cloud Linux 3 images are applicable only to some instance families. For more information, see [Release notes of images that are applicable only to some instance families](#section_gb2_fnv_vbn).

## Release notes

|Image ID|Release date|Description|
|--------|------------|-----------|
|aliyun\_3\_x64\_20G\_alibase\_20210425.vhd|2021-04-25|-   The `Alibaba Cloud Linux 3.2104 64-bit` base image is updated.
-   Kernel updates: The kernel is updated to the 5.10.23-5.al8.x86\_64 version. |
|aliyun\_3\_x64\_20G\_alibase\_20210415.vhd|2021-04-16|-   The `Alibaba Cloud Linux 3.2104 64-bit` base image is released.
-   Kernel description:
    -   The kernel is based on the 5.10 kernel version supported in the Linux community. The 5.10.23-4.al8.x86\_64 kernel version is used in the base image.
    -   The ARM 64-bit architecture supports the PV-Panic, PV-Unhalt, and PV-Preempt features.
    -   The ARM 64-bit architecture supports Kernel Live Patching \(KLP\).
    -   TCP-layer service monitoring \(TCP-RT\) is supported.
    -   The memcg backend asynchronous reclaim feature is supported.
    -   The memcg quality of service \(QoS\) and Pressure Stall Information \(PSI\) features implemented based on cgroup v1 interfaces are supported.
    -   The cgroup writeback feature is supported.
    -   The monitoring of block I/O throttling is enhanced.
    -   An interface is provided to optimize JBD2 of ext4.
    -   The open source kernel of Alibaba Cloud is optimized and vulnerabilities in multiple subsystems including the scheduler, memory, file system, and block layer are fixed.
-   Image description:
    -   The base image is compatible with the CentOS 8 and RHEL 8 software ecosystems. Common vulnerabilities and exposures \(CVEs\) are fixed.
    -   GCC 10.2.1 and glibc 2.32 are supported.
    -   Python 3.6 and Python 2.7 are supported.
    -   AppStream is supported.
-   Applicable regions: China \(Hangzhou\). |

## Release notes of images that are applicable only to some instance families

|Image ID|Release date|Applicable instance family|Description|
|--------|------------|--------------------------|-----------|
|aliyun\_3\_x64\_20G\_uefi\_alibase\_20210425.vhd|2021-04-25|-   ecs.c7
-   ecs.g7
-   ecs.r7
-   ecs.c7t
-   ecs.g7t
-   ecs.r7t

|-   The `Alibaba Cloud Linux 3.2104 64-bit (UEFI)` image is released.
-   This image is derived from the aliyun\_3\_x64\_20G\_alibase\_20210425.vhd version of the `Alibaba Cloud Linux 3.2104 64-bit` base image.
-   Boot mode is changed to the Unified Extensible Firmware Interface \(UEFI\) mode. This is the only supported mode.
-   Applicable regions: China \(Beijing\), China \(Hangzhou\), China \(Shanghai\), and China \(Shenzhen\). |

