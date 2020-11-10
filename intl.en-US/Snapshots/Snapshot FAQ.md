---
keyword: [Alibaba Cloud, reduce snapshot fees, storage plan, file system, backup]
---

# Snapshot FAQ

This topic provides answers to commonly asked questions about ECS snapshots.

-   Commonly asked questions
    -   [How is the size of the first full snapshot of a disk calculated?](#section_h7p_t3y_viq)
    -   [Where can I view a list of snapshot prices by Alibaba Cloud region?](#section_nom_iuk_an9)
    -   [Is there a free tier for the snapshot service?](#section_h58_338_rau)
    -   [Can I download or export ECS instance snapshots to a local device?](#section_1ff_9s6_3i5)
-   OSS FAQ
    -   [If I have activated Object Storage Service \(OSS\), are snapshots automatically saved to my OSS buckets?](/intl.en-US/Snapshots/Snapshot FAQ.md)
    -   [Can a custom image that was created from a snapshot be saved to an OSS bucket?](#section_agb_789_ug8)
-   Billing FAQ
    -   [How is the storage fee for snapshots calculated?](#section_svk_hax_cq5)
    -   [Where can I view a list of snapshot prices by Alibaba Cloud region?](#section_nom_iuk_an9)
    -   [What impact do overdue payments have on my stored snapshots?](#section_qs5_lyg_4gb)
    -   [I use snapshots frequently. How can I reduce the amount of fees incurred?](#section_75v_zgn_06k)
    -   [Is there a free tier for the snapshot service?](#section_h58_338_rau)
-   FAQ about snapshot and block storage type
    -   [Do automatic snapshots differ from or conflict with manual snapshots?](#section_vj5_5ws_ngb)
    -   [Can I create snapshots for local disks?](#section_8bp_ymj_xsh)
    -   [I have created a snapshot for an encrypted data disk and generated an image, but I cannot share the image. Why?](#section_m0o_tpa_pb2)
    -   [After an enhanced SSD \(ESSD\) is released, are its local snapshots deleted?](#section_pz2_64g_6th)
-   FAQ about snapshot size
    -   [How is the size of the first full snapshot of a disk calculated?](#section_h7p_t3y_viq)
    -   [Does deleting files from an ECS instance release storage space?](#section_akt_4yg_4gb)
    -   [Why is the size of a snapshot larger than the disk capacity displayed in the file system?](#section_rr2_pyg_4gb)
    -   [What is the relationship between a file system and a disk or a snapshot?](#section_tsa_qqu_wdx)
-   FAQ about snapshot deletion
    -   [How can I prevent snapshots from being deleted by Alibaba Cloud?](#section_wj5_5ws_ngb)
    -   [How can I delete snapshots to reduce backup costs?](#section_pjl_hqz_ngb)
    -   [Are automatic snapshots deleted after the system disk is changed, the instance expires, or the disk is released?](#section_ck5_5ws_ngb)
    -   [How can I delete snapshots that have been used to create images and disks?](#section_hji_juh_uhk)
    -   [Why does the system prompt "RequestId: xxx" is associated when I delete a snapshot in the snapshot chain?](#section_72i_6dy_wdp)
-   FAQ about automatic snapshot policy
    -   [If I have used an automatic snapshot to create a custom image or a disk, does the automatic snapshot policy fail to be executed?](#section_xj5_5ws_ngb)
    -   [Can I create multiple automatic snapshot policies for a disk?](#section_dx2_bzg_4gb)
-   FAQ about disk rollback by using snapshots
    -   [How can I avoid losing data due to incorrect operations?](#section_oou_9ap_jvp)
    -   [After I change the system disk, can I use a snapshot of the previous system disk to roll back the new system disk?](#section_hpz_qkh_mgb)
    -   [I created an instance in China \(Hangzhou\) and created snapshots for data disks of the instance. I purchased another instance in China \(Hangzhou\) after the previous one expired and was released. Can I use the snapshots to restore the previous instance?](#section_c7y_3ij_f53)
    -   [Why am I unable to use a snapshot to roll back a disk of an ECS instance?](#section_2sn_6vw_p3l)
-   FAQ about relationship between snapshots and images
    -   [What are the differences and relationships between snapshots and images?](#section_bmh_2xf_3ds)
    -   [How do I migrate snapshots from one account to another?](#section_ed5_k10_dzu)
    -   [Can I use a data disk snapshot to create a custom image?](#section_lyx_6pb_932)
    -   [Can I download or export ECS instance snapshots to a local device?](#section_1ff_9s6_3i5)
    -   [Why does the system prompt "RequestId: xxx" is associated when I delete a snapshot in the snapshot chain?](#section_72i_6dy_wdp)

## If I have activated Object Storage Service \(OSS\), are snapshots automatically saved to my OSS buckets?

No, snapshots are not automatically saved to existing OSS buckets. Snapshots are independently stored from your OSS buckets. You do not need to create new buckets for snapshots.

## Can a custom image that was created from a snapshot be saved to an OSS bucket?

Yes. You can export a custom image to your OSS bucket for future download. For more information, see [Export a custom image](/intl.en-US/Images/Custom image/Export a custom image.md). However, custom images cannot be directly saved to an OSS bucket.

## How is the storage fee for snapshots calculated?

Snapshots are billed on a pay-as-you-go basis. The price per GiB for snapshot storage is the same as that for the OSS Standard storage class. The pay-as-you-go billing is charged on a monthly basis. For more information about snapshot prices of various Alibaba Cloud regions, see the Pricing tab on the [Elastic Compute Service](https://www.alibabacloud.com/product/ecs) page.

For more information about examples of the pay-as-you-go billing method, see [Snapshot](/intl.en-US/Pricing/Billing items/Snapshot billing.md).

## Where can I view a list of snapshot prices by Alibaba Cloud region?

The price per GiB for snapshot storage is the same as that for the OSS Standard storage class. The pay-as-you-go billing is charged on a monthly basis. For more information about snapshot prices of various Alibaba Cloud regions, see the Pricing tab on the [Elastic Compute Service](https://www.alibabacloud.com/product/ecs) page. Scroll down to the **Snapshot Fee** section to view the price list based on the regions. You can also download the list of snapshot prices based on Alibaba Cloud regions in the CSV or JSON format by clicking **Download price**.

![Download price](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0865319951/p51569.png)

## What impact do overdue payments have on my stored snapshots?

The snapshot service is suspended 24 hours after your account payments become overdue. After your account has overdue payments:

-   In the first 15 days, snapshots that exceed the retention periods are deleted, and other snapshots are retained.
-   After 15 days, all snapshots are deleted except for those that have been used to create disks or custom images. The automatic snapshot policy is also deleted.

## I use snapshots frequently. How can I reduce the amount of fees incurred?

We recommend that you maintain a manageable number of snapshots, and delete snapshots that are no longer required. For more information, see [Reduce snapshot fees](/intl.en-US/Snapshots/Use snapshots/Reduce snapshot fees.md).

## Is there a free tier for the snapshot service?

No, you need to pay for the snapshot service. Snapshots start to incur fees after you create your first snapshot. For more information, see [Snapshot](/intl.en-US/Pricing/Billing items/Snapshot billing.md).

## Do automatic snapshots differ from or conflict with manual snapshots?

No, both manual and automatic snapshots are data files of a disk or at a specific point in time. However, you cannot create manual snapshots when automatic snapshots are being created. You must wait till the automatic snapshots are created.

## Can I create snapshots for local disks?

No. If you want to improve the availability of applications, we recommend that you use data redundancy at the application layer or create deployment sets for clusters.

## I have created a snapshot for an encrypted data disk and generated an image, but I cannot share the image. Why?

To ensure data privacy, custom images created from encrypted snapshots cannot be shared. We recommend that you use unencrypted snapshots to create custom images. This allows you to share these images with other users.

## After an enhanced SSD \(ESSD\) is released, are its local snapshots deleted?

Manual snapshots are never deleted by Alibaba Cloud regardless of whether the corresponding disk or instance has been released.

## How is the size of the first full snapshot of a disk calculated?

The first snapshot created for a disk is a full snapshot. This snapshot contains all the data stored on the disk at the time the snapshot is created. Therefore, the snapshot size is equal to the used capacity of the disk. For example, if the capacity of a disk is 200 GiB and 122 GiB has been used, the first full disk snapshot is 122 GiB in size. For more information, see [Incremental snapshots](/intl.en-US/Snapshots/Incremental snapshots.md) and [View the snapshot size](/intl.en-US/Snapshots/Use snapshots/View the snapshot size.md).

## Does deleting files from an ECS instance release storage space?

No, no storage space is released. When you delete files from an ECS instance, the space is not cleared on the disks. In this case, only tags are added to the headers of the deleted files.

## Why is the size of a snapshot larger than the disk capacity displayed in the file system?

-   Problem description: Assume that you create a snapshot after you deleted files from the ECS instance, but the size of the snapshot is not reduced or is larger than the disk capacity displayed in the file system.
-   Cause analysis: After snapshots are created, the system identifies empty blocks to reduce the size of the snapshot. However, these empty blocks are filled when you format the file system, delete files, or write data to blocks. Therefore, the snapshot size may be larger than the disk capacity that is currently displayed in the file system. Potential causes:
    -   File system metadata occupies disk space.
    -   During file system initialization, data is written into a large number of blocks that are equally divided from the logical block address \(LBA\). This write operation also occupies disk space.
    -   To improve performance, the file system only adds tags to the headers of files when the files are deleted. The disk cannot detect the deleting instruction. Therefore, the deleted data blocks are still allocated and copied to snapshots.
    -   The KVM virtio block and Xen block front drivers do not support the TRIM instruction, which indicates that data in the LBA is no longer in use and can be deleted. As a result, the disk cannot determine whether data can be deleted.

## What is the relationship between a file system and a disk or a snapshot?

You can create a file system in a disk partition. The file system manages disk space. These management tasks take the form of I/O requests in the disk. The disk records the status of data blocks and copies data to Object Storage Service \(OSS\). Snapshots are created in this process. The following figure shows the relationship between a file system and a snapshot.

![Relationship between a file system and a disk or a snapshot](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/0132984061/p39434.png)

**Note:** In the preceding figure, all data blocks that have data written to them are recorded in the snapshot. This applies even if the related files have been deleted from the disk. In the file system, only tags are added to the headers of files to be deleted but space is not cleared from disks.

## How can I prevent snapshots from being deleted by Alibaba Cloud?

-   Manual snapshots are never deleted by Alibaba Cloud regardless of whether the corresponding disk or instance has been released.
-   To prevent automatic snapshots from being deleted, you can set the **Keep Snapshots** parameter to **Always Keep** when you modify the automatic snapshot policy. Then, only the earliest snapshots are deleted when the quota limit of the snapshots is reached. For more information, see [Modify an automatic snapshot policy](/intl.en-US/Snapshots/Automatic snapshot policies/Modify an automatic snapshot policy.md). For more information about the snapshot quota, see [Limits](/intl.en-US/Product Introduction/Limits.md).

## How can I delete snapshots to reduce backup costs?

-   Manual snapshots: You can manually delete manual snapshots.
-   Automatic snapshots: You can manually delete automatic snapshots. When the maximum number of snapshots has been reached, the system also automatically deletes the earliest automatic snapshot.

## Are automatic snapshots deleted after the system disk is changed, the instance expires, or the disk is released?

-   If **Delete Automatic Snapshots While Releasing Disk** is selected for the automatic snapshot policy, automatic snapshots are deleted when the corresponding instance or disk is released.
-   If **Delete Automatic Snapshots While Releasing Disk** is not selected for the automatic snapshot policy, the retention period specified by the automatic snapshot policy applies. You can modify the automatic snapshot policy. For more information see [Modify an automatic snapshot policy](/intl.en-US/Snapshots/Automatic snapshot policies/Modify an automatic snapshot policy.md).

## How can I delete snapshots that have been used to create images and disks?

-   You can delete snapshots that have been used to create disks. After a snapshot is deleted, you cannot perform operations based on the status of the original snapshot data, such as the operation to re-initialize the system disk. For more information, see [Reinitialize a system disk](/intl.en-US/Block Storage/Cloud disks/Reinitialize a cloud disk/Re-initialize a system disk.md).
-   If the snapshot has been used to create custom images, you must delete those custom images before you can delete the snapshot.
-   You can delete images that have been used to create instances. After an image is deleted, you cannot perform operations based on the status of the original snapshot data, such as the operation to re-initialize the system disk. For more information, see [Reinitialize a system disk](/intl.en-US/Block Storage/Cloud disks/Reinitialize a cloud disk/Re-initialize a system disk.md).

## If I have used an automatic snapshot to create a custom image or a disk, does the automatic snapshot policy fail to be executed?

No, the automatic snapshot policy does not fail to be executed.

## Can I create multiple automatic snapshot policies for a disk?

No, you cannot create multiple automatic snapshot policies for a disk.

## How can I avoid losing data due to incorrect operations?

You can create snapshots to back up data before you perform high-risk operations. For example, you can create a snapshot if you need to modify critical system files, migrate instances from the classic network to a VPC, back up data, or restore an instance that was released by mistake. You can also create a snapshot to prevent network attacks, change operating systems, or provide data support for a production environment. If an error occurs, you can roll back the disk to reduce risks. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md) and [Roll back a disk by using a snapshot](/intl.en-US/Snapshots/Use snapshots/Roll back a disk by using a snapshot.md).

## After I change the system disk, can I use a snapshot of the previous system disk to roll back the new system disk?

No, you cannot use a snapshot of the previous system disk to roll back the new system disk.

## I created an instance in China \(Hangzhou\) and created snapshots for data disks of the instance. I purchased another instance in China \(Hangzhou\) after the previous one expired and was released. Can I use the snapshots to restore the previous instance?

No, if you want to use snapshots to restore an instance, you must make sure that the instance from which the snapshots were created is not released. You can use one of the snapshots of the original data disk to create a disk and attach the new disk to the new instance. For more information, see [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md) and [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).

## Why am I unable to use a snapshot to roll back a disk of an ECS instance?

You can check the snapshot based on the returned error message. For more information about the common issues and solutions regarding snapshots to roll back disks, see [Block Storage FAQ](/intl.en-US/Block Storage/Block Storage FAQ.md).

## What are the differences and relationships between snapshots and images?

The following section describes the differences between snapshots and images:

-   Images can be directly used to create ECS instances, but snapshots cannot.
-   Images can be used to restore instance data across regions, but snapshots cannot. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).
-   A snapshot can be a data backup of the system disk or a data disk of an ECS instance. However, an image must contain the system disk data of an ECS instance.
-   You can use snapshots to back up data on a disk, and use images to create one or more ECS instances.

The following section describes the relationships between snapshots and images:

-   When you create a custom image from an instance, ECS creates a snapshot for each disk of the instance. The created custom image contains the snapshots of all the disks of this ECS instance. For more information, see [Create a custom image from an instance](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from an instance.md).
-   You can also create custom images by using system disk snapshots. For more information, see [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md).

## How do I migrate snapshots from one account to another?

Snapshots cannot be migrated. You can create an image from the snapshot that you want to migrate and share the image with another account. For more information, see [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md) and [Share or unshare custom images](/intl.en-US/Images/Custom image/Share or unshare custom images.md).

To migrate a data disk snapshot from Account A to Account B, perform the following operations:

1.  Create an image from the original instance of the data disk snapshot. For more information, see [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md).
2.  Share the image to Account B. For more information, see [Share or unshare custom images](/intl.en-US/Images/Custom image/Share or unshare custom images.md).
3.  In Account B, use the image to create a pay-as-you-go instance. For more information, see [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md).
4.  Create a snapshot from a data disk of the new instance. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).
5.  Release the new instance. For more information, see [Release an instance](/intl.en-US/Instance/Manage instances/Release an instance.md).

## Can I use a data disk snapshot to create a custom image?

No, the snapshot that is used to create a custom image must be a snapshot of a system disk.

## Can I download or export ECS instance snapshots to a local device?

No, snapshots cannot be downloaded or exported to a local device. You can create an image from a system disk snapshot and then export the image. For more information, see [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md) and [Export a custom image](/intl.en-US/Images/Custom image/Export a custom image.md). You can also use the Operation Orchestration Service \(OOS\) template named [ACS-ECS-BulkyCreateAndExportImage](https://oos.console.aliyun.com/cn-hangzhou/template/public/detail/ACS-ECS-BulkyCreateAndExportImage) to create multiple custom images at a time and export the images to an OSS bucket in a specific region. Then, you can download the custom images in the OSS console.

## Why does the system prompt "RequestId: xxx" is associated when I delete a snapshot in the snapshot chain?

Your snapshot was used to create a custom image. You must delete the custom image before you can delete the snapshot. For more information, see [Delete a custom image](/intl.en-US/Images/Custom image/Delete a custom image.md).

