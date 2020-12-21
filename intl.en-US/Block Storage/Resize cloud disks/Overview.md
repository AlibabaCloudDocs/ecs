---
keyword: [Alibaba Cloud, ECS, disk resizing, resizing, Elastic Block Storage]
---

# Overview

You can resize disks to meet your storage requirements as your business and application data grow. This topic describes the maximum sizes to which disks can be resized and how to resize disks in different scenarios.

## Scenarios

You can increase the storage capacity of an instance by using one of the following methods:

-   Resize an existing disk. You must resize the existing partitions of the disk or create new partitions on the disk.

    The following methods can be used to resize an existing disk.

    |Method|Limit|Reference|
    |------|-----|---------|
    |Resize a disk online|The instance to which the disk is attached must be in the **Running** \(Running\) state. After the disk is resized, the new size takes effect automatically without the need to restart the instance.

|    -   [Resize disks online for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md)
    -   [Resize disks online for Windows instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Windows instances.md) |
    |Resize a disk offline|The instance to which the disk is attached must be in the **Running** \(Running\) or **Stopped** \(Stopped\) state. After the disk is resized, you must restart the instance by using the ECS console or by calling the RebootInstance operation for the new size to take effect.

|    -   [Resize disks offline for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks offline for Linux instances.md)
    -   [Resize disks offline for Windows instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks offline for Windows instances.md) |

-   Create a new disk, attach the disk to the instance, and then partition and format the disk.
-   Replace the system disk of the instance and specify a larger size for the new system disk. For more information, see [Replace the system disk \(public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace the system disk (public images).md).

## Size ranges of resized system disks

For a resized system disk, the new size must be greater than the original size but less than or equal to 500 GiB. The following table describes the size ranges of resized system disks that correspond to different images used by instances.

|Image|Size range of a resized system disk \(GiB\)|
|:----|:------------------------------------------|
|CoreOS and FreeBSD|\[Max\{30, the original size of the system disk\}, 500\]|
|Other Linux distributions|\[Max\{20, the original size of the system disk\}, 500\]|
|Windows Server|\[Max\{40, the original size of the system disk\}, 500\]|

For example, the system disk on a CentOS instance is 35 GiB in size. When you resize this system disk, the specified new size must be greater than 35 GiB but less than or equal to 500 GiB.

## Maximum sizes of resized data disks

For a resized data disk, the new size must be greater than the original size. The following table lists the maximum sizes of resized data disks of different categories.

|Disk category|Maximum size of a resized data disk \(GiB\)|
|:------------|:------------------------------------------|
|Basic disk|2,000|
|Enhanced SSD \(ESSD\), standard SSD, or ultra disk|32,768|

