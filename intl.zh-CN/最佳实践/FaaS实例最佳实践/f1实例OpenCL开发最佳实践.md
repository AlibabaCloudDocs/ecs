# f1实例OpenCL开发最佳实践

本文介绍如何在f1实例上使用OpenCL（Open Computing Language）制作镜像文件，并烧写到FPGA芯片中。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.alibabacloud.com/register/intl_register.htm)。
-   已创建f1实例并且实例能访问公网。

    **说明：** f1实例只能使用镜像市场的FaaS F1基础镜像。更多详情，请参见[创建f1实例](/intl.zh-CN/实例/选择实例规格/FPGA计算型/创建f1实例.md)。

-   已在f1实例所在的安全组中添加规则并放行SSH（22）端口。
-   已在[ECS管理控制台](https://ecs.console.aliyun.com/#/home)f1实例详情页上获取实例ID。
-   已创建OSS Bucket专门用于FaaS服务。

    Bucket与f1实例必须属于同一个账号、同一个地域。若尚未创建，请参见[创建一个OSS Bucket](/intl.zh-CN/快速入门/控制台快速入门/创建存储空间.md)。

-   如需加密文件，请先开通密钥管理服务（KMS）。

    若尚未开通，请参见[开通密钥管理服务（KMS）](/intl.zh-CN/快速入门/入门概述.md)。

-   使用RAM用户操作FPGA，必须先完成以下操作：
    -   创建RAM用户并授权，详情请参见[创建RAM用户](/intl.zh-CN/用户管理/创建RAM用户.md)及[为RAM用户授权](/intl.zh-CN/用户管理/为RAM用户授权.md)。

        您需要为RAM用户授予的权限为：AliyunECSReadOnlyAccess、AliyunOSSFullAccess和AliyunRAMFullAccess。

    -   授权FaaS服务角色，授权页面请参见[授权FaaS服务角色](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunFAASDefaultRole%22%2C%20%22TemplateId%22%3A%20%22DefaultRole%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//ecs.console.aliyun.com/%23/home%22%2C%20%22Service%22%3A%20%22FAAS%22%7D)。
    -   获取AccessKey ID和AccessKey Secret。

开始操作之前，请阅读以下注意事项：

-   本教程中所有操作都必须由同一个账号在同一地域里执行。
-   强烈建议您使用RAM用户操作FaaS实例。为了防止意外操作，您需要让RAM用户仅执行必要的操作。在操作FPGA镜像及下载时，因为您需要从指定的OSS Bucket下载原始DCP工程，所以您必须为FaaS管理账号创建一个角色，并授予临时权限，让FaaS管理账号访问指定的OSS Bucket。如果需要对IP加密，必须授予RAM用户KMS相关权限。如果需要做权限检查，必须授予查看用户资源的权限。

## 操作步骤

在f1实例上，使用OpenCL Example制作镜像文件，并烧写到FPGA芯片中的操作步骤如下：

1.  [步骤一：远程连接实例](#section_0xw_r1j_tak)
2.  [步骤二：安装基础环境](#section_gob_p8r_eox)
3.  [步骤三：拷贝官方的OpenCL Example](#section_jrm_tz5_d4k)
4.  [步骤四：上传配置文件](#section_hbq_4vp_q7d)
5.  [步骤五：下载镜像到f1实例](#section_nxl_txt_iep)
6.  [步骤六：将FPGA镜像烧录到FPGA芯片](#section_bcs_ojs_uae)

## 步骤一：远程连接实例

具体操作，请参见[远程连接Linux实例](/intl.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/使用用户名密码验证连接Linux实例.md)。

## 步骤二：安装基础环境

运行以下脚本安装基础环境。

```
source /opt/dcp1_1/script/f1_env_set.sh
```

## 步骤三：拷贝官方的OpenCL Example

1.  依次运行以下命令创建并切换到/opt/tmp目录。

    ```
    mkdir -p /opt/tmp         
    ```

    ```
    cd /opt/tmp            
    ```

    此时，您位于/opt/tmp目录下。

    ![进入tmp目录](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4775688951/p11994.png)

2.  运行以下命令将Example文件拷贝至当前目录。

    ```
    cp /opt/dcp1_1/opencl/exm_opencl_vector_add_x64_linux.tgz ./
    ```

3.  依次运行以下命令进入vector\_add目录并执行编译命令。

    ```
    cd vector_add             
    ```

    ```
    aoc -v -g -report ./device/vector_add.cl             
    ```

    编译过程可能会持续数个小时，您可以再开一个会话，使用top命令监控系统资源占用情况，确定编译状态。


## 步骤四：上传配置文件

1.  依次运行以下命令初始化faascmd工具。

    ```
    #配置环境变量
    export PATH=$PATH:/opt/dcp1_1/script/
    ```

    ```
    #为faascmd工具添加可执行权限
    chmod +x /opt/dcp1_1/script/faascmd
    ```

    ```
    #将命令中的<hereIsYourSecretId>换为您的AccessKey ID，<hereIsYourSecretKey>替换为您的AccessKey Secret
    faascmd config --id=<hereIsYourSecretId> --key=<hereIsYourSecretKey>
    ```

    ```
    #将命令中的<hereIsYourBucket>换为您的Bucket名称
    faascmd auth --bucket=<hereIsYourBucket>
    ```

2.  依次运行以下面命令进入vector\_add/output\_files目录并上传配置文件。

    ```
    cd vector_add/output_files         
    ```

    此时，您应该在/opt/tmp/vector\_add/vector\_add/output\_files目录下。

    ```
    faascmd upload_object --object=afu_fit.gbs --file=afu_fit.gbs           
    ```

3.  运行以下命令使用gbs制作FPGA镜像。

    ```
    #将命令中的<hereIsYourImageName>换为您的镜像名，将<hereIsYourImageTag>替换为您的镜像标签
    faascmd create_image --object=dma_afu.gbs --fpgatype=intel --name=<hereIsYourImageName> --tags=<hereIsYourImageTag> --encrypted=false --shell=V1.1             
    ```

4.  运行以下命令查看镜像是否制作成功。

    ```
    faascmd list_images
    ```

    若返回结果中显示"State":"success"，表示镜像制作成功。请记录返回结果中显示的FpgaImageUUID，稍后会用到。

    ![镜像制作成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4775688951/p11996.png)


## 步骤五：下载镜像到f1实例

1.  运行以下命令获取FPGA ID。

    ```
    #将命令中的<hereIsYourInstanceId>替换为您的FPGA实例ID
    faascmd list_instances --instanceId=<hereIsYourInstanceId>                 
    ```

    返回结果如下图所示。请记录FpgaUUID。

    ![fpgaUUID](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4775688951/p11997.png)

2.  运行以下命令下载镜像到f1实例。

    ```
    #将命令中的<hereIsYourInstanceID>替换为刚刚保存的实例ID；将<hereIsFpgaUUID>替换为上一条命令中记下的FpgaUUID；将<hereIsImageUUID>替换为上一步记下的FpgaImageUUID
    faascmd download_image  --instanceId=<hereIsYourInstanceID> --fpgauuid=<hereIsFpgaUUID> --fpgatype=intel --imageuuid=<hereIsImageUUID> --imagetype=afu --shell=V0.11                 
    ```

3.  运行以下命令检查是否下载成功。

    ```
    # 将命令中的<hereIsYourInstanceID>替换为刚刚保存的实例ID；将<hereIsFpgaUUID>替换为上一条命令中记下的FpgaUUID
    faascmd fpga_status --fpgauuid=<hereIsFpgaUUID> --instanceId=<hereIsYourInstanceID>            
    ```

    若返回结果中显示"TaskStatus":"operating"，说明下载成功。

    ![下载成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4775688951/p11998.png)


## 步骤六：将FPGA镜像烧录到FPGA芯片

1.  打开步骤二环境的窗口。如果已关闭，重新执行[步骤二](#section_gob_p8r_eox)操作。

2.  运行以下命令配置OpenCL的运行环境。

    ```
    sh /opt/dcp1_1/opencl/opencl_bsp/linux64/libexec/setup_permissions.sh                 
    ```

3.  运行以下命令返回上级目录。

    ```
    cd ../..           
    ```

    此时，您位于/opt/tmp/vector\_add目录下。

4.  执行编译命令。

    ```
    make
    # 输出环境配置
    export CL_CONTEXT_COMPILER_MODE_ALTERA=3
    cp vector_add.aocx ./bin/vector_add.aocx
    cd bin
    host vector_add.aocx               
    ```

    当您看到如下输出时，说明配置完成。请注意，最后一行必须为`Verification: PASS`。

    ```
    [root@iZbpXXXXXZ bin]# ./host vector_add.aocx
    Matrix sizes:
      A: 2048 x 1024
      B: 1024 x 1024
      C: 2048 x 1024
    Initializing OpenCL
    Platform: Intel(R) FPGA SDK for OpenCL(TM)
    Using 1 device(s)
      skx_fpga_dcp_ddr : SKX DCP FPGA OpenCL BSP (acl0)
    Using AOCX: vector_add.aocx
    Generating input matrices
    Launching for device 0 (global size: 1024, 2048)
    Time: 40.415 ms
    Kernel time (device 0): 40.355 ms
    Throughput: 106.27 GFLOPS
    Computing reference output
    Verifying
    Verification: PASS             
    ```


