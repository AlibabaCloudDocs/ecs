---
keyword: [Alibaba Cloud Linux, Windows Server, CentOS, Ubuntu, Debian, CoreOS, Red Hat, OpenSUSE]
---

# Overview

This topic provides an overview of public images provided by Alibaba Cloud, including Alibaba Cloud Linux images, third-party images, and open source images. The public images are fully licensed to provide a secure and stable operating environment for applications on ECS instances.

## Types of public images

The following table describes two types of public images provided by Alibaba Cloud. Windows Server and Red Hat Enterprise Linux images cannot be used free of charge. However, you can use other free public images to create ECS instances. For more information, see [Image prices](/intl.en-US/Images/Image overview.md).

|Type|Description|Technical support|
|:---|:----------|:----------------|
|Alibaba Cloud Linux images|Alibaba Cloud Linux images are custom, proprietary operating systems provided by Alibaba Cloud to create ECS instances. Alibaba Cloud Linux images are fully tested to ensure their security, stability, and normal startup and operation.|Alibaba Cloud provides technical support for problems that occur when you use Alibaba Cloud Linux images.|
|Third-party images and open source images|Third-party and open source images are fully tested and released by Alibaba Cloud to ensure their security, stability, and normal startup and operation. The following third-party public images are available: -   Windows: Windows Server
-   Linux: Ubuntu, CentOS, Red Hat Enterprise Linux, Debian, OpenSUSE, SUSE Linux, FreeBSD, and CoreOS

|We recommend that you contact the corresponding operating system vendors or open source communities for technical support. Alibaba Cloud also provides information about image- and system-related problems.|

## Alibaba Cloud Linux images

Alibaba Cloud Linux is a Linux public image developed by Alibaba Cloud. The following table describes the versions of Alibaba Cloud Linux images.

|Operating system|Version|Description|
|:---------------|:------|:----------|
|Alibaba Cloud Linux 2|-   Alibaba Cloud Linux 2.1903 LTS 64-bit
-   Alibaba Cloud Linux 2.1903 64-bit \(Quick Start\)
-   Alibaba Cloud Linux 2.1903 64-bit \(Trusted\)
-   Alibaba Cloud Linux 2.1903 LTS 64-bit \(AMD-compatible\)

|A next-generation operating system that supports various Alibaba Cloud instance types including ECS Bare Metal Instance types. By default, Alibaba Cloud Linux 2 is also equipped with [Alibaba Cloud CLI]() and other software packages.

If you want to replace other Linux distributions with Alibaba Cloud Linux 2, you can select Public Image and then Alibaba Cloud Linux 2 when you create an ECS instance or when you replace the system disk of an ECS instance.

For more information, see [Overview](/intl.en-US/Images/Alibaba Cloud Linux 2/Overview.md) and [Release notes of Alibaba Cloud Linux 2](/intl.en-US/Images/Alibaba Cloud Linux 2/Release notes of Alibaba Cloud Linux 2.md). |

## Third-party images and open source images

