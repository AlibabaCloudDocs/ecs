# 在f1实例中使用CTAccel图像处理（CIP）加速器

如果您的某些业务要求ECS实例内不能使用AccessKey，您可以为ECS实例配置RAM角色，ECS实例中部署的应用需要通过实例元数据获取临时授权Token，才可以访问指定资源。本教程介绍如何以无AccessKey的方式访问f1实例资源，从而便捷地为f1实例加载CTAccel CIP加速器。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。
-   已完成实名认证。如还未认证，请先完成[实名认证](https://account.console.aliyun.com/v2/#/authc/types)。
-   联系服务商完成以下准备工作，联系方式请参见[CTAccel CIP加速器服务商](https://market.aliyun.com/tasksubmitToSupplier?supplierId=2404532)。
    -   获取开发套件包。
    -   了解支持的镜像类型，并为ECS实例准备自定义镜像。
    -   关联ECS实例镜像和FPGA镜像。

        **说明：** ECS实例镜像必须为自定义镜像，申请关联镜像时请提供镜像ID。

    -   获取FPGA镜像的FPGAImageUUID。

CTAccel图像处理（CIP）加速器是一款基于FPGA的图像处理加速解决方案，可通过将计算负载从CPU转移至FPGA，显著提高图像处理及图像分析的性能。

## 操作步骤

-   [步骤一：创建RAM角色并授予权限](#section_sep_md2_o57)
-   [步骤二：创建f1实例并配置RAM角色和标签](#section_p4k_tbd_wwd)
-   [步骤二：为已有f1实例配置RAM角色和标签](#section_b61_khi_eb2)
-   [步骤三：安装faascmd](#section_17r_bh1_7ka)
-   [步骤四：配置CTAccel环境](#section_3re_cgb_zer)

## 步骤一：创建RAM角色并授予权限

创建RAM角色并配置RAM权限用于实现无AccessKey访问。更多实例RAM角色说明，请参见[实例RAM角色概述](/cn.zh-CN/安全/实例RAM角色/概述.md)。

1.  云账号登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  创建权限策略。

    1.  单击**权限管理** \> **权限策略管理**。

    2.  单击**创建权限策略**。

    3.  填写策略名称。

        本示例中使用faasEcsRamPolicy。

    4.  配置模式选择**脚本配置**。

    5.  填入权限策略内容。

        以下权限策略用于允许受信服务查看绑定对应标签的ECS实例资源。您可以自定义标签的键和标签值，本示例中使用faas和image。

        ```
        {
            "Version": "1",
            "Statement": [
                {
                    "Action": "ecs:DescribeInstances",
                    "Effect": "Allow",
                    "Resource": "acs:ecs:*:*:*",
                    "Condition": {
                        "StringEquals": {
                            "ecs:tag/faas": "image"
                        }
                    }
                }
            ]
        }
        ```

    6.  单击**确定**。

3.  创建RAM角色。

    如果已存在AliyunFAASDefaultRole，您可以在已有基础上增加信任策略的内容并授予权限。

    **说明：** 如果其它子账号也使用了AliyunFAASDefaultRole，请谨慎修改。

    1.  单击**RAM角色管理**。

    2.  单击**创建RAM角色**。

    3.  类型选择**阿里云服务**。

    4.  填写角色名称，必须是AliyunFAASDefaultRole。

    5.  受信服务选择**云服务器**。

    6.  单击**完成**。

    7.  单击**关闭**。

4.  修改RAM角色的信任策略。

    1.  找到创建的AliyunFAASDefaultRole，在**RAM角色名称列**中，单击名称。

    2.  单击**信任策略管理**。

    3.  单击**修改信任策略**。

    4.  按以下信任策略修改，然后单击**确定**。

        以下信任策略用于允许ECS服务和FaaS服务扮演该RAM角色。

        ```
        {
            "Statement": [
                {
                    "Action": "sts:AssumeRole",
                    "Effect": "Allow",
                    "Principal": {
                        "Service": [
                            "ecs.aliyuncs.com",
                            "faas.aliyuncs.com"
                        ]
                    }
                }
            ],
            "Version": "1"
        }
        ```

5.  授予RAM角色权限。

    1.  单击**权限管理**。

    2.  单击**精确授权**。

    3.  单击**自定义策略**。

    4.  输入策略名称。

        例如本示例中的faasEcsRamPolicy。

    5.  单击**确定**。

    6.  单击**关闭**。

    授权后，ECS服务和FaaS服务可以通过扮演RAM角色AliyunFAASDefaultRole，获取查看绑定标签`faas:image`的ECS实例资源的权限，无需再提供AccessKey。


## 步骤二：创建f1实例并配置RAM角色和标签

请参见以下步骤创建一台f1实例，并在创建过程中配置RAM角色和标签。

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，单击**实例与镜像** \> **实例**。

3.  单击**创建实例**。

4.  完成实例创建。

    下表中只列出需要重点关注的配置项，请视需要完成其它配置，更多说明请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。

    |配置页面|配置项|说明|
    |----|---|--|
    |**基本配置**|**实例**|    -   如果处理JPEG和WebP格式的图片，建议选择ecs.f1-c8f1.2xlarge。
    -   如果处理HEIF格式的图片，建议选择ecs.f1-c28f1.7xlarge。
您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。 |
    |**镜像**|选择您创建好的自定义镜像。|
    |**系统配置**|**实例RAM角色**|AliyunFAASDefaultRole|
    |**分组设置**|**标签**|权限策略中定义的标签键和标签值，本示例中使用`faas:image`。|

5.  在实例列表中，找到f1实例，然后在**实例ID/名称**列中，单击实例ID。

    确认已成功为f1实例授予RAM角色并绑定标签。

    ![添加RAM角色和绑定标签](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1008304061/p77385.png)

    ![ram](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1008304061/p178013.png)


## 步骤二：为已有f1实例配置RAM角色和标签

如果您已经创建了f1实例，且f1实例的实例规格和镜像满足要求，请参见以下步骤配置RAM角色和标签。

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，单击**实例与镜像** \> **实例**。

3.  找到待操作的f1实例。

4.  为f1实例授权RAM角色。

    1.  在实例列表中，找到待操作f1实例，然后单击**更多** \> **实例设置** \> **授予/收回RAM角色**。

    2.  选择RAM角色AliyunFAASDefaultRole，然后单击**确定**。

5.  为f1实例绑定标签。

    1.  在实例列表中，找到待操作f1实例，然后单击**更多** \> **实例设置** \> **编辑标签**。

    2.  单击**新建标签**，输入上文信任策略中定义的标签键和标签值，然后单击**确定**。

    3.  标签绑定完毕后，单击**确定**。

6.  在实例列表中，找到f1实例，然后在**实例ID/名称**列中，单击实例ID。

    确认已成功为f1实例授予RAM角色并绑定标签。

    ![添加RAM角色和绑定标签](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1008304061/p77385.png)

    ![ram](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1008304061/p178013.png)


## 步骤三：安装faascmd

faascmd是阿里云FPGA云服务器（FaaS平台）提供的命令行工具，是基于阿里云Python SDK开发的脚本，您可以通过faascmd命令方便地操作FaaS平台的资源。

1.  [远程连接Linux实例](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  检查是否安装了Python，且确保Python版本号必须为2.7.x。

    ```
    python -V
    ```

    返回Python版本号表示已安装Python。如果版本过低，请先升级至2.7.x。如果版本过高，请使用2.7.x版本，否则可能存在语法兼容问题。

    ![检查Python安装](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7775688951/p77387.png)

3.  安装Python模块。

    ```
    pip install oss2
    pip install aliyun-python-sdk-core
    pip install aliyun-python-sdk-faas
    pip install aliyun-python-sdk-ram
    ```

4.  检查aliyun-python-sdk-core版本号，确保版本号为2.11.0或以上版本。

    ```
    pip list | grep aliyun-python-sdk-core
    ```

    如果版本过低，请先升级至2.11.0或以上版本。

    ![检查Python SDK版本](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7775688951/p77390.png)

5.  下载faascmd。

    ```
    curl -o /bin/faascmd http://fpga-tools.oss-cn-shanghai.aliyuncs.com/faascmd-sts
    ```

6.  为faascmd添加可执行权限。

    ```
    chmod +x /bin/faascmd
    ```


## 步骤四：配置CTAccel环境

您可以从服务商提供的开发套件包中获取OPAE和CIP SDK安装包。

1.  安装图片lib库。

    ```
    yum install libjpeg-turbo-* libpng-* libwebp-* libtiff-* jasper jasper-devel
    ```

2.  切换至OPAE安装包目录，运行以下命令安装OPAE。

    ```
    yum install opae-*
    ```

3.  切换至CIP SDK安装包目录，运行以下命令安装CIP SDK。

    ```
    yum install accel-*
    ```

4.  下载初始化配置脚本。

    ```
    curl -o ctaccel-aliyun-init.sh https://fpga-tools.oss-cn-shanghai.aliyuncs.com/ctaccel-aliyun-init.sh
    ```

5.  加载您从服务商处获取的FPGA镜像，并初始化软件环境。

    ```
    sh ctaccel-aliyun-init.sh <yourFPGAImageUUID> 
    ```

    如果出现报错HTTP Status: 404 Error:IMAGE NOT FOUND The fpga image you specify is not found!，原因为未关联ECS镜像和FPGA镜像。请联系服务商进行关联操作。其它faascmd报错的处理方法，请参见[faascmd工具FAQ](/cn.zh-CN/最佳实践/FaaS实例最佳实践/faascmd工具/faascmd工具FAQ.md)。

6.  查看acceld service状态。

    ```
    service acceld status
    ```

    配置成功后，acceld service需要为running状态。

    **说明：** 请记录服务启动日期用于查看日志文件。

    ![acceld service状态](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7775688951/p77396.png)

7.  查看日志文件状态。

    ```
    cat /var/log/acceld-<年-月-日>.log
    ```

    配置成功后，日志文件中需要正确读取版本号。图中版本号仅为示例，版本号应和购买时服务商提供的版本一致。

    ![读取加速设备版本号](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7775688951/p77399.png)


**相关文档**  


[AttachInstanceRamRole](/cn.zh-CN/API参考/实例/AttachInstanceRamRole.md)

[TagResources](/cn.zh-CN/API参考/标签/TagResources.md)

