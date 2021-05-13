# f3实例RTL开发最佳实践

本文描述基于f3实例的RTL（Register Transfer Level）开发流程。

-   已创建f3实例，并且实例能访问公网。具体操作，请参见[创建f3实例](/cn.zh-CN/实例/选择实例规格/FPGA计算型/创建f3实例.md)。
-   已在f3实例所在安全组中添加规则放行SSH（22）端口。具体操作，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。
-   登录[ECS管理控制台](https://ecs.console.aliyun.com/#/home)，在f3实例的详情页上，获取实例ID。
-   已在华东2创建一个OSS Bucket，专门用于FaaS服务。具体操作，请参见[创建一个OSS Bucket](/cn.zh-CN/快速入门/控制台快速入门/创建存储空间.md)。

    **说明：** 这个Bucket会对FaaS管理账号开通读写权限，因此不建议您存储与FaaS无关的内容。

-   使用RAM用户操作FPGA，必须先完成以下操作：
    -   创建RAM用户并授权，详情请参见[创建RAM用户](/cn.zh-CN/用户管理/基本操作/创建RAM用户.md)及[为RAM用户授权](/cn.zh-CN/用户管理/授权管理/为RAM用户授权.md)。

        您需要为RAM用户授予的权限为：AliyunECSReadOnlyAccess、AliyunOSSFullAccess和AliyunRAMFullAccess。

    -   授权FaaS服务角色，授权页面请参见[授权FaaS服务角色](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunFAASDefaultRole%22%2C%20%22TemplateId%22%3A%20%22DefaultRole%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//ecs.console.aliyun.com/%23/home%22%2C%20%22Service%22%3A%20%22FAAS%22%7D)。
    -   获取AccessKey ID和AccessKey Secret。

开始操作之前，您需要了解以下注意事项：

-   本文所述所有操作必须由同一个账号在同一个地域执行。
-   强烈建议您使用RAM用户操作FPGA实例。基于最小授权原则，建议您不要对RAM用户过度授权，而只授予RAM用户刚好满足其工作所需的权限，例如访问OSS bucket获取原始DCP/xclbin文件、上传Vivado编译log、操作指定的ECS实例等。您还需要指定RAM角色AliyunFAASDefaultRole，FaaS服务默认使用此角色来访问您在其他云产品中的资源，其权限策略AliyunFAASRolePolicy还包括KMS相关的权限，以便您使用KMS服务对IP进行加密。

## 操作步骤

1.  [远程连接Linux实例](/cn.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/使用用户名密码验证连接Linux实例.md)。

    **说明：** 编译工程时需要2~3小时。建议您使用nohup或者VNC连接实例，以免编译时意外退出。

2.  下载并解压[RTL参考设计](https://faas-ref-design.oss-cn-hangzhou.aliyuncs.com/FaaS_F3/f3_hdk.tar.gz)。

3.  配置环境。

    -   如果驱动为`xdma`，需要运行以下命令来配置环境。

        ```
        source /root/xbinst_oem/F3_env_setup.sh xdma #每打开一个终端窗口就需要执行该命令一次  
        ```

    -   如果驱动为`xocl`，则需要运行以下命令来配置环境。

        ```
        source /root/xbinst_oem/F3_env_setup.sh xocl #每打开一个终端窗口就需要执行该命令一次
        ```

    **说明：** 配置环境主要包括安装xdma驱动或xocl驱动，设置vivado环境变量，检查vivado license，检测aliyun-f3 sdaccel平台，2018.2 runtime配置和faascmd版本检测 。

4.  指定OSS存储空间。

    ```
    faascmd config --id=<hereIsYourSecretId> --key=<hereIsYourSecretKey> #将<hereIsYourSecretId>和<hereIsYourSecretKey>替换为您的RAM用户AK信息
    faascmd auth --bucket=hereIsYourBucket # 将<hereIsYourBucket>替换为您创建的OSS Bucket名称                        
    ```

5.  运行以下命令编译RTL工程。

    ```
    cd <您之前解压的路径>/hw/ # 进入解压后的hw路径
    sh compiling.sh               
    ```

    **说明：** 编译工程需要2~3小时。

6.  上传网表文件，并下载FPGA镜像。

    使用faascmd工具上传网表文件并下载FPGA镜像。关于faascmd命令的用法，请参见[使用faascmd](/cn.zh-CN/最佳实践/FaaS实例最佳实践/faascmd工具/使用faascmd.md)。

    1.  依次运行以下命令，将压缩包上传到您个人的OSS Bucket，再将存放在您个人OSS Bucket中的gbs上传到FaaS管理单元的OSS Bucket中。

        ```
        faascmd upload_object --object=bit.tar.gz --file=bit.tar.gz
        faascmd create_image --object=bit.tar.gz --fpgatype=xilinx --name=<hereIsFPGAImageName> --tags=<hereIsFPGAImageTag> --encrypted=false --shell=<hereIsShellVersionOfFPGA>                      
        ```

        ![upload_object](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2875688951/p12112.png)

        ![create_image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2875688951/p12113.png)

    2.  运行命令查看FPGA镜像是否处于可下载状态。

        ```
        faascmd list_images
        ```

        在返回结果中：

        -   如果"State"为compiling，表示FPGA镜像处于编译状态，您需要继续等待。
        -   如果"State"为success，表示FPGA镜像已经可以下载。您需要找到并记录FpgaImageUUID。
        ![list_images](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2875688951/p12115.png)

    3.  运行以下命令。在命令返回结果中，您需要找到并记录FpgaUUID。

        ```
        faascmd list_instances --instanceId=<hereIsYourInstanceId> # 将<hereIsYourInstanceId>替换为f3实例ID
        ```

    4.  运行以下命令下载FPGA镜像。

        ```
        # 将<hereIsYourInstanceId>替换为f3的实例ID，<hereIsFpgaUUID>替换为您获取的FpgaUUID，<hereIsImageUUID>替换为您获取的FpgaImageUUID
        faascmd download_image --instanceId=<hereIsYourInstanceId> --fpgauuid=<hereIsFpgaUUID> --fpgatype=xilinx --imageuuid=<hereIsImageUUID> --imagetype=afu --shell=<hereIsShellVersionOfFpga>
        ```

        ![download_image](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2875688951/p12116.png)

    5.  运行以下命令查看镜像是否下载成功。

        ```
        # 将<hereIsFpgaUUID>替换为您获取的FpgaUUID，<hereIsYourInstanceId>替换为f3实例ID。
        faascmd fpga_status --fpgauuid=<hereIsFpgaUUID> --instanceId=<hereIsYourInstanceId> 
        ```

        以下为返回结果示例。如果显示的FpgaImageUUID与您获取的FpgaImageUUID一致，并且显示"TaskStatus":"valid"，说明镜像下载成功。

        ![fpga_status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2875688951/p12117.png)


## FAQ

问题一：上传镜像时出现异常，如何查看异常详情？

如果您的工程在上传生成镜像的过程中出现异常，例如云上编译服务器编译报错，您可以通过以下两种方式来查看异常详情：

-   查看faas\_compiling.log。使用上传脚本faas\_upload\_and\_create\_image.sh时，如果编译失败会自动下载并打印faas\_compiling.log到terminal中。
-   手动执行命令查看编译log文件：`sh /root/xbinst_oem/tool/faas_checklog.sh <bit.tar.gz之前上传的压缩包文件名>`

问题二：如何重新加载镜像？

您可以参考以下步骤重新加载镜像：

1.  卸载驱动。

    -   如果您安装了`xdma`驱动，则需要在实例中运行`sudo rmmod xdma`命令卸载驱动。
    -   如果您安装了`xocl`驱动，则需要在实例中运行`sudo rmmod xocl`命令卸载驱动。
2.  下载镜像。

    您可以使用以下两种方式之一：

    -   使用脚本：

        ```
        sh faas_download_image.sh bit.tar.gz <0/1> #最后的数字为实例中FPGA的序号
        ```

    -   使用faascmd：

        ```
        faascmd download_image --instanceId=hereIsYourInstanceId --fpgauuid=hereIsFpgaUUID --fpgatype=xilinx --imageuuid=hereIsImageUUID --imagetype=afu --shell=hereIsShellVersionOfFpga
        ```

3.  安装驱动。

    -   如果您需要安装`xdma`驱动，请运行以下命令。

        ```
        sudo depmod
        sudo modprobe xdma
        ```

    -   如果您需要安装`xocl`驱动，请运行以下命令。

        ```
        sudo depmod 
        sudo modprobe xocl
        ```


