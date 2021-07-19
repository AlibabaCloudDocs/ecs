---
keyword: [Alibaba Cloud Linux, Windows Server, CentOS, Ubuntu, Debian, CoreOS, Red Hat, OpenSUSE]
---

# Overview

Public images provided by Alibaba Cloud are fully licensed to provide a secure and stable operating environment for applications on Elastic Compute Service \(ECS\) instances. This topic describes types of public images such as Alibaba Cloud Linux images, third-party images, and open source images.

## Types of public images

The following table describes two types of public images provided by Alibaba Cloud. Windows Server and Red Hat Enterprise Linux images are not free to use. However, you can use other free public images to create ECS instances. For more information, see [Image prices](/intl.en-US/Images/Image overview.md).

|Type|Description|Technical support|
|:---|:----------|:----------------|
|Alibaba Cloud Linux images|Alibaba Cloud Linux images are custom, proprietary operating systems provided by Alibaba Cloud to create ECS instances. Alibaba Cloud Linux images are fully tested to ensure their security, stability, and normal startup and operation.|Alibaba Cloud provides technical support for problems that occur when you use Alibaba Cloud Linux images.|
|Third-party images and open source images|Third-party and open source images are fully tested and released by Alibaba Cloud to ensure their security, stability, and normal startup and operation. The following third-party public images are available: -   Windows: Windows Server
-   Linux:Anolis OS, Ubuntu, CentOS, Red Hat Enterprise Linux, Debian, OpenSUSE, SUSE Linux, FreeBSD, Fedora CoreOS, Fedora, and CoreOS

|We recommend that you contact the corresponding operating system vendors or open source communities for technical support. Alibaba Cloud also provides information about image-related and system-related problems.|

## Alibaba Cloud Linux images

Alibaba Cloud Linux is a Linux public image developed by Alibaba Cloud. The following table describes the versions of Alibaba Cloud Linux images.

|Operating system|Version|Description|
|:---------------|:------|:----------|
|Alibaba Cloud Linux 3|-   Alibaba Cloud Linux 3.2104 64-bit
-   Alibaba Cloud Linux 3.2104 64-bit \(UEFI\)

|The operating system supports various Alibaba Cloud instance types including ECS Bare Metal Instance types. By default, Alibaba Cloud Linux 3 is also equipped with [Alibaba Cloud CLI]() and other software packages.

If you want to replace other Linux distributions with Alibaba Cloud Linux 3, you can select Public Image and select Alibaba Cloud Linux 3 when you create an ECS instance or when you replace the system disk of an ECS instance.

For more information, see [Overview](/intl.en-US/Images/Alibaba Cloud Linux 3/Overview.md) and [Release notes](/intl.en-US/Images/Alibaba Cloud Linux 3/Release notes.md). |
|Alibaba Cloud Linux 2|-   Alibaba Cloud Linux 2.1903 LTS 64-bit
-   Alibaba Cloud Linux 2.1903 64-bit \(Quick Start\)
-   Alibaba Cloud Linux 2.1903 64-bit \(Trusted\)
-   Alibaba Cloud Linux 2.1903 64-bit \(UEFI\)

|The operating system supports various Alibaba Cloud instance types including ECS Bare Metal Instance types. By default, Alibaba Cloud Linux 2 is also equipped with [Alibaba Cloud CLI]() and other software packages.

If you want to replace other Linux distributions with Alibaba Cloud Linux 2, you can select Public Image and select Alibaba Cloud Linux 2 when you create an ECS instance or when you replace the system disk of an ECS instance.

For more information, see [Overview](/intl.en-US/Images/Alibaba Cloud Linux 2/Overview.md) and [Release notes](/intl.en-US/Images/Alibaba Cloud Linux 2/Release notes.md). |

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

    **Note:** On January 14, 2020, Microsoft stopped providing support for Windows Server 2008 and Windows Server 2008 R2 operating systems. In light of this, Alibaba Cloud no longer provides technical support for ECS instances that use these operating systems. If you have ECS instances that use these operating systems, upgrade them to Windows Server 2012 or later at your earliest opportunity.

