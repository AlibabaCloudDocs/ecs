---
keyword: [Alibaba Cloud, Alibaba Cloud Linux, ecs, native Linux]
---

# Overview

Alibaba Cloud Linux 2 \(formerly known as Aliyun Linux 2\) is an operating system developed by Alibaba Cloud and is fully compatible with the CentOS 7 ecosystem. It provides a safe, stable, and customized high-performance environment for applications on Elastic Compute Service \(ECS\) instances. Alibaba Cloud Linux 2 is optimized for the cloud infrastructure and aims to deliver a better runtime experience. You can create an instance from an Alibaba Cloud Linux 2 image. Alibaba Cloud Linux 2 images are free to use, and Alibaba Cloud provides long-term technical support \(LTS\) for them.

For more information, visit the [Alibaba Cloud Linux 2 product page](https://www.alibabacloud.com/en/products/alinux).

## Scenarios

Alibaba Cloud Linux 2 is suitable for the following scenarios:

-   Various workloads in cloud environments, such as databases, cloud native containers, data analytics, web applications, and other workloads in the production environment.
-   Various instance families, including ECS Bare Metal Instance families. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).
    -   Alibaba Cloud Linux 3 supports instance types that have up to 768 vCPUs.
    -   Alibaba Cloud Linux 3 supports instance types that have 0.5 GiB to 12,288 GiB of memory.
    -   Alibaba Cloud Linux 3 does not support non-I/O optimized instances.

## Benefits

Compared with other Linux distributions, Alibaba Cloud Linux 2 has the following advantages:

-   Alibaba Cloud provides free long-term software maintenance and technical support for Alibaba Cloud Linux 2.
-   Alibaba Cloud Linux 2 is optimized for integration with the Alibaba Cloud infrastructure and provides faster system startup and higher runtime performance. Alibaba Cloud Linux 2 has been long-tested and refined in a large number of scenarios within the Alibaba Economy to provide optimal stability.
-   Alibaba Cloud Linux 2 is equipped with an updated Linux kernel, user-mode packages, and toolkits, and provides the latest enhanced operating system features from the Linux community to power cloud-based application environments.
-   Alibaba Cloud Linux 2 offers a streamlined kernel and increased protection against security risks. Alibaba Cloud Linux 2 provides policies to monitor and fix security vulnerabilities and ensure constant system security.

## Features

-   Alibaba Cloud Linux 2 is distributed with the latest version of the Alibaba Cloud kernel. The kernel has the following features:
    -   The Alibaba Cloud kernel is based on Linux kernel V4.19 with the LTS from the kernel community. The Alibaba Cloud kernel is optimized for cloud-based scenarios, improved performance, and bug fixes. For more information, see [Release notes](/intl.en-US/Images/Alibaba Cloud Linux 2/Release notes.md).
    -   Alibaba Cloud Linux 2 provides customized and optimized kernel startup parameters and system configuration parameters for the ECS instance environment.
    -   Alibaba Cloud Linux 2 provides kdump, which is a kernel dumping mechanism used when the operating system fails. You can enable or disable this feature without the need to restart the operating system.
    -   Alibaba Cloud Linux 2 provides Kernel Live Patching \(KLP\).
