---
keyword: [snapshots and images, paid image, ECS instance migration, replace an image, select an operating system, ]
---

# Image FAQ

This topic provides answers to frequently asked questions about Elastic Compute Service \(ECS\) images.

-   Common FAQ
    -   [Can I replace the selected image of an ECS instance?](#section_ovb_trx_fhb)
    -   [Do the system disks of ECS instances support Key Management Service \(KMS\) encryption? How do I use KMS encryption based on Terraform or Packer?](#section_bjd_h5l_93s)
    -   [What are the differences between snapshots and images? How are snapshots and images related?](#section_bmh_2xf_3ds)
    -   [Which instance families do Red Hat Enterprise Linux \(RHEL\) images support?](#section_kv6_hyb_55i)
    -   [How do Windows versions differ in terms of memory limits?](#section_yd4_b0j_p8u)
-   FAQ about custom images
    -   [Can I use a snapshot of a data disk to create a custom image?](#section_lyx_6pb_932)
    -   [How do I view data disk usage?](#section_hrq_fgx_fhb)
    -   [How do I unmount file systems and delete disk table data?](#section_lzy_rgx_fhb)
    -   [How do I confirm that a data disk has been unmounted and that a new custom image can be created?](#section_wdy_3ty_dhb)
    -   [Does a custom image still exist after the instance from which the image was created is released?](#section_qbd_ghx_fhb)
    -   [When an instance expires or its data is deleted, are custom images that were created from the instance affected? Are instances created from the custom images affected?](#section_zc5_shx_fhb)
    -   [Can I replace the operating system of an instance created from a custom image? Can the custom image still be used after the operating system is replaced?](#section_j1z_thx_fhb)
    -   [Can I select a custom image with a different operating system when I replace the system disk of an instance?](#section_b21_zhx_fhb)
    -   [Can I use a custom image to overwrite the system disk data of an ECS instance?](#section_cv1_g3x_fhb)
    -   [Can I upgrade the CPU, memory, bandwidth, and hard disks of an ECS instance that was created from a custom image?](#section_y35_m3x_fhb)
    -   [Can I use a custom image across regions?](#section_twm_n3x_fhb)
    -   [Can a custom image created from a subscription instance be used to create a pay-as-you-go instance?](#section_t5m_cjx_fhb)
    -   [I created an ECS instance from a custom image and specified a system disk capacity greater than that in the image. However, the system disk capacity of the new ECS instance is the same as that in the image. What do I do?](#section_oqc_u0t_5ri)
    -   [Why do I need to comment out mount entries when I create a custom image or an instance?](#section_uar_ern_zbt)
    -   [How do I configure and use a private Docker image registry?](#section_4wu_r5p_bi1)
    -   [How do I clone an ECS instance?](#section_wnw_26f_axp)
    -   [Some custom images cannot be used to create I/O optimized instances. What do I do?](#section_nvl_tpi_ffj)
    -   [Where do I view the progress of an image import task? How long does it take to import an image?](#section_o5a_k1v_smp)
    -   [Where do I view the progress of an image creation task? How long does it take to create an image?](#section_ioj_atj_1te)
-   FAQ about copying images
    -   [When do I need to copy a custom image?](#section_pbs_h4c_ghb)
    -   [Which images can be copied?](#section_j4j_n4c_ghb)
    -   [Which regions support copying custom images?](#section_jcb_44c_ghb)
    -   [How long does it take to copy a custom image?](#section_wzx_44c_ghb)
    -   [How am I charged when I copy a custom image?](#section_nbz_q4c_ghb)
    -   [What limits apply to the original image \(image copied\) and the new image \(image copy\) during an image copy process?](#section_inj_s4c_ghb)
    -   [How do I copy images within my Alibaba Cloud account to other regions within other Alibaba Cloud accounts?](#section_kyv_54c_ghb)
    -   [Do size limits apply to copying an image?](#section_k14_x4c_ghb)
    -   [Can I copy a custom image derived from an Alibaba Cloud Marketplace image across regions?](#section_1w2_og0_5js)
    -   [How do I migrate data from regions outside mainland China to regions inside mainland China?](#section_oqq_9z9_t00)
-   FAQ about sharing images
    -   [How many images can be shared to me?](#section_xry_y4c_ghb)
    -   [How many users can an image be shared to?](#section_pwp_ypc_ghb)
    -   [I have accounts on different Alibaba Cloud sites. Can I share images between these accounts?](#section_jeb_xr5_8wn)
    -   [Do shared images accrue towards my image quota?](#section_agd_2qc_ghb)
    -   [Do geographical limits apply when shared images are used to create instances?](#section_mls_2qc_ghb)
    -   [What are the risks of creating an instance from a shared image?](#section_p4w_lqc_ghb)
    -   [What risks may arise if I share a custom image to other accounts?](#section_r4q_nqc_ghb)
    -   [After an account shares an image to me, can I share this image to another account?](#section_abm_4qc_ghb)
    -   [After I share an image, can I still use this image to create an instance?](#section_xny_pqc_ghb)
    -   [Can an image created from Instance A in one region be used by Instance B in a different region?](#section_b5i_fn9_i06)
-   FAQ about importing images
    -   [Is Bring Your Own License \(BYOL\) supported when I import custom images?](#section_dhc_07k_xgz)
    -   [What types of licenses can be used when I import custom images?](#section_988_25j_qkp)
    -   [How are the imported BYOL images charged?](#section_bn1_o19_a61)
    -   [How are BYOL licenses authenticated and subscribed by using Alibaba Cloud when their subscriptions expire?](#section_gko_ai0_s3o)
-   FAQ about exporting images
    -   [I want to export an image to my computer for testing. What do I do?](#section_9dl_9cs_oba)
    -   [Can an image exported from ECS be started on other platforms?](#section_l7x_6jq_hh9)
-   FAQ about deleting images
    -   [Can I delete a custom image after it is used to create an ECS instance?](#section_lvj_dht_8a4)
    -   [Can I delete a custom image from my account after the image is shared to another account?](#section_fqt_49s_s3v)
    -   [What happens if I unshare Custom Image M to Account A?](#section_qn6_1dm_1tn)
    -   [Why am I prompted with a message similar to "The specified image cannot be deleted because it is associated with instances" when I attempt to delete an image?](#section_qe9_38d_hvk)
-   FAQ about replacing images or operating systems
    -   [When I replace a system disk, can I select an image that contains data disk snapshots?](#section_053_0tw_h6a)
    -   [I want to replace the operating system of my ECS instance by using an existing image. What do I do?](#section_69i_52e_jfd)
    -   [Can I use an image created from an instance within Account A to replace a system disk within Account B?](#section_oww_crp_0j9)
-   FAQ about image pricing
    -   [I am creating an ECS instance. Why is the total instance cost displayed when I select a custom image higher than that displayed when I select a public image?](#section_k04_yg7_uoa)
-   FAQ about the commercial availability of images
    -   [What features do Alibaba Cloud Marketplace images provide?](#section_8wl_8ju_9pi)
    -   [What are the benefits of Alibaba Cloud Marketplace images?](#section_c0p_y2e_36h)
    -   [What server environments and scenarios do Alibaba Cloud Marketplace images support?](#section_4aa_s13_huj)
    -   [Are Alibaba Cloud Marketplace images safe?](#section_hng_971_32q)
    -   [What do I do if I encounter a problem when I am installing or using an Alibaba Cloud Marketplace image?](#section_jyl_7r1_85r)
    -   [How do I purchase an Alibaba Cloud Marketplace image?](#section_hxc_rqc_ghb)
    -   [How long can I use a purchased image?](#section_hqw_prc_ghb)
    -   [Are Alibaba Cloud Marketplace images refundable?](#section_gzm_qrc_ghb)
    -   [Are free Alibaba Cloud Marketplace images still available after Alibaba Cloud Marketplace images are commercially available?](#section_okl_src_ghb)
    -   [I bought an Alibaba Cloud Marketplace image in the China \(Hangzhou\) region. Can I use it to create an ECS instance or replace a system disk in the China \(Beijing\) region?](#section_ndz_src_ghb)
    -   [I have an instance created from an Alibaba Cloud Marketplace image. Do I need to make further payments for the image when I renew the instance or upgrade the configurations of the instance?](#section_jwc_fsx_fhb)
    -   [I have an ECS instance created from an Alibaba Cloud Marketplace image. After the instance is released, can I continue to use that image free of charge when I purchase another ECS instance?](#section_yqb_wrc_ghb)
    -   [I created an ECS instance from an Alibaba Cloud Marketplace image and then created a custom image from the instance. Do I need to pay for the custom image when I use it to create an ECS instance?](#section_pnn_yrc_ghb)
    -   [If I copy an Alibaba Cloud Marketplace image that I bought to another region to create an ECS instance, do I need to pay for the image?](#section_bqm_zrc_ghb)
    -   [I created an ECS instance from an Alibaba Cloud Marketplace image and then created a custom image from that instance. If I share the custom image to Account B, does Account B need to pay for the custom image when it uses this image to create an ECS instance?](#section_ymk_1sc_ghb)
    -   [Is a fee charged if I replace a system disk by using an Alibaba Cloud Marketplace image or an image derived from an Alibaba Cloud Marketplace image?](#section_uj5_1sc_ghb)
    -   [My ECS instance is using an Alibaba Cloud Marketplace image. Is a fee charged if I replace the system disk of the instance?](#section_nj4_bsc_ghb)
    -   [How do I call an ECS API operation to use an Alibaba Cloud Marketplace image or a custom or shared image that derives from an Alibaba Cloud Marketplace image to create an ECS instance or replace a system disk?](#section_xl1_csc_ghb)
    -   [If I do not purchase an Alibaba Cloud Marketplace image or an image that derives from an Alibaba Cloud Marketplace image, is an error reported when I call an ECS API operation to use the image to create an ECS instance or replace a system disk?](#section_sxt_hsc_ghb)
    -   [I have configured a scaling group for which the minimum number of instances is set to 10 and the maximum number of instances is set to 100. What do I do with Alibaba Cloud Marketplace images to ensure that ECS instances are created to meet my computing needs?](#section_nfx_5sc_ghb)
    -   [Can I purchase multiple Alibaba Cloud Marketplace images at a time?](#section_clp_ysc_ghb)
    -   [If an image \(such as jxsc000010 or jxsc000019\) in use in an active scaling configuration no longer exists in Alibaba Cloud Marketplace, what do I do to ensure that ECS instances can continue to be created based on the scaling configuration in the corresponding scaling group?](#section_stt_zsc_ghb)
    -   [Can one product code support images in different regions?](#section_os3_btc_ghb)
    -   [I bought 100 images that have the same product code. Can I use the images within all regions?](#section_uzj_ctc_ghb)
    -   [After I select I/O Optimized, I cannot select Alibaba Cloud Marketplace images when I purchase an ECS instance. What is the cause and how can I solve this problem?](#section_tch_39p_cv5)
-   FAQ about subscription Alibaba Cloud Marketplace images
    -   [What are yearly, monthly, and weekly subscription Alibaba Cloud Marketplace images?](#section_zxy_n5c_ghb)
    -   [On which ECS instances can I use a subscription image?](#section_fts_45c_ghb)
    -   [How do I purchase a subscription image? Can I separately purchase it?](#section_rfp_s5c_ghb)
    -   [How do I pay for subscription images?](#section_xhj_w5c_ghb)
    -   [Can I use a subscription image after it expires? How do I continue to use it?](#section_cc4_x5c_ghb)
    -   [After I purchase a subscription image, can I request a refund if I no longer want to use it?](#section_gwb_z5c_ghb)
    -   [What can I expect when a refund is made?](#section_hvt_z5c_ghb)
    -   [Can a subscription image be converted into a pay-as-you-go image?](#section_hpg_1vc_ghb)
    -   [Can I replace a subscription image with an image of another type or vice versa? How is the fee calculated?](#section_sqw_1vc_ghb)
    -   [Where do I view and manage the subscription images that I purchased?](#section_fmx_fvc_ghb)
    -   [Is a fee charged for a custom image derived from a subscription image? How is the custom image affected if the subscription image expires?](#section_klq_gvc_ghb)
-   FAQ about ECS instances and operating system images
    -   [Why am I unable to use an SSH key pair that uses the ssh-rsa signature algorithm to connect to an instance that runs Fedora 33 64-bit?](#section_pn6_cmc_lji)
    -   [How do I install patches and compile the kernel on FreeBSD?](#section_pyg_sg6_555)
    -   [Why does the load average become high on ECS instances that run Ubuntu operating systems of specific versions after the Server Guard \(AliYunDun\) process is started on the instances?](#section_5cs_9h3_ty6)
    -   [Why am I unable to select a Windows operating system for ECS instances?](#section_ajg_qwc_ghb)
    -   [Does Alibaba Cloud support Windows Server 2008 and Windows Server 2008 R2?](#section_790_hza_ttg)
    -   [The operating system of my instance is Windows Server. I am prompted with a message indicating that the operating system is not genuine. What do I do?](#section_44i_ufz_9m1)
    -   [Are fees charged for the images used by ECS instances?](#section_ttw_qwc_ghb)
    -   [Can I install or upgrade the operating systems of ECS instances on my own?](#section_zhs_twc_ghb)
    -   [Do operating systems have graphical interfaces?](#section_ulp_xwc_ghb)
    -   [How do I choose an operating system?](#section_wqy_zwc_ghb)
    -   [Do public images come with the FTP service?](#section_jtv_dxc_ghb)
    -   [Which SUSE versions do Alibaba Cloud public images support?](#section_mgc_fxc_ghb)
    -   [What service support is available for SUSE operating systems?](#section_jpr_fxc_ghb)
    -   [If an image was manually created from an ECS instance, can I retrieve the instance data after the instance is released on expiration?](#section_uj1_il5_0xb)
    -   [I have an ECS instance and I want to create another ECS instance from the image of this existing ECS instance. What do I do?](#section_d2a_pl9_3vq)
    -   [I have purchased an ECS instance. How do I restore my shared image to the newly purchased instance?](#section_54f_mg4_r2p)
    -   [I have multiple Alibaba Cloud accounts. I want to transfer an instance from Account A to Account B or migrate the environment and applications of an instance within Account A to an instance within Account B. What do I do?](#section_cvk_0gm_ods)
    -   [How do I migrate data between ECS instances?](#section_pkf_2xq_13z)
    -   [Can ECS instances in different VPCs communicate with each other?](#section_lqt_tci_xa6)
    -   [How do I handle a CentOS DNS resolution timeout?](#section_x8y_les_u5u)
    -   [Why does ECS disable virtual memory and leave swap partitions unconfigured by default?](#section_m02_5j5_qf2)
    -   [How do I enable the kdump service in a public image?](#section_kwb_4l4_a16)
    -   [How do I obtain the dump file for RHEL images?](#section_a8i_3s9_rc8)
    -   [How do I enable the kdump service on an instance that uses a Red Hat 8.1 image?](#section_boi_ntx_xq0)
    -   [Red Hat 8.1 and Red Hat 8.2 images start slowly on ECS bare metal instances. How do I solve this issue?](#section_lns_how_l2p)
    -   [How do I enable or disable the Meltdown and Spectre patches for Linux images?](#section_mf9_75m_jnp)
    -   [After I use a CentOS or Windows ECS instance for an extended period of time without restarting it, the instance is disconnected from the network, the network is no longer available, or the public or private IP address of the instance cannot be pinged. What do I do?](#section_29l_kc7_8hw)
    -   [The "UNEXPECTED INCONSISTENCY; RUN fsck MANUALLY." error is reported when an ECS instance starts. What do I do?](#section_1qr_p2r_fp0)
    -   [How do I upgrade RHEL 7 to RHEL 8?](#section_d8g_9su_f1e)
    -   [How do I enable a program to distinguish ECS instances when I deploy my business?](#section_n0c_nxo_1hi)

## Can I replace the selected image of an ECS instance?

Yes, you can replace the image of your ECS instance by selecting Replace System Disk in the ECS console. Be aware that if you replace the image of an instance, data stored on the system disk of the instance is lost. Make sure that you back up your data before you replace the image. For more information, see [Change the operating system](/intl.en-US/Images/Change the operating system.md).

## Do the system disks of ECS instances support Key Management Service \(KMS\) encryption? How do I use KMS encryption based on Terraform or Packer?

-   Yes, the system disks of ECS instances can be encrypted by using bring your own keys \(BYOKs\) and CMKs stored in KMS. For more information, see [Encryption overview](/intl.en-US/Block Storage/Encrypt a disk/Encryption overview.md).
-   Support for Packer-based encryption will be added soon.
-   In Terraform, you can set the encrypted parameter to enable or disable KMS encryption. For more information, see [alicloud\_disks](https://www.terraform.io/docs/providers/alicloud/d/disks.html).

## What are the differences between snapshots and images? How are snapshots and images related?

Images and snapshots differ in the following ways:

-   Images can be used to create ECS instances, whereas snapshots cannot.
-   A snapshot can be a data backup of the system disk or a data disk of an ECS instance, whereas an image must contain the system disk data of an ECS instance.
-   Snapshots can be used only to restore data of disks on existing instances, whereas images can be used to replace the system disks of other instances or create instances.
-   Images and snapshots suits different scenarios. The following section describes some scenarios for which snapshots and custom images are suitable:

    Snapshots can be used to:

    -   Back up data on a regular basis. You can use automatic snapshot policies to automatically create snapshots to back up data on a daily, weekly, or monthly basis.
    -   Temporarily back up data. Examples:
        -   You can manually create a snapshot to back up the system data before a temporary system change such as system update or application release.
        -   You can create a snapshot to back up data before you resize a system disk.
        -   To migrate data from a disk, you can create a snapshot for the disk and use the snapshot to create a disk.
    Custom images can be used to:

    -   Back up systems that do not change in a short term, such as released or updated application systems.
    -   Create ECS instances. For example, you can use a custom image to create an ECS instance that has multiple applications deployed.
    -   Migrate systems and data. For example, you can migrate ECS instances from the classic network to VPCs.
    -   Restore systems across regions and zones.

Snapshots and images have the following relationships:

-   When you create a custom image from an instance, ECS creates a snapshot for each disk of the instance. The created custom image consists of the snapshots of all the disks of the instance. For more information, see [Create a custom image from an instance](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from an instance.md).
-   You can also create custom images from system disk snapshots. For more information, see [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md).

## Which instance families do Red Hat Enterprise Linux \(RHEL\) images support?

RHEL images support the following instance families. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).

-   ecs.r6 \(supported only by RHEL 7.7 and later\)
-   ecs.c6 \(supported only by RHEL 7.7 and later\)
-   ecs.g6 \(supported only by RHEL 7.7 and later\)
-   ecs.r5
-   ecs.c5
-   ecs.g5
-   ecs.re4
-   ecs.t5

    We recommend that you do not use RHEL images for the following instance types. This is because the memory of these instance types is smaller than 1.5 GiB and cannot meet the minimum requirements of RHEL images:

    -   ecs.t5-lc2m1.nano
    -   ecs.t5-lc1m1.small
-   ecs.hfc5
-   ecs.hfg5
-   ecs.i2
-   ecs.sn1ne
-   ecs.sn2ne
-   ecs.se1ne
-   ecs.sn1
-   ecs.sn2
-   ecs.se1

For more information, see the following topics:

-   [RHEL certification](https://catalog.redhat.com/cloud/images/detail/3245731)
-   [Which Instance Types are RHEL Guest supported with on Aliyun](https://access.redhat.com/solutions/3336161)
-   [Red Hat Enterprise Linux technology capabilities and limits](https://access.redhat.com/articles/rhel-limits)

## How do Windows versions differ in terms of memory limits?

Different Windows versions have different upper limits on memory. For more information, see [Memory Limits for Windows and Windows Server Releases](https://docs.microsoft.com/zh-cn/windows/win32/memory/memory-limits-for-windows-releases). Choose appropriate instance types based on the memory limits of your Windows version.

## Can I use a snapshot of a data disk to create a custom image?

No, you cannot use data disk snapshots to create custom images. Only system disk snapshots can be used to create custom images.

However, you can add a data disk snapshot when you use a system disk snapshot to create a custom image. For more information, see [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md).

## How do I view data disk usage?

You can run the df command to view data disk usage and the locations where file systems are mounted. Example: df –lh.

You can run the fdisk command to view the partition information of a data disk. Example: fdisk -l.

## How do I unmount file systems and delete disk table data?

If /dev/hda5 is mounted to /mnt/hda5, you can run one of the following commands to unmount the file system:

-   ```
umount /dev/hda5
```

-   ```
umount /mnt/hda5
```

-   ```
umount /dev/hda5 /mnt/hda5
```


/etc/fstab is an important configuration file in Linux systems. It contains detailed information about the file systems and storage devices that are automatically mounted on system startup.

If you do not want a partition to be automatically mounted on instance startup, you must delete the corresponding statement from the /etc/fstab file. For example, after the following statement is deleted from the /etc/fstab file, xvdb1 is not mounted on system startup:

```
/dev/xvdb1 /leejd ext4 defaults 0 0
```

The following table lists other important configuration files in Linux systems.

|Configuration file|Description|Risk of modifying the file|
|:-----------------|:----------|:-------------------------|
|/etc/issue\*, /etc/\*-release, /etc/\*\_version|The system distribution configuration file|Modifications to /etc/issue\* cause failures to recognize system distributions and to create the system.|
|/boot/grub/menu.lst, /boot/grub/grub.conf|The system boot configuration file|Modifications to /boot/grub/menu.lst cause kernel load and system boot failures.|
|/etc/fstab|The configuration file for mounting partitions on system startup|Modifications to /etc/fstab cause partition load and system boot failures.|
|/etc/shadow|The system password-related configuration file|Changes of /etc/shadow to read-only cause failures to modify password files and to create the system.|
|/etc/selinux/config|The system security policy configuration file|Modifications to /etc/selinux/config to enable SELinux cause system boot failures.|

## How do I confirm that a data disk has been unmounted and that a new custom image can be created?

1.  Confirm that the statement used to automatically mount the partitions of the data disk has been deleted from the /etc/fstab file.
2.  Run the mount command to view the mount information of all devices. Confirm that information about the corresponding data disk partitions is not displayed in the command output.

## Does a custom image still exist after the instance from which the image was created is released?

Yes, the custom image still exists after the instance from which the image was created is released. After an instance is manually or automatically released, the custom images created from the instance are unaffected.

## When an instance expires or its data is deleted, are custom images that were created from the instance affected? Are instances created from the custom images affected?

No, the custom images and the instances created from the custom images are unaffected. After an instance is manually released or automatically released when it expires, the custom images created from the instance and the instances created from the custom images are unaffected.

## Can I replace the operating system of an instance created from a custom image? Can the custom image still be used after the operating system is replaced?

Yes, you can replace the operating system of an instance created from a custom image. The custom image can still be used after the operating system is replaced.

## Can I select a custom image with a different operating system when I replace the system disk of an instance?

Yes, you can select a custom image with a different operating system when you replace the system disk of an instance. For more information, see [Replace a system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md).

**Note:** When a custom image is used to replace a system disk, all data on the original system disk is overwritten.

## Can I use a custom image to overwrite the system disk data of an ECS instance?

Yes, you can use a custom image to overwrite the system disk data of an ECS instance. For more information, see [Replace a system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md).

**Note:** When you use a custom image to replace the image of an instance, the custom image overwrites all data on the system disk of the instance.

## Can I upgrade the CPU, memory, bandwidth, and hard disks of an ECS instance that was created from a custom image?

Yes, you can upgrade the CPU, memory, bandwidth, and hard disks of an ECS instance that was created from a custom image. For more information, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md).

## Can I use a custom image across regions?

No, custom images cannot be used across regions. For example, a custom image created from an instance in the China \(Hangzhou\) region cannot be used to create an ECS instance in the China \(Shanghai\) region.

If you want to use a custom image across regions, you can copy the image to the destination region. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).

## Can a custom image created from a subscription instance be used to create a pay-as-you-go instance?

Yes, a custom image created from a subscription instance can be used to create a pay-as-you-go instance. The usage of custom images has nothing to do with the billing methods of instances.

## I created an ECS instance from a custom image and specified a system disk capacity greater than that in the image. However, the system disk capacity of the new ECS instance is the same as that in the image. What do I do?

The system disk capacity of an instance created from a custom image may fail to be expanded due to one of the following reasons: The cloud-init service is not installed, the cloud-init service fails, or the file systems do not support the capacity expansion.

You can manually expand the system disk capacity.

## Why do I need to comment out mount entries when I create a custom image or an instance?

When you create an instance from a custom image, the following situations may cause failures to mount disks:

-   The created instance does not have data disks.
-   Data disks are new disks and are not formatted or partitioned.
-   The mount entries for the data disks are not commented out in the /etc/fstab file of the custom image.

The following example shows the failure to mount a data disk. In this example, a data disk of an instance that was created from a custom image is not partitioned, and the mount entry for this data disk is not commented out in the /etc/fstab file of the custom image.

1.  A data disk of the instance is not partitioned, as shown in the following figure.

    ![Data disk not partitioned](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3173559951/p49584.png)

2.  In the instance, the mount entry for the data disk is not commented out in the /etc/fstab file, as shown in the following figure.

    ![Entry for the data disk](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3173559951/p49589.png)

3.  When the instance starts, the system attempts to mount the data disk based on the configurations in the /etc/fstab file. The mount operation fails because the data disk is not partitioned, as shown in the following figure.

    ![Failure to mount a data disk](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3173559951/p49591.png)


You do not need to comment out the mount entries for the data disks of an instance if these disks are created along the instance from snapshots of partitioned and formatted data disks.

If the problem persists, submit a ticket.

## How do I configure and use a private Docker image registry?

Image management is at the core of Docker. To allow organizations to share images internally, Docker has created the open source docker-registry project on GitHub to provide Docker Registry. Docker Registry is a tool used to manage private Docker image registries.

Start docker-registry that supports Alibaba Cloud OSS. You can download docker-registry from [GitHub](https://github.com/docker/docker-registry), install docker-registry, and then run the pip install docker-registry-driver-alioss command to install the OSS driver.

1.  Run a Docker Registry container.

    ```
     docker run -e OSS_BUCKET=-e STORAGE_PATH=/docker/ -e OSS_KEY=-e OSS_SECRET=-p 5000:5000 -d chrisjin/registry:ali_oss
    ```

2.  Configure config.yml.

    ```
     ```local: &local
     <<: *common
     storage: alioss
     storage_path: _env:STORAGE_PATH:/devregistry/
     oss_bucket: _env:OSS_BUCKET[:default_value]
     oss_accessid: _env:OSS_KEY[:your_access_id]
     oss_accesskey: _env:OSS_SECRET[:your_access_key]```
    ```

3.  Start Docker Registry.

    ```
     DOCKER_REGISTRY_CONFIG=[your_config_path] gunicorn -k gevent -b 0.0.0.0:5000 -w 1 docker_registry.wi:application
    ```


If the problem persists, submit a ticket.

## How do I clone an ECS instance?

You can clone the environment and data of an existing ECS instance within your account to create identical ECS instances. Use one of the following methods:

-   Method 1: Manually clone an ECS instance within the same region by using the ECS console.
    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).
    2.  Find the ECS instance that you want to clone and create a custom image from the instance. For more information, see [Create a custom image from an instance](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from an instance.md).
    3.  Use the created custom image to create an ECS instance by following the instructions in [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md). When you create the ECS instance, take note of the following parameters:
        -   Region: You must select the region where the custom image is located.
        -   Image: In the **Image** section, select **Custom Image**. Then, select the custom image that you created in the previous step from the drop-down list.

            **Note:** If the selected custom image contains one or more data disk snapshots, an equal number of data disks are automatically created from the snapshots. Each disk has the same size as the snapshot from which it is created. You can extend a data disk but cannot shrink it.

-   Method 2: Manually clone an ECS instance across regions by using the ECS console.
    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).
    2.  Select the ECS instance that you want to clone and create snapshots for its system disk and data disks. For more information, see [Create a snapshot for a disk](/intl.en-US/Snapshots/Use snapshots/Create a snapshot for a disk.md).

        **Note:** To ensure data consistency, create snapshots only when the instance is in the **Stopped** state.

    3.  Copy the snapshots to a different region in which you want to create an instance. For more information, see [Copy a snapshot](/intl.en-US/Snapshots/Use snapshots/Copy a snapshot.md).
    4.  Create a custom image from the copy of the system disk snapshot. In the Create Image dialog box, select **Add Data Disk Snapshot** and click **Add** to add one or more data disk snapshots to the image. For more information, see [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md).
    5.  Use the created custom image to create an ECS instance by following the instructions in [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md). When you create the ECS instance, take note of the following parameters:
        -   Region: You must select the region where the custom image is located.
        -   Image: In the **Image** section, select **Custom Image**. Then, select the custom image that you created in the previous step from the drop-down list.

            **Note:** If the selected custom image contains one or more data disk snapshots, an equal number of data disks are automatically created from the snapshots. Each disk has the same size as the snapshot from which it is created. You can extend a data disk but cannot shrink it.

    6.  Use the created custom image to create an ECS instance by following the instructions in [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md). When you create the ECS instance, take note of the following parameters:
        -   Region: You must select the region where the custom image is located.
        -   Image: In the **Image** section, select **Custom Image**. Then, select the custom image that you created in the previous step from the drop-down list.

            **Note:** If the selected custom image contains one or more data disk snapshots, an equal number of data disks are automatically created from the snapshots. Each disk has the same size as the snapshot from which it is created. You can extend a data disk but cannot shrink it.

-   Method 3: Automatically clone an ECS instance by using Operation Orchestration Service \(OOS\).
    -   To clone an ECS instance across regions, access the [ACS-ECS-CloneInstancesAcrossRegion](https://oos.console.aliyun.com/cn-hangzhou/execution/create/ACS-ECS-CloneInstancesAcrossRegion) public template in the OOS console. In the top navigation bar, select the region where the instance is located. Use the ACS-ECS-CloneInstancesAcrossRegion public template to clone the ECS instance to a different region.
    -   To clone an ECS instance across zones within a region, access the [ACS-ECS-CloneInstancesAcrossAZ](https://oos.console.aliyun.com/cn-hangzhou/execution/create/ACS-ECS-CloneInstancesAcrossAZ) public template in the OOS console. In the top navigation bar, select the region where the instance is located. Use the ACS-ECS-CloneInstancesAcrossAZ public template to clone the ECS instance from one zone to another.

## Some custom images cannot be used to create I/O optimized instances. What do I do?

Some custom images cannot be used to create I/O optimized instances. If you want to use such a custom image to create an I/O optimized instance, submit a ticket in which the image name is specified.

## Where do I view the progress of an image import task? How long does it take to import an image?

You can view the progress of an image import task on the Images page in the ECS console. It may take an extended period of time to import a custom image. The amount of time it takes to import an image depends on the image size and the number of concurrent import tasks in the queue.

## Where do I view the progress of an image creation task? How long does it take to create an image?

You can view the progress of an image creation task on the Images page in the ECS console. The amount of time it takes to create an image depends on the size of the disk that is used to create the image.

## When do I need to copy a custom image?

Each custom image can be used only within a single region and cannot be used across regions. You can copy custom images to achieve the following goals:

-   Deploy applications in ECS instances to multiple regions.
-   Migrate ECS instances to other regions.
-   Use custom images across regions.

You can copy a custom image from one region to another within the same account and use the custom image to deploy the same application environment in the destination region.

## Which images can be copied?

Only custom images can be copied. Public images, Alibaba Cloud Marketplace images, and images shared by other accounts cannot be copied.

## Which regions support copying custom images?

All Alibaba Cloud regions support copying custom images.

## How long does it take to copy a custom image?

When you copy a custom image across regions, the image file is transmitted from one region to another. The amount of time it takes to copy a custom image depends on the network transmission speed and the number of transmission tasks in the queue.

To copy a large image such as an image larger than 2 TiB in size across regions, you can first copy the associated snapshots to the destination region and then create a custom image from these snapshots in the destination region. This procedure takes less time than the procedure to directly copy the image. For more information, see [Copy a snapshot](/intl.en-US/Snapshots/Use snapshots/Copy a snapshot.md) and [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md). For information about snapshot fees, see [Snapshots](/intl.en-US/Pricing/Billing items/Snapshots.md).

## How am I charged when I copy a custom image?

You must perform the following operations to copy a custom image:

1.  Copy the snapshot from which the custom image was created from the source region to the destination region.
2.  Create a custom image from the snapshot in the destination region.

You may be charged the following fees for the preceding operations:

-   Fees for traffic between the two regions. Alibaba Cloud does not charge you for cross-region traffic. For the latest billing details, see the official Alibaba Cloud website for announcements.
-   The new snapshot \(snapshot copy\) consumes snapshot storage space in the destination region. Snapshots are billed based on the storage space used. For more information, see [Snapshots](/intl.en-US/Pricing/Billing items/Snapshots.md).

## What limits apply to the original image \(image copied\) and the new image \(image copy\) during an image copy process?

During an image copy process, the original image cannot be deleted, and the new image cannot be used to replace a system disk or create an ECS instance. The image copy process can be canceled.

## How do I copy images within my Alibaba Cloud account to other regions within other Alibaba Cloud accounts?

You must copy your own images to the destination regions and then share the images to the intended Alibaba Cloud accounts. After the images are shared, they are displayed in the shared image lists of those accounts.

## Do size limits apply to copying an image?

No, no size limits apply to copying an image. However, if you click **Copy Image** in the ECS console to copy an image whose size exceeds 500 GiB, you are prompted to submit a ticket.

## Can I copy a custom image derived from an Alibaba Cloud Marketplace image across regions?

If an Alibaba Cloud Marketplace image is available in the destination region, you can copy custom images derived from the Alibaba Cloud Marketplace image to the destination region. Otherwise, the following error message is reported when you copy such a custom image.

![Copy a custom image derived from an Alibaba Cloud Marketplace image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3173559951/p69663.png)

## How do I migrate data from regions outside mainland China to regions inside mainland China?

You can migrate data from regions outside mainland China to regions inside mainland China by copying images. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).

## How many images can be shared to me?

A maximum of 100 images can be shared to you.

## How many users can an image be shared to?

An image can be shared to a maximum of 50 users.

## I have accounts on different Alibaba Cloud sites. Can I share images between these accounts?

Yes, you can share images between the accounts. Images \(except for custom images derived from Alibaba Cloud Marketplace images\) can be shared between your accounts on the China site \(aliyun.com\), International site \(alibabacloud.com\), and Japan site \(jp.alibabacloud.com\).

## Do shared images accrue towards my image quota?

No, shared images do not accrue towards your image quota.

## Do geographical limits apply when shared images are used to create instances?

Yes, shared images can be used to create instances only in the regions where the shared images are located.

## What are the risks of creating an instance from a shared image?

The image owner can check how the image is shared and can delete the image. After a shared image is deleted by its owner, the system disks of the ECS instances that use this image cannot be re-initialized.

Alibaba Cloud does not guarantee the integrity and security of images shared by other accounts. We recommend that you select only images shared by trusted accounts. After an ECS instance is created from a shared image, you must log on to the ECS instance to check the security and integrity of the shared image.

## What risks may arise if I share a custom image to other accounts?

If you share a custom image to other accounts, data and software may be leaked or stolen. Before you share a custom image to other accounts, check whether the image contains sensitive or important data. After the image is shared to other accounts, they can use the shared image to create ECS instances, which can then be used to create more custom images. During this process, data can be repeatedly spread. This creates a risk of data being disclosed beyond your original intentions.

## After an account shares an image to me, can I share this image to another account?

No, only the owner of an image can share the image to other accounts.

## After I share an image, can I still use this image to create an instance?

Yes, after you share an image to another account, you can still use the image to create an ECS instance and then create a custom image from the instance.

## Can an image created from Instance A in one region be used by Instance B in a different region?

-   If Instances A and B belong to the same account, you can copy the image to the region where Instance B is located and then apply the image to Instance B. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).
-   If instances A and B belong to different accounts, you can copy the image to the region where Instance B is located and then share the image to the account to which Instance B belongs. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md) and [Share or unshare custom images](/intl.en-US/Images/Custom image/Share or unshare custom images.md).

## Is Bring Your Own License \(BYOL\) supported when I import custom images?

Yes, BYOL is supported when you import custom images. You can configure the license types by using the image import feature in the ECS console or by calling the ImportImage operation. For more information, see [Import custom images](/intl.en-US/Images/Custom image/Import images/Import custom images.md) and [ImportImage](/intl.en-US/API Reference/Images/ImportImage.md).

## What types of licenses can be used when I import custom images?

When you import custom images, you can select one of the following license types:

-   Aliyun

    Aliyun licenses are provided by Alibaba Cloud and include the licenses for Windows Server operating systems. If cloud-init is installed on the imported images, Alibaba Cloud uses KMS to activate the operating systems and provides Windows Server Update Services \(WSUS\).

-   BYOL

    BYOL licenses are used in the following scenarios:

    -   Microsoft

        Microsoft BYOL licenses are used in the following scenarios:

        -   BYOL implemented by using Software Assurance \(SA\)

            BYOL can be implemented for software programs such as SQL Server and SharePoint that support License Mobility when ECS instances are created.

        -   Windows operating system

            Windows [client access licenses \(CALs\)](https://docs.microsoft.com/zh-cn/windows-server/remote/remote-desktop-services/rds-client-access-license) do not support License Mobility. Therefore, existing Windows licenses cannot be used within shared hardware environments. You must deploy Windows operating systems within a dedicated physical environment, which can be an Alibaba Cloud dedicated host or an ECS bare metal instance. For more information, see [Dedicated Host documentation](/intl.en-US/Product Introduction/What is DDH?.md) and [ECS Bare Metal Instance documentation](/intl.en-US/Instance/Instance type families/ECS Bare Metal Instance types/Overview.md).

            For this type of ECS instances, Alibaba Cloud does not provide KMS, WSUS, or software technical support. You can contact Microsoft for software technical support.

        -   No SA or no support for BYOL implemented by using SA

            This scenario is similar to the Windows operating system scenario. You can reuse software licenses that you have purchased and download and deploy software programs in a dedicated hardware environment.

    -   Redhat

        Red Hat provides the Cloud Access program. If your Red Hat subscription to be migrated uses Bring Your Own Subscription \(BYOS\), you can sign up with Red Hat Cloud Access. For more information, see [Enroll in the Red Hat Cloud Access program](https://www.alibabacloud.com/help/doc-detail/90933.html).

-   Auto

    Auto is the default value for License Type. When Auto is selected, a license type is automatically configured based on the operating system distribution to be imported.

    -   For operating systems such as Windows Server for which Alibaba Cloud has a signed licensing agreement and provides official licenses, the license type is Aliyun.
    -   For other operating systems such as noncommercial Linux images, the license type is BYOL. Alibaba Cloud does not provide software technical support for these operating systems.

## How are the imported BYOL images charged?

You are not charged for operating system components of BYOL images. This rule is applicable to newly created, renewed, or re-initialized ECS instances as well as ECS instances that have their configurations upgraded or downgraded.

## How are BYOL licenses authenticated and subscribed by using Alibaba Cloud when their subscriptions expire?

You can change BYOL images to public images provided by Alibaba Cloud or Alibaba Cloud Marketplace images.

-   For Windows Server operating systems, you can use the public images provided by Alibaba Cloud. For more information, see [Overview](/intl.en-US/Images/Public image/Overview.md).
-   You can obtain SQL Server and Red Hat images in Alibaba Cloud Marketplace. For more information, see [Alibaba Cloud Marketplace images](/intl.en-US/Images/Alibaba Cloud Marketplace images.md).

## I want to export an image to my computer for testing. What do I do?

By default, images are exported as .raw.tar.gz files, from which you can extract .raw files. You can search for the relevant documentation for using images in the .raw format. Alibaba Cloud has no limits on how to use images in the .raw format.

## Can an image exported from ECS be started on other platforms?

Images exported from ECS may not be started normally on other platforms. You can mount the disk files in the images to obtain data.

## Can I delete a custom image after it is used to create an ECS instance?

You can select **Proceed to Forcibly Delete** in the Delete Image dialog box to forcibly delete the image. However, after the image is deleted, the cloud disks of the ECS instances created from the image cannot be re-initialized. For more information, see [Reinitialize a cloud disk](/intl.en-US/Block Storage/Cloud disks/Reinitialize a cloud disk/Re-initialize a system disk.md).

## Can I delete a custom image from my account after the image is shared to another account?

Yes, you can delete a custom image from your account after the image is shared to another account. However, after the shared image is deleted, the system disks of all ECS instances created from the image cannot be re-initialized. We recommend that you unshare the custom image before you delete it.

## What happens if I unshare Custom Image M to Account A?

If you unshare Custom Image M to Account A, Account A is unable to query Custom Image M by using the ECS console or by calling ECS API operations, and cannot use Custom Image M to create ECS instances or replace system disks. If Account A has created ECS instances from Custom Image M before the image is unshared, the system disks of these instances cannot be re-initialized.

## Why am I prompted with a message similar to "The specified image cannot be deleted because it is associated with instances" when I attempt to delete an image?

You may have created the image from a snapshot. To delete this image, you must select **Proceed to Forcibly Delete**. After the image is forcibly deleted, instances created from it are still available, but their cloud disks cannot be re-initialized. For more information, see [Delete a custom image](/intl.en-US/Images/Custom image/Delete a custom image.md).

## When I replace a system disk, can I select an image that contains data disk snapshots?

No, you cannot select an image that contains data disk snapshots when you replace a system disk. If you want to use such an image to replace a system disk, we recommend that you use the image to create a pay-as-you-go instance and create a snapshot for the system disk of this new instance. You can then use the snapshot to create a custom image that contains only a system disk snapshot, and use the created custom image to replace the system disk of the target instance.

## I want to replace the operating system of my ECS instance by using an existing image. What do I do?

For information about how to use an existing image to replace the operating system of an ECS instance, see [Change the operating system](/intl.en-US/Images/Change the operating system.md).

**Note:** We recommend that you create snapshots to back up data before you proceed.

## Can I use an image created from an instance within Account A to replace a system disk within Account B?

Yes, you can use an image created from an instance within Account A to replace a system disk within Account B. You can share the image to Account B and then replace the system disk. For more information, see [Share or unshare custom images](/intl.en-US/Images/Custom image/Share or unshare custom images.md).

**Note:** To use an image to replace a system disk, make sure that the image contains only a system disk snapshot.

## I am creating an ECS instance. Why is the total instance cost displayed when I select a custom image higher than that displayed when I select a public image?

This situation may occur in the following circumstances:

-   The custom image contains data disk snapshots. When such an image is selected, the costs of the data disks cause the total cost of the instance to be higher than that of an instance created from a public image.
-   The custom image was derived from a paid public image such as a Windows Server or RHEL image.

## What features do Alibaba Cloud Marketplace images provide?

A software environment such as the PHP, .NET, Java, or LAMP runtime environment and a variety of features such as the control panel and website building systems are pre-installed on the operating systems in Alibaba Cloud Marketplace images. You can use Alibaba Cloud Marketplace images to deploy runtime environments or software applications to ECS instances.

## What are the benefits of Alibaba Cloud Marketplace images?

You can use an Alibaba Cloud Marketplace image to create an ECS instance and deploy the pre-installed system environment or software of the image to the ECS instance. This eliminates the need to manually configure the environment or install software and enables you to create a ready-to-run runtime environment and conveniently build and manage services.

## What server environments and scenarios do Alibaba Cloud Marketplace images support?

Alibaba Cloud Marketplace provides hundreds of high-quality third-party images. These images not only support the deployment of runtime environments such as PHP, .NET, JAVA, LAMP, and Docker virtual containers, but can also meet personalized demands for website building, application development, and visual management.

## Are Alibaba Cloud Marketplace images safe?

All image service providers in Alibaba Cloud Marketplace have a wealth of experience in system maintenance and environment configuration. All images are made based on the official Alibaba Cloud operating systems that are installed with Alibaba Cloud Security. All images have passed strict security reviews and are safe to use.

## What do I do if I encounter a problem when I am installing or using an Alibaba Cloud Marketplace image?

You can view the service information on the buy page and contact the image service provider by TradeManager, phone, or email. They will answer your questions as soon as possible.

## How do I purchase an Alibaba Cloud Marketplace image?

You can purchase an Alibaba Cloud Marketplace image from Alibaba Cloud Marketplace or from the ECS instance buy page when you create an ECS instance.

## How long can I use a purchased image?

Theoretically, a purchased image can be used indefinitely. However, an image is a piece of software and has its own lifecycle. In addition, image providers provide services only over a limited period of time, which is described in the product details.

## Are Alibaba Cloud Marketplace images refundable?

Alibaba Cloud Marketplace images support money-back guarantee within a period of time based on the Alibaba Cloud Marketplace rules. However, you are ineligible for a refund in the following situations:

-   You have deployed the purchased image to an ECS instance within the money-back guarantee period.
-   You have deployed the purchased image to an ECS instance before your application for a refund for this image is approved.
-   You can receive refunds only for images that have not been used.

## Are free Alibaba Cloud Marketplace images still available after Alibaba Cloud Marketplace images are commercially available?

Free Alibaba Cloud Marketplace images are still available. However, you must purchase them at a price of USD 0.00 before you can use them.

## I bought an Alibaba Cloud Marketplace image in the China \(Hangzhou\) region. Can I use it to create an ECS instance or replace a system disk in the China \(Beijing\) region?

No, Alibaba Cloud Marketplace images are region-specific. You can use an Alibaba Cloud Marketplace image that you purchased in a region to create ECS instances or replace system disks only within that region.

## I have an instance created from an Alibaba Cloud Marketplace image. Do I need to make further payments for the image when I renew the instance or upgrade the configurations of the instance?

No, you do not need to make further payments for the image. After you purchase an Alibaba Cloud Marketplace image, you can use it on instances at no additional costs.

## I have an ECS instance created from an Alibaba Cloud Marketplace image. After the instance is released, can I continue to use that image free of charge when I purchase another ECS instance?

Yes, you can continue to use that image free of charge when you purchase an ECS instance.

## I created an ECS instance from an Alibaba Cloud Marketplace image and then created a custom image from the instance. Do I need to pay for the custom image when I use it to create an ECS instance?

Yes, you must pay the original price of the Alibaba Cloud Marketplace image.

## If I copy an Alibaba Cloud Marketplace image that I bought to another region to create an ECS instance, do I need to pay for the image?

Yes, you must pay the original price of the Alibaba Cloud Marketplace image.

## I created an ECS instance from an Alibaba Cloud Marketplace image and then created a custom image from that instance. If I share the custom image to Account B, does Account B need to pay for the custom image when it uses this image to create an ECS instance?

Yes, Account B must pay the original price of the Alibaba Cloud Marketplace image.

## Is a fee charged if I replace a system disk by using an Alibaba Cloud Marketplace image or an image derived from an Alibaba Cloud Marketplace image?

It depends. If the current image of your ECS instance is a different version of the replacement image, no fees are charged. Otherwise, a fee is charged.

## My ECS instance is using an Alibaba Cloud Marketplace image. Is a fee charged if I replace the system disk of the instance?

No, no fees are charged if you replace the system disk of the instance.

## How do I call an ECS API operation to use an Alibaba Cloud Marketplace image or a custom or shared image that derives from an Alibaba Cloud Marketplace image to create an ECS instance or replace a system disk?

1.  Check whether the image in use is an Alibaba Cloud Marketplace image or an image that derives from an Alibaba Cloud Marketplace image. You can call the DescribeImages operation to query the image information.

    If the product ID \(`ProductCode`\) of your image is not empty, your image is an Alibaba Cloud Marketplace image or a custom or shared image that derives from an Alibaba Cloud Marketplace image. For example, if the `ProductCode` of your image is `abcd000111`, you can access the image at `http://market.aliyun.com/products/123/abcd000111.html`.

2.  Select the version and region of the image and then purchase the image.

    An image can be used only on ECS instances that are deployed within the same region in which the image was purchased. In addition, you can purchase only one image at a time. If you want to create multiple ECS instances, you must purchase multiple images.

3.  You can use the image that you purchase to create an ECS instance or replace a system disk.

## If I do not purchase an Alibaba Cloud Marketplace image or an image that derives from an Alibaba Cloud Marketplace image, is an error reported when I call an ECS API operation to use the image to create an ECS instance or replace a system disk?

Yes, an error is reported with the `QuotaExceed.BuyImage` error code.

## I have configured a scaling group for which the minimum number of instances is set to 10 and the maximum number of instances is set to 100. What do I do with Alibaba Cloud Marketplace images to ensure that ECS instances are created to meet my computing needs?

If you want to automatically create n instances that use the same image, you must purchase the image n times from Alibaba Cloud Marketplace in advance.

## Can I purchase multiple Alibaba Cloud Marketplace images at a time?

No, you cannot purchase multiple Alibaba Cloud Marketplace images at a time.

## If an image \(such as jxsc000010 or jxsc000019\) in use in an active scaling configuration no longer exists in Alibaba Cloud Marketplace, what do I do to ensure that ECS instances can continue to be created based on the scaling configuration in the corresponding scaling group?

We recommend that you select a suitable replacement image from Alibaba Cloud Marketplace to ensure that ECS instances are properly created in your scaling group.

## Can one product code support images in different regions?

Yes, one product code can support images in different regions if the regions already support the images.

## I bought 100 images that have the same product code. Can I use the images within all regions?

Alibaba Cloud Marketplace images are region-specific. If you want to use an image within a specific region, you must purchase the image in that region.

## After I select I/O Optimized, I cannot select Alibaba Cloud Marketplace images when I purchase an ECS instance. What is the cause and how can I solve this problem?

View the details about and solution to this problem.

-   Problem description: When you purchase an ECS instance on the official Alibaba Cloud website, you cannot select Alibaba Cloud Marketplace images.
-   Cause: If you select **I/O Optimized** when you purchase an ECS instance, you cannot select Alibaba Cloud Marketplace images.

    Compared with non-I/O optimized ECS instances, I/O optimized ECS instances provide better network capabilities between instances and disks to maximize the storage performance of standard SSDs. However, not all images support I/O optimized instances because the related optimization operations involve networks, storage, and internal drivers.

-   Solution: When you purchase an I/O optimized instance, we recommend that you select an official standard image supported by the instance and then deploy your business environment on the instance.

If the problem persists, submit a ticket.

## What are yearly, monthly, and weekly subscription Alibaba Cloud Marketplace images?

Yearly, monthly, or weekly subscription Alibaba Cloud Marketplace images are images that are purchased from Alibaba Cloud Marketplace and billed on a subscription basis. These images are developed and maintained by image providers, who are responsible for both pre-sales consultation and after-sales services. In this topic, these images are collectively referred to as subscription images.

## On which ECS instances can I use a subscription image?

A subscription image can be used only on a subscription instance with the same subscription duration.

## How do I purchase a subscription image? Can I separately purchase it?

No, you cannot separately purchase a subscription image.

You can use one of the following methods to purchase a subscription image:

-   When you create an instance, set Billing Method to **Subscription**, select an **Alibaba Cloud Marketplace** image, and then specify a subscription duration by setting Duration.

    **Note:** In this case, you must pay for both the instance and the image. The instance is created on successful payment for both the image and instance.

-   To use a subscription image on an existing subscription ECS instance, you can use the image to replace the operating system of the instance. In this case, you must select the image subscription duration based on the instance subscription duration. For more information, see [Replace a system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md).

    **Note:** In this case, you need only to pay for the image.


## How do I pay for subscription images?

Subscription images require payment upfront. The subscription duration of a subscription image must be the same as that of the subscription instance on which the image is used.

Image prices are set by the image providers.

## Can I use a subscription image after it expires? How do I continue to use it?

When a subscription image expires, it cannot be used unless it is renewed in a timely manner.

You cannot separately renew a subscription image. If you want to continue to use the image, you must renew the image together with the corresponding ECS instance. After the image is renewed, you can continue to use it.

## After I purchase a subscription image, can I request a refund if I no longer want to use it?

The image provider determines whether to make a refund. You can consult the image provider before you purchase the image.

## What can I expect when a refund is made?

If a refund is available, the image provider makes the refund based on your usage.

## Can a subscription image be converted into a pay-as-you-go image?

Subscription images cannot be converted into pay-as-you-go images. This conversion feature is under development for release in the future. Stay updated on the official Alibaba Cloud website.

## Can I replace a subscription image with an image of another type or vice versa? How is the fee calculated?

Yes, you can replace images when you replace system disks of ECS instances. You can make the following replacements:

-   Replace an image of another type \(such as public image, custom image, or shared image\) with a subscription image. After the image is replaced, the system calculates the actual cost based on the image cost and the remaining subscription duration of the ECS instance.
-   Replace a subscription image with an image of another type \(such as public image, custom image, or shared image\). If the image provider allows for refunds, a refund is made based on your actual usage.
-   Replace one subscription image with another subscription image. If a refund is available for the replaced image after the replacement, the refund is made based on the refund policy. The actual cost of the replacement image is calculated based on the image price and the remaining subscription duration of the ECS instance.

## Where do I view and manage the subscription images that I purchased?

You can log on to the [ECS console](https://ecs.console.aliyun.com). In the left-side navigation pane, choose **Instances & Images** \> **Images**. Then, click the Marketplace Images tab to view and manage the subscription images that you purchased.

## Is a fee charged for a custom image derived from a subscription image? How is the custom image affected if the subscription image expires?

When you use a custom image derived from a subscription image to create an instance or replace a system disk, you are re-ordering the subscription image on Alibaba Cloud Marketplace. The custom image is not affected regardless of whether the subscription image expires.

## Why am I unable to use an SSH key pair that uses the ssh-rsa signature algorithm to connect to an instance that runs Fedora 33 64-bit?

When you use an SSH key pair that uses the ssh-rsa signature algorithm to log on to an ECS instance that runs Fedora 33 64-bit, you may not be able to connect to the instance. You can use one of the following methods to solve this problem:

-   Replace the SSH key pair that uses the ssh-rsa signature algorithm with an SSH key pair that uses other signature algorithms such as the ECDSA signature algorithm.
-   Run the update-crypto-policies --set LEGACY command in the system to change `POLICY` to `LEGACY`. Then, you can continue to use the SSH key pair that uses the ssh-rsa signature algorithm.

## How do I install patches and compile the kernel on FreeBSD?

Alibaba Cloud FreeBSD public images already have their kernels patched to meet the startup requirements for instance families in Generation V or later. To query the relevant instance families, call the [DescribeInstanceTypeFamilies](/intl.en-US/API Reference/Instances/DescribeInstanceTypeFamilies.md) operation with the `Generation` parameter set.

In the following situations, you can use the FreeBSD kernel source code to install patches and compile the kernel to solve the problem:

-   If you use a FreeBSD image that is not provided by Alibaba Cloud or a custom image derived from such a FreeBSD image to create an ECS instance of an instance family in Generation V or later, the instance may fail to start.
-   If you use a FreeBSD public image to create an ECS instance of an instance family in Generation V or later and use freebsd-update to update the kernel with new patches, the instance may fail to start.

In this example, the FreeBSD kernel source code is used to demonstrates how to install patches and compile the kernel. FreeBSD 12.1 is used in this example.

1.  Download and decompress the FreeBSD kernel source code package.

    ```
    wget https://mirrors.aliyun.com/freebsd/releases/amd64/12.1-RELEASE/src.txz -O /src.txz
    cd /
    tar -zxvf /src.txz
    ```

2.  Download patches.

    In this example, the following patches to virtio drivers are downloaded: `0001-virtio.patch`.

    ```
    cd /usr/src/sys/dev/virtio/
    wget https://ecs-image-tools.oss-cn-hangzhou.aliyuncs.com/0001-virtio.patch
    patch -p4 < 0001-virtio.patch
    ```

3.  Copy the kernel files and compile and install the kernel.

    N in the `make -j<N>` command indicates the number of jobs that run in parallel. Set N based on your compiling environment. The ratio of the number of vCPUs to the N value must be `-j2`. For example, for a single-vCPU environment, set -j<N\> to `1:2`.

    ```
    cd /usr/src/
    cp ./sys/amd64/conf/GENERIC .
    make -j2 buildworld KERNCONF=GENERIC
    make -j2 buildkernel KERNCONF=GENERIC
    make -j2 installkernel KERNCONF=GENERIC
    ```

4.  After the kernel is compiled, delete the source code.

    ```
    rm -rf /usr/src/*
    rm -rf /usr/src/.*
    ```


## Why does the load average become high on ECS instances that run Ubuntu operating systems of specific versions after the Server Guard \(AliYunDun\) process is started on the instances?

After the Server Guard process is started on ECS instances that run Ubuntu operating systems of specific versions such as Ubuntu 18.04, the load average of the instances becomes high. After the Server Guard process is terminated, the average loads drop to a normal level.

For the causes of and solutions to this problem, see [The system load is high after the Ubuntu 18.04 process is started on an ECS instance of the Server Guard version](https://www.alibabacloud.com/help/en/doc-detail/170051.htm).

## Why am I unable to select a Windows operating system for ECS instances?

When you create an ECS instance based on a Windows operating system, make sure that the instance memory size is greater than or equal to 1 GiB. For ECS instances that have less than 1 GiB of memory, you can select only Linux and Windows Server 1709 images.

## Does Alibaba Cloud support Windows Server 2008 and Windows Server 2008 R2?

On January 14, 2020, Microsoft stopped providing support for Windows Server 2008 and Windows Server 2008 R2 operating systems. In light of this, Alibaba Cloud no longer provides technical support for ECS instances that use these operating systems. If you have ECS instances that use these operating systems, upgrade them to Windows Server 2012 or later at your earliest opportunity.

## The operating system of my instance is Windows Server. I am prompted with a message indicating that the operating system is not genuine. What do I do?

Activate the Windows operating system. For more information, see [How to activate the VPC-type Windows instances by using KMS servers](https://www.alibabacloud.com/help/faq-detail/41056.htm).

## Are fees charged for the images used by ECS instances?

The Windows Server and Red Hat public images are charged. The fees depend on instance types. Other public images are free of charge. For more information about the fees for other types of images, see [Image overview](/intl.en-US/Images/Image overview.md).

## Can I install or upgrade the operating systems of ECS instances on my own?

No, you cannot install or upgrade the operating systems of ECS instances on your own. ECS instances must use images provided by Alibaba Cloud, which you cannot add or upgrade on your own. However, you can perform the following operations:

-   Replace system disks and select new operating systems. For more information, see [Change the operating system](/intl.en-US/Images/Change the operating system.md) or [Upgrade the operating systems of ECS instances in batches by replacing the system disks]().
-   Create ECS instances from custom images that are imported from your computers.
    -   For information about how to import an image, see [Instructions for importing images](/intl.en-US/Images/Custom image/Import images/Instructions for importing images.md).
    -   For more information about how to create ECS instances from a custom image, see [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md).
-   Patch operating systems.

## Do operating systems have graphical interfaces?

Each Windows operating system except for Windows Server Semi-Annual Channel offers a management desktop. For information about how to use Windows Server Semi-Annual Channel operating systems, see [Manage Windows Server Semi-Annual Channel images and instances](/intl.en-US/Images/FAQ/Manage Windows Server Semi-Annual Channel images and instances.md).

Each Linux operating system offers a command-line interface. You can install a graphical desktop.

## How do I choose an operating system?

For information about how to choose an operating system, see [Select an image](/intl.en-US/Images/Select an image.md).

## Do public images come with the FTP service?

No, public images do not come with the FTP service. You must configure the FTP service on your own. For more information, see [Manually build an FTP site on a Windows instance](/intl.en-US/Tutorials/Build an application/Build an FTP site on an ECS instance/Manually build an FTP site on a Windows instance.md) and [Manually build an FTP site on a CentOS 7 instance](/intl.en-US/Tutorials/Build an application/Build an FTP site on an ECS instance/Manually build an FTP site on a CentOS 7 instance.md).

## Which SUSE versions do Alibaba Cloud public images support?

Alibaba Cloud public images support SUSE versions. For the SUSE versions that Alibaba Cloud public images support, see the "Alibaba Cloud Linux images" section in [Overview](/intl.en-US/Images/Public image/Overview.mdtable_esz_rzj_dhb).

## What service support is available for SUSE operating systems?

SUSE Linux Enterprise Server \(SLES\) operating systems that are sold in Alibaba Cloud Marketplace are synchronized with SUSE update sources on a regular basis. For instances created from Alibaba Cloud SLES public images, the support for their operating systems is covered by the Alibaba Cloud enterprise-level support service. If you have purchased the enterprise-level support service and encounter a problem when you use an SLES operating system, submit a ticket to contact Alibaba Cloud technical support personnel.

## If an image was manually created from an ECS instance, can I retrieve the instance data after the instance is released on expiration?

Yes, you can retrieve instance data by using one of the following methods:

-   Create an instance from the previously created image. For more information, see [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md).
-   Use the previously created image to replace the system disk of an existing instance. For more information, see [Replace a system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md).

    **Note:** When you replace the system disk, take note of the following items:

    -   All data on the replaced system disk is lost, and the disk is released.
    -   The replacement image must be in the same region as the existing instance.

## I have an ECS instance and I want to create another ECS instance from the image of this existing ECS instance. What do I do?

You can create a custom image from the existing ECS instance and then use the custom image to create an ECS instance. For more information, see [Create a custom image from an instance](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from an instance.md) and [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md).

## I have purchased an ECS instance. How do I restore my shared image to the newly purchased instance?

Make sure that you have shared the image to the account to which the newly purchased instance belongs. Use one of the following methods to restore the image to the instance:

-   If the shared image and the instance are located in the same region, replace the system disk of the instance and select the shared image for the new system disk. For more information, see [Replace a system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md).
-   If the shared image and the instance are not located in the same region, copy the image to the region where the instance is located. Then, replace the system disk of the instance and select this image for the new system disk. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md) and [Replace a system disk \(non-public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace a system disk (non-public images).md).

**Note:** The following risks may arise when you replace the system disk of an instance:

-   The original system disk will be released. We recommend that you create a snapshot to back up your data in advance.
-   You must stop the instance before you can replace its system disk. When the instance is stopped, the services that run on the instance are interrupted.
-   After you replace the system disk, you must re-deploy the service environment on the new system disk. This may cause services on the instance to be interrupted for an extended period of time.
-   When the system disk is replaced, a new system disk with a different disk ID is allocated to the instance. The snapshots of the original system disk cannot be used to roll back the new system disk.

## I have multiple Alibaba Cloud accounts. I want to transfer an instance from Account A to Account B or migrate the environment and applications of an instance within Account A to an instance within Account B. What do I do?

You can perform the following steps:

1.  Create a custom image from the instance within Account A. For more information, see [Create a custom image from an instance](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from an instance.md).
2.  Share the image to Account B. For more information, see [Share or unshare custom images](/intl.en-US/Images/Custom image/Share or unshare custom images.md).
3.  Create an instance within Account B from the shared image. For more information, see [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md).

## How do I migrate data between ECS instances?

You can perform the following steps to migrate data from one ECS instance to another:

1.  Create a custom image from the source ECS instance.
2.  Copy or share the custom image.
    -   If the source and destination instances are located within the same region and belong to the same account, go to the next step.
    -   If the source and destination instances are located within different regions but belong to the same account, copy the image to the region where the destination instance is located. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md).
    -   If the source and destination instances are located within the same region but belong to different accounts, share the custom image to the account to which the destination instance belongs. For more information, see [Share or unshare custom images](/intl.en-US/Images/Custom image/Share or unshare custom images.md).
    -   If the source and destination instances are located within different regions and belong to different accounts, copy the image to the region where the destination instance is located. Then, share the image to the account to which the destination instance belongs. For more information, see [Copy custom images](/intl.en-US/Images/Custom image/Copy custom images.md) and [Share or unshare custom images](/intl.en-US/Images/Custom image/Share or unshare custom images.md).
3.  Use the shared image to create an ECS instance or replace the image of the destination instance. For more information, see [Create an ECS instance by using a custom image](/intl.en-US/Instance/Create an instance/Create an ECS instance by using a custom image.md) or [Change the operating system](/intl.en-US/Images/Change the operating system.md).

    **Note:** If you want to replace the image of the destination instance, make sure that the original image does not contain data disk snapshots.


If the preceding steps are not applicable, see [Migrate data between Alibaba Cloud VMs]().

## Can ECS instances in different VPCs communicate with each other?

Express Connect and Cloud Enterprise Network \(CEN\) can be used to allow ECS instances in different VPCs to communicate with each other. For more information, see [Step 1: Network planning]() in *CEN documentation*.

## How do I handle a CentOS DNS resolution timeout?

View the details about and solution to the CentOS DNS resolution timeout problem.

-   Cause

    The DNS resolution mechanism of CentOS 6 and CentOS 7 has changed. A DNS resolution timeout may occur in CentOS 6 or CentOS 7 instances that were created before February 22, 2017 or that use custom images created before February 22, 2017.

-   Solutions

    You can perform the following steps to solve this problem:

    1.  Download the [fix\_dns.sh](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/59344/cn_zh/1505957231428/fix_dns%20%281%29.sh) script.
    2.  Place the downloaded script in the /tmp directory of the CentOS system.
    3.  Run the bash /tmp/fix\_dns.sh command to execute the script.
-   Script role

    The script determines whether the /etc/resolv.conf file contains the `options`\>`single-request-reopen` configuration. For more information, see [resolv.conf - resolver configuration file](http://man7.org/linux/man-pages/man5/resolv.conf.5.html).

    The DNS resolution mechanism of CentOS 6 and CentOS 7 uses the same 5-tuple to send IPv4 and IPv6 DNS requests, for which the `single-request-reopen` option must be added. When two requests from the same port need to be handled after the option is added, the resolver closes the socket after the resolver sends the first request and then opens a new socket before the resolver sends the second request. The option takes effect immediately after it is added. You do not need to restart the instance.

-   Script logic
    1.  Determine whether the operating system of the instance is CentOS.
        -   If the operating system is not CentOS \(for example, the operating system is Ubuntu or Debian\), the script stops running.
        -   If the operating system is CentOS, the script continues to run.
    2.  Check the /etc/resolv.conf file for the `options` configuration.
        -   If the `options` configuration is unavailable:

            By default, the Alibaba Cloud `options` configuration \(`options timeout:2 attempts:3 rotate single-request-reopen`\) is used.

            ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3173559951/p46335.png)

        -   If the `options` configuration is available:
            -   If the `single-request-reopen` option does not exist, append this option to the `options` configuration.
            -   If the `single-request-reopen` option exists, the script stops running and the DNS nameserver configuration does not change.

## Why does ECS disable virtual memory and leave swap partitions unconfigured by default?

When physical memory is insufficient, the memory manager saves memory data that has been inactive for an extended period of time to a swap partition or virtual memory file. This mechanism helps increase the available memory.

However, if memory usage is already high and I/O performance is poor, the mechanism decreases the available memory instead. Alibaba Cloud ECS cloud disks use distributed file systems for storage and provide multiple strongly consistent replicas for each piece of data. This mechanism ensures the security of user data but deteriorates the storage and I/O performance of local disks by tripling the number of I/O operations.

Therefore, virtual memory is not enabled for Windows and swap partitions are not configured for Linux by default to avoid further decreasing I/O performance when system resources are insufficient.

## How do I enable the kdump service in a public image?

By default, the kdump service is disabled in public images. If you want your instance to generate a core file when the instance goes down so that you can analyze the downtime cause based on the file, you can perform the following steps to enable the kdump service. In the following example, the CentOS 7.2 public image is used:

1.  Configure the directory in which to generate the core file.
    1.  Run the vim /etc/kdump.conf command to open the kdump configuration file.
    2.  Run the path command to configure the directory in which to generate the core file. In this example, the directory is /var/crash, and the following path command is used:

        ```
        path /var/crash
        ```

    3.  Save and close the /etc/kdump.conf file.
2.  Enable the kdump service.

    Use one of the following methods based on the operating system to enable the kdump service. In this example, the kdump service is enabled in CentOS 7.2 by using Method 1.

    -   Method 1: Run the following commands to enable the kdump service:

        ```
        systemctl enable kdump.service
        ```

        ```
        systemctl start kdump.service
        ```

    -   Method 2: Run the following commands to enable the kdump service:

        ```
        chkconfig kdump on
        ```

        ```
        service kdump start
        ```

3.  Run the following command to simulate the scenario where the instance is down:

    ```
    echo c > /proc/sysrq-trigger
    ```

    **Note:** After the command is run, the instance is disconnected from the network. You must reconnect the instance to the network to perform the subsequent operations.

4.  Analyze the core file.
    1.  Run the following command to install the Crash analysis tool:

        ```
        yum install crash
        ```

    2.  Download the debuginfo installation package.

        Run the uname -r command to view the operating system kernel version and download the debuginfo installation package that matches the kernel version.

        -   kernel-debuginfo-common-x86\_64-<Kernel version\>.rpm
        -   kernel-debuginfo-<Kernel version\>.rpm
        **Note:** The download URLs for the debuginfo package vary with the CentOS versions. You can find the download link that corresponds to your kernel version on the official CentOS website. For more information, see [CentOS debuginfo packages](http://debuginfo.centos.org/).

        In this example, the kernel is `3.10.0-514.26.2.el7.x86_64`. The following download commands are used:

        ```
        wget http://debuginfo.centos.org/7/x86_64/kernel-debuginfo-common-x86_64-3.10.0-514.26.2.el7.x86_64.rpm
        ```

        ```
        wget http://debuginfo.centos.org/7/x86_64/kernel-debuginfo-3.10.0-514.26.2.el7.x86_64.rpm
        ```

    3.  Run the following commands to install the debuginfo package:

        ```
        rpm -ivh kernel-debuginfo-common-x86_64-3.10.0-514.26.2.el7.x86_64.rpm
        ```

        ```
        rpm -ivh kernel-debuginfo-3.10.0-514.26.2.el7.x86_64.rpm
        ```

    4.  Run the following commands to use the Crash analysis tool to analyze the core file:

        ```
        cd <core file directory>
        ```

        ```
        crash /usr/lib/debug/lib/modules/<Kernel version>/vmlinux vmcore
        ```

        In this example, the core file directory is /var/crash/127.0.0.1-2019-07-08-15:52:25, and the kernel version is `3.10.0-514.26.2.el7.x86_64`. The following commands are used:

        ```
        cd /var/crash/127.0.0.1-2019-07-08-15:52:25
        ```

        ```
        crash /usr/lib/debug/lib/modules/3.10.0-514.26.2.el7.x86_64/vmlinux vmcore
        ```


## How do I obtain the dump file for RHEL images?

Some RHEL images do not have the kdump service enabled by default. You can submit a ticket to obtain the dump file. For instances that have memory of greater than 16 GiB, you may fail to obtain the dump file by submitting a ticket. Details on the ticket prevail.

## How do I enable the kdump service on an instance that uses a Red Hat 8.1 image?

By default, the kdump service is disabled in Red Hat 8.1 v1 images. To enable the kdump service, run the following commands:

```
systemctl enable kdump
systemctl start kdump
```

## Red Hat 8.1 and Red Hat 8.2 images start slowly on ECS bare metal instances. How do I solve this issue?

When used on an ECS bare metal instance, a Red Hat 8.1 or Red Hat 8.2 image takes up to 2 minutes longer to start than a Red Hat 7 image. To solve this issue, you can change the kernel startup parameter settings from `console=ttyS0 console=ttyS0,115200n8` to `console=tty0 console=ttyS0,115200n8` in the /boot/grub2/grubenv file of the Red Hat 8.1 or Red Hat 8.2 image, and restart the instance for the change to take effect.

## How do I enable or disable the Meltdown and Spectre patches for Linux images?

For information about the security vulnerabilities and public images involved as well as how to enable or disable security vulnerability patches, see [How do I enable or disable the Meltdown and Spectre patches for Linux images?]().

## After I use a CentOS or Windows ECS instance for an extended period of time without restarting it, the instance is disconnected from the network, the network is no longer available, or the public or private IP address of the instance cannot be pinged. What do I do?

For the cause of and solution to this issue, see [Troubleshoot IP address faults in CentOS 7 instances and Windows instances](https://www.alibabacloud.com/help/doc-detail/94181.html).

## The "UNEXPECTED INCONSISTENCY; RUN fsck MANUALLY." error is reported when an ECS instance starts. What do I do?

This indicates that a file system error occurs due to data loss in the memory of the ECS instance, which may be caused by conditions such as poweroff. For more information about the problem and the solution to it, see [How to solve the "UNEXPECTED INCONSISTENCY; RUN fsck MANUALLY" error returned when the ECS instance operating system fails to start](https://www.alibabacloud.com/help/doc-detail/136317.html).

## How do I upgrade RHEL 7 to RHEL 8?

For information about how to upgrade RHEL 7 to RHEL 8, see [Upgrading from RHEL 7 to RHEL 8](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/upgrading_to_rhel_8/index).

## How do I enable a program to distinguish ECS instances when I deploy my business?

If you want to enable your program to distinguish ECS instances when you deploy your business on a Linux operating system, you can run the systemd-machine-id-setup command to reset /etc/machine-id. This method requires you to re-generate the machine ID on each ECS instance. To avoid excessive operations, we recommend that you use the /sys/class/dmi/id/product\_uuid file to distinguish ECS instances. The /sys/class/dmi/id/product\_uuidis file is one of the unique external identifiers of an instance and can replace the /etc/machine-id file. This method is easy to use. You need only to obtain the UUID of the corresponding instance. You can run the following command to view the /sys/class/dmi/id/product\_uuid file of an ECS instance:

```
cat /sys/class/dmi/id/product_uuid
```

The following figure shows an example command output.

![product_uuid](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3106487161/p244711.png)