-   Linux images

    |Operating system|Version|
    |:---------------|:------|
    |Anolis OS|    -   Anolis OS 8.2 RHCK 64-bit |
    |CentOS|    -   CentOS 8.3 64-bit
    -   CentOS 8.2 64-bit
    -   CentOS 8.1 64-bit
    -   CentOS 8.0 64-bit
    -   CentOS 7.9 64-bit
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
    -   CoreOS 1745.7.0 64-bit
**Note:** Based on the end-of-life announcement from the Fedora CoreOS community, updates are no longer provided for CoreOS Container Linux as of May 26, 2020. In light of this, Alibaba Cloud has issued the following announcements:

    -   As of May 26, 2020, Alibaba Cloud no longer provides technical support for ECS instances that use the CoreOS Container Linux operating system. However, you can still use existing ECS instances that run this operating system.
    -   You can still obtain CoreOS Container Linux images from Alibaba Cloud before September 30, 2020. After September 30, 2020, you will be unable to use CoreOS Container Linux public images provided by Alibaba Cloud to create ECS instances.
    -   As of May 26, 2020, CoreOS Container Linux can continue to be used on instances on which it is already installed. However, no security patches are available because the operating system has reached its end of life. For security concerns, we recommend that you no longer use CoreOS Container Linux images.
    -   The Fedora CoreOS community recommends that you use Fedora CoreOS in place of CoreOS Container Linux. Alibaba Cloud will bring Fedora CoreOS public images online soon. |
    |Debian|    -   Debian 10.9 64-bit
    -   Debian 10.7 64-bit
    -   Debian 10.7 64-bit \(AMD-compatible\)
    -   Debian 10.6 64-bit
    -   Debian 10.5 64-bit
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
    |FreeBSD|    -   FreeBSD 12.1 64-bit
    -   FreeBSD 11.4 64-bit
    -   FreeBSD 11.3 64-bit
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
**Note:** Before you use a Red Hat image, you must check whether the Red Hat image is supported by the instance family that you select. For more information, see [Which instance families do Red Hat Enterprise Linux \(RHEL\) images support?](/intl.en-US/Images/FAQ/Image FAQ.md). |
    |SUSE Linux|    -   SUSE Linux Enterprise Server 15 SP2 64-bit
    -   SUSE Linux Enterprise Server 15 SP1 64-bit
    -   SUSE Linux Enterprise Server 12 SP5 64-bit
    -   SUSE Linux Enterprise Server 12 SP4 64-bit
    -   SUSE Linux Enterprise Server 12 SP2 64-bit
    -   SUSE Linux Enterprise Server 11 SP4 64-bit |
    |Ubuntu|    -   Ubuntu 20.04 64-bit
    -   Ubuntu: 20.04 64-bit \(AMD-compatible\)
    -   Ubuntu 18.04 64-bit
    -   Ubuntu: 18.04 64-bit \(AMD-compatible\)
    -   Ubuntu 16.04 64-bit
    -   Ubuntu 16.04 32-bit
    -   Ubuntu 14.04 64-bit
    -   Ubuntu 14.04 32-bit
**Note:** If you are using a 32-bit operating system, you must select an instance type that has a memory of less than or equal to 4 GiB. For more information, see [Select an image](/intl.en-US/Images/Select an image.md). |
    |Fedora CoreOS|    -   Fedora CoreOS 33.20210217.3.0\_3
When you use this image, take note of the following items:    -   When you create an instance or replace the system disk for an instance, you can use only a key pair as your logon credential. You can use only the key pair that you initially configured for your instance to log on to the instance. You cannot change or unbind the key pair.
    -   When you have created an instance or replaced the system disk for an instance, you cannot change the password for the instance. |
    |Fedora|    -   Fedora 33 64-bit |