-   Alibaba Cloud Linux 2 has software pre-installed or updated.
    -   The user-mode package is compatible with the latest version of CentOS 7 and can run on Alibaba Cloud Linux 2.
    -   Alibaba Cloud Linux 2 is pre-installed with Alibaba Cloud CLI.
    -   The network module is changed from network.service to systemd-networkd.
    -   Fixes for common vulnerabilities and exposures \(CVE\) are continuously updated until the end of life \(EOL\) of Alibaba Cloud Linux 2. For more information, see [Alibaba Cloud Linux 2.1903 Security Advisories](http://mirrors.aliyun.com/alinux/cve/alinux2.xml). Alibaba Cloud Linux 2 provides solutions to automatically fix vulnerabilities. For more information, see [Use YUM to perform security updates](/intl.en-US/Images/Alibaba Cloud Linux 2/Features and interfaces supported by Alibaba Cloud Linux 2/Use YUM to perform security updates.md).
-   Alibaba Cloud Linux 2 accelerates the startup process, improves runtime performance, and enhances system stability in the following ways:
    -   Alibaba Cloud Linux 2 optimizes the startup speed of ECS instances. Tests have proven that Alibaba Cloud Linux 2 can reduce the startup time by up to 60% compared with other operating systems.
    -   Alibaba Cloud Linux 2 optimizes scheduling, memory, I/O, and network subsystems. In some open source benchmark tests, Alibaba Cloud Linux 2 offers a performance increase of 10% to 30% compared with other operating systems.
    -   Alibaba Cloud Linux 2 provides enhanced system stability and can reduce downtime by 50% compared with other operating systems.

## Images

|Image|ID of the latest version|Description|
|-----|------------------------|-----------|
|Alibaba Cloud Linux 2.1903 LTS 64-bit|aliyun\_2\_1903\_x64\_20G\_alibase\_20210325.vhd|The default standard image version of Alibaba Cloud Linux 2.|
|Alibaba Cloud Linux 2.1903 64-bit \(Quick Start\)|aliyun\_2\_1903\_x64\_20G\_qboot\_alibase\_20210325.vhd|This image version is a customized image based on the Alibaba Cloud kernel. It supports quick boot \(Qboot\) and starts instances from the kernel. Instances created from images of this version start faster than those created from other images, and share the same default run time as those created from images of standard versions. This image version has the following characteristics:

-   It accelerates only the initial startup of instances, and subsequently starts instances at a normal speed.
-   It optimizes and accelerates the process of initializing memory, modularizes devices such as mice that take time to start, and speeds up the kernel boot.
-   It replaces the cloud-init service with the latest AliyunInit service. This reduces the amount of time required to initialize the operating system.
-   The kernel startup parameter of the Quick Start version cannot be modified.
-   The following instance families are not supported: GPU-accelerated compute-optimized instance families, vGPU-accelerated instance families, FPGA-accelerated compute-optimized instance families, NPU-accelerated compute-optimized instance families, heterogeneous service type instance families, Super Computing Cluster \(SCC\) instance families, and security-enhanced instance families.
-   Images of this version are available in the following regions: China \(Hangzhou\), China \(Shenzhen\), China \(Beijing\), China \(Zhangjiakou\), and China \(Hong Kong\). |
|Alibaba Cloud Linux 2.1903 LTS 64-bit \(AMD-compatible\)|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20210218.vhd|This image version is derived from Alibaba Cloud Linux 2.1903 LTS 64-bit and can be used to create Alibaba Cloud AMD-compatible instances. This image version supports only the Unified Extensible Firmware Interface \(UEFI\) boot mode. **Note:** Instances of only Alibaba Cloud AMD-compatible ECS Bare Metal Instance families can use this image version. For more information, see [Release notes of images that are applicable only to some instance families](/intl.en-US/Images/Alibaba Cloud Linux 2/Release notes.mdsection_zai_t2o_j01). |
|Alibaba Cloud Linux 2.1903 64-bit \(Trusted\)|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20210325.vhd|The image version is derived from Alibaba Cloud Linux 2.1903 LTS 64-bit and can be used to create Alibaba Cloud trusted instances. **Note:** Instances of only Alibaba Cloud trusted instance families can use this image version. For more information, see [Release notes of images that are applicable only to some instance families](/intl.en-US/Images/Alibaba Cloud Linux 2/Release notes.mdsection_zai_t2o_j01). |

## Billing

Alibaba Cloud Linux 2 images are provided for free. However, you must pay for other resources such as vCPUs, memory, storage, public bandwidth, and snapshots. For more information, see [Billing overview](/intl.en-US/Pricing/Billing overview.md).

## Obtain Alibaba Cloud Linux 2 images

You can use one of the following methods to obtain and use Alibaba Cloud Linux 2 images:

-   ECS instances
    -   When you create an ECS instance, select **Public Image**, and then select Alibaba Cloud Linux 2 and its version.
        -   For information about how to create an instance, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).
        -   For information about the differences among Alibaba Cloud Linux 2 images, see [What are the differences among Alibaba Cloud Linux 2 images?](/intl.en-US/Images/Alibaba Cloud Linux 2/FAQ.md).
    -   Change the operating system of an existing ECS instance to Alibaba Cloud Linux 2 by replacing the system disk. For more information, see [Replace the system disk \(public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace the system disk (public images).md).
-   On-premises environments such as a virtualization environment based on Kernel-based Virtual Machine \(KVM\)

    Download and install an Alibaba Cloud Linux 2 image, and then restart the system. For more information, see [Use Alibaba Cloud Linux 2 images in an on-premises environment](/intl.en-US/Images/Alibaba Cloud Linux 2/Features and interfaces supported by Alibaba Cloud Linux 2/Use Alibaba Cloud Linux 2 images in an on-premises environment.md).


## Use Alibaba Cloud Linux 2

-   View or modify system parameters

    You can run the sysctl command to view or modify the runtime system parameters of Alibaba Cloud Linux 2. Alibaba Cloud Linux 2 has the following kernel configuration parameters updated in the /etc/sysctl.d/50-aliyun.conf file.

    |System parameter setting|Description|
    |------------------------|-----------|
    |`kernel.hung_task_timeout_secs = 240`|Increases the kernel hung\_task timeout period in seconds to avoid frequent hung\_task prompts.|
    |`kernel.panic_on_oops = 1`|Throws the kernel panic exception when an Oops error occurs in the kernel. System failure details are automatically captured if kdump is configured.|
    |`kernel.watchdog_thresh = 50`|Increases the thresholds for events such as hrtimer, NMI, soft lockup, and hard lockup to avoid potential kernel false positives.|
    |`kernel.hardlockup_panic = 1`|Throws the kernel panic exception when a hard lockup error occurs in the kernel. System failure details are automatically captured if kdump is configured.|

-   View kernel parameters

    You can run the `cat /proc/cmdline` command to view the runtime kernel parameters of Alibaba Cloud Linux 2. Alibaba Cloud Linux 2 has the following kernel parameters updated.

    |Kernel parameter setting|Description|
    |------------------------|-----------|
    |`crashkernel=0M-2G:0M,2G-8G:192M,8G-:256M`|Reserves memory space for kdump.|
    |`cryptomgr.notests`|Disables crypto self-check during kernel startup to accelerate system startup.|
    |`cgroup.memory=nokmem`|Disables the kernel memory statistics feature of the memory cgroup to avoid potential kernel instability.|
    |`rcupdate.rcu_cpu_stall_timeout=300`|Increases the timeout threshold of RCU CPU Stall Detector to 300 seconds to avoid kernel false positives.|

-   Enable or disable kdump

    Alibaba Cloud Linux 2 provides the kdump service. After this service is enabled, kernel errors can be captured to help you analyze kernel failures.

    **Note:** If the memory of the selected instance type is smaller than or equal to 2 GiB, the kdump service cannot be used.

    -   Run the following commands to enable the kdump service:

        ```
        # Enable the kdump service.
        sudo systemctl enable kdump.service
        # Restart the kdump service.
        sudo systemctl restart kdump.service
        ```

    -   Run the following commands in sequence to return the memory address space reserved by the kdump service to the operating system and disable the kdump service:

        ```
        # Change the configuration in the /sys/kernel/kexec_crash_size file.
        sudo sh -c 'echo 0 > /sys/kernel/kexec_crash_size'
        # Disable the kdump service.
        sudo systemctl disable kdump.service
        # Stop the kdump service.
        sudo systemctl stop kdump.service
        ```

        **Note:** After the memory address space reserved by the kdump service is returned to the operating system, you must restart the operating system before you can re-enable the kdump service.

-   Configure the network

    By default, Alibaba Cloud Linux 2 uses systemd-networkd to configure the network. The configuration file for DHCP or static IP addresses is located in the /etc/systemd/network/ directory.

    ```
    # Restart the network.
    sudo systemctl restart systemd-networkd
    ```

-   Obtain the Debuginfo package and the source code package
    -   Run the following commands to obtain the Debuginfo package:

        ```
        # Install yum-utils.
        sudo yum install -y yum-utils
        # Install the Debuginfo package. packageName specifies the name of the software package to be installed.
        sudo debuginfo-install -y <packageName>
        ```

    -   Run the following commands to obtain the source code package:

        ```
        # Install the source code.
        sudo yum install -y alinux-release-source
        # Install yum-utils.
        sudo yum install -y yum-utils
        # Install the source code package. sourcePackageName specifies the name of the software package to be installed.
        sudo yumdownloader --source <sourcePackageName>
        ```

-   Use experimental software packages

    Experimental software packages are provided by Alibaba Cloud, but are not fully tested. Alibaba Cloud do not guarantee the quality of these packages. Alibaba Cloud Linux 2 provides the following types of experimental packages:

    -   Experimental software packages that serve common purposes

        -   `Golang 1.12`
        -   `Golang 1.13`
        Run the following commands to install an experimental software package that serves common purposes:

        ```
        # Enable support for YUM repositories.
        sudo yum install -y alinux-release-experimentals
        # Install an experimental software package that serves common purposes. packageName specifies the name of the software package to be installed.
        sudo yum install -y <packageName>
        ```

    -   Development kits that support SCL plug-ins

        -   Development kit based on `GCC-7.3.1`: devtoolset-7
        -   Development kit based on `GCC-8.2.1`: devtoolset-8
        -   Development kit based on `GCC-9.1.1`: devtoolset-9
        Run the following commands to install an experimental software package that serves common purposes:

        ```
        # Install `scl-utils`.
        sudo yum install -y scl-utils
        # Enable support for YUM repositories.
        sudo yum install -y alinux-release-experimentals
        # Install the software packages that you need from the YUM repositories. The following sample commands are run to install all development kits that support SCL plug-ins:
        sudo yum install -y devtoolset-7-gcc devtoolset-7-gdb devtoolset-7-binutils devtoolset-7-make
        sudo yum install -y devtoolset-8-gcc devtoolset-8-gdb devtoolset-8-binutils devtoolset-8-make
        sudo yum install -y devtoolset-9-gcc devtoolset-9-gdb devtoolset-9-binutils devtoolset-9-make
        ```

        After the software packages are installed, you can use the later versions of GCC and related tools. The following code provides an example of how to run SCL software:

        ```
        # Specify the repository name to view an existing SCL. In this example, the devtoolset-7 repository is used.
        scl -l devtoolset-7
        # Run the related SCL software.
        scl enable devtoolset-7 'gcc --version'
        ```


## Update history

-   For information about the release notes of Alibaba Cloud Linux 2, see [Release notes](/intl.en-US/Images/Alibaba Cloud Linux 2/Release notes.md).
-   For information about the CVE updates of Alibaba Cloud Linux 2, see [Alibaba Cloud Linux 2.1903 Security Advisories](http://mirrors.aliyun.com/alinux/cve/alinux2.xml).

## Technical support

Alibaba Cloud provides the following technical support for Alibaba Cloud Linux 2:

-   Five years of LTS is guaranteed in the form of security updates and vulnerability fixes until the release lifecycle ends on March 31, 2024. You can use one of the following methods to obtain free LTS:
    -   [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)
    -   [GitHub](https://alibaba.github.io/cloud-kernel/os.html?spm=5176.cnalinux.0.0.1f8323d1WpS5ZY&aly_as=32Di8ZOj)
-   Images are updated every four months. Updates cover new features, security updates, and vulnerability fixes.
-   Security updates are provided from YUM repositories. You can run the yum update command to update an image to the latest version.

