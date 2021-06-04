---
keyword: [enhanced SSD, Elastic Block Storage, storage plan, select a disk, attach a disk, format, file system, public preview, release, storage package, standard SSD]
---

# Elastic Block Storage FAQ

This topic provides answers to frequently asked questions about the use of Elastic Block Storage \(EBS\).

-   FAQ about SCUs
    -   [What is a storage capacity unit \(SCU\)?](#section_emy_jk9_ezz)
    -   [Which EBS devices can use SCUs?](#section_f89_rep_dy5)
    -   [Can an SCU be used on its own?](#section_kj0_pgc_ccr)
    -   [What are the rules when you use SCUs?](#section_n4r_cyq_psp)
    -   [How am I billed for SCUs?](#section_dzj_hua_jn1)
-   FAQ about ESSDs
    -   [What is an enhanced SSD \(ESSD\)?](#section_exq_8tt_oqw)
    -   [What specifications do ESSDs have?](#section_cw3_bmw_boh)
    -   [What are the similarities and differences between ESSDs, standard SSDs, and ultra disks?](#section_amv_05u_7k0)
    -   [How is the performance level of an ESSD measured?](#section_tn9_l2d_g0h)
    -   [How do I test the performance of an ESSD?](#ESSDperfor)
    -   [What is the relationship between the storage performance of an ESSD and the storage performance of the instance to which the ESSD is attached?](#section_l0c_cer_qu7)
    -   [How are you billed for ESSDs?](#section_6j1_ta3_nyy)
    -   [Which instance families can be attached with ESSDs?](#section_br8_0h3_7d6)
-   Common FAQ
    -   [What must I consider when I select zones to create disks and then attach the disks to ECS instances?](#section_nks_1y2_gcr)
    -   [What are the common operations that can be performed on a disk?](#section_xs4_pdh_fhb)
    -   [How do I query the usage and free space of EBS devices?](#section_sf9_0jy_k1d)
    -   [Can I shrink a disk?](#section_1oc_in1_pqy)
    -   [How do I release a subscription disk that has not expired?](#section_dyp_yj5_sex)
    -   [What is I/O optimization? Can I upgrade the configurations of an existing ECS instance to those of an I/O optimized instance?](#section_zxg_r7a_vdt)
-   FAQ about performance testing
    -   [What tools can I use to test the performance of EBS devices?](#section_vyv_qlf_4rg)
    -   [Why did my instance shut down when I used fio to test the I/O performance of the instance?](#section_gdt_ekx_3rp)
    -   [How do I test the performance of an ESSD?](#ESSDperfor)
-   FAQ about standard SSDs
    -   [What is the I/O performance of a standard SSD?](#section_f2w_rch_fhb)
    -   [What scenarios are standard SSDs ideal for?](#section_sf1_sch_fhb)
    -   [Can I replace a basic disk with a standard SSD?](#section_z0c_kiu_c6o)
    -   [How do I purchase a standard SSD? What are the pricing options for I/O optimized instances and standard SSDs?](#section_gpx_xch_fhb)
    -   [Can I upgrade a standard SSD after I purchase it?](#section_n5t_cdh_fhb)
    -   [Why is an error reported when I attempt to mount the partitions of a standard SSD to an I/O optimized Linux instance?](#section_md2_ddh_fhb)
    -   [What must I be aware of before I add mount information about basic disks or standard SSDs to Linux instances?](#section_vjf_tos_b2o)
-   FAQ about attaching and detaching disks
    -   [What is a device name \(mount point\)?](#section_c9t_aqp_8au)
    -   [What is an independent disk?](#section_lth_2jp_fhb)
    -   [Can I attach one disk to multiple ECS instances at the same time?](#section_g5g_b2r_fhb)
    -   [Do I need to partition and format a pay-as-you-go disk after I purchase and attach it to an ECS instance?](#section_gps_gpr_fhb)
    -   [Why am I unable to find the data disk that I purchased for a Linux instance?](#section_7hm_z6c_ttx)
    -   [How many cloud disks can be attached to one ECS instance?](#section_hl8_hn5_p3n)
    -   [Why am I unable to find the desired ECS instance when I attempt to attach a disk to it?](#section_ewk_3gr_fhb)
    -   [Can I attach a disk to an ECS instance that is in a different zone?](#section_izt_uhb_fxk)
    -   [Will data in a data disk be lost when I detach the disk?](#section_xzy_pnk_by6)
    -   [Can I detach system disks?](#section_2my_ijk_gy1)
-   FAQ about independent disks
    -   [How is a separately purchased pay-as-you-go data disk billed?](#section_v4m_b2r_fhb)
    -   [I attached a separately created disk to an ECS instance. Why is the disk released when the instance is released?](#section_bjw_8f4_ju1)
    -   [Can I attach a separately purchased pay-as-you-go data disk to a subscription instance?](#section_xtp_b2r_fhb)
    -   [Can I detach a data disk from a subscription instance?](#section_tsb_3gr_fhb)
    -   [I changed the configurations of a disk when I renewed the disk. Can I change the billing method of the disk from subscription to pay-as-you-go within the remaining time of the current subscription period?](#section_nql_jnr_fhb)
-   FAQ about disk snapshots
    -   [When I delete a disk, will its snapshots also be deleted?](#section_a41_mgr_fhb)
    -   [Why are some automatic snapshots on my disk missing?](#section_jvf_shr_fhb)
    -   [Can I use a snapshot to create an independent disk?](#section_tz3_jnr_fhb)
-   FAQ about re-initializing disks
    -   [I cannot access the data in a Linux data disk because an error occurred when I attached the disk. What do I do?](#section_fz4_jnr_fhb)
    -   [Are my snapshots retained if I re-initialize a disk?](#section_mx6_x6w_wn8)
    -   [Data disks of a Linux instance cannot be found after I restarted the instance or re-initialized the system disk. What do I do?](#section_eja_zx1_w6o)
    -   [How do I re-attach data disks after I re-initialize the system disk of a Linux instance?](#section_vaw_x75_0rr)
-   FAQ about extending disks
    -   [Are my snapshots retained if I replace a system disk?](#section_2u6_pq5_q3f)
    -   [What must I be aware of before I replace a system disk?](#section_pc0_x40_gh9)
    -   [How do I extend a system disk?](#section_wdn_d4r_fhb)
    -   [Can I shrink a system disk after I extend it?](#section_iiz_k8i_vkr)
    -   [What EBS devices can be extended when they are used as system disks? Do any regional limits apply to this operation?](#section_cbz_pdh_fhb)
    -   [Can the system disks of both subscription ECS instances and pay-as-you-go ECS instances be extended?](#section_tjd_xqr_fhb)
    -   [What is the storage capacity range of a system disk?](#section_nx3_xqr_fhb)
    -   [I changed the configurations of an instance when I renewed the instance. Can I specify a new size for the system disk when I replace the system disk?](#section_k1m_xqr_fhb)
    -   [How do I create a disk from a snapshot of a data disk to extend the data disk without risking data loss?](#section_idx_soz_yoe)
    -   [What do I do if the "Bad magic number in super-block while trying to open /dev/xvdb1" error message is returned when I extend a disk of a Linux instance?](#section_td6_w72_q3x)
-   FAQ about partitions
    -   [Can I partition a data disk for data storage?](#section_ppz_43v_fhb)
    -   [For a disk with multiple partitions, are snapshots created for the entire disk or only for a specific partition?](#section_q5b_p3v_fhb)
    -   [What must I be aware of before I re-partition a disk?](#section_nx1_3mv_fhb)
    -   [What is the relationship between writing data, and partitioning and formatting?](#section_rhr_eke_n2u)
-   FAQ about rolling back disks
    -   [I rolled back a data disk by using a snapshot after I re-partitioned the disk. How many partitions are available in the disk?](#section_nyd_3mv_fhb)
    -   [An error message similar to the following one is returned when I attempt to roll back a disk: "A disk can be rolled back only when the instance to which the disk is attached has been stopped and the disk has no snapshots being created. If the operating system of the current ECS instance has been replaced, the snapshot taken before the operating system is replaced cannot be used to roll back the new system disk." What do I do?](#section_psz_3vy_ghb)
-   Other FAQ
    -   [How do I migrate data from the system disk of a Linux instance?](#section_0ty_1b5_d3j)
    -   [How do I copy data across instances?](#section_i3j_nrv_fhb)

## What is a storage capacity unit \(SCU\)?

SCUs are subscription storage coupons that can be used to offset pay-as-you-go bills of storage services such as disks. Compared with disks purchased together with subscription Elastic Compute Service \(ECS\) instances, SCUs used together with pay-as-you-go disks are more cost-effective and flexible. For more information, see [Overview](/intl.en-US/Block Storage/Storage capacity units/Overview.md).

## Which EBS devices can use SCUs?

SCUs can be used to offset the bills of eligible pay-as-you-go storage resources. Take note of the following items:

-   SCUs can be used to offset bills of enhanced SSDs \(ESSDs\), standard SSDs, ultra disks, and basic disks. SCUs cannot be used to offset the bills of local SSDs.
-   SCUs can be used to offset bills of Capacity NAS and Performance NAS. SCUs cannot be used to offset the bills of Extreme NAS or Infrequent Access NAS.
-   SCUs can be used to offset bills of normal snapshots. SCUs cannot be used to offset the bills of local snapshots.
-   SCUs can be used to offset bills of OSS Standard, Infrequent Access, and Archive storage classes.

## Can an SCU be used on its own?

No, SCUs cannot be used on their own. SCUs must be used to match pay-as-you-go disks to offset the bills.

## What are the rules when you use SCUs?

SCUs offset the bills of pay-as-you-go disks at discounted rates. For more information, see [Usage rules](/intl.en-US/Block Storage/Storage capacity units/Usage rules.md).

## How am I billed for SCUs?

You are billed for SCUs based on the storage capacity. Storage capacity prices vary with regions.

## What is an enhanced SSD \(ESSD\)?

An ESSD is an ultra-high performance disk provided by Alibaba Cloud. ESSDs use the 25GE and remote direct memory access \(RDMA\) technologies to deliver up to 1 million random input/output operations per second \(IOPS\) with low one-way latency. For more information, see [ESSDs](/intl.en-US/Block Storage/Block Storage overview/ESSDs.md).

## What specifications do ESSDs have?

ESSDs have different specifications based on their performance levels. For information about the latest details of ESSD performance, see [ESSDs](/intl.en-US/Block Storage/Block Storage overview/ESSDs.md).

The performance of a storage device is closely related to the capacity of the device. A storage device that has a larger capacity provides higher data processing capabilities. All ESSDs have the same I/O performance per unit of capacity. However, the performance of ESSDs linearly increases together with its capacity until the maximum performance per disk at the PL is reached.

|PL|ESSD capacity range \(GiB\)|Maximum IOPS|Maximum throughput \(MB/s\)|
|--|---------------------------|------------|---------------------------|
|PL0|40~32,768|10,000|180|
|PL1|20~32,768|50,000|350|
|PL2|461~32,768|100,000|750|
|PL3|1,261~32,768|1,000,000|4,000|

## What are the similarities and differences between ESSDs, standard SSDs, and ultra disks?

-   Similarities: All three categories of disks are based on a distributed EBS architecture, provide high reliability and scalability, and support snapshots and data encryption.
-   Differences: ESSDs have the best performance among the three categories of disks. For more information, see [ESSDs](/intl.en-US/Block Storage/Block Storage overview/ESSDs.md) and [EBS performance](/intl.en-US/Block Storage/Performance/EBS performance.md).

## How is the performance level of an ESSD measured?

The performance level of an ESSD is proportional to its storage capacity. An ESSD that has a larger storage capacity delivers better performance. Compared with standard SSDs, ESSDs have better performance. For more information, see [ESSDs](/intl.en-US/Block Storage/Block Storage overview/ESSDs.md).

## How do I test the performance of an ESSD?

You can use fio \(flexible IO tester\) to perform a stress test on an ESSD. For more information, see [Test the IOPS performance of an enhanced SSD](/intl.en-US/Block Storage/Performance/Test the IOPS performance of an enhanced SSD.md).

## What is the relationship between the storage performance of an ESSD and the storage performance of the instance to which the ESSD is attached?

Instance types impact the performance of instance-level storage. The higher specifications an instance type has, the higher IOPS and throughput the instance type delivers.

For example, when you create an instance of the g6se storage optimized instance family with enhanced performance and attach ESSDs to the instance, the following situations may occur:

-   If the total storage performance of the ESSDs does not exceed the maximum storage performance that the instance type can deliver, the instance delivers the total storage performance of the ESSDs.
-   If the total storage performance of the ESSDs exceeds the maximum storage performance that the instance type can deliver, the storage performance of the instance is limited to the maximum storage performance that the instance type can deliver.

    For example, you create a 16 GiB instance of the ecs.g6se.xlarge instance type that can deliver up to 60,000 IOPS. If you attach an ESSD to the instance and the ESSD has a storage capacity of 2 TiB with a maximum IOPS of 101,800, the maximum IOPS of the instance is 60,000, instead of 101,800.


For information about the performance and specifications of the g6se instance family, see [Instance families](/intl.en-US/Instance/Instance families.md).

## How are you billed for ESSDs?

Enhanced SSDs support the subscription and pay-as-you-go billing methods. For more information, see the [Pricing](https://www.alibabacloud.com/product/ecs) tab of the Elastic Compute Service page.

## Which instance families can be attached with ESSDs?

For information about instance families that can be attached with ESSDs, see [Instance families](/intl.en-US/Instance/Instance families.md).

## What tools can I use to test the performance of EBS devices?

For more information, see [Test the performance of Elastic Block Storage devices](/intl.en-US/Block Storage/Performance/Test the performance of Elastic Block Storage devices.md).

## Why did my instance shut down when I used fio to test the I/O performance of the instance?

You can use fio to test the I/O performance of an instance by testing raw disk partitions or file systems. If you perform this test on raw disk partitions, the metadata of the file systems in the raw disk partitions may be damaged. This prevents you from accessing files in the partitions and can also cause the instance to shut down. This problem does not occur when you use fio to test the I/O performance of the instance by testing file systems.

## What must I consider when I select zones to create disks and then attach the disks to ECS instances?

A pay-as-you-go disk can be attached only to an ECS instance that is in the same zone as the disk.

-   For high-availability applications, we recommend that you create data disks in different zones and attach them to ECS instances.
-   For low-latency applications, we recommend that you create data disks in the same zone as the ECS instances and attach them to the instances.

## What are the common operations that can be performed on a disk?

For information about the common operations that you can perform on a disk, see the "Related operations" section in [Cloud disks](/intl.en-US/Block Storage/Block Storage overview/Cloud disks.md).

## How do I query the usage and free space of EBS devices?

You can log on to an ECS instance to query the usage and free space of EBS devices in the instance. You cannot query the usage and free space of EBS devices by using the ECS console or by calling ECS API operations.

## Can I shrink a disk?

No, you cannot shrink disks. If you want to shrink a disk that you purchased, we recommend that you create a disk of your desired size and attach it to the same instance as the original disk. Then, copy the data stored on the original disk to the new disk and release the original disk.

## How do I release a subscription disk that has not expired?

Alibaba Cloud subscription data disks cannot be released before they expire. To release a subscription data disk, you must change its billing method to pay-as-you-go. Before you release the resulting pay-as-you-go data disk, make sure that you have backed up all important data stored in it. For more information, see [Change billing methods of disks](/intl.en-US/Block Storage/Cloud disks/Change billing methods of disks.md) and [Release a disk](/intl.en-US/Block Storage/Cloud disks/Release a disk.md).

**Note:** After the billing method of a data disk is changed from subscription to pay-as-you-go, you are billed for the data disk by hour. You are not charged for the pay-as-you-go data disk one hour after the disk is released. After the disk billing method is changed from subscription to pay-as-you-go, the refund amount is displayed in the ECS console. The coupons that have been used are not refundable.

## What is I/O optimization? Can I upgrade the configurations of an existing ECS instance to those of an I/O optimized instance?

I/O optimization provides better network capabilities and storage performance for instances and disks. For example, you can optimize the storage performance of a standard SSD by attaching the standard SSD to an I/O optimized instance.

You can call the [ModifyInstanceSpec](/intl.en-US/API Reference/Instances/ModifyInstanceSpec.md) and [ModifyPrepayInstanceSpec](/intl.en-US/API Reference/Instances/ModifyPrepayInstanceSpec.md) operations to upgrade the configurations of your non-I/O optimized instances to those of I/O optimized instances.

## What is the I/O performance of a standard SSD?

For more information, see [EBS performance](/intl.en-US/Block Storage/Performance/EBS performance.md).

## What scenarios are standard SSDs ideal for?

Standard SSDs provide high performance and high reliability. They are ideal for I/O-intensive applications, such as MySQL, SQL Server, Oracle, PostgreSQL, and other small and medium-sized relational databases. They are also ideal for small and medium-sized development and testing environments that require high data reliability.

## Can I replace a basic disk with a standard SSD?

No, standard SSDs cannot be used to replace basic disks because standard SSDs use SSDs as the physical storage media.

## How do I purchase a standard SSD? What are the pricing options for I/O optimized instances and standard SSDs?

For more information about pricing, see the [Pricing](https://www.alibabacloud.com/product/ecs) tab of the Elastic Compute Service page.

## Can I upgrade a standard SSD after I purchase it?

Yes, you can upgrade and scale up your standard SSDs. For more information, see [Overview](/intl.en-US/Block Storage/Resize cloud disks/Overview.md).

## Why is an error reported when I attempt to mount the partitions of a standard SSD to an I/O optimized Linux instance?

In the Linux operating system, the mount points for standard SSDs are in the /dev/vd\* format, and the mount points for basic disks are in the /dev/xvd\* format. If you specify the mount point in the /dev/xvd\* format in a command to mount a standard SSD partition, an error is reported. Specify a mount point in the /dev/vd\* format in the command to mount a partition of the standard SSD.

## What must I be aware of before I add mount information about basic disks or standard SSDs to Linux instances?

To attach a data disk to a Linux instance, you must format and partition the disk. When you perform this operation, note that /dev/xvdb1 is the mount point for a basic disk, and /dev/vdb1 is the mount point for an ultra disk, a standard SSD, or an ESSD. If the information specified in the `mount -a` command is invalid, the disk fails to be attached. To avoid this problem, perform the following steps:

1.  Run the `fdisk -l` command to view information about the data disk.
2.  Check whether the information about the data disk added to `/etc/fstab` is the same as that in Step 1.

    **Note:** Do not add duplicate mount information because this will cause a system startup failure.

3.  Run the vim command to modify the `/etc/fstab` file.
4.  Comment out or delete invalid information and add valid mount information.
5.  Run the `mount -a` command to check whether the disk is attached.

For more information, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md).

## What is a device name \(mount point\)?

A device name \(mount point\) is the location of an ECS disk on the disk controller bus. The selected device name matches the disk device number in Linux and matches the disk sequence number in the disk manager of Windows.

## What is an independent disk?

An independent disk is a pay-as-you-go data disk that you separately purchase. An independent disk can be attached to or detached from any ECS instance in the same zone as the disk. You must attach an independent disk to an instance, and partition and format the disk before you can use it. For more information, see [Create a disk](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk.md).

## Can I attach one disk to multiple ECS instances at the same time?

No, you cannot attach a disk to multiple ECS instances at the same time. A disk can be attached only to one ECS instance in the same zone as the disk.

## Do I need to partition and format a pay-as-you-go disk after I purchase and attach it to an ECS instance?

Yes, you must attach a pay-as-you-go disk to an ECS instance, and then partition and format the disk after you separately purchase the disk. For more information, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md) and [Format a data disk for a Windows ECS instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Windows ECS instance.md).

## Why am I unable to find the data disk that I purchased for a Linux instance?

If you separately purchase a pay-as-you-go data disk, you must attach it to the instance and partition it before you can view and use its storage space. For more information, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md) and [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).

## How many cloud disks can be attached to one ECS instance?

When cloud disks are used as data disks, A maximum of 16 data disks can be attached to a single instance. For more information, see the "Elastic Block Storage \(EBS\) limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).

## Why am I unable to find the desired ECS instance when I attempt to attach a disk to it?

Check whether the ECS instance is released. If the ECS instance is not released, make sure that it is in the same zone as the disk.

## Can I attach a disk to an ECS instance that is in a different zone?

No, you cannot attach a disk to an ECS instance that is in a different zone. A pay-as-you-go disk can be attached only to an ECS instance in the same zone as the disk.

## Will data in a data disk be lost when I detach the disk?

-   In Windows, we recommend that you stop all read and write operations on all file systems of the disk to ensure data integrity. Otherwise, the data that is being read or written will be lost.
-   In Linux, you must log on to the ECS instance and run the umount command on the disk. After the command is executed, log on to the ECS console to detach the disk.

## Can I detach system disks?

Yes, you can detach system disks.

## How is a separately purchased pay-as-you-go data disk billed?

A pay-as-you-go data disk is billed by hour. Note that if you have insufficient balance within your account, the services of the data disk is suspended.

## I attached a separately created disk to an ECS instance. Why is the disk released when the instance is released?

This is because you have configured the disk to be released along with the instance. You can change this configuration by using the ECS console or by calling an API operation. For more information, see [Release a disk](/intl.en-US/Block Storage/Cloud disks/Release a disk.md).

## Can I attach a separately purchased pay-as-you-go data disk to a subscription instance?

Yes, you can attach a separately purchased pay-as-you-go data disk to a subscription instance.

## Can I detach a data disk from a subscription instance?

No, you cannot detach data disks from subscription instances. Data disks expire at the same time as the subscription instances to which they are attached, and are released together with the instances. To release a subscription data disk, convert it into a pay-as-you-go data disk first. Then, detach and release the data disk. For information about how to change the billing method of disks, see [Change billing methods of disks](/intl.en-US/Block Storage/Cloud disks/Change billing methods of disks.md).

## I changed the configurations of a disk when I renewed the disk. Can I change the billing method of the disk from subscription to pay-as-you-go within the remaining time of the current subscription period?

No, you cannot change the billing method of the disk within the remaining time of the current subscription period. You can change the billing method of the disk from subscription to pay-as-you-go only by changing the configurations of the instance after the current subscription period ends.

## When I delete a disk, will its snapshots also be deleted?

If you have enabled the **Delete Automatic Snapshots While Releasing Disk** feature for the disk, the automatic snapshots of the disk are also deleted when you delete the disk. However, the manual snapshots are retained. You can change this setting at any time. For more information, see [Delete automatic snapshots while releasing a disk](/intl.en-US/Snapshots/Automatic snapshot policies/Delete automatic snapshots while releasing a disk.md).

## Why are some automatic snapshots on my disk missing?

When the number of snapshots reaches the upper limit, the earliest automatic snapshots are automatically deleted but manual snapshots are not affected.

**Note:** The automatic snapshot policy that is applied to a disk can be executed only after the disk is attached to an instance.

## Can I use a snapshot to create an independent disk?

Yes, you can use a snapshot to create an independent disk. You can use an existing snapshot to create an independent pay-as-you-go disk. For more information, see [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md).

## I cannot access the data in a Linux data disk because an error occurred when I attached the disk. What do I do?

Perform the following operations to troubleshoot the error for the Linux operating system:

1.  Find the data disk and use one of the following methods to check whether the disk is attached to the corresponding ECS instance:
    -   View the disk in the ECS console. For more information, see [View the monitoring data of a cloud disk](/intl.en-US/Block Storage/Cloud disks/View the monitoring data of a cloud disk.md).
    -   Log on to the instance, and run the `fdisk -l` command to check whether the data disk partition information is correct. Run the `df -h` and `mount | grep "<devpath>"` commands to view the mount information.
2.  Run the cat command to view the /etc/fstab file and check whether two disks are attached to the same directory.
    -   If two disks are attached to the same directory, the second disk replaces the first disk. This causes data of the first disk to become inaccessible. We recommend that you attach the second disk to a different directory.
    -   If two disks are attached to different directories but the mount information shows that they are in the same directory, run the ll command to check whether a connection exists between the two directories. If a connection exists between the two directories, run the mkdir command to create a directory, and attach one of the disks to the new directory. Then, check whether the data can be accessed.

## What do I do if data is lost after I restart a Linux instance?

-   Problem description: All data in a directory such as /alidata is lost after you restart a Linux instance.
-   Cause: After you run the `df -h` command, the command output shows that none of the data disk partitions is mounted to the directory.
-   Solution: An I/O-optimized instance is used in this example. If your ECS instance is a non-I/O optimized instance, enter the device names of the disk partitions in the /dev/xvd\*1 format in the mount command.
    1.  Run the `fdisk -l` command to view the data disk partitions that are not mounted.
    2.  Run the `mount /dev/vdb1 /alidata` command to mount the data disk partitions to the preceding directory.
    3.  Run the `df -h` command to check whether the data disk partitions are mounted to the directory.
    4.  \(Optional\) Configure the /etc/fstab file for the system to automatically mount the disk partitions on next system startup to avoid this problem.

## Are my snapshots retained if I re-initialize a disk?

Yes, both manual and automatic snapshots in the disk are retained.

## Data disks of a Linux instance cannot be found after I restarted the instance or re-initialized the system disk. What do I do?

-   Problem description: After you restart a Linux instance or re-initialize the system disk, you log on to the instance and run the `df -h` command. The command output shows that no data disks are found.
-   Cause:
    -   Restart of an instance: Mount information was not written to the /etc/fstab file before you restart the instance. As a result, data disks are not automatically attached after the instance restarts.
    -   Reinitialization of the system disk: The /etc/fstab file is reset after the system disk is re-initialized. Therefore, data disks are not automatically attached on system startup.
-   Solution:
    1.  Run the `mount /dev/xvdb1` command to remount the data disk partitions.
    2.  Run the mount command to check the file system of the /dev/xvdb1 partition.
    3.  Assume that the format of files in the /dev/xvdb1 partition is ext3. Run the following command to write the partition mount information to the /etc/fstab file:

        ```
        echo '/dev/xvdb1 /data ext3 defaults 0 0' >> /etc/fstab
        ```

    4.  Restart the instance in the ECS console.

## How do I re-attach data disks after I re-initialize the system disk of a Linux instance?

After you re-initialize the system disk of a Linux instance, data in the data disks that are attached to the instance remains unchanged, but the mount information about the data disks is lost. Assume that before the system disk is re-initialized, a data disk partition mounted to the instance is named /dev/vdb1, and its mount point is named /InitTest. Perform the following operations to remount the data disk partition after you restart the Linux instance:

1.  Run the `mount` command to view the mount information about the data disk.

    The command output does not contain information about /dev/vdb1.

2.  Run the `fdisk -l` command to view information about data disk partitions.
3.  Run the `cat /etc/fstab` command to view the original mount point name of the /dev/vdb1 data disk partition.
4.  Run the `mkdir /InitTest` command to recreate the mount point for the data disk partition.

    For the /dev/vdb1 data disk partition, the new mount point name must be the same as the original one.

5.  Run the `mount /dev/vdb1 /InitTest` command to remount the data disk partition.
6.  Run the `df -h` command to check whether the data disk partition is mounted.
7.  Perform the following operations to check whether the/dev/vdb1 data disk partition can be automatically mounted:
    1.  Run the `umount /dev/vdb1` command to unmount the /dev/vdb1 data disk partition.
    2.  Run the `mount` command to check the mount information.

        If the command output does not contain information about /dev/vdb1, the partition is unmounted.

    3.  Run the `mount -a` command to automatically mount /dev/vdb1.
    4.  Run the `mount` command to check the mount information.

        If the command output contains information about /dev/vdb1, the partition is automatically mounted.


## Are my snapshots retained if I replace a system disk?

This depends on how the snapshots are created. Manual snapshots are retained, but automatic snapshots are deleted if the Delete Automatic Snapshots While Releasing Disk feature is enabled.

**Note:** After a system disk is replaced, the disk ID changes. You cannot use the snapshots of the original system disk to roll back the new system disk.

## What must I be aware of before I replace a system disk?

We recommend that you create snapshots of the current system disk before you replace it. Make sure that the new system disk has sufficient space available. The recommended available disk space is 1 GiB or larger. If disk space is insufficient, the instance may not start properly after you replace the system disk.

## How do I extend a system disk?

You can extend a system disk by using the ECS console or by calling the [ResizeDisk](/intl.en-US/API Reference/Disk/ResizeDisk.md) operation.

## Can I shrink a system disk after I extend it?

No, you cannot shrink a system disk after you extend it. We recommend that you extend the system disk reasonably based on your needs.

## What EBS devices can be extended when they are used as system disks? Do any regional limits apply to this operation?

Ultra disks, standard SSDs, and ESSDs can be extended when they are used as system disks. You can extend system disks in all regions.

## Can the system disks of both subscription ECS instances and pay-as-you-go ECS instances be extended?

Yes, the system disks of both subscription ECS instances and pay-as-you-go ECS instances can be extended.

## What is the storage capacity range of a system disk?

The capacity range of a system disk varies with the operating system. For more information, see [Overview](/intl.en-US/Block Storage/Resize cloud disks/Overview.md).

## I changed the configurations of an instance when I renewed the instance. Can I specify a new size for the system disk when I replace the system disk?

After you downgrade the configurations of a subscription instance when you renew the instance, you can extend its system disk only when the new billing cycle starts.

## How do I create a disk from a snapshot of a data disk to extend the data disk without risking data loss?

If a data disk cannot be extended without data loss due to a disk error, you can purchase a pay-as-you-go disk to temporarily store data from the original data disk, and then format the original data disk. Perform the following operations:

1.  Create a snapshot of the current data disk \(original data disk\). For more information, see [Create a snapshot for a disk](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).
2.  Go to the [disk buy](https://ecs-buy.aliyun.com/#/clouddisk) page. Select the region and zone of the ECS instance to purchase a pay-as-you-go disk. Click **Create from Snapshot**. In the dialog box that appears, select the snapshot created in the previous step.
3.  Log on to the ECS console and then attach the new data disk you purchased in the previous step to the ECS instance.
4.  Log on to the ECS instance and run the mount command to attach the new data disk to the instance. For more information about how to attach a disk created from a snapshot, see [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md).
5.  Check whether files in the new data disk are the same as those in the original data disk.
6.  Run the fdisk command to delete the original partition table. Then, run commands such as fdisk and mkfs.ext3 to re-partition and re-format the new data disk, extending it to the target capacity. For more information, see [Resize partitions and file systems of Linux data disks](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.md).
7.  Run the `cp -R` command to copy all the data in the new data disk back to the original data disk.

    You can add the --preserve=all setting to retain the file properties when you copy the files.

8.  Run the umount command to detach the new data disk.
9.  In the ECS console, detach the new data disk from the ECS instance and release the disk.

## What do I do if the "Bad magic number in super-block while trying to open /dev/xvdb1" error message is returned when I extend a disk of a Linux instance?

-   Problem description: When you run the `e2fsck -f /dev/xvdb` command to extend a disk of a Linux instance, the "Bad magic number in super-block while trying to open /dev/xvdb1" error message is returned.
-   Cause: The disk to be extended is not partitioned.
-   Solution: Run the `e2fsck -f /dev/xvdb` and `resize2fs /dev/xvdb` commands to extend the disk. Then, run the mount command to mount the disk.

## Can I partition a data disk for data storage?

Yes, data disks can be partitioned for data storage. You can split a data disk into multiple partitions. We recommend that you use the system tool for partitioning.

## For a disk with multiple partitions, are snapshots created for the entire disk or only for a specific partition?

Snapshots are created for the entire disk, instead of for a specific partition.

## What must I be aware of before I re-partition a disk?

To ensure data security, we recommend that you create a snapshot of a disk before you re-partition the disk. This way, you can roll back the disk if you perform an invalid operation. For more information, see [Create a snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md) and [Roll back a disk by using a snapshot](/intl.en-US/Snapshots/Use snapshots/Roll back a disk by using a snapshot.md).

## What is the relationship between writing data, and partitioning and formatting?

A new disk or disk partition can be used only after it is initialized and has its data structure recorded on the disk. The goal of formatting is to create file systems. Therefore, when a file system is created on a disk, data of the file system is written to the disk. The amount of data written to disks during formatting varies based on the file system.

-   In a Windows instance, you can use one of the following methods to format a data disk:
    -   Quick formatting: This method allows you to allocate only file systems to partitions and rewrite the directory table. Quick formatting takes up less space.
    -   Full formatting: This method allows you to allocate files systems to partitions, rewrite the directory table, and scan for and mark damaged sectors. Additionally, during the formatting process, empty data blocks on the disk are filled in, which is equivalent to writing data to the entire disk. In this case, the size of the first full snapshot is approximately equal to the disk size.
-   In a Linux instance, if no data is written to a disk after you format the disk, the size of the first snapshot depends on the format of file systems on the disk.

## I rolled back a data disk by using a snapshot after I re-partitioned the disk. How many partitions are available in the disk?

When you roll back a data disk by using a snapshot, the disk returns to the state it was in when the snapshot was taken. If the disk has not been re-partitioned when the snapshot was taken, only one partition is available in the disk.

## An error message similar to the following one is returned when I attempt to roll back a disk: "A disk can be rolled back only when the instance to which the disk is attached has been stopped and the disk has no snapshots being created. If the operating system of the current ECS instance has been replaced, the snapshot taken before the operating system is replaced cannot be used to roll back the new system disk." What do I do?

-   Problem description: When you attempt to roll back a disk by using a snapshot, an error message similar to the following one is returned: "A disk can be rolled back only when the instance to which the disk is attached has been stopped and the disk has no snapshots being created. If the operating system of the current instance has been replaced, the snapshot taken before the operating system is replaced cannot be used to roll back the new system disk."
-   Cause: The problem may be caused by an invalid disk property or disk state.
-   Solution: You can troubleshoot the problem based on the instance status or snapshot status.
    -   Check whether the instance to which the disk is attached is stopped.

        You can roll back disks only when the instance to which the disks are attached is in the Stopped state. You can log on to the ECS console and check the status of the instance on the Instances page.

    -   Check whether the system disk of the instance associated with the snapshot is replaced.

        If you selected an image to replace the system disk, a new system disk is automatically recreated from the new image, and the system disk ID changes. Therefore, you cannot use the snapshots taken for the original system disk to roll back the new system disk. However, you can create a custom image from one of these snapshots and then use the custom image to replace the system disk of the instance. This way, the instance returns to the state it was in when the snapshot was taken. For more information, see [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md) and [Replace a system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md).

    -   Check whether the disk to be rolled back has a snapshot being created.

        To ensure data consistency, Alibaba Cloud does not allow users to roll back a disk when a snapshot is being created from the disk. In the left-side navigation pane of the instance details page, click the **Snapshot** tab and check the status of snapshots. A snapshot is being created if the **Progress** value is not **100%** and the **Status** value is **Progressing**.****

        If you want to forcibly terminate the creation process of a snapshot to roll back the disk, select the snapshot and click **Delete**.


## How do I migrate data from the system disk of a Linux instance?

If you purchase a Linux instance without attaching any data disks to it. After the instance is used for a period of time, its system disk usage approaches 100% and can no longer meet your business needs. To solve this problem, you can purchase a data disk and attach it to the instance. Then, run the mv command to migrate data from the system disk to the data disk.

## How do I copy data across instances?

You can choose data copy methods based on the operating system:

-   Copy data between Linux instances
    -   Use the lrzsz tool

        Log on to the Linux instances, install the lrzsz tool, run the rz command to upload files to one Linux instance, and then run the sz command to download the files to the other Linux instance.

        You can also first run the sz command to download files to your computer and then run the rz command to upload these files to the other Linux instance.

    -   Use the FTP service

        If you use the SFTP tool, we recommend that you use the root account to log on to instances and to upload or download files.

    -   Use the wget command

        On one instance, compress a file or a folder and then save it to the web directory to generate a download URL. Then, run the wget command on the other Linux instance to download the file or folder.

-   Copy data between a Linux instance and a Windows instance

    We recommend that you use the SFTP tool to download files from the Linux instance to your computer and then use the FTP service to upload the files to the Windows instance.

-   Copy data between Windows instances
    -   Use the FTP service
    -   Use TradeManager

