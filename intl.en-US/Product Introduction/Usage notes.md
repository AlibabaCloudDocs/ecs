# Usage notes

To ensure the proper operation of your ECS instances, take note of the following items before you start to use the instances.

## Operation notes

-   After you create an ECS instance, only you have the administrator permissions on this instance.
-   You are not allowed to resell or sublicense any bandwidth assigned to your ECS instances without authorization. Failure to comply may cause your instances to be stopped, locked, and released.
-   Do not use your ECS instances for malicious, fraudulent, or unlawful activities, such as click farming or fraudulent transactions, on e-commerce websites such as Taobao. Failure to comply will result in suspension or termination of your account.
-   Do not uninstall relevant hardware drivers.
-   Do not modify the MAC addresses of ENIs unless necessary.
-   Do not enable SELinux.
-   ECS instances with 4 GiB or higher memory must use 64-bit operating systems. A 32-bit operating system can address a maximum of 4 GiB of memory. Alibaba Cloud allows you to create instances that have the following 64-bit operating systems. The operating system versions on the instance buy page prevail.
    -   Alibaba Cloud Linux 64-bit
    -   CoreOS 64-bit
    -   CentOS 64-bit
    -   Debian 64-bit
    -   FreeBSD 64-bit
    -   openSUSE 64-bit
    -   SUSE Linux 64-bit
    -   Ubuntu 64-bit
    -   Red Hat 64-bit
    -   Windows 64-bit
-   To ensure service continuity and avoid failover-induced service unavailability, we recommend that you enable automatic startup upon instance boot for relevant software. If service applications are connected to databases, we recommend that you enable auto-reconnection for these service applications.
-   We recommend that you do not upgrade the kernel or operating system. To upgrade the kernel, see [How to avoid Linux instance startup failure after kernel upgrade](https://www.alibabacloud.com/help/faq-detail/59360.htm).

## Notes on Windows instances

-   Do not stop the built-in AliyunService or shutdownmon.exe process. Otherwise, ECS instances may not be stopped or restarted.
-   Do not modify the hostname of the domain controller.
-   We recommend that you do not create custom images by using a virtual machine that acts as a domain controller.
-   Do not rename, delete, or disable the administrator account. Otherwise, the use of the server may be affected.
-   We recommend that you do not use the virtual memory if basic disks are used. For ultra disks, standard SSDs, or enhanced SSDs \(ESSDs\), you can use the virtual memory.
-   Exercise caution when you use the administrator account to resize disks, manage spanned volumes or the registry, and update the system. Failure to comply can result in data loss.
-   A 32-bit Windows operating system supports up to four CPU cores.
-   Make sure that a minimum of 2 GiB memory is available when you build a website or deploy a web environment on a Windows instance. Instances with 1-core CPU and 1 GiB memory cannot start MySQL.
-   For more information, see [Select an image](/intl.en-US/Images/Select an image.md).

## Notes on Linux instances

-   Do not modify the content of the default /etc/issue file on Linux instances. If you modify the /etc/issue file on a Linux instance and then use this instance to create a custom image, the operating system distribution of this image cannot be recognized. This causes the instances created from this image fail to start
-   Do not modify permissions of the directories in the root partition, especially /etc, /sbin, /bin, /boot, /dev, /usr, and /lib. Improper modifications of permissions may cause errors.
-   Do not rename, delete, or disable the root account.
-   Do not compile the Linux kernel or perform any other operations on it.
-   We recommend that you do not use swap partitions if basic disks are used. However, for ultra disks, standard SSDs, or ESSDs, you can use swap partitions.
-   Do not enable the NetWorkManager service. This service conflicts with the internal network service of the system, which may cause network errors.
-   Exercise caution when you use the root account to run fio, mkfs, or fsck commands or resize disks. Failure to comply can result in data loss.
-   For more information, see [Select an image](/intl.en-US/Images/Select an image.md).

## Limits

For the limits that apply to ECS, see [Limits](/intl.en-US/Product Introduction/Limits.md).

