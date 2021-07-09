# Install a NVIDIA GRID driver on a GPU-accelerated Linux instance

This topic describes how to install a NVIDIA GRID driver and build a desktop environment on a GPU-accelerated Linux instance.

-   A GPU-accelerated instance is created and is able to access the Internet.

    **Note:** This topic describes how to install NVIDIA GRID drivers on GPU-accelerated Linux instances. For GPU-accelerated Windows instances, you can select paid images that have NVIDIA GRID drivers pre-installed when you create the instances. For more information, see [Create an NVIDIA GPU-accelerated instance]().

    When you create an instance, we recommend that you select an image from the **Public Image** drop-down list. If you select an image pre-installed with the NVIDIA GRID driver in the **Image Marketplace** dialog box, you must disable the nouveau driver after you create the instance.

    nouveau is an open source driver. It must be disabled before you can install another driver. You can create a nouveau.conf file in the /etc/modprobe.d directory and add `blacklist nouveau` to the file to disable nouveau.

-   A Virtual Network Computing \(VNC\) application is installed. In this example, VNC Viewer is used.
-   A GRID license is obtained from [NVIDIA](https://www.nvidia.com/object/nvidia-enterprise-account.html). You must build a license server. You can purchase an Elastic Compute Service \(ECS\) instance and build a license server by following the tutorial on the NVIDIA official website.

You must install a NVIDIA GRID driver if your GPU-accelerated instances \(excluding ecs.vgn6i-m4-vws.xlarge and ecs.vgn6i-m8-vws.2xlarge instances\) need to support Open Graphics Library \(OpenGL\). By default, the NVIDIA GRID license that is granted to NVIDIA GPUs such as P100, P4, and V100 is not activated. You can use a trial license to activate the license and use OpenGL.

**Note:** Only NVIDIA partners can download the driver from the NVIDIA official website. This topic describes how to obtain the installation package of the NVIDIA GRID driver from Alibaba Cloud.

This topic describes how to install NVIDIA GRID drivers on GPU-accelerated instances that are not equipped with vGPUs. For information about how to install NVIDIA GRID drivers on vgn6i or vgn5i GPU-accelerated instances that are equipped with vGPUs, see [Install an NVIDIA GRID driver on a GPU-accelerated virtualization Linux instance](/intl.en-US/Instance/Instance type families/Compute optimized type family with GPU/Install NVIDIA GRID drivers on vgn6i or vgn5i Linux instances.md).

## Procedure

Perform the following operations to install a NVIDIA GRID driver:

-   Ubuntu 16.04 64-bit:
    1.  [Install a NVIDIA GRID driver on a Linux instance that runs Ubuntu 16.04 64-bit](#section_zsd_ytk_ngb)
    2.  [Test the NVIDIA GRID driver installed on an instance that runs Ubuntu 16.04 64-bit](#section_itd_ytk_ngb)
-   CentOS 7.3 64-bit:
    1.  [Install a NVIDIA GRID driver on a Linux instance that runs CentOS 7.3 64-bit](#section_tvd_ytk_ngb)
    2.  [Test the NVIDIA GRID driver installed on an instance that runs CentOS 7.3 64-bit](#section_dwd_ytk_ngb)

## Install a NVIDIA GRID driver on a Linux instance that runs Ubuntu 16.04 64-bit

1.  [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using a username and password.md).

2.  Run the following commands in sequence to upgrade the system and install KDE:

    ```
    apt-get update
    apt-get upgrade
    apt-get install kubuntu-desktop
    ```

3.  Run the `reboot` command to restart the system.

4.  Connect to the Linux instance again. Run the following commands to download and decompress the NVIDIA GRID driver package.

    The NVIDIA GRID driver package contains the drivers for various operating systems. For example, the NVIDIA GRID driver for Linux operating systems is NVIDIA-Linux-x86\_64-410.39-grid.run.

    ```
    wget http://grid-9-4.oss-cn-hangzhou.aliyuncs.com/NVIDIA-Linux-x86_64-430.99-grid.run
    ```

5.  Run the following commands in sequence and follow the on-screen tips to install the NVIDIA GRID driver:

    ```
    chmod 777 NVIDIA-Linux-x86_64-430.99-grid.run
    ./NVIDIA-Linux-x86_64-430.99-grid.run
    ```

6.  Run the `nvidia-smi` command to test whether the NVIDIA GRID driver is installed.

    If a command output similar to the following one is returned, the NVIDIA GRID driver is installed.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5896264061/p11965.png)

7.  Add a license server and activate the license.

    1.  Run the `cd /etc/nvidia` command to go to the /etc/nvidia directory.

    2.  Run the `cp gridd.conf.template gridd.conf` command to create a file named gridd.conf.

    3.  Add the license server information to the gridd.conf file.

        ```
        ServerAddress=<IP address of the license server>
        ServerPort=<Port of the license server (default port: 7070)>
        FeatureType=2
        EnableUI=TRUE
        ```

8.  Run the following command to install x11vnc:

    ```
    apt-get install x11vnc
    ```

9.  Run the `lspci | grep NVIDIA` command to query the GPU BusID.

    In this example, the GPU BusID is `00:07.0`.

10. Configure the X Server environment and restart the system.

    1.  Run the `nvidia-xconfig --enable-all-gpus --separate-x-screens` command.

    2.  Add the GPU BusID that you obtained to `Section "Device"` in the /etc/X11/xorg.conf file. In this example, `BusID "PCI:0:7:0"` is added.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3590359951/p11966.png)

    3.  Run the `reboot` command to restart the system.


## Test the NVIDIA GRID driver installed on an instance that runs Ubuntu 16.04 64-bit

1.  Run the following command to install the GLX application:

    ```
    apt-get install mesa-utils                    
    ```

2.  Run the `startx` command to start X Server.

    -   If the `startx` command is unavailable, run the `apt-get install xinit` command to install the GLX application.
    -   If you run the `startx` command, the `hostname: Name or service not known` error may be prompted. This error does not affect the startup of X Server. You can run the `hostname` command to query the hostname of the instance. Then, you can modify the /etc/hosts file by replacing the `hostname` that follows `127.0.0.1` with the actual hostname of your instance.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2590359951/p11967.png)

3.  Start a new terminal session of the SSH client and run the following command to start x11vnc:

    ```
    x11vnc -display :1
    ```

    If a command output similar to the following one is returned, x11vnc is started. In this case, you can connect to the instance by using a VNC application. In this example, VNC Viewer is used.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3590359951/p11968.png)

4.  Log on to the ECS console and add security group rules to a security group to which the instance is added. The security group rules allow inbound traffic on TCP port 5900. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

5.  On your computer, start VNC Viewer and enter `<Public IP address of the instance>:5900` to connect to the instance and go to KDE.

6.  Run the `glxinfo` command to view the configurations supported by the current NVIDIA GRID driver.

    1.  Start a new terminal session of the SSH client.

    2.  Run the `export DISPLAY=:1` command.

    3.  Run the `glxinfo -t` command to list the configurations supported by the current NVIDIA GRID driver.

7.  Run the `glxgears` command to test the NVIDIA GRID driver.

    1.  On KDE, right-click the desktop and select **Run Command**.

    2.  Run the `glxgears` command to start the testing application.

        If a window similar to the following one is displayed, the NVIDIA GRID driver runs normally.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3590359951/p11970.png)


