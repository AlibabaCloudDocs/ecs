# 创建NPU计算型实例

NPU计算型实例必须安装NPU驱动才可以使用NPU的计算能力。本文介绍如何创建NPU计算型实例并自动安装驱动和SDK。

完成创建ECS实例的准备工作：

1.  创建账号，以及完善账号信息。
    -   注册阿里云账号，并完成实名认证。具体操作，请参见[阿里云账号注册流程](https://help.aliyun.com/knowledge_detail/37195.htm)。
    -   如果创建按量付费实例，您的阿里云账户余额、代金券和优惠券的总值不得小于100.00元人民币。具体充值操作，请参见[如何充值](https://help.aliyun.com/document_detail/37107.html?spm=a2c4g.11186623.2.5.CscUFl)。
2.  阿里云提供一个默认的专有网络VPC，如果您不想使用默认专有网络VPC，可以在目标地域创建一个专有网络和交换机。具体操作，请参见[搭建IPv4专有网络](/cn.zh-CN/快速入门/搭建IPv4专有网络.md)。
3.  阿里云提供一个默认的安全组，如果您不想使用默认安全组，可以在目标地域创建一个安全组。具体操作，请参见[创建安全组](/cn.zh-CN/安全/安全组/创建安全组.md)。

如果您需要使用其它扩展功能，也需要完成相应的准备工作，例如：

-   如果创建Linux实例时要绑定SSH密钥对，需要在目标地域创建一个SSH密钥对。具体操作，请参见[创建SSH密钥对](/cn.zh-CN/安全/SSH密钥对/使用SSH密钥对/创建SSH密钥对.md)。
-   如果要设置自定义数据，需要准备实例自定义数据。具体操作，请参见[ECS实例自定义数据概述](/cn.zh-CN/实例/管理实例/使用实例自定义数据/ECS实例自定义数据概述.md)。
-   如果要为ECS实例关联某个角色，需要创建、授权实例RAM角色，并将其授予ECS实例。具体操作，请参见[授予实例RAM角色](/cn.zh-CN/安全/实例RAM角色/授予实例RAM角色.md)。

本文介绍如何在管理控制台创建一台NPU计算型实例，如果您调用RunInstances接口创建实例，可以通过UserData参数上传自动安装脚本，脚本内容需要使用Base64方式编码。

## 操作步骤

本步骤重点介绍NPU计算型实例相关的配置，如果您想了解其他通用配置，请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。

1.  前往[实例创建页](https://ecs-buy.aliyun.com/wizard/#/)。

2.  完成基础配置，然后单击**下一步：网络和安全组**。

    **说明：** NPU计算型实例在特定地域和可用区售卖，您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)页面查看。选择您需要的付费模式，输入实例规格名称搜索即可。

    请注意以下配置：

    -   **实例**：定位到**异构计算GPU/FPGA/NPU** \> **NPU计算型**，然后选择实例规格。
    -   **镜像**：NPU计算型实例使用部分公共镜像时，支持自动安装NPU驱动和SDK。选中**自动安装驱动**复选框和**自动安装SDK**复选框，实例创建完成后会执行自动安装脚本，安装最新版本的NPU驱动和SDK。支持自动安装的公共镜像如下：

        -   CentOS 7.6 64位
        -   CentOS 7.7 64位
        -   Ubuntu 16.04 64位
        ![自动安装驱动](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1404359951/p137803.png)

    -   **存储**：安装NPU驱动和SDK后，可以执行例程体验使用NPU。为保证顺利执行例程，建议系统盘不小于60 GiB。
3.  完成网络和安全组配置，然后单击**下一步：系统配置**。

4.  完成系统配置，然后单击**下一步：分组配置**。

    请注意以下配置：

    -   **登录凭证**：建议选择**密钥对**或**自定义密码**。如果您选择了**创建后设置**，登录实例前必须先绑定SSH密钥对或者重置密码，然后重启实例使修改生效。如果此时NPU驱动尚未安装完成，重启实例会导致安装失败。
    -   **实例自定义数据**： 用于输入自动安装脚本。
        -   如果您在**基础配置**页面中选中了**自动安装驱动**复选框和**自动安装SDK**复选框，实例自定义数据区域会自动输入脚本，且内容不可编辑。

            ![实例自定义数据](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1404359951/p137801.png)

        -   如果您未在**基础配置**页面中选中**自动安装驱动**复选框和**自动安装SDK**复选框，仍可以自行在实例自定义数据区域输入脚本，参考脚本内容请参见[自动安装NPU驱动和SDK](#section_01q_l33_grl)。
5.  完成分组设置，然后单击**下一步：确认订单**。

6.  根据页面提示下单并完成支付。

    如果您配置了自动安装脚本，实例启动后会自动安装NPU驱动和SDK，安装耗时约为5~10分钟。如果未配置自动安装脚本，您也可以在创建实例后自行执行脚本，参考脚本内容请参见[自动安装NPU驱动和SDK](#section_01q_l33_grl)。

    **说明：** 在安装过程中无法使用NPU，请勿对实例进行任何操作，以防因自动安装失败导致实例不可用。

    您可以登录实例查看安装进度：

    -   如果正在安装，您可以看到安装进度条。
    -   如果已经安装成功，您可以看到安装结果提示**SUCCESS INSTALL DRIVER**和**SUCCESS INSTALL SDK**。
    -   如果安装失败，您将看到安装结果提示**ERROR**以及相关错误信息。
    您也可以在登录实例后查看安装日志文件，文件名为/root/auto\_install/auto\_install.log。


## 自动安装NPU驱动和SDK

如果通过实例自定义数据传入了自动安装脚本，NPU计算型实例首次启动时会通过cloud-init自动执行脚本，安装NPU驱动和SDK。

-   NPU驱动：支持的版本、镜像要求、实例规格要求下表所示。

    |NPU驱动|支持的公共镜像版本|支持的实例规格|
    |-----|---------|-------|
    |1.0.5|    -   CentOS 7.6 64位
    -   CentOS 7.7 64位
    -   Ubuntu 16.04 64位
|ebman1|

-   SDK：SDK为通过Python Conda环境安装的Tensorflow和MXNet深度学习框架，版本信息如下表所示。

    |Conda环境|相关版本信息|
    |-------|------|
    |alinpu\_tensorflow\_py36|    -   agraph=1.0.2
    -   hgai=1.0.5
    -   tensorflow=1.13.2 |
    |alinpu\_mxnet\_py36|    -   agraph=1.0.2
    -   hgai=1.0.5
    -   mxnet=1.5.1 |


如果您自行在实例自定义数据区域配置自动安装脚本或者手动执行脚本，请参考以下脚本内容：

```
#!/usr/bin/env bash

IS_INSTALL_DRIVER="TRUE"
IS_INSTALL_SDK="TRUE"

INSTALL_DIR="/root/auto_install"
AUTO_INSTALL_SCRIPT="auto_install.sh"

INSTANCE_TYPE=$(curl http://100.100.100.200/latest/meta-data/instance/instance-type)
INSTANCE_ARRAY=(${INSTANCE_TYPE//./ })
INSTANCE_FAMILY=${INSTANCE_ARRAY[1]}

BASE_URL=$(curl http://100.100.100.200/latest/meta-data/source-address | head -1)
DOWNLOAD_URL="${BASE_URL}/opsx/ecs/linux/binary"
DOWNLOAD_URL_SCRIPT=${DOWNLOAD_URL}/script/${INSTANCE_FAMILY}/${AUTO_INSTALL_SCRIPT}

echo ${DOWNLOAD_URL_SCRIPT}

mkdir -p ${INSTALL_DIR} && cd ${INSTALL_DIR} && wget -t 10 --timeout=10 ${DOWNLOAD_URL_SCRIPT}
bash ${INSTALL_DIR}/${AUTO_INSTALL_SCRIPT} ${IS_INSTALL_DRIVER} ${IS_INSTALL_SDK}
```

**说明：** 如果不需要安装SDK，将IS\_INSTALL\_SDK的值修改为FALSE即可。

自动安装脚本具有以下优势：

-   提供最新版本的NPU驱动和SDK。
-   登录实例后可以查看安装进度，如果正在安装可以看到安装进度条，如果已经完成安装可以看到安装结果。

## NPU使用示例

成功安装NPU驱动和SDK后，您可以执行以下例程体验使用SDK编写一个运行在NPU上的推理应用，实现使用NPU进行图像分类。

**说明：** 模型量化过程中会产生中间数据，为保证顺利执行例程，需要预留约60 GiB的磁盘空间。

-   NPU TensorFlow例程

    NPU TensorFlow例程以预训练模型resnet\_v2\_50为例，执行该例程时包括以下模式：

    -   convert mode：此模式下会加载原始FP32模型，经过量化、编译生成适合NPU处理的INT8模型。生成的NPU INT8模型文件会放在output\_resnet\_v2\_50目录下，命名为resnet\_v2\_50.npu.pb。
    -   npu mode：此模式下会加载NPU INT8模型进行模型评估。
    脚本内容如下：

    ```
    # 激活NPU TensorFlow环境。
    conda activate alinpu_tensorflow_py36
    
    # 下载测试数据集。
    mkdir -p /root/.cache/agraph/tf/datasets/imagenet_val/tf_record_cal
    source_address=$(curl http://100.100.100.200/latest/meta-data/source-address|head -n 1)
    source_address="${source_address}/opsx/ecs/linux/binary/alinpu"
    wget -t 100 --timeout=10 ${source_address}/data/tf_record.tgz
    tar -zxf tf_record.tgz
    mv tf_record /root/.cache/agraph/tf/datasets/imagenet_val
    cp /root/.cache/agraph/tf/datasets/imagenet_val/tf_record/validation-00000-of-00128 /root/.cache/agraph/tf/datasets/imagenet_val/tf_record_cal
    
    # 下载resnet_v2_50 FP32模型。
    mkdir -p /root/.cache/agraph/tf/models/resnet_v2_50
    wget ${source_address}/models/tensorflow/resnet_v2_50/resnet_v2_50.pb
    mv resnet_v2_50.pb /root/.cache/agraph/tf/models/resnet_v2_50
    
    # 下载例程测试脚本。
    wget ${source_address}/example/tf_resnet_v2_50.py
    
    # 在convert mode下执行，生成的NPU INT8模型文件会放在output_resnet_v2_50目录下，命名为resnet_v2_50.npu.pb。
    python tf_resnet_v2_50.py --mode convert
    
    # 在npu mode下执行，使用生成的NPU INT8模型进行模型评估。
    python tf_resnet_v2_50.py --mode npu
    ```

    成功执行脚本后，模型评估结果如下图所示。

    ![tensorflow convert](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1404359951/p137799.png)

-   NPU MXNet例程

    NPU MXNet例程以预训练模型resnet50\_v2为例，执行该例程时包括以下模式：

    -   convert mode：此模式下会加载原始FP32模型，经过量化、编译生成适合NPU处理的INT8模型。生成的NPU INT8模型文件会放在output\_resnet50\_v2的目录下，命名为resnet50\_v2.npu-symbol.json以及resnet50\_v2.npu-0000.params。
    -   npu mode：此模式会加载NPU INT8模型进行模型评估。
    脚本内容如下：

    ```
    # 激活NPU MXNet环境。
    conda activate alinpu_mxnet_py36
    
    # 下载测试数据集。
    mkdir -p /root/.cache/agraph/mxnet/datasets/imagenet_mxnet
    source_address=$(curl http://100.100.100.200/latest/meta-data/source-address|head -n 1)
    source_address="${source_address}/opsx/ecs/linux/binary/alinpu"
    wget -t 100 --timeout=10 ${source_address}/data/ILSVRC2012_img_out.tgz
    tar -zxf ILSVRC2012_img_out.tgz
    mv ILSVRC2012_img_out /root/.cache/agraph/mxnet/datasets/imagenet_mxnet/
    
    # 下载resnet50_v2 FP32模型。
    mkdir -p /root/.cache/agraph/mxnet/models/resnet50_v2
    wget ${source_address}/models/mxnet/resnet50_v2/resnet50_v2-0000.params
    wget ${source_address}/models/mxnet/resnet50_v2/resnet50_v2-symbol.json
    mv resnet50_v2-0000.params resnet50_v2-symbol.json /root/.cache/agraph/mxnet/models/resnet50_v2/
    
    # 下载例程测试脚本。
    wget ${source_address}/example/mxnet_resnet50_v2.py
    
    # 在convert mode下执行，生成的NPU INT8模型文件会放在output_resnet50_v2目录下，命名为resnet50_v2.npu-symbol.json以及resnet50_v2.npu-0000.params。
    python mxnet_resnet50_v2.py --mode convert
    
    # 在npu mode下执行，使用生成的NPU INT8模型进行模型评估。
    python mxnet_resnet50_v2.py --mode npu
    ```

    成功执行脚本后，模型评估结果如下图所示。

    ![mxnet convert](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2404359951/p137798.png)


