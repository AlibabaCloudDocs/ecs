---
keyword: [ECS, Alibaba Cloud Linux, Alibaba Cloud Linux 3, Linux, image, operating system]
---

# Overview

Alibaba Cloud Linux 3 is the third release of the Linux operating system provided by Alibaba Cloud. In addition to all of the features inherited from Alibaba Cloud Linux 2, Alibaba Cloud Linux 3 offers a better cloud operating system experience and provides improved security, stability, and runtime performance. You can create Elastic Compute Service \(ECS\) instances from Alibaba Cloud Linux 3 images. Alibaba Cloud Linux 3 images are free to use, and Alibaba Cloud provides long-term technical support \(LTS\) for them.

## Scenarios

Alibaba Cloud Linux 3 is suitable for the following scenarios:

-   Various workloads in cloud environments, such as databases, cloud native containers, data analytics, web applications, and other workloads in the production environment.
-   Various instance families, including ECS Bare Metal Instance families. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).
    -   Alibaba Cloud Linux 3 supports instance types that have up to 768 vCPUs.
    -   Alibaba Cloud Linux 3 supports instance types that have 0.5 GiB to 12,288 GiB of memory.
    -   Alibaba Cloud Linux 3 does not support non-I/O optimized instances.

## Benefits

Alibaba Cloud Linux 3 inherits all of the benefits of Alibaba Cloud Linux 2. Compared with other Linux distributions, Alibaba Cloud Linux 3 has the following advantages:

-   Alibaba Cloud provides free software maintenance and technical support for Alibaba Cloud Linux 3 until April 30, 2029.
-   Alibaba Cloud Linux 3 uses Linux Kernel 5.10 LTS as the kernel to provide the latest enhanced operating system features from the Linux community to power cloud-based application environments.
-   Alibaba Cloud Linux 3 uses GCC 10.2, binutils 2.35, and glibc 2.32 to enhance stability and improve compatibility with other software.
-   Alibaba Cloud Linux 3 is compatible with the CentOS 8 and RHEL 8 software ecosystems.
-   Alibaba Cloud Linux 3 is optimized for integration with the Alibaba Cloud infrastructure and provides faster system startup and higher runtime performance.
-   Alibaba Cloud Linux 3 provides feature adaptation, performance tuning, and stability hardening for Intel, AMD, and ARM processors to ensure that the operating system can keep running in a stable and reliable manner.

## Images

|Image|ID of the latest version|Description|
|-----|------------------------|-----------|
|Alibaba Cloud Linux 3.2104 64-bit|aliyun\_3\_x64\_20G\_alibase\_20210425.vhd|The default standard image version of Alibaba Cloud Linux 3.|

## Billing

Alibaba Cloud Linux 3 images are provided for free. However, you must pay for other resources such as vCPUs, memory, storage, public bandwidth, and snapshots. For more information, see [Billing overview](/intl.en-US/Pricing/Billing overview.md).

## Obtain Alibaba Cloud Linux 3 images

You can use the following methods to obtain and use Alibaba Cloud Linux 3 images:

-   When you create an ECS instance, select **Public Image**, and then select Alibaba Cloud Linux 3 and its version. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).
-   Change the operating system of an existing ECS instance to Alibaba Cloud Linux 3 by replacing the system disk. For more information, see [Replace the system disk \(public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace the system disk (public images).md).

## Update history

For more information about the release notes of Alibaba Cloud Linux 3 images, see [Release notes](/intl.en-US/Images/Alibaba Cloud Linux 3/Release notes.md).

## Technical support

Alibaba Cloud provides the following technical support for Alibaba Cloud Linux 3:

-   Eight years of LTS is provided in the form of security updates and vulnerability fixes until the release lifecycle ends on April 30, 2029. You can use one of the following methods to obtain free LTS:
    -   [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)
    -   [GitHub](https://alibaba.github.io/cloud-kernel/os.html?spm=5176.cnalinux.0.0.1f8323d1WpS5ZY&aly_as=32Di8ZOj)
-   Images are updated every four months. Updates cover new features, security updates, and vulnerability fixes.
-   Security updates are provided from YUM repositories. You can run the yum update command to update an image to the latest version.

