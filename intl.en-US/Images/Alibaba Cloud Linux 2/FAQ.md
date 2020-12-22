# FAQ

This topic provides answers to commonly asked questions about Alibaba Cloud Linux 2 images.

-   [What are the differences between Aliyun Linux and Alibaba Cloud Linux 2?](#section_imn_fim_626)
-   [What are the differences among Alibaba Cloud Linux 2 images?](#section_9bw_q66_hep)
-   [How do I use Alibaba Cloud Linux 2 in Alibaba Cloud?](#section_ih8_6n8_aty)
-   [Am I charged for using Alibaba Cloud Linux 2 in Alibaba Cloud ECS?](#section_7na_hla_jpe)
-   [Which ECS instance types does Alibaba Cloud Linux 2 support?](#section_dja_kr5_fuo)
-   [Does Alibaba Cloud Linux 2 support 32-bit applications or libraries?](#section_esh_mwl_ir7)
-   [Does Alibaba Cloud Linux 2 provide a graphical user interface \(GUI\) desktop?](#section_o24_dn0_rae)
-   [Can I view the source code of Alibaba Cloud Linux 2 components?](#section_wtr_xdj_ktn)
-   [Is Alibaba Cloud Linux 2 backward-compatible with the current Aliyun Linux versions?](#section_a7h_hcy_6ps)
-   [Can I use Alibaba Cloud Linux 2 in an on-premises environment?](#section_2go_rnh_810)
-   [Which third-party applications can run on Alibaba Cloud Linux 2?](#section_37f_kfg_e2f)
-   [What are the advantages of Alibaba Cloud Linux 2 over other Linux operating systems?](#section_0hi_2xq_mb4)
-   [How does Alibaba Cloud Linux 2 protect data security?](#section_2gz_az0_nd6)
-   [Does Alibaba Cloud Linux 2 support data encryption?](#section_dn9_qtz_eoz)
-   [How do I grant permissions to manage Alibaba Cloud Linux 2?](#section_z2y_011_tl5)

## What are the differences between Aliyun Linux and Alibaba Cloud Linux 2?

Alibaba Cloud Linux 2 was originally called Aliyun Linux 2 and is an upgraded version of Aliyun Linux. Alibaba Cloud Linux 2 differs from Aliyun Linux in the following aspects:

-   Alibaba Cloud Linux 2 is optimized for containers to better support cloud native applications.
-   Alibaba Cloud Linux 2 is equipped with an updated Linux kernel and updated user-mode packages.

## What are the differences among Alibaba Cloud Linux 2 images?

For the release notes of Alibaba Cloud Linux 2 images, see [Release notes of Alibaba Cloud Linux 2](/intl.en-US/Images/Alibaba Cloud Linux 2/Release notes of Alibaba Cloud Linux 2.md). Different Alibaba Cloud Linux 2 images have the following relationships:

-   Alibaba Cloud Linux 2.1903 LTS 64-bit: the default standard image version.
-   Alibaba Cloud Linux 2.1903 64-bit \(Quick Start\): vertically optimized from Alibaba Cloud Linux 2.1903 LTS 64-bit and based on Alibaba Cloud infrastructure. The boot speed of instances created by using images of this version is significantly improved and the default runtime of images of this version is the same as that of the standard version.

    **Note:** The kernel startup parameter of the Quick Start version cannot be modified.

-   Alibaba Cloud Linux 2.1903 LTS 64-bit \(AMD-compatible\): derived from Alibaba Cloud Linux 2.1903 LTS 64-bit and can be used to create AMD-compatible instances. Only the Unified Extensible Firmware Interface \(UEFI\) boot mode is supported.

    **Note:** Images of this version can be used to create instances of only the following Alibaba Cloud Bare Metal Instance families \(AMD-compatible\): ecs.ebmg6a, ecs.ebmc6a, and ecs.ebmr6a.

-   Alibaba Cloud Linux 2.1903 64-bit \(Trusted\): derived from Alibaba Cloud Linux 2.1903 LTS 64-bit and can be used to create Alibaba Cloud trusted instances.

    **Note:** Images of this version can be used to create instances of only the following trusted instance families: ecs.g6t and ecs.c6t.


## How do I use Alibaba Cloud Linux 2 in Alibaba Cloud?

Alibaba Cloud provides public images based on Alibaba Cloud Linux 2. When you create an ECS instance, you can click Public Image and then select a version of Alibaba Cloud Linux 2 images.

## Am I charged for using Alibaba Cloud Linux 2 in Alibaba Cloud ECS?

No, Alibaba Cloud Linux 2 images are provided free of charge. You are charged for only the ECS instances to which the images are applied.

## Which ECS instance types does Alibaba Cloud Linux 2 support?

Alibaba Cloud Linux 2 supports most ECS instance types, including ECS Bare Metal Instance types.

**Note:** Alibaba Cloud Linux 2 does not support instances that run on the Xen virtual machine monitor.

## Does Alibaba Cloud Linux 2 support 32-bit applications or libraries?

No, Alibaba Cloud Linux 2 does not support 32-bit applications or libraries.

## Does Alibaba Cloud Linux 2 provide a graphical user interface \(GUI\) desktop?

No, Alibaba Cloud Linux 2 does not provide a GUI desktop.

## Can I view the source code of Alibaba Cloud Linux 2 components?

Yes, Alibaba Cloud Linux 2 is open source. You can use the yumdownloader tool or visit the official Alibaba Cloud download pages to download the source code package. You can also download the source code tree of the Alibaba Cloud Linux 2 kernel from GitHub. For more information, visit [Github](https://github.com/alibaba/cloud-kernel).

## Is Alibaba Cloud Linux 2 backward-compatible with the current Aliyun Linux versions?

Yes, Alibaba Cloud Linux 2 is compatible with Aliyun Linux 17.01.

**Note:** You may need to re-compile a compiled kernel module on Alibaba Cloud Linux 2 before the module can be used.

## Can I use Alibaba Cloud Linux 2 in an on-premises environment?

Yes, you can use Alibaba Cloud Linux 2 in an on-premises environment. Alibaba Cloud Linux 2 provides local images in the QCOW2 format. These images support only kernel-based virtual machines \(KVMs\). For more information, see [Use Alibaba Cloud Linux 2 images in an on-premises environment](/intl.en-US/Images/Alibaba Cloud Linux 2/Features and interfaces supported by Alibaba Cloud Linux 2/Use Alibaba Cloud Linux 2 images in an on-premises environment.md).

## Which third-party applications can run on Alibaba Cloud Linux 2?

Alibaba Cloud Linux 2 is binary compatible with CentOS 7.6.1810. Therefore, applications that can run on CentOS can also run on Alibaba Cloud Linux 2.

## What are the advantages of Alibaba Cloud Linux 2 over other Linux operating systems?

Alibaba Cloud Linux 2 is binary compatible with CentOS 7.6.1810 and provides differentiated operating system features.

Compared with CentOS and RHEL, Alibaba Cloud Linux 2 has the following advantages:

-   Updates are released at a faster pace. Updated Linux kernels, user-mode software, and toolkits are provided.
-   Alibaba Cloud Linux 2 works out of the box and requires minimal configurations.
-   Alibaba Cloud Linux 2 is optimized to work with the hypervisor and maximizes performance for users.
-   Unlike RHEL, Alibaba Cloud Linux 2 does not have any runtime charges. Different from CentOS, Alibaba Cloud provides commercial support for Alibaba Cloud Linux 2.

## How does Alibaba Cloud Linux 2 protect data security?

Alibaba Cloud Linux 2 is binary compatible with CentOS 7.6.1810 and RHEL 7.6 and complies with the RHEL safety specifications. Alibaba Cloud Linux 2 uses the following methods to protect your data:

-   Uses industry-standard vulnerability scan and security test tools to perform periodical security scanning.
-   Periodically assesses the CVE patch updates of CentOS 7 to fix operating system security vulnerabilities.
-   Supports existing solutions of Alibaba Cloud for operating system security hardening.
-   Uses the same mechanism as CentOS 7 to release user security alerts and patch updates.

## Does Alibaba Cloud Linux 2 support data encryption?

Yes, Alibaba Cloud Linux 2 retains the CentOS 7 data encryption toolkit and supports the data encryption solution coordinately implemented by Key Management Service \(KMS\) and CentOS 7.

## How do I grant permissions to manage Alibaba Cloud Linux 2?

You can grant management permissions in Alibaba Cloud Linux 2 in the same manner as you would in CentOS 7. This means you can use the same commands to grant management permissions in Alibaba Cloud Linux 2 as you would in CentOS 7. The default permission configurations in images of these two operating systems are the same.

