# Replace the system disk by using a public image {#concept_n4k_x3j_ydb .concept}

This topic describes how to replace the system disk by using a public image.

## Scenarios {#section_j44_1ph_qgb .section}

We recommend that you replace the system disk in the following scenarios:

-   You selected an incorrect OS when creating an ECS instance.
-   You need to replace the current OS.

To replace the system disk, you can replace the disk image with a public image, shared image, custom image, or any other image found on the Alibaba Cloud Marketplace. This topic uses a public image as an example. If you need to use an image that is not a public image, see [Replace the system disk \(non-public image\)](reseller.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

After you replace the system disk:

-   A new system disk with a new ID is allocated to your instance, and the original system disk is released.
-   The cloud disk type remains unchanged.
-   The IP address and the MAC address remain unchanged.
-   We recommend that you [delete snapshots or automatic snapshot policies](reseller.en-US/Snapshots/Use snapshots/Manage snapshots.md#) to ensure that you have sufficient snapshots available for the automatic snapshot policies of the new system disk.

## Precautions {#section_h1y_y3j_ydb .section}

**Note:** Microsoft has ended extended technical support for Windows Server 2003. For data security purposes, we recommend that you discontinue running Windows Server 2003 on your ECS instances, and update the OS running on your instances. Alibaba Cloud no longer provides an image of this OS. For more information, see [Offline announcement of Windows Server 2003 system image](https://partners-intl.aliyun.com/help/faq-detail/59513.htm).

**Risks** 

Replacing the system disk may involve the following risks:

-   The original system disk will be released. Therefore, we recommend that you [create a snapshot](http://icms.alibaba-inc.com/document/content/1243?version=274&topic=9687) to back up your data before replacing the system disk.

-   Your instance will be stopped and your services interrupted.

-   You must redeploy the service environment on the new system disk. However, this may result in an interruption to your services.

-   The disk ID will be changed. Therefore, snapshots of the original system disk cannot be used to roll back the new system disk.

    **Note:** 

    After you replace the system disk, the snapshots you have manually created are not affected. You can still use them to create custom images.

    If you have configured automatic snapshot policies for the original system disk to allow automatic snapshots to be released along with the disk, the snapshot policies will no longer apply. All automatic snapshots of the original system disk will be automatically deleted.


**Precautions during cross-OS disk replacements** 

Cross-OS disk replacements refer to replacing the system disk from one OS to another, specifically a switch between Linux and Windows.

**Note:** Regions outside Mainland China do not support disk replacements between Linux and Windows, but they do support disk replacements between different Linux or Windows editions.

During cross-OS disk replacements, the file format of the data disk may be unidentifiable.

-   In case no important data exists on the data disk, we recommend that you [reinitialize the disk](reseller.en-US/Block Storage/Block storage/Reinitialize a cloud disk.md#) and format it to the default file system of your OS.

-   In case important data exists in your data disk, perform the following operations as required:

    -   For switches from Windows to Linux, you must install a software application, such as NTFS-3G, because Linux cannot identify NTFS.
    -   For switches from Linux to Windows, you also must install a software application, such as Ext2Read or Ext2Fsd, because Windows cannot identify ext3, ext4, or XFS.

**Precautions during Windows OS replacements**

-   Windows OS only supports password authentication.

**Note:** Linux OS supports password authentication and SSH key pair authentication. As a result, when you replace Windows OS with Linux OS on your instance, you will have more optional authentication methods.

-   If you are using a non-I/O-optimized instance, you can only replace your OS with the following Windows Server OSs by calling [ReplaceSystemDisk](../reseller.en-US/API Reference/Disk/ReplaceSystemDisk.md#).

|OS version|Image ID|
|:---------|:-------|
|Windows Server 2008 R2 Enterprise Edition \(English\)|win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20170915.vhd|
|Windows Server 2008 R2 Enterprise Edition \(Chinese\)|win2008r2\_64\_ent\_sp1\_zh-cn\_40G\_alibase\_20170915.vhd|
|Windows Server 2012 R2 Datacenter Edition \(Chinese\)|win2012r2\_64\_dtc\_17196\_zh-cn\_40G\_alibase\_20170915.vhd|
|Windows Server 2012 R2 Datacenter Edition \(English\)|win2012r2\_64\_dtc\_17196\_en-us\_40G\_alibase\_20170915.vhd|
|Windows Server 2016 Datacenter Edition \(Chinese\)|win2016\_64\_dtc\_1607\_zh-cn\_40G\_alibase\_20170915.vhd|
|Windows Server 2016 Datacenter Edition \(English\)|win2016\_64\_dtc\_1607\_en-us\_40G\_alibase\_20170915.vhd|


## Preparations {#section_n1y_y3j_ydb .section}

-   Make sure that there is sufficient system disk space. We recommend that you reserve 1 GiB. Otherwise, the OS may not properly start after system disk replacement.

-   If you want to replace the OS to Linux and use an SSH key pair for authentication, you need to [create an SSH key pair](reseller.en-US/Security/Key pairs/Use an SSH key pair.md#) first.

-   System disk replacement may lead to data loss or service interruption. To minimize the impact on your services, we recommend that you [create a snapshot](reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) for the original system disk during off-peak hours before starting the replacement process.

    **Note:** Creating a snapshot of 40 GiB takes about 40 minutes the first time. Creating a snapshot may also reduce I/O performance of a block storage device by up to 10%.


## Procedure {#section_p1y_y3j_ydb .section}

To replace the system disk, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  In the **Actions** column of the target instance, choose **More** \> **Instance Status** \> **Stop** and stop the instance as prompted.

    **Note:** If the instance is a Pay-As-You-Go VPC instance with the **No Fees for Stopped Instances** function enabled, the instance may not be properly started after system disk replacement. We recommend that you disable this function when you stop the instance.

4.  From the **Actions** column, choose **More** \> **Disk and Image** \> **Replace System Disk**.
5.  In the displayed dialog box, read the precautionary statement about system disk replacement and then click **OK**.
6.  On the Replace System Disk page, set the following parameters:
    1.  **Image Type**: Select **Public Image** and then select the image version.
    2.  **System Disk**: Unchangeable. However, you can expand the disk space to meet the requirements of your system disk and services. The maximum disk space is 500 GiB. The minimum disk space you can configure depends on the current disk space and image type.

        |Image|Space range \(GiB\)|
        |:----|:------------------|
        |Linux \(excluding CoreOS\) + FreeBSD|\[Max\{20, current space of the system disk\}, 500\]|
        |CoreOS|\[Max\{30, current space of the system disk\}, 500\]|
        |Windows|\[Max\{40, current space of the system disk\}, 500\]|

        **Note:** If you have renewed your instance and downgraded the configurations, the system disk space cannot be changed until the next billing cycle starts.

    3.  **Security enhancement**:
        -   If the new OS is Windows, you can only select password for the authentication.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9682/15623087395517_en-US.png)

        -   If the instance is an I/O optimized instance and the new OS is Linux, you can select key pair, password, or set after change. In this case, we recommend you to bind an SSH key pair, if needs must refer to [create an SSH key pair](reseller.en-US/Security/Key pairs/Use an SSH key pair.md#).

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9682/15623087395518_en-US.png)

    4.  Confirm **Instance Cost**, which includes the image fee and system disk fee. For more information, see the pricing page of ECS.
    5.  Check your settings and click **Confirm to change**.

Replacing the OS and updating the system status take about 10 minutes. After the OS is replaced, the instance automatically starts.

## What to do next {#section_bby_y3j_ydb .section}

After replacing the system disk, perform the following operations as needed:

-   \(Optional\) [Apply automatic snapshot policies to disks](reseller.en-US/Snapshots/Use snapshots/Apply automatic snapshot policies to disks.md#). Automatic snapshot policies are bound to the disk ID. After the system disk is replaced, automatic snapshot policies applied on the original disk will fail automatically. Therefore, you need to configure automatic snapshot policies for the new system disk.

-   Write the new partition information to the /etc/fstab file of the new system disk and mount the partition as follows:

**Note:** If the OS before and after disk replacement is Linux, and if a data disk is mounted to the instance and the partition is set to be mounted automatically at instance startup, then all mounting information will be lost. For more information, see [Format and mount data disks for Linux instances](../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).

    1.  Back up the /etc/fstab file.
    2.  Write information about the new partition to the /etc/fstab file.
    3.  Check the information in the /etc/fstab file.
    4.  Run the `mount` command to mount the partition.
    5.  Run the `df-h -h` command to check the file system space and usage.

        After the data partition is mounted, the data disk is ready for use without the need for instance restart.


## Related API {#section_eby_y3j_ydb .section}

[ReplaceSystemDisk](../reseller.en-US/API Reference/Disk/ReplaceSystemDisk.md#)

