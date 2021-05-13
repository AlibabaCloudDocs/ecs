# f3实例OpenCL开发最佳实践

本文介绍如何在f3实例上使用OpenCL（Open Computing Language）制作镜像文件，并烧录到FPGA芯片中。

-   已创建f3实例并为实例分配公网IP。

    若尚未创建，请参见[创建f3实例](/intl.zh-CN/实例/选择实例规格/FPGA计算型/创建f3实例.md)。

    **说明：** f3实例只能使用阿里云共享给您的镜像。

-   已在f3实例所在安全组中添加规则并放行SSH（22）端口。
-   已在ECS控制台f3实例的详情页上，获取实例ID。
-   已创建一个OSS Bucket专门用于FaaS服务。

    Bucket与f3实例必须属于同一个账号、同一个地域。若尚未创建，请参见[创建一个OSS Bucket](/intl.zh-CN/快速入门/控制台快速入门/创建存储空间.md)。

-   使用RAM用户操作FPGA，必须先完成以下操作：
    -   创建RAM用户并授权，详情请参见[创建RAM用户](/intl.zh-CN/用户管理/基本操作/创建RAM用户.md)及[为RAM用户授权](/intl.zh-CN/用户管理/授权管理/为RAM用户授权.md)。

        您需要为RAM用户授予的权限为：AliyunECSReadOnlyAccess、AliyunOSSFullAccess和AliyunRAMFullAccess。

    -   授权FaaS服务角色，授权页面请参见[授权FaaS服务角色](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunFAASDefaultRole%22%2C%20%22TemplateId%22%3A%20%22DefaultRole%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//ecs.console.aliyun.com/%23/home%22%2C%20%22Service%22%3A%20%22FAAS%22%7D)。
    -   获取AccessKey ID和AccessKey Secret。

开始操作之前，您需要了解以下注意事项：

-   本文所述所有操作都必须由同一个账号在同一地域里执行。
-   建议您使用RAM用户操作FaaS实例。您需要为FaaS管理账号创建一个角色，并授予临时权限，让FaaS管理账号能访问指定的OSS Bucket。
-   本文的示例步骤和命令均基于2018.2版本Sdaccel开发环境。若您使用其他版本Sdaccel开发环境，步骤和命令可能会稍有差异。

## 操作步骤

在f3实例上，使用OpenCL制作镜像文件，并烧写到FPGA芯片中的操作步骤如下：

1.  [步骤一：配置环境](#section_wvk_ntl_2fb)
2.  [步骤二：编译二进制文件](#section_qcn_vtl_2fb)
3.  [步骤三：检查打包脚本](#section_rjl_d5l_2fb)
4.  [步骤四：制作镜像](#section_h1l_g5l_2fb)
5.  [步骤五：下载镜像](#section_ft5_k5l_2fb)
6.  [步骤六：运行Host程序](#section_tft_w5l_2fb)

## 步骤一：配置环境

1.  [远程连接f3实例](/intl.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/使用用户名密码验证连接Linux实例.md)。

    **说明：** 后面步骤中的编译工程可能会持续数小时，建议您使用screen或者nohup等方式登录，防止ssh超时退出。

2.  运行以下命令安装Screen。

    ```
    yum install screen -y                        
    ```

3.  运行以下命令进入Screen。

    ```
    screen -S f3opencl                        
    ```

4.  运行以下命令配置环境。

    ```
    source /root/xbinst_oem/F3_env_setup.sh xocl  #每打开一个终端窗口就需要执行该命令一次
    ```

    **说明：**

    -   配置环境主要包括安装xocl驱动，设置vivado环境变量， 检查vivado license， 检测aliyun-f3 sdaccel平台，2018.2 runtime配置和faascmd版本检测。
    -   如果您要运行sdaccel的仿真，请勿运行以上命令配置环境。您只需要单独配置vivado的环境变量即可。
    -   推荐您使用Makefile方式仿真。

## 步骤二：编译二进制文件

完成以下步骤，编译vadd二进制文件和kernel\_global\_bandwidth二进制文件：

-   示例一 ：编译vadd二进制文件
    1.  复制example目录。

        ```
        cp -rf /opt/Xilinx/SDx/2018.2/examples ./
        ```

    2.  进入vadd目录。

        ```
        cd examples/vadd/
        ```

    3.  运行命令cat sdaccel.mk \| grep "XDEVICE="查看XDEVICE的值，确保其配置为`XDEVICE=xilinx_aliyun-f3_dynamic_5_0`。
    4.  按以下步骤修改common.mk文件。
        1.  运行vim ../common/common.mk命令打开该文件。
        2.  在第 61行代码（参数可能在 60~62 行，视您的文件而定）的末尾添加编译参数--xp param:compiler.acceleratorBinaryContent=dcp，修改后的代码如下：

            ```
            CLCC_OPT += $(CLCC_OPT_LEVEL) ${DEVICE_REPO_OPT} --platform ${XDEVICE} ${KERNEL_DEFS} ${KERNEL_INCS} --xp param:compiler.acceleratorBinaryContent=dcp
            ```

            **说明：** 由于您必须向编译服务器提交DCP文件，所以需要添加--xp param:compiler.acceleratorBinaryContent=dcp编译参数，使得Xilinx® OpenCL™ Compiler（xocc）编译生成一个布局布线后的DCP文件，而不是bit文件。

    5.  运行以下命令编译程序。

        ```
        make -f sdaccel.mk xbin_hw
        ```

        如果您看到如下界面，说明二进制文件编译已经开始。编译过程可能会持续数个小时，请您耐心等待。

        ![f3_opencl_1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9775688951/p12150.png)

-   示例二：编译kernel\_global\_bandwidth二进制文件
    1.  依次运行以下命令克隆`xilinx 2018.2 example`。

        ```
        git clone https://github.com/Xilinx/SDAccel_Examples.git
        ```

        ```
        cd SDAccel_Examples/
        ```

        ```
        git checkout 2018.2
        ```

        **说明：** git分支必须为2018.2版本。

    2.  运行cd getting\_started/kernel\_to\_gmem/kernel\_global\_bandwidth/命令进入目录。
    3.  按以下步骤修改Makefile文件。
        1.  运行vim Makefile命令打开该文件。
        2.  设置`DEVICES=xilinx_aliyun-f3_dynamic_5_0`。
        3.  在第33行代码中添加编译参数--xp param:compiler.acceleratorBinaryContent=dcp，修改后的代码如下：

            ```
            CLFLAGS +=--xp "param:compiler.acceleratorBinaryContent=dcp" --xp "param:compiler.preserveHlsOutput=1" --xp "param:compiler.generateExtraRunData=true" --max_memory_ports bandwidth -DNDDR_BANKS=$(ddr_banks)
            ```

    4.  运行以下命令编译程序。

        ```
        make TARGET=hw
        ```

        如果您看到该界面，说明二进制文件编译已经开始。编译工程可能会持续数小时，请您耐心等待。

        ![f3_opencl_2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9775688951/p36971.png)


## 步骤三：检查打包脚本

运行以下命令检查打包脚本是否存在。

```
file /root/xbinst_oem/sdaccel_package.sh
```

如果返回结果中包含cannot open \(No such file or directory\)，说明不存在该文件，您需要运行以下命令手动下载打包脚本。

```
wget http://fpga-tools.oss-cn-shanghai.aliyuncs.com/sdaccel_package.sh
```

## 步骤四：制作镜像

1.  初始化faascmd工具并配置OSS环境。

    1.  运行以下命令设置RAM账号的AccessKey信息。

        ```
        #将<hereIsYourSecretId>和<hereIsYourSecretKey>替换为您的RAM用户AK信息
        faascmd config --id=<hereIsYourSecretId> --key=<hereIsYourSecretKey>  
        ```

    2.  运行以下命令设置FaaS服务要使用的OSS Bucket。

    ```
    #将<hereIsYourBucket>替换为您创建的OSS Bucket名称
    faascmd auth --bucket=<hereIsYourBucket>  
    ```

2.  运行ls，获取后缀为`.xclbin`的文件名。

    ![f3_opencl_3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9775688951/p12152.png)

3.  运行以下命令打包二进制文件。

    ```
    /root/xbinst_oem/sdaccel_package.sh -xclbin=/opt/Xilinx/SDx/2018.2/examples/vadd/bin_vadd_hw.xclbin
    ```

    打包完成后，您会在同一目录下看到一个打包好的文件，如下图所示。

    ![f3_opencl_4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9775688951/p12154.png)


## 步骤五：下载镜像

本小节介绍如何使用faascmd工具上传网表文件并下载FPGA镜像。关于faascmd命令的用法，请参见[使用faascmd工具](/intl.zh-CN/最佳实践/FaaS实例最佳实践/faascmd工具/使用faascmd.md)。

1.  依次运行以下命令，将压缩包上传到您个人的OSS Bucket，再将存放在您个人OSS Bucket中的gbs上传到FaaS管理单元的OSS Bucket中。

    ```
    faascmd upload_object --object=bit.tar.gz --file=bit.tar.gz
    ```

    ```
    faascmd create_image --object=bit.tar.gz --fpgatype=xilinx --name=<hereIsFPGAImageName> --tags=<hereIsFPGAImageTag> --encrypted=false --shell=<hereIsShellVersionOfFPGA>
    ```

    ![f3_opencl_6](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2875688951/p12112.png)

    ![f3_opencl_7](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2875688951/p12113.png)

2.  运行以下命令查看FPGA镜像是否处于可下载状态。

    ```
    faascmd list_images
    ```

    返回结果中：

    -   如果FPGA镜像的"State"为"compiling"，表示FPGA镜像处于编译状态，您需要继续等待。
    -   如果FPGA镜像的"State"为"success"，表示FPGA镜像已可以下载，您需要找到并记录FpgaImageUUID。

        ![f3_opencl_8](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2875688951/p12115.png)

3.  运行以下命令在返回结果中，找到并记录FpgaUUID。

    ```
    faascmd list_instances --instanceId=<hereIsYourInstanceId> #将<hereIsYourInstanceId>替换为f3实例ID
    ```

4.  运行以下命令下载FPGA镜像。

    ```
    #将<hereIsYourInstanceId>替换为f3的实例ID，<hereIsFpgaUUID>替换为您获取的FpgaUUID，<hereIsImageUUID>替换为您获取的FpgaImageUUID
    faascmd download_image --instanceId=<hereIsYourInstanceId> --fpgauuid=<hereIsFpgaUUID> --fpgatype=xilinx --imageuuid=<hereIsImageUUID> --imagetype=afu --shell=<hereIsShellVersionOfFpga>
    ```

    ![f3_opencl_9](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0875688951/p62372.png)

5.  运行以下命令查看镜像是否下载成功。

    ```
    faascmd fpga_status --fpgauuid=<hereIsFpgaUUID> --instanceId=<hereIsYourInstanceId> #将<hereIsFpgaUUID>替换为您获取的FpgaUUID，<hereIsYourInstanceId>替换为f3实例ID。
    ```

    以下为返回结果示例。如果显示的FpgaImageUUID与您获取的FpgaImageUUID一致，并且显示"TaskStatus":"valid"，说明镜像下载成功。

    ![f3_opencl_10](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0875688951/p62374.png)


## 步骤六：运行Host程序

1.  运行以下命令配置环境。

    ```
    source /root/xbinst_oem/F3_env_setup.sh xocl  #每打开一个终端窗口就需要执行该命令一次
    ```

2.  配置sdaccel.ini文件。

    在Host二进制文件所在目录下，运行vim sdaccel.ini命令创建sdaccel.ini文件并输入下列内容。

    ```
    [Debug]
    profile=true
    [Runtime]
    runtime_log = "run.log"
    hal_log = hal.log
    ert=false
    kds=false
    ```

3.  运行host。

    -   vadd运行命令如下：

        ```
        make -f sdaccel.mk host
        ```

        ```
        ./vadd bin_vadd_hw.xclbin
        ```

    -   kernel\_global\_bandwidth运行命令如下：

        ```
        ./kernel_global
        ```

    如果返回结果中出现Test Passed，说明测试通过。


## 其他操作

这里介绍FPGA实例部分常用的操作。

|任务|命令|
|:-|:-|
|查看帮助文档|`make -f ./sdaccel.mk help`|
|软件仿真|`make -f ./sdaccel.mk run_cpu_em`|
|硬件仿真|`make -f ./sdaccel.mk run_hw_em`|
|只编译host代码|`make -f ./sdaccel.mk host`|
|编译生成可以下载的文件|`make -f sdaccel.mk xbin_hw`|
|清理工作目录|`make -f sdaccel.mk clean`|
|强力清除工作目录|`make -f sdaccel.mk cleanall`|

**说明：**

-   仿真时只需要按照Xilinx标准流程操作，不需要配置F3\_env\_setup环境。
-   SDAccel runtime和SDAccel开发平台已在阿里云f3官方镜像中提供。 您也可以点击后面的链接直接下载[SDAccel runtime](https://faas-ref-design.oss-cn-hangzhou.aliyuncs.com/FaaS_F3/xbinst_oem.tar.gz)和[SDAccel开发平台](https://faas-ref-design.oss-cn-hangzhou.aliyuncs.com/FaaS_F3/platforms.tar.gz)。