Alibaba Cloud releases and updates public images of third-party and open source image vendors on a regular basis. For more information, see [Release notes](/intl.en-US/Images/Public image/Release notes.md). In the ECS console, you can select a region and view all the public images available in that region on the [Public Images](https://ecs.console.aliyun.com/#image/region/cn-hangzhou/systemImageList) tab. For more information, see [Find an image](/intl.en-US/Images/Find an image.md).

The following tables describe the versions of third-party and open source public images for Windows and Linux provided by Alibaba Cloud.

-   Windows images

    |Operating system|Version|
    |:---------------|:------|
    |Windows Server 2019|    -   Windows Server 2019 with Container Datacenter Edition 64-bit \(Chinese\)
    -   Windows Server 2019 with Container Datacenter Edition 64-bit \(English\)
    -   Windows Server 2019 Datacenter Edition 64-bit \(Chinese\)
    -   Windows Server 2019 Datacenter Edition 64-bit \(English\) |
    |Windows Server 2016|    -   Windows Server 2016 Datacenter Edition 64-bit \(Chinese\)
    -   Windows Server 2016 Datacenter Edition 64-bit \(English\) |
    |Windows Server 2012|    -   Windows Server 2012 R2 Datacenter Edition 64-bit \(Chinese\)
    -   Windows Server 2012 R2 Datacenter Edition 64-bit \(English\) |
    |Windows Server Version \*\*\*\* \(Semi-Annual Channel\)|    -   Windows Server Version \*\*\*\* Datacenter Edition 64-bit \(Chinese\)
    -   Windows Server Version \*\*\*\* Datacenter Edition 64-bit \(English\)
The asterisks \(\*\*\*\*\) indicate the latest version number of the Semi-Annual Channel release. |

    **Note:** On January 14, 2020, Microsoft stopped providing support for Windows Server 2008 and Windows Server 2008 R2 operating systems. Therefore, Alibaba Cloud no longer provides technical support for ECS instances that use the preceding operating systems. If you have ECS instances that use the preceding operating systems, upgrade them to Windows Server 2012 or later in a timely manner.

-   Linux images

    |Operating system|Version|
    |:---------------|:------|
    |CentOS|    -   CentOS 8.2 64-bit
    -   CentOS 8.1 64-bit
    -   CentOS 8.0 64-bit
    -   CentOS 7.8 64-bit \(Trusted\)
    -   CentOS 7.8 64-bit
    -   CentOS 7.7 64-bit
    -   CentOS 7.6 64-bit
    -   CentOS 7.5 64-bit
    -   CentOS 7.4 64-bit
    -   CentOS 7.3 64-bit
    -   CentOS 7.2 64-bit
    -   CentOS 6.10 64-bit
    -   CentOS 6.9 64-bit
    -   CentOS 6.8 32-bit
**Note:** If you are using a 32-bit operating system, you must select an instance type that has a memory of less than or equal to 4 GiB. For more information, see [Select an image](/intl.en-US/Images/Select an image.md). |
    |CoreOS|    -   CoreOS 2345.3.0 64-bit
    -   CoreOS 2303.4.0 64-bit
    -   CoreOS 2303.3.0 64-bit
    -   CoreOS 2247.6.0 64-bit
    -   CoreOS 2023.4.0 64-bit
    -   CoreOS 1745.7.0 64-bit |
    |Debian|    -   Debian 10.5 64-bit
    -   Debian 10.4 64-bit
    -   Debian 10.3 64-bit
    -   Debian 10.2 64-bit
    -   Debian 9.13 64-bit
    -   Debian 9.12 64-bit
    -   Debian 9.11 64-bit
    -   Debian 9.9 64-bit
    -   Debian 9.8 64-bit
    -   Debian 9.6 64-bit
    -   Debian 8.11 64-bit
    -   Debian 8.9 64-bit |
    |FreeBSD|    -   FreeBSD 11.3 64-bit
    -   FreeBSD 11.2 64-bit |
    |OpenSUSE|    -   OpenSUSE 15.2 64-bit
    -   OpenSUSE 15.1 64-bit
    -   OpenSUSE 42.3 64-bit |
    |Red Hat|    -   Red Hat Enterprise Linux 8.2 64-bit
    -   Red Hat Enterprise Linux 8.1 64-bit
    -   Red Hat Enterprise Linux 8.0 64-bit
    -   Red Hat Enterprise Linux 7.8 64-bit
    -   Red Hat Enterprise Linux 7.7 64-bit
    -   Red Hat Enterprise Linux 7.6 64-bit
    -   Red Hat Enterprise Linux 7.5 64-bit
    -   Red Hat Enterprise Linux 7.4 64-bit
    -   Red Hat Enterprise Linux 6.10 64-bit
    -   Red Hat Enterprise Linux 6.9 64-bit
**Note:** Before you use a Red Hat image, you must check whether the Red Hat image is supported by the instance family. For more information, see [Which instance families do Red Hat Enterprise Linux \(RHEL\) images support?](/intl.en-US/Images/Image FAQ.md). |
    |SUSE Linux|    -   SUSE Linux Enterprise Server 15 SP2 64-bit
    -   SUSE Linux Enterprise Server 15 SP1 64-bit
    -   SUSE Linux Enterprise Server 12 SP5 64-bit
    -   SUSE Linux Enterprise Server 12 SP4 64-bit
    -   SUSE Linux Enterprise Server 12 SP2 64-bit
    -   SUSE Linux Enterprise Server 11 SP4 64-bit |
    |Ubuntu|    -   Ubuntu 20.04 64-bit
    -   Ubuntu: 18.04 64-bit \(AMD-compatible\)
    -   Ubuntu 18.04 64-bit
    -   Ubuntu 16.04 64-bit
    -   Ubuntu 16.04 32-bit
    -   Ubuntu 14.04 64-bit
    -   Ubuntu 14.04 32-bit
**Note:** If you are using a 32-bit operating system, you must select an instance type that has a memory of less than or equal to 4 GiB. For more information, see [Select an image](/intl.en-US/Images/Select an image.md). |


