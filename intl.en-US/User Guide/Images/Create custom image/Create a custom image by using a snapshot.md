# Create a custom image by using a snapshot {#concept_gpg_t5l_xdb .concept}

Custom images allow you to create multiple ECS instances with identical OS and environment data.

Custom images are based on ECS disk snapshots. You can set up identical or different configurations for ECS instances that are created from images.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9696/15504763934584_en-US.png)

You can also use an instance to create an image. For more information, see [create a custom image by using an instance](reseller.en-US/User Guide/Images/Create custom image/Create a custom image by using an instance.md#).

To enhance the security of custom images created from snapshots, see [security suggestions for Alibaba Cloud custom images](https://partners-intl.aliyun.com/help/faq-detail/54903.htm?spm=a2c63.q38357.a3.3.358654ffzwageD).

**Note:** 

-   Custom images cannot be used across regions.
-   You can change the operating system of an instance created from a custom image, and the custom image remains usable. For details, see [change the system disk \(custom image\)](reseller.en-US/User Guide/Cloud disks/Replace the system disk (non-public image).md#).
-   You can upgrade the instance created from a custom image, including upgrading the CPU, memory, bandwidth, and disks.
-   Custom images are created independently from the billing methods of the instances from which they were created. For example, custom images created from Subscription instances can used for creating Pay-As-You-Go instances. The converse method also applies.
-   If the ECS instance used for creating a custom image expires, or the data is erased \(that is, the system disk used for the snapshot expires or is released\), the custom image and the ECS instances created from the custom image are not affected. However, automatic snapshots are cleared when an ECS instance is released.

## Restrictions for Linux instances {#section_tx3_vvl_xdb .section}

-   Do not load data disk information in the /etc/fstab file. Otherwise, instances created using this image cannot start.
-   We recommend that you umount all data disks before creating a custom image, and then use a snapshot to create a custom image. Otherwise, ECS instances that are created based on this custom image may not start.
-   Do not upgrade the kernel or operating system version.
-   Do not change the system disk partitions. The system disk only supports single root partitions.
-   We recommend you check the available space of the system disk to make sure that the system has available space.
-   Do not modify critical system files such as /sbin, /bin, /lib, and so on.
-   Do not modify the default logon user name root.

## Procedure {#section_p1r_rwl_xdb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Select the region.
3.  In the left-side navigation pane, click **Instances**.
4.  Find the target instance and click its instance ID, or click **Manage** in the **Actions** column.
5.  In the left-side navigation pane, click **Instance Snapshots**. Find the target system disk and then click **Create Custom Image** in the **Actions** column.

    The snapshot must be created from system disks. Data disks cannot be used to create custom images. 

    You can also click **Snapshots and Images** \> **Snapshots**, and select a snapshot created from a system disk to **Create Custom Image**.

6.  In the Create Custom Image dialog box, complete the following:
    -   Confirm the snapshot ID.
    -   Enter a name and description of the custom image.
    -   Optional. Check **Add Data Disk Snapshot**, select multiple snapshots of data disks for the image, and click **Add** to add a data disk.

        **Note:** 

        -   We recommend that you remove sensitive data from the data disk before creating a custom image to guarantee data security.
        -   If the snapshot disk capacity is left blank, an empty disk is created with the default capacity of 5 GiB.
        -   If you select available snapshots, the disk size is the same as the size of the snapshots. 
        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9696/15504763934594_en-US.png)

7.  Click **Create**. Then, in the left-side navigation pane, select **Snapshots and Images** \> **Images** to view the images you have created.

## Linux instance image FAQ {#section_jwm_ryl_xdb .section}

**How to umount a disk and delete disk table data?**

If `/dev/hda5` is attached to `/mnt/hda5`, run any of the following three commands to detach the file system.

```
umount/dev/hda5
umount/mnt/hda5
umount/dev/hda5/mnt/hda5
```

`/etc/fstab` is an important configuration file in Linux. It contains the details of mounting the file system and storage devices upon startup. If you do not want to mount a specified partition when starting the instance, delete the corresponding lines from `/etc/fstab`. For example, you can delete the following statement to disconnect xvdb1 upon startup: `/dev/xvdb1 /leejd ext4 defaults 0 0`.

**How to determine whether a data disk is detached and a custom image can be created?**

You must make sure that the statement line for automatically attaching mounting data disk has been deleted from the fstab file.

Use the mount command to view the information of all mounted devices. Make sure that the execution results do not contain the information of the data disk partition.

**Relevant configuration files**

Before creating an image, make sure that the key configuration files listed in the following table have not been modified. Otherwise, the new instance cannot start.

|Configuration file|Related to|Risks if modified|
|:-----------------|:---------|:----------------|
|`/etc/issue*`, `/etc/*-release`, and `/etc/*_version`|System release version|Modifying /etc/issue\* makes the system release version unidentifiable, which can cause instance creation failure.|
|`/boot/grub/menu.lst` and `/boot/grub/grub.conf`|System startup|Modifying /boot/grub/menu.lst results in kernel loading failure, which means the system cannot start.|
|/etc/fstab|Partitions upon startup|Modifying /etc/fstab causes partition mounting failure, which means the system cannot start.|
|/etc/shadow|System passwords|If this file is set to read-only, the password file cannot be edited, which means instance creation fails.|
|/etc/selinux/config|System security policies|Modifying /etc/selinux/config and enabling SELinux results in start failure.|

