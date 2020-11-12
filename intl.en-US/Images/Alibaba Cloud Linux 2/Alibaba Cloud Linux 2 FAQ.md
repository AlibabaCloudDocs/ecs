# Alibaba Cloud Linux 2 FAQ

This topic describes the frequently asked questions \(FAQ\) about Aliyun Linux 2 images and their solutions.

-   [What are the differences between Aliyun Linux and Alibaba Cloud Linux 2?](#section_imn_fim_626)
-   [How do I use Alibaba Cloud Linux 2 in Alibaba Cloud public cloud?](#section_ih8_6n8_aty)
-   [Will I be charged for using Alibaba Cloud Linux 2 in Alibaba Cloud ECS?](#section_7na_hla_jpe)
-   [Which ECS instance types does Alibaba Cloud Linux 2 support?](#section_dja_kr5_fuo)
-   [Does Alibaba Cloud Linux 2 support 32-bit applications or libraries?](#section_esh_mwl_ir7)
-   [Does Alibaba Cloud Linux 2 provide a graphical user interface \(GUI\) desktop?](#section_o24_dn0_rae)
-   [Can I view the source code of Alibaba Cloud Linux 2 components?](#section_wtr_xdj_ktn)
-   [Is Alibaba Cloud Linux 2 backward-compatible with the current Aliyun Linux version?](#section_a7h_hcy_6ps)
-   [Can I use Alibaba Cloud Linux 2 in an on-premises environment?](#section_2go_rnh_810)
-   [Which third-party applications can run on Alibaba Cloud Linux 2?](#section_37f_kfg_e2f)
-   [What are the advantages of Alibaba Cloud Linux 2 compared with other Linux operating systems?](#section_0hi_2xq_mb4)
-   [How does Alibaba Cloud Linux 2 protect data security?](#section_2gz_az0_nd6)
-   [Does Alibaba Cloud Linux 2 support data encryption?](#section_dn9_qtz_eoz)
-   [How do I grant permissions to manage Alibaba Cloud Linux 2?](#section_z2y_011_tl5)

## What are the differences between Aliyun Linux and Alibaba Cloud Linux 2?

Alibaba Cloud Linux 2 differs in the following aspects:

-   Alibaba Cloud Linux 2 is optimized for containers to better support cloud-native applications.
-   Alibaba Cloud Linux 2 is equipped with an updated Linux kernel and updated user-mode packages.

## How do I use Alibaba Cloud Linux 2 in Alibaba Cloud public cloud?

Alibaba Cloud provides public images for Alibaba Cloud Linux 2. You can choose **Public Image** \> **Alibaba Cloud Linux**, and then select a version of Alibaba Cloud Linux 2 image when you create an ECS instance.

## Will I be charged for using Alibaba Cloud Linux 2 in Alibaba Cloud ECS?

No, Alibaba Cloud Linux 2 images are free of charge. You will only be charged for the ECS instances to which the images are applied.

## Which ECS instance types does Alibaba Cloud Linux 2 support?

Alibaba Cloud Linux 2 supports most ECS instance types, including ECS Bare Metal Instance types.

**Note:** Alibaba Cloud Linux 2 does not support instances on the Xen virtual machine monitor.

## Does Alibaba Cloud Linux 2 support 32-bit applications or libraries?

No. Alibaba Cloud Linux 2 does not support 32-bit applications or libraries.

## Does Alibaba Cloud Linux 2 provide a graphical user interface \(GUI\) desktop?

No. Alibaba Cloud Linux 2 does not provide a GUI desktop.

## Can I view the source code of Alibaba Cloud Linux 2 components?

Yes. Alibaba Cloud Linux 2 is open source. You can use the yumdownloader tool or visit the official Alibaba Cloud download pages to download the source code package. You can also download the source code tree of the Aliyun Linux kernel from GitHub. For more information, visit [Github](https://github.com/alibaba/cloud-kernel).

## Is Alibaba Cloud Linux 2 backward-compatible with the current Aliyun Linux version?

Yes. Alibaba Cloud Linux 2 is compatible with Aliyun Linux 17.01.

**Note:** You may need to re-compile a compiled kernel module on Alibaba Cloud Linux 2 before it can be used.

## Can I use Alibaba Cloud Linux 2 in an on-premises environment?

Yes, you can use Alibaba Cloud Linux 2 on an on-premises environment. Alibaba Cloud Linux 2 provides local images in the qcow2 format. These images are supported only for Kernel-based virtual machines \(KVMs\). For more information, see [Use Alibaba Cloud Linux 2 images in an on-premises environment](/intl.en-US/Images/Alibaba Cloud Linux 2/Features and interfaces supported by Alibaba Cloud Linux 2/Use Alibaba Cloud Linux 2 images in an on-premises environment.md).

## Which third-party applications can run on Alibaba Cloud Linux 2?

Alibaba Cloud Linux 2 is binary compatible with CentOS 7.6.1810. Applications that can run on CentOS can also run on Alibaba Cloud Linux 2.

## What are the advantages of Alibaba Cloud Linux 2 compared with other Linux operating systems?

Alibaba Cloud Linux 2 is binary compatible with CentOS 7.6.1810 and provides differentiated operating system features.

Compared with CentOS and RHEL, Alibaba Cloud Linux 2 has the following advantages:

-   Updates are released at a faster pace. Updated Linux kernels, user-mode software, and toolkits are provided.
-   Alibaba Cloud Linux 2 works out of the box and requires minimal configuration.
-   Alibaba Cloud Linux 2 is optimized to work with the optimized hypervisor and maximizes performance for users.
-   Unlike RHEL, Alibaba Cloud Linux 2 does not have any runtime charges. Different from CentOS, Alibaba Cloud provides commercial support for Alibaba Cloud Linux 2.

## How does Alibaba Cloud Linux 2 protect data security?

Alibaba Cloud Linux 2 is binary compatible with CentOS 7.6.1810 and RHEL 7.6 and complies with the RHEL safety specifications. Alibaba Cloud Linux 2 uses the following tools to protect your data:

-   Uses industry-standard vulnerability scan and security test tools to perform periodical security scanning.
-   Periodically assesses the CVE patch updates of CentOS 7 to fix operating system security vulnerabilities.
-   Supports existing solutions of Alibaba Cloud for operating system security hardening.
-   Uses the same mechanism as CentOS 7 to release user security alerts and patch updates.

## Does Alibaba Cloud Linux 2 support data encryption?

Yes. Alibaba Cloud Linux 2 uses the CentOS 7 data encryption toolkit implemented by Key Management Service \(KMS\) to encrypt data.

## How do I grant permissions to manage Alibaba Cloud Linux 2?

You can grant management permissions in Alibaba Cloud Linux 2 in the same manner as you would in CentOS 7. This means the same commands can be used to grant management permissions in both Alibaba Cloud CentOS 7 images and Alibaba Cloud Linux 2.

