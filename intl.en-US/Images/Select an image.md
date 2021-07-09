---
keyword: [select an image, select an operating system, 32-bit, 64-bit, Windows Server 2016, Windows Server 2019, Windows Server 2008, Windows Server 2012, Windows Server 2003, differences between CentOS and Red Hat, differences between Ubuntu and Debian, Alibaba Cloud Linux]
---

# Select an image

This topic describes how to select an appropriate image from multiple image types and operating systems to suit your business needs. You must select an image when you create an Elastic Compute Service \(ECS\) instance.

When you select an image, you must consider the following factors:

-   [Region](#section_okd_bqv_hhb)
-   [Image type](#section_9op_qir_5qk)
-   [Image fee](#section_rc2_iv0_l8f)
-   [Operating system](#section_x1t_f35_hhb)
-   [Built-in software](#section_0r4_eja_g94) \(such as MySQL and other applications\)

## Region

An image is tied to its region and can be used to create instances only within the same region. For example, if you want to create an instance in the China \(Beijing\) region, you can use images only in the China \(Beijing\) region. For more information about regions, see [Regions and zones]().

If you want to use an image that belongs to a different region, you must first copy the image to your current region. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).

## Image type

ECS images are classified into public images, custom images, shared images, community images,and Alibaba Cloud Marketplace images based on image sources. For more information, see [Image types](/intl.en-US/Images/Image overview.md).

## Image fee

You may be charged for images that you use. For more information, see [Image prices](/intl.en-US/Images/Image overview.md).

## Operating system

When you select an operating system, you must consider the following factors:

-   Operating system architecture: 32-bit or 64-bit

    |System architecture|Applicable memory|Limit|
    |:------------------|:----------------|:----|
    |32-bit|Up to 4 GiB memory|    -   If the memory of an instance type is larger than 4 GiB, you cannot use a 32-bit operating system.
    -   A 32-bit Windows operating system supports up to four CPU cores. |
    |64-bit|Up to 4 GiB memory|If you want to use a memory of at least 4 GiB for your applications, use a 64-bit operating system.|

-   Operating system type such as Windows, Linux, or Unix-like

    |Operating system type|Logon type|Feature|Scenario|
    |:--------------------|:---------|:------|:-------|
    |Windows|Remote Desktop Connection|A Windows public image is installed with a genuine activated system.|    -   Applicable to Windows-based programs such as .NET programs.
    -   Supports SQL Server and other databases \(manual installation required\). |
    |Linux and Unix-like|SSH|    -   A common, stable, and secure server-side operating system.
    -   An open source operating system that provides fast deployment and easy source code compilation.
|    -   Typically used for server applications, such as high-performance web servers, and supports common programming languages such as PHP and Python.
    -   Supports MySQL and other databases \(manual installation required\). |

    Alibaba Cloud provides a list of public images that run the Windows, Linux, or Unix-like operating systems. For more information, see [Overview](/intl.en-US/Images/Public image/Overview.md).

-   Considerations for Windows

    We recommend that you use a recent version of Windows. More recent versions of Windows have fewer vulnerabilities than earlier versions. IIS 7.5 provides more features and a more convenient console than IIS 6.

    Read the following considerations and select the suitable hardware configuration and Windows version:

    -   Instance types that have only one vCPU and 1 GiB memory do not support MySQL databases.
    -   Windows instances must have at least 2 GiB memory to build websites and deploy web environments.
    -   To ensure service availability, we recommend that you select an instance type that has at least 2 GiB memory when you use Windows 2012.
    -   You must select an instance type that has at least 2 GiB memory if you want to use Windows 2016 or Windows 2019. If your selected instance type has memory of less than 2 GiB, Windows 2016 or Windows 2019 may not be displayed in the public image list on the buy page.
    -   Alibaba Cloud no longer provides technical support for Windows Server 2003 system images. For more information, see [Offline announcement of Windows Server 2003 system images](https://www.alibabacloud.com/help/faq-detail/59513.htm).
-   Considerations for Linux and Unix-like operating systems

    Alibaba Cloud Linux and Unix-like public images contain the following distributions:

    -   Alibaba Cloud Linux

        Alibaba Cloud Linux is an operating system that provides a safe, stable, and high-performance runtime environment for applications on ECS instances. Alibaba Cloud Linux 2 supports various cloud scenarios and instance types \(excluding instances of the classic network type and non-I/O optimized instances\). For more information, see [Overview](/intl.en-US/Images/Alibaba Cloud Linux 2/Overview.md).

    -   Red Hat series

        -   CentOS
        -   Red Hat
        The following table compares CentOS with Red Hat.

        |Operating system|Software package format|Package manager|Billing|Feature|Relationship|
        |:---------------|-----------------------|---------------|:------|:------|:-----------|
        |CentOS|.rpm|yum|Free of charge|        -   Has stable but less frequent patch updates than Red Hat.
        -   Supports online and timely updates.
|        -   CentOS is a free version derived from the source code of Red Hat.
        -   They can use the same RPM package.
        -   They can use the same commands. |
        |Red Hat|Paid usage|Stable with enterprise-level technical support.|

    -   Debian series

        -   Debian
        -   Ubuntu
        The following table compares Debian with Ubuntu.

        |Operating system|Software package format|Package manager|Feature|Relationship|
        |:---------------|-----------------------|---------------|:------|:-----------|
        |Debian|.deb|aptitude|Stable.|Ubuntu is built on the Debian architecture and infrastructure. Ubuntu is the enhanced version of Debian.|
        |Ubuntu|apt-get|        -   User-friendly system configuration.
        -   Timely software updates.
        -   Easy to use and learn. |

    -   SUSE series

        -   SUSE Linux
        -   openSUSE
        The following table compares openSUSE with SUSE Linux.

        |Operating system|Feature|Relationship|
        |----------------|-------|------------|
        |openSUSE|        -   openSUSE is the community edition of SUSE Linux. SUSE Linux Enterprise is the enterprise edition of SUSE Linux.
        -   SUSE Linux Enterprise is more mature and stable, but its official distribution contains fewer software features than openSUSE.
        -   openSUSE provides advanced software versions, better extensibility \(desktop and server installation available\), and free updates \(official technical support available\).
        -   SUSE Linux Enterprise is more suitable for work and production environments, whereas openSUSE is more suitable for personal entertainment and other professional purposes.
|        -   As of version 10.2, SUSE Linux is officially renamed openSUSE.
        -   openSUSE uses the same kernel as SUSE Linux. |
        |SUSE Linux|

    -   CoreOS

        CoreOS is an open source lightweight operating system based on the Linux kernel and designed to provide infrastructure for clustered deployments. CoreOS features automation, ease of application deployment, security, reliability, and scalability. CoreOS provides the underlying functionalities required to deploy applications inside software containers in conjunction with a set of built-in tools for service discovery and configuration sharing.

    -   FreeBSD

        FreeBSD is a Unix-like operating system for a variety of platforms that focuses on features, speed, and stability. FreeBSD provides advanced networking, performance, security, and compatibility features that are still missing in other operating systems, even some of the best commercial ones. For more information, see [FreeBSD Documentation](https://www.freebsd.org/about.html).


## Built-in software

Alibaba Cloud Marketplace images are typically pre-installed with a runtime environment or software applications. You can purchase appropriate images to create ECS instances based on your actual needs. For more information, see [Alibaba Cloud Marketplace images](/intl.en-US/Images/Alibaba Cloud Marketplace images.md).

## What to do next

-   Use an image to create an ECS instance. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).
-   Use an image to change the operating system of an instance. For more information, see [Change the operating system](/intl.en-US/Images/Change the operating system.md).

