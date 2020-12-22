---
keyword: [cloud disk, disk, ESSD, standard SSD, ultra disk]
---

# Cloud disks

Cloud disks are block-level Elastic Block Storage \(EBS\) products provided by Alibaba Cloud for ECS and provide low latency, high performance, high durability, and high reliability. Cloud disks use a distributed triplicate mechanism to ensure 99.9999999% \(nine 9's\) data durability for ECS instances. If service disruptions occur within a zone \(for example, due to hardware failures\), data within the zone is copied to an available disk in another zone to help ensure data availability.

## Disk categories

Cloud disks are classified into the following categories based on their performance:

-   Enhanced SSDs \(ESSDs\): ESSDs are based on the next-generation distributed block storage architecture and the 25 Gigabit Ethernet \(25 GE\) and remote direct memory access \(RDMA\) technologies. Each ESSD has low latency and can deliver up to one million input/output operations per second \(IOPS\). For more information, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).

    We recommend that you use ESSDs for scenarios such as online transactional processing \(OLTP\) databases, NoSQL databases, and Elasticsearch, Logstash, and Kibana \(ELK\) log analysis.

-   Standard SSDs: Standard SSDs are high-performance disks that provide consistent high random IOPS and high data reliability.

    We recommend that you use standard SSDs for scenarios such as I/O-intensive applications, small and medium-sized relational databases, and NoSQL databases.

-   Ultra disks: Ultra disks are cost-effective and provide medium random IOPS and high data reliability.

    We recommend that you use ultra disks as system disks or for scenarios such as development and testing.

-   Basic disks: Basic disks are the previous generation of disks and are unavailable for purchase.

For more information about disk performance, see [EBS performance](/intl.en-US/Block Storage/Performance/EBS performance.md).

Cloud disks are classified into system disks and data disks based on their purpose.

-   System disks contain operating systems and can be created only along with instances. The lifecycle of a system disk is the same as that of the instance to which the system disk is attached.
-   Data disks are used to store application data and can be created separately or along with instances.

**Note:** When a cloud disk is created, the disk capacity displayed in the ECS console includes the capacity occupied by the operating system, and the remaining available capacity may be less than the disk capacity displayed in the ECS console. For example, if the capacity of a system disk displayed in the ECS console is 40 GiB, the remaining available capacity may be less than 40 GiB because the operating system occupies some of the disk capacity.

## Limits

A cloud disk can be attached to only one ECS instance in the same zone.

The following table describes other limits.

|Item|Limit|Adjustable|
|:---|:----|:---------|
|Permissions to create a pay-as-you-go disk|You must complete real-name verification before you can create a disk within a region in mainland China.|None.|
|Quota for pay-as-you-go disks in all regions for an account|This quota is calculated by using the following formula: Number of ECS instances across all regions × 5. A minimum of ten pay-as-you-go disks can be created in each account.|Submit a ticket.|
|Quota for system disks on an instance|1|None.|
|Quota for data disks on an instance|16 \(including cloud disks and Shared Block Storage devices\)|None.|
|Quota for instances to which a Shared Block Storage device can be attached|8|None.|
|Quota for Shared Block Storage devices in all regions for an account|10|Submit a ticket.|
|Capacity of a basic disk|5 GiB to 2,000 GiB|None.|
|Capacity of a standard SSD|20 GiB to 32,768 GiB|None.|
|Capacity of an ultra disk|20 GiB to 32,768 GiB|None.|
|Capacity of an enhanced SSD \(ESSD\)|20 GiB to 32,768 GiB|None.|
|Capacity of a local SSD|5 GiB to 800 GiB|None.|
|Total capacity of all local SSDs on an instance|1,024 GiB|None.|
|Capacity of a local NVMe SSD|1,456 GiB|None.|
|Total capacity of all local NVMe SSDs on an instance|2,912 GiB|None.|
|Capacity of a local SATA HDD|5,500 GiB|None.|
|Total capacity of all local SATA HDDs on an instance|154, 000 GiB|None.|
|Capacity of a Shared SSD Block Storage device|32,768 GiB|None.|
|Total capacity of all Shared SSD Block Storage devices on an instance|128 TiB|None.|
|Capacity of a Shared Ultra Block Storage device|32, 768 GiB|None.|
|Total capacity of all Shared Ultra Block Storage devices on an instance|128 TiB|None.|
|Capacity of a system disk|-   Windows Server: 40 GiB to 500 GiB
-   CoreOS and FreeBSD: 30 GiB to 500 GiB
-   Linux systems excluding CoreOS: 20 GiB to 500 GiB

