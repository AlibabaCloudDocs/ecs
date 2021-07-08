# 手动安装GPU驱动

如果您在创建实例时没有选择自动安装GPU驱动，为保证您能正常使用您创建的实例，请在创建后手动安装驱动。本文为您介绍如何为GPU实例手动安装GPU驱动。

GPU虚拟化型实例（vgn6i和vgn5i）仅支持安装GRID驱动，因此，本章节操作不适用于vgn6i和vgn5i实例。GRID驱动的具体安装方法，请参见[创建GPU实例]()和[在GPU虚拟化型实例中安装GRID驱动（Linux）](/intl.zh-CN/实例/选择实例规格/GPU计算型/在vgn6i和vgn5i实例中安装GRID驱动（Linux）.md)。

GPU实例仅支持安装与其操作系统一致的GPU驱动。因此，请根据您实例的操作系统选择如下对应操作指导：

-   [安装Windows操作系统的GPU驱动](#section_61l_xm5_b8y)
-   [安装Linux操作系统的GPU驱动](#section_iz5_ail_6bt)

## 安装Windows操作系统的GPU驱动

1.  远程连接实例。

    选择以下方式远程连接GPU实例。

    |连接方式|操作指引|
    |----|----|
    |VNC|[通过密码认证登录Windows实例](/intl.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Windows实例.md)|

2.  在远程桌面中，通过浏览器访问[NVIDIA驱动下载](https://www.nvidia.com/Download/Find.aspx?lang=cn)地址。

3.  手动查找适用的驱动程序。

    ![NVIDIA-windows](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9201545261/p291095.png)

    1.  根据实例规格配备的GPU选择对应的产品类型、产品系列和产品家族。

        各GPU计算型规格的GPU信息如下表所示：

        |信息项|gn4|gn5|gn5i|gn6v|gn6i|
        |:--|:--|:--|:---|:---|----|
        |产品类型|Data Center / Tesla|Data Center / Tesla|Data Center / Tesla|Data Center / Tesla|Data Center / Tesla|
        |产品系列|M-Class|P-Series|P-Series|V-Series|T-Series|
        |产品家族|M40|Tesla P100|Tesla P4|Tesla V100|Tesla T4|

    2.  根据实例使用的镜像选择对应的Windows操作系统版本。

        本示例选择的操作系统为**Windows 10 64-bit**。

    3.  选择CUDA Toolkit版本。

    4.  选择语言。

    5.  单击**搜索**，然后选择需要下载的驱动版本，单击对应的驱动名称。

        ![2021-07-02_17-53-16](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9201545261/p291103.png)

4.  在打开**驱动程序下载页面**，单击**下载**，然后在**NVIDIA驱动程序下载**页面再次单击**下载**。

    ![2021-07-02_18-08-08](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9201545261/p291114.png)

5.  下载完成后，打开下载驱动程序所在的文件夹。然后双击安装文件，按提示完成安装。

    **说明：** 对于Windows系统，在GPU驱动安装生效后，由于Windows自带的远程连接（RDP）协议不支持DirectX、OpenGL等相关应用，您需要自行安装VNC服务和客户端，或使用其它支持此类应用的协议，例如PCOIP、XenDesktop HDX 3D等。


## 安装Linux操作系统的GPU驱动

1.  访问[NVIDIA驱动下载](https://www.nvidia.com/Download/Find.aspx?lang=cn)。

2.  手动查找适用的驱动程序。

    ![2021-07-02_18-25-40](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9201545261/p291121.png)

    1.  根据实例规格配备的GPU选择对应的产品类型、产品系列和产品家族。

        各GPU计算型规格的GPU信息如下表所示：

        |信息项|gn4|gn5|gn5i|gn6v|gn6i|
        |:--|:--|:--|:---|:---|----|
        |产品类型|Data Center / Tesla|Data Center / Tesla|Data Center / Tesla|Data Center / Tesla|Data Center / Tesla|
        |产品系列|M-Class|P-Series|P-Series|V-Series|T-Series|
        |产品家族|M40|Tesla P100|Tesla P4|Tesla V100|Tesla T4|

    2.  根据实例使用的镜像选择对应的Linux操作系统版本。

        如果下拉列表中没有显示所需的操作系统，请单击下拉列表底部的**选择所有操作系统**。如果您的实例使用的是Debian、CentOS等Linux操作系统，无法在驱动下载页面中找到完全一致的操作系统或版本，请选择**Linux 64-bit**。关于镜像中操作系统及版本的更多信息，请参见[公共镜像概述](/intl.zh-CN/镜像/公共镜像/公共镜像概述.md)。

    3.  选择CUDA Toolkit版本。

    4.  选择语言。

    5.  单击**搜索**，然后选择需要下载的驱动版本，单击对应的驱动名称。

3.  在打开**驱动程序下载页面**，单击**下载**，然后在**NVIDIA驱动程序下载**页面，右键单击**下载**并选择**复制链接地址**。

    ![download-linux](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7577745261/p291486.png)

4.  远程连接实例。

    选择以下方式远程连接GPU实例。

    |连接方式|操作指引|
    |----|----|
    |VNC|[通过密码认证登录Linux实例](/intl.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)|

5.  使用`wget`命令，并粘贴您在[步骤3](#step_mnf_id8_xwt)中复制的驱动下载链接，执行命令下载安装包。命令示例如下所示：

    ```
    wget https://cn.download.nvidia.com/tesla/460.73.01/NVIDIA-Linux-x86_64-460.73.01.run
    ```

6.  安装GPU驱动。

    1.  执行以下命令，查询实例中是否安装kernel-devel和kernel-headers包。

        以下操作以CentOS操作系统的实例为例。

        ```
        rpm  -qa | grep $(uname -r)
        ```

        -   如果回显类似如下信息，即包含了kernel-devel和kernel-headers包的版本信息，表示已安装。

            ```
            kernel-3.10.0-1062.18.1.el7.x86_64
            kernel-devel-3.10.0-1062.18.1.el7.x86_64
            kernel-headers-3.10.0-1062.18.1.el7.x86_64
            ```

        -   如果在回显信息中，您没有找到kernel-devel-\*和kernel-headers-\*内容，您需要自行下载并安装kernel对应版本的[kernel-devel](https://pkgs.org/download/kernel-devel)和[kernel-headers](http://www.rpmfind.net/linux/rpm2html/search.php?query=kernel-headers)包。

            **说明：** kernel-devel和kernel版本不一致会导致在安装driver rpm过程中driver编译出错。因此，请您确认回显信息中kernel-\*的版本号后，再下载对应版本的kernel-devel。在示例回显信息中，kernel的版本号为3.10.0-1062.18.1.el7.x86\_64。

    2.  安装GPU驱动。

        以操作系统是Linux 64-bit的驱动为例，您下载的GPU驱动为.run格式，例如：NVIDIA-Linux-x86\_64-xxxx.run。分别执行以下命令，授权并安装GPU驱动。

        ```
        chmod +x NVIDIA-Linux-x86\_64-xxxx.run
        ```

        ```
        sh NVIDIA-Linux-x86\_64-xxxx.run
        ```

    3.  安装完成后，执行如下命令，查看是否安装成功。

        ```
        nvidia-smi
        ```

        回显信息类似如下所示，表示GPU驱动安装成功。

        ![kernel](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9262694261/p290192.png)


