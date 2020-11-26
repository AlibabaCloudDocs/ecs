# Create an NVIDIA GPU-accelerated instance

NVIDIA GPU-accelerated instances must be installed with drivers to use the GPUs. You can configure the drivers to be automatically installed when you create instances or manually install the drivers after the instances are created.

You must complete the following preparations to create an ECS instance:

1.  Create an account and complete the account information.
    -   Create an Alibaba Cloud account. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/doc-detail/50482.htm).
    -   Bind your credit card or PayPal account. For more information, see [Add a payment method](https://www.alibabacloud.com/help/doc-detail/50517.htm).
    -   To purchase ECS instances in mainland China regions, you must complete real-name verification. For more information, see [Real-name registration FAQ](https://www.alibabacloud.com/help/doc-detail/52595.htm).
2.  Alibaba Cloud provides a default VPC in each region. If you do not want to use the default VPC, you can create a VPC and a VSwitch in the region in which to create the instance. For more information, see [Create an IPv4 VPC network](/intl.en-US/Quick Start/Create an IPv4 VPC network.md).
3.  Alibaba Cloud provides a default security group in each region. If you do not want to use the default security group, you can create a security group in the region in which to create the instance. For more information, see [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md).

If you need other extended features, you must complete corresponding preparations:

-   To specify an SSH key pair when you create a Linux instance, you must create the SSH key pair in the corresponding region. For more information, see [Create an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Create an SSH key pair.md).
-   To add user data for the instance, you must first prepare user data. For more information about how to prepare user data, see [Prepare user data](/intl.en-US/Instance/Manage instances/User data/Prepare user data.md).
-   To associate an ECS instance with an instance RAM role, you must create the RAM role, attach permission policies to the role, and then bind the role to the instance. For more information, see [Bind an instance RAM role](/intl.en-US/Security/Instance RAM roles/Bind an instance RAM role.md).

The following drivers are involved:

-   GPU drivers: used to drive physical GPUs. GPU drivers can be installed only on GPU-accelerated instances that are not equipped with vGPUs.
-   GRID drivers: used to provide instances with graphics acceleration capabilities. You can install GRID drivers on GPU-accelerated instances regardless of whether the instances are equipped with vGPUs. Instances of the vgn6i and vgn5i instance families are equipped with vGPUs.

The following table describes whether the preceding drivers can be installed on different types of GPU-accelerated instances.

|Driver|GPU-accelerated instance equipped with vGPUs \(instance of the vgn6i or vgn5i instance family\)|GPU-accelerated instance not equipped with vGPUs|
|------|-----------------------------------------------------------------------------------------------|------------------------------------------------|
|GPU driver|Not supported|Supported|
|GRID driver|Supported|Supported|

## Procedure

The following procedure focuses on the configurations related to NVIDIA GPUs when you create NVIDIA GPU-accelerated instances. For information about other general configurations, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

1.  Go to the [Custom Launch](https://ecs-buy.aliyun.com/wizard/#/) tab of the instance buy page in the ECS console.

2.  Configure the settings in the Basic Configurations step.

    **Note:** GPU-accelerated instance types are available only in specific regions and zones. For more information, see [ECS Instance Types Available for Each Region](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion). Select a billing method and enter an instance type name to search for the instance type.

    The vGPUs on the vgn6i and vgn5i instances are generated from a full GPU virtualization solution with mediated pass-through. You can install only GRID drivers on these instances. Configure the instance and the image based on the instance type.

    -   Create a GPU-accelerated instance equipped with vGPUs \(vgn6i and vgn5i\)
        -   **Instance Type**: Set Architecture to **Heterogeneous Computing** \> ****, set Category to Visualization Compute Optimized Type with GPU, and then select an instance type.
        -   **Image**: No images that are pre-installed with GRID drivers are provided. You must purchase a GRID license, and manually install a GRID driver and activate the license after the instance is created.
    -   Create a GPU-accelerated instance not equipped with vGPUs
        -   **Instance Type**: Set **Architecture to** \> **Heterogeneous Computing**, set Category to Visualization Compute Optimized Type with GPU, and then select an instance type.
        -   **Image**: You can install GPU drivers on GPU-accelerated instances that are not equipped with vGPUs. You can use one of the following methods to install GPU drivers.

            **Note:** If you select Shared Image or Custom Image, make sure that the selected image is pre-installed with the required GPU driver and relevant software.

            -   Select Auto-install GPU Driver.

                Public images are base images provided by Alibaba Cloud or third-party vendors. The following Linux images allow GPU drivers to be automatically installed:

                -   CentOS 64-bit images that are supplied and tested by Alibaba Cloud
                -   Ubuntu 16.04 64-bit images
                -   Ubuntu 18.04 64-bit images
                -   SUSE Linux Enterprise Server 12 SP2 64-bit images
                -   Alibaba Cloud Linux 64-bit images
                If you select an image that allows GPU drivers to be automatically installed, select **Auto-install GPU Driver**, and then select the versions of the GPU driver, CUDA, and cuDNN library. If you want to create an instance for a new business system, we recommend that you select the latest versions.

                After you select **Auto-install GPU Driver**, you can choose whether to automatically install the GPU cloud accelerator. Apsara AI Accelerator \(AIACC\) is the GPU cloud accelerator provided by Alibaba Cloud. It enables you to build a deep learning training system based on a high-performance distributed architecture and accelerate AI training performance. For more information, see [Use the GPU cloud accelerator AIACC](/intl.en-US/Instance/Instance type families/Compute optimized type family with GPU/Use the GPU cloud accelerator AIACC.md).

                **Note:** The GPU cloud accelerator is not supported in CentOS 8, CentOS 6, SUSE Linux, or Alibaba Cloud Linux.

                If you select an image that allows GPU drivers to be automatically installed but do not select **Auto-install GPU Driver**, you can still configure the installation script of the GPU driver in the **User Data** section. For more information, see the [Automatic installation script V3.1](#section_wrk_m0g_0zr) section.

                **Note:** If you call the RunInstances operation to create an NVIDIA GPU-accelerated instance, you must use the UserData parameter to upload the installation script. The script must be Base64-encoded.

                ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9490359951/p39823.png)

            -   In Alibaba Cloud Marketplace, select an image that is pre-installed with a GPU driver and relevant software.

                Alibaba Cloud Marketplace provides images that have operating systems, application environments, and various software pre-installed. Alibaba Cloud Marketplace images are reviewed by Alibaba Cloud to ensure quality and stability. You can use these images to deploy ECS instances without additional configurations. The NVIDIA GPU Cloud VM Image provides an optimized environment for running deep learning frameworks, HPC applications, and HPC visualization tools available from the NVIDIA GPU Cloud \(NGC\) container registry. For more information, see [Deploy an NGC environment on instances with GPU capabilities](/intl.en-US/Best Practices/GPU instances/Deploy an NGC environment on instances with GPU capabilities.md).

            -   Manually install a GRID driver after the instance is created. For more information, see [Manually install a GPU driver](/intl.en-US/Instance/Instance type families/Compute optimized type family with GPU/Manually install a GPU driver.md).
            You can also install a GRID driver on a GPU-accelerated instance that is not equipped with vGPUs. However, no images that is pre-installed with GRID drivers are provided. You must purchase a GRID license, and manually install a GRID driver and activate the license after the instance is created.

3.  Configure the settings in the Networking step.

    When you configure the parameters, take note of the following items:

    -   **Network Type**: Select **VPC**.
    -   **Public IP Address**: Configure the settings for network usage.

        **Note:** If you select an image of Windows 2008 R2 or earlier in the **Basic Configurations** step, you cannot connect to the NVIDIA GPU-accelerated instance by using a VNC management terminal after the GPU driver is installed and activated. A black screen or the startup interface persists when you attempt to connect to the instance. You must select **Assign Public IP Address** in the Public IP Address section, or associate an elastic IP address \(EIP\) after you create the instance. This way, you can connect to the instance over another protocol such as Remote Desktop in Windows \(RDP\), PCOIP, or XenDeskop HDX 3D. RDP does not support applications such as DirectX and OpenGL. You must install the VNC service and client on your own.

4.  Configure the settings in the System Configurations step.

    When you configure the parameters, take note of the following items:

    -   **Logon Credentials**: We recommend that you select **Key Pair** or **Password**. If you select **Set Later** and want to log on to the instance by using a VNC management terminal, you must bind an SSH key pair or reset the password. Then, you must restart the instance for the modification to take effect. If you restart the instance while the GPU driver is being installed, the installation fails.
    -   **User Data**:
        -   If you select **Auto-install GPU Driver** in the **Image** section in the **Basic Configurations** step, the precautions and shell script for automatically installing the GPU driver and CUDA are displayed in the User Data section. The automatic installation script is updated to V3.1.

            ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0590359951/p39825.png)

        -   If you do not select **Auto-install GPU Driver**, you can configure the installation script in the **User Data** section. For information about a sample script, see the [Automatic installation script V3.1](#section_wrk_m0g_0zr) section.
5.  Configure the parameters in the Grouping step, confirm the configurations in the Preview step, and then click Create Order or Create Instance.

    If an automatic installation script is configured, the system automatically installs the GPU driver when the instance is started. After the GPU driver is installed, the instance is automatically restarted for the GPU driver to run.

    **Note:** The GPU driver is more stable in persistence mode. The script automatically enables the persistence mode for the GPU driver. Then, the script adds the corresponding commands as a Linux system service to ensure that the persistence mode is automatically enabled for the GPU driver on instance startup.

    The automatic installation process may take 10 to 20 minutes based on the internal bandwidth and CPU cores of different instance types. During the process, the GPUs are not available. To prevent installation failures and keep the instance available, we recommend that you do not perform operations or install any other GPU-related software on the instance until the installation is complete. You can connect to the instance and view the installation progress and results in the installation log:

    -   If the installation is in progress, you can check the progress of the installation in the progress bar.
    -   If the installation succeeds, **ALL INSTALL OK** is displayed in the result.
    -   If the installation fails, **INSTALL FAIL** is displayed in the result.
    -   You can check the detailed installation log entries in the /root/auto\_install/auto\_install.log file.
    **Note:** If you replace the operating system after the instance is created, make sure that you use an image that allows GPU drivers and CUDA to be automatically installed to prevent failures in automatic installation.


## Script for automatically installing a GPU driver

When the instance is started for the first time, cloud-init automatically runs the shell script to install the GPU driver, CUDA, and cuDNN library.

-   The following table lists the versions of the GPU driver, CUDA, and cuDNN library that are available when you select **Auto-install GPU Driver**.

    |CUDA|GPU driver|cuDNN|Version of a supported public image \(only images supplied and tested by Alibaba Cloud\)|Supported instance family|
    |----|----------|-----|----------------------------------------------------------------------------------------|-------------------------|
    |10.2.89|440.64.00|7.6.5|    -   Alibaba Cloud Linux 2
    -   Ubuntu 18.04 and Ubuntu 16.04
    -   CentOS 8.x, CentOS 7.x, and CentOS 6.x
|    -   gn6v, gn6i, gn6e, gn5, gn5i, and gn4
    -   ebmgn6v, ebmgn6i, ebmgn6e, and ebmgn5i |
    |10.1.168|    -   440.64.00
    -   418.126.02
|    -   7.6.5
    -   7.5.0
|    -   Ubuntu 18.04 and Ubuntu 16.04
    -   CentOS 7.x and CentOS 6.x
|    -   gn6v, gn6i, gn6e, gn5, gn5i, and gn4
    -   ebmgn6v, ebmgn6i, ebmgn6e, and ebmgn5i |
    |10.0.130|    -   440.64.00
    -   418.126.02
|    -   7.6.5
    -   7.5.0
    -   7.4.2
    -   7.3.1
|    -   Ubuntu 18.04 and Ubuntu 16.04
    -   CentOS 7.x and CentOS 6.x
|    -   gn6v, gn6i, gn6e, gn5, gn5i, and gn4
    -   ebmgn6v, ebmgn6i, ebmgn6e, and ebmgn5i |
    |9.2.148|    -   440.64.00
    -   418.126.02
    -   390.116
|    -   7.6.5
    -   7.5.0
    -   7.4.2
    -   7.3.1
    -   7.1.4
|    -   Ubuntu 16.04
    -   CentOS 7.x and CentOS 6.x
|    -   gn6v, gn6e, gn5, gn5i, and gn4
    -   ebmgn6v, ebmgn6e, and ebmgn5i |
    |9.0.176|    -   440.64.00
    -   418.126.02
    -   390.116
|    -   7.6.5
    -   7.5.0
    -   7.4.2
    -   7.3.1
    -   7.1.4
    -   7.0.5
|    -   Ubuntu 16.04
    -   CentOS 7.x and CentOS 6.x
    -   SUSE 12sp2
|    -   gn6v, gn6e, gn5, gn5i, and gn4
    -   ebmgn6v, ebmgn6e, and ebmgn5i |
    |8.0.61|    -   440.64.00
    -   418.126.02
    -   390.116
|    -   7.1.3
    -   7.0.5
|    -   Ubuntu 16.04
    -   CentOS 7.x and CentOS 6.x
|    -   gn5, gn5i, and gn4
    -   ebmgn5i |

-   To configure an installation script in the **User Data** section, you can refer to the script described in the [Automatic installation script V3.1](#section_wrk_m0g_0zr) section.

    The automatic installation script V3.1 has the following benefits:

    -   It provides the latest versions of GPU driver, CUDA, and cuDNN library.
    -   You can log on to the instance while the GPU driver is being installed and view the installation progress bar. If the installation succeeds, the instance is automatically restarted. After you log on to the instance again, **ALL INSTALL OK** appears in the result. If the installation fails, **INSTALL FAIL** is displayed in the result.
    To use the automatic installation script V3.1, you must modify the version numbers of the GPU driver, CUDA, and cuDNN library in the script, and specify whether to install AIACC. If you do not need to install AIACC, change the value of IS\_INSTALL\_PERSEUS to FALSE. Example:

    ```
    IS_INSTALL_PERSEUS="FALSE"
    DRIVER_VERSION="440.64.00"
    CUDA_VERSION="10.2.89"
    CUDNN_VERSION="7.6.5"
    ```

    **Note:** If the image is a CentOS or SUSE image, the installation script uses the .run installation package. If the image is an Ubuntu image, the installation script uses the .deb installation package.


## Automatic installation script V3.1

```
#! /bin/sh

#Please input version to install
IS_INSTALL_PERSEUS=""
DRIVER_VERSION=""
CUDA_VERSION=""
CUDNN_VERSION=""
IS_INSTALL_RAPIDS="FALSE"

INSTALL_DIR="/root/auto_install"

#using .deb to install driver and cuda on ubuntu OS
#using .run to install driver and cuda on ubuntu OS
auto_install_script="auto_install.sh"

script_download_url=$(curl http://100.100.100.200/latest/meta-data/source-address | head -1)"/opsx/ecs/linux/binary/script/${auto_install_script}"
echo $script_download_url

mkdir $INSTALL_DIR && cd $INSTALL_DIR
wget -t 10 --timeout=10 $script_download_url && sh ${INSTALL_DIR}/${auto_install_script} $DRIVER_VERSION $CUDA_VERSION $CUDNN_VERSION $IS_INSTALL_PERSEUS $IS_INSTALL_RAPIDS
```

**References**  


[RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md)

[Manually install a GPU driver](/intl.en-US/Instance/Instance type families/Compute optimized type family with GPU/Manually install a GPU driver.md)

[Install NVIDIA GRID drivers on GPU-accelerated Linux instances](/intl.en-US/Instance/Instance type families/Compute optimized type family with GPU/Install NVIDIA GRID drivers on GPU-accelerated Linux instances.md)

[Manually uninstall the GPU driver](/intl.en-US/Instance/Instance type families/Compute optimized type family with GPU/Manually uninstall the GPU driver.md)

[GPU monitoring](/intl.en-US/Host monitoring/GPU monitoring.md)