|None.|
|Permissions to attach new local disks to instances that are equipped with local disks|Not allowed.|None.|
|Permissions to change configurations of instances that are equipped with local disks|Only bandwidth configurations of instances that are equipped with local disks can be changed.|None.|
|Mount points of system disks|/dev/vda|None.|
|Mount points of data disks|/dev/vd\[b-z\]|None.|

## Billing methods

For more information, see the Pricing tab on the [Elastic Compute Service page](https://www.alibabacloud.com/product/ecs#pricing).

Cloud disks support the subscription and pay-as-you-go billing methods. For more information, see [Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md) and [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md).

-   Cloud disks that are created along with subscription instances or created separately for subscription instances are billed on a subscription basis.
-   Cloud disks that are created along with pay-as-you-go instances or created separately for pay-as-you-go instances are billed on a pay-as-you-go basis. Storage capacity units \(SCUs\) can be used to offset the bills of pay-as-you-go disks.

After a cloud disk is created, you can change its billing method. For more information, see [Change billing methods of disks](/intl.en-US/Block Storage/Cloud disks/Change billing methods of disks.md).

## Related operations

The following table describes the operations that you can perform on cloud disks.

|Operation|Reference|
|---------|---------|
|Attach an idle pay-as-you-go disk to an ECS instance|1.  [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md)
2.  Format the data disk based on the operating system:
    -   [Partition and format a data disk larger than 2 TiB in size](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB in size.md)
    -   [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md)
    -   [Format a data disk for a Windows ECS instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Windows ECS instance.md) |
|Create and use a data disk|1.  [Create a disk](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk.md)
2.  [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md)
3.  Format the data disk based on the operating system:
    -   [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md)
    -   [Format a data disk for a Windows ECS instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Windows ECS instance.md) |
|Encrypt data stored on a cloud disk|[Encryption overview](/intl.en-US/Block Storage/Encrypt a disk/Encryption overview.md)-   [Encrypt a system disk](/intl.en-US/Block Storage/Encrypt a disk/Encrypt a system disk.md)
-   [Encrypt a data disk](/intl.en-US/Block Storage/Encrypt a disk/Encrypt a data disk.md) |
|Resize a system disk or a data disk|[Overview](/intl.en-US/Block Storage/Resize cloud disks/Overview.md)

-   [Resize disks online for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md)
-   [Resize disks online for Windows instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Windows instances.md) |
|Replace a system disk|[Replace the system disk \(public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace the system disk (public images).md)|
|Back up disk data|-   [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md)
-   [Apply or disable an automatic snapshot policy](/intl.en-US/Snapshots/Automatic snapshot policies/Apply or disable an automatic snapshot policy.md) |
|Restore a disk to its initial status|[Re-initialize a system disk](/intl.en-US/Block Storage/Cloud disks/Reinitialize a cloud disk/Re-initialize a system disk.md)|
|Restore a disk to its status at a specific point in time|[Roll back a disk by using a snapshot](/intl.en-US/Block Storage/Cloud disks/Roll back a disk by using a snapshot.md)|
|Detach the damaged system disk of an instance and attach the disk back to the original instance after the disk is repaired|[Detach or attach a system disk](/intl.en-US/Block Storage/Cloud disks/Detach or attach a system disk.md)|
|Release an instance and retain data stored on its system disk|-   [Detach or attach a system disk](/intl.en-US/Block Storage/Cloud disks/Detach or attach a system disk.md)
-   [Enable or disable the Release Disk with Instance feature for disks when you create an instance](/intl.en-US/Block Storage/Cloud disks/Release a disk.mdsection_ufq_ii2_5h8)
-   [Enable or disable the Release Disk with Instance feature for a disk on the Disks page](/intl.en-US/Block Storage/Cloud disks/Release a disk.mdsection_wz5_ryw_8s5) |
|Release a subscription disk that is no longer needed|1.  [Change billing methods of disks](/intl.en-US/Block Storage/Cloud disks/Change billing methods of disks.md)
2.  [Detach a data disk](/intl.en-US/Block Storage/Cloud disks/Detach a data disk.md)
3.  [Release a disk](/intl.en-US/Block Storage/Cloud disks/Release a disk.md) |
|Release a pay-as-you-go disk that is no longer needed|1.  [Detach a data disk](/intl.en-US/Block Storage/Cloud disks/Detach a data disk.md)
2.  [Release a disk](/intl.en-US/Block Storage/Cloud disks/Release a disk.md) |

