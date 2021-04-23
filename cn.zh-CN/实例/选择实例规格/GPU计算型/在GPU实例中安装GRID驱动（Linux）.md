# 在GPU实例中安装GRID驱动（Linux）

本章节介绍如何在运行Linux操作系统的GPU实例中安装GRID驱动，并搭建桌面显示环境。

-   创建一台GPU实例，确保实例能访问公网。

    **说明：** 本文介绍如何为运行Linux操作系统的GPU实例安装GRID驱动，对需要运行Windows操作系统的GPU实例，在创建GPU实例时选用预装GRID驱动的付费镜像即可，请参见[创建配备NVIDIA GPU的实例]()。

    建议您选择**公共镜像**中的镜像。如果您选择了**镜像市场**中预装NVIDIA驱动的镜像，创建实例后您必须禁用nouveau驱动。

    nouveau是一款开源驱动，必须禁用nouveau才能成功安装新的驱动，禁用方法：在/etc/modprobe.d目录下创建一个nouveau.conf文件，添加`blacklist nouveau`。

-   在本地机器上已经安装了VNC连接软件，例如本示例中使用的VNC Viewer。
-   向[NVIDIA](https://www.nvidia.com/object/nvidia-enterprise-account.html)购买了GRID License。该方式需要自建License服务器，您可以购买ECS实例并参考NVIDIA官网教程搭建。

如果您的GPU实例需要OpenGL图形支持，必须在实例上安装GRID驱动（ecs.vgn6i-m4-vws.xlarge和ecs.vgn6i-m8-vws.2xlarge除外）。GPU实例自带的NVIDIA GPU计算卡，例如P100、P4、V100等，因为NVIDIA GRID License而限制了GPU图形功能，您可以使用NVIDIA官方发布的GRID驱动满足使用OpenGL图形功能的需求。

**说明：** 非NVIDIA合作伙伴不能从NVIDIA官网下载该驱动，本章节操作步骤中介绍了从阿里云获取GRID驱动安装包的方法。

本文介绍如何为非vGPU的GPU实例安装GRID驱动，如果您需要为配备vGPU的GPU实例（vgn6i和vgn5i）安装GRID驱动，请参见[在GPU虚拟化型实例中安装GRID驱动（Linux）](/cn.zh-CN/实例/选择实例规格/GPU计算型/在vgn6i和vgn5i实例中安装GRID驱动（Linux）.md)。

## 操作步骤

安装GRID驱动的步骤如下：

-   Ubuntu 16.04 64-bit：
    1.  [在Ubuntu 16.04 64-bit中安装GRID驱动](#section_zsd_ytk_ngb)
    2.  [在Ubuntu 16.04 64-bit中测试GRID驱动](#section_itd_ytk_ngb)
-   CentOS 7.3 64-bit：
    1.  [在CentOS 7.3 64-bit中安装GRID驱动](#section_tvd_ytk_ngb)
    2.  [在CentOS 7.3 64-bit中测试GRID驱动](#section_dwd_ytk_ngb)

## 在Ubuntu 16.04 64-bit中安装GRID驱动

1.  [远程连接Linux实例](/cn.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/使用用户名密码验证连接Linux实例.md)。

2.  依次运行以下命令升级系统并安装KDE桌面。

    ```
    apt-get update
    apt-get upgrade
    apt-get install kubuntu-desktop
    ```

3.  运行`reboot`命令重启系统。

4.  再次远程连接Linux实例，并运行以下命令下载NVIDIA GRID驱动包。

    NVIDIA GRID驱动包中有多个系统的GRID驱动。Linux GRID驱动是NVIDIA-Linux-x86\_64-430.99-grid.run。

    ```
    wget http://grid-9-4.oss-cn-hangzhou.aliyuncs.com/NVIDIA-Linux-x86_64-430.99-grid.run
    ```

5.  依次运行以下命令，并按界面提示安装NVIDIA GRID驱动。

    ```
    chmod 777 NVIDIA-Linux-x86_64-430.99-grid.run
    ./NVIDIA-Linux-x86_64-430.99-grid.run
    ```

6.  运行命令`nvidia-smi`测试驱动安装结果。

    如果返回以下类似结果，说明驱动已经成功安装。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9307654061/p11965.png)

7.  按以下步骤添加License服务器并激活License。

    1.  切换到/etc/nvidia目录：`cd /etc/nvidia`。

    2.  创建gridd.conf文件：`cp gridd.conf.template gridd.conf`。

    3.  在gridd.conf文件中添加License服务器的信息。

        ```
        ServerAddress=<License服务器的IP>
        ServerPort=<License服务器的端口（默认为7070）>
        FeatureType=2
        EnableUI=TRUE
        ```

8.  运行命令安装x11vnc。

    ```
    apt-get install x11vnc
    ```

9.  运行命令`lspci | grep NVIDIA`查询GPU BusID。

    本示例中，查询到的GPU BusID为`00:07.0`。

10. 配置X Server环境并重启。

    1.  运行命令`nvidia-xconfig --enable-all-gpus --separate-x-screens`。

    2.  编辑/etc/X11/xorg.conf，在`Section "Device"`段添加GPU BusID，如本示例中为`BusID "PCI:0:7:0"`。

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5304359951/p11966.png)

    3.  运行`reboot`命令重启系统。


## 在Ubuntu 16.04 64-bit中测试GRID驱动

1.  运行命令安装GLX测试程序。

    ```
    apt-get install mesa-utils                    
    ```

2.  运行命令`startx`启动X Server。

    -   如果没有`startx`命令，执行`apt-get install xinit`命令安装。
    -   `startx`启动时可能会提示`hostname: Name or service not known`。这个提示不会影响X Server启动。您可以运行命令`hostname`查得主机名后，再修改/etc/hosts文件，将`127.0.0.1`后的`hostname`改为本机的hostname。

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4304359951/p11967.png)

3.  开启一个新的SSH客户端终端，运行命令启动x11vnc。

    ```
    x11vnc -display :1
    ```

    如果看到如下图所示的信息，表示x11vnc已经成功启动。此时，您能通过VNC Viewer等VNC远程连接软件连接实例。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5304359951/p11968.png)

4.  登录ECS控制台，在实例所在安全组中添加安全组规则，允许TCP 5900端口的入方向访问。具体操作，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

5.  在本地机器上，使用VNC Viewer等VNC远程连接软件，通过`实例公网IP地址:5900`连接实例，进入KDE桌面。

6.  按以下步骤使用`glxinfo`命令查看当前GRID驱动支持的配置。

    1.  开启一个新的SSH客户端终端。

    2.  运行命令`export DISPLAY=:1`。

    3.  运行命令`glxinfo –t`列出当前GRID驱动支持的配置。

7.  按以下步骤使用`glxgears`命令测试GRID驱动。

    1.  在KDE桌面上，右键单击桌面，并选择**Run Command**。

    2.  运行`glxgears`启动齿轮图形测试程序。

        如果出现如下图所示的窗口，表明GRID驱动正常工作。

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5304359951/p11970.png)