## Install a NVIDIA GRID driver on a Linux instance that runs CentOS 7.3 64-bit

1.  [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using a username and password.md).

2.  Run the following commands in sequence to upgrade the system and install KDE:

    ```
    yum update
    yum install kernel-devel
    yum groupinstall "KDE Plasma Workspaces"
    ```

3.  Run the `reboot` command to restart the system.

4.  Connect to the Linux instance again. Run the following command to download and decompress the NVIDIA GRID driver package.

    The NVIDIA GRID driver package contains the drivers for various operating systems. For example, the NVIDIA GRID driver for Linux operating systems is NVIDIA-Linux-x86\_64-430.99-grid.run.

    ```
    wget http://grid-9-4.oss-cn-hangzhou.aliyuncs.com/NVIDIA-Linux-x86_64-430.99-grid.run
    ```

5.  Disable the nouveau driver.

    1.  Run the `vim /etc/modprobe.d/blacklist.conf` command and add `blacklist nouveau` to the file.

    2.  Run the `vim /lib/modprobe.d/dist-blacklist.conf` command and add the following content:

        ```
        blacklist nouveau
        options nouveau modeset=0
        ```

    3.  Run the `mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r)-nouveau.img` command.

    4.  Run the `dracut /boot/initramfs-$(uname -r).img $(uname -r)` command.