## 在CentOS 7.3 64-bit中安装GRID驱动

1.  [远程连接Linux实例](/cn.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/使用用户名密码验证连接Linux实例.md)。

2.  依次运行以下命令升级系统并安装KDE桌面。

    ```
    yum update
    yum install kernel-devel
    yum groupinstall "KDE Plasma Workspaces"
    ```

3.  运行`reboot`重启系统。

4.  再次远程连接Linux实例，并运行以下命令下载并解压NVIDIA GRID驱动包。

    NVIDIA GRID驱动包中包含多个系统的GRID驱动，其中，Linux GRID驱动是NVIDIA-Linux-x86\_64-430.99-grid.run。

    ```
    wget http://grid-9-4.oss-cn-hangzhou.aliyuncs.com/NVIDIA-Linux-x86_64-430.99-grid.run
    ```

5.  按以下步骤关闭nouveau驱动。

    1.  运行`vim /etc/modprobe.d/blacklist.conf`，添加`blacklist nouveau`。

    2.  运行`vim /lib/modprobe.d/dist-blacklist.conf`，添加以下内容。

        ```
        blacklist nouveau
        options nouveau modeset=0
        ```

    3.  运行`mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r)-nouveau.img`。

    4.  运行`dracut /boot/initramfs-$(uname -r).img $(uname -r)`。

6.  运行`reboot`重启系统。

7.  依次运行以下命令，并按界面提示安装NVIDIA GRID驱动。

    ```
    chmod 777 NVIDIA-Linux-x86_64-430.99-grid.run
    ./NVIDIA-Linux-x86_64-430.99-grid.run
    ```

8.  运行命令`nvidia-smi`测试驱动是否安装成功。

    如果返回以下类似结果，说明驱动已经成功安装。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0407654061/p11971.png)

9.  按以下步骤添加License服务器并激活License。

    1.  切换到/etc/nvidia目录：`cd /etc/nvidia`。

    2.  创建gridd.conf文件：`cp gridd.conf.template gridd.conf`。

    3.  在gridd.conf文件中添加License服务器的信息。

        ```
        ServerAddress=<License服务器的IP>
        ServerPort=<License服务器的端口（默认为7070）>
        FeatureType=2
        EnableUI=TRUE
        ```

10. 安装x11vnc。

    ```
    yum install x11vnc
    ```

11. 运行命令`lspci | grep NVIDIA`查询GPU BusID。

    本示例中，查询到的GPU BusID为`00:07.0`。

12. 配置X Server环境。

    1.  运行命令`nvidia-xconfig --enable-all-gpus --separate-x-screens`。

    2.  编辑/etc/X11/xorg.conf，在`Section "Device"`段添加GPU BusID，如本示例中为`BusID "PCI:0:7:0"`。

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5304359951/p11966.png)

13. 运行`reboot`重启系统。


## 在CentOS 7.3 64-bit中测试GRID驱动

1.  运行命令`startx`启动X Server。

2.  开启一个新的SSH客户端终端，运行命令启动x11vnc。

    ```
    x11vnc -display :0
    ```

    如果看到如下图所示的信息，表示x11vnc已经成功启动。此时，您能通过VNC Viewer等VNC远程连接软件连接实例。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5304359951/p11968.png)

3.  登录ECS管理控制台，在实例所在安全组中添加安全组规则，允许TCP 5900端口的入方向访问。具体操作，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

4.  在本地机器上，使用VNC Viewer等VNC远程连接软件，通过`实例公网IP地址:5900`连接实例，进入KDE桌面。

5.  按以下步骤使用`glxinfo`命令查看当前GRID驱动支持的配置。

    1.  开启一个新的SSH客户端终端。

    2.  运行命令`export DISPLAY=:0`。

    3.  运行命令`glxinfo –t`列出当前GRID驱动支持的配置。

6.  按以下步骤使用`glxgears`命令测试GRID驱动。

    1.  在KDE桌面上，右键单击桌面，并选择**Run Command**。

    2.  运行`glxgears`启动齿轮图形测试程序。

        如果出现如下图所示的窗口，表明GRID驱动正常工作。

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5304359951/p11970.png)