6.  Run the `reboot` command to restart the system.

7.  Run the following commands in sequence and follow the on-screen tips to install the NVIDIA GRID driver:

    ```
    chmod 777 NVIDIA-Linux-x86_64-430.99-grid.run
    ./NVIDIA-Linux-x86_64-430.99-grid.run
    ```

8.  Run the `nvidia-smi` command to test whether the NVIDIA GRID driver is installed.

    If a command output similar to the following one is returned, the NVIDIA GRID driver is installed.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6896264061/p11971.png)

9.  Add a license server and activate the license.

    1.  Run the `cd /etc/nvidia` command to go to the /etc/nvidia directory.

    2.  Run the `cp gridd.conf.template gridd.conf` command to create a file named gridd.conf.

    3.  Add the license server information to the gridd.conf file.

        ```
        ServerAddress=<IP address of the license server>
        ServerPort=<Port of the license server (default port: 7070)>
        FeatureType=2
        EnableUI=TRUE
        ```

10. Run the following command to install x11vnc:

    ```
    yum install x11vnc
    ```

11. Run the `lspci | grep NVIDIA` command to query the GPU BusID.

    In this example, the GPU BusID is `00:07.0`.

12. Configure the X Server environment.

    1.  Run the `nvidia-xconfig --enable-all-gpus --separate-x-screens` command.

    2.  Add the GPU BusID that you obtained to `Section "Device"` in the /etc/X11/xorg.conf file. In this example, `BusID "PCI:0:7:0"` is added.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3590359951/p11966.png)

13. Run the `reboot` command to restart the system.


## Test the NVIDIA GRID driver installed on an instance that runs CentOS 7.3 64-bit

1.  Run the `startx` command to start X Server.

2.  Start a new terminal session of the SSH client and run the following command to start x11vnc:

    ```
    x11vnc -display :0
    ```

    If a command output similar to the following one is returned, x11vnc is started. In this case, you can connect to the instance by using a VNC application. In this example, VNC Viewer is used.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3590359951/p11968.png)

3.  Log on to the ECS console and add security group rules to a security group of the instance. The security group rules allow inbound traffic on TCP port 5900. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

4.  On your computer, start VNC Viewer and enter `<Public IP address of the instance>:5900` to connect to the instance and go to KDE.

5.  Run the `glxinfo` command to view the configurations supported by the current NVIDIA GRID driver.

    1.  Start a new terminal session of the SSH client.

    2.  Run the `export DISPLAY=:0` command.

    3.  Run the `glxinfo -t` command to list the configurations supported by the current NVIDIA GRID driver.

6.  Run the `glxgears` command to test the NVIDIA GRID driver.

    1.  On KDE, right-click the desktop and select **Run Command**.

    2.  Run the `glxgears` command to start the testing application.

        If a window similar to the following one is displayed, the NVIDIA GRID driver runs normally.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3590359951/p11970.png)


