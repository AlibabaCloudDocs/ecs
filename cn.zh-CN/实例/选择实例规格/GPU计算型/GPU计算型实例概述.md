---
keyword: [阿里云, ecs, 服务器, 弹性计算]
---

# GPU计算型实例概述

本文介绍云服务器ECS GPU计算型实例规格族的特点，并列出了具体的实例规格。

-   推荐
    -   [GPU计算型实例规格族gn7](#section_4xh_rvo_jxy)
    -   [轻量级GPU计算型实例规格族vgn6i](#section_dti_hon_urw)
    -   [GPU计算型实例规格族gn6i](#section_e88_tau_vwf)
    -   [GPU计算型实例规格族gn6e](#section_8gr_min_yk3)
    -   [GPU计算型实例规格族gn6v](#section_698_e4v_7rh)
-   其他在售（如果售罄，建议使用推荐规格族）
    -   [轻量级GPU计算型实例规格族vgn5i](#section_lip_fsm_g9e)
    -   [GPU计算型实例规格族gn5](#section_8ir_i5x_nvl)
    -   [GPU计算型实例规格族gn5i](#section_ye9_eyj_ek2)

## GPU计算型实例规格族gn7

该规格族正在邀测中，暂未开放售卖。

gn7的特点如下：

-   计算：
    -   采用NVIDIA A100 GPU计算卡，多卡之间以NVSwitch实现两两互联
        -   创新的Ampere架构
        -   单GPU显存40 GB HBM2
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8269CY（Cascade Lake）
-   存储：
    -   I/O优化实例
    -   支持ESSD云盘、SSD云盘和高效云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   深度学习，例如图像分类、无人驾驶、语音识别等人工智能算法的训练应用
    -   高GPU负载的科学计算，例如计算流体动力学、计算金融学、分子动力学、环境分析等

gn7包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|GPU|GPU显存|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|
|:---|:---|:------|:--|:----|------------|:----------|:--|:---|
|ecs.gn7-c12g1.3xlarge|12|95.0|NVIDIA A100 \* 1|40GB \* 1|4.0|250|4|8|
|ecs.gn7-c13g1.13xlarge|52|380.0|NVIDIA A100 \* 4|40GB \* 4|15.0|900|16|8|
|ecs.gn7-c13g1.26xlarge|104|760.0|NVIDIA A100 \* 8|40GB \* 8|30.0|1800|16|16|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。

## 轻量级GPU计算型实例规格族vgn6i

vgn6i的特点如下：

-   如果您需要vgn6i实例支持OpenGL图形显示等图形功能，请使用NVIDIA vGPU相关软件，软件License的获取方式和实例规格、实例镜像类型有关：
    -   ecs.vgn6i-m4-vws.xlarge和ecs.vgn6i-m8-vws.2xlarge：已包含NVIDIA Quadro vWS的软件License，您可以使用任意镜像类型。
    -   其他vgn6i实例（Windows镜像）：创建实例时在镜像市场中搜索关键词GRID，并选用预装GRID驱动的收费镜像。这些收费镜像带有已经激活License的GRID驱动，不用再手动安装GRID驱动。关于如何选择镜像市场镜像，请参见[创建配备NVIDIA GPU的实例]()。
    -   其他vgn6i实例（Linux镜像）：请自行向[NVIDIA](https://www.nvidia.com/object/nvidia-enterprise-account.html)购买GRID License，并在创建实例后手动安装GRID驱动和激活License。关于如何安装GRID驱动，请参见[在GPU虚拟化型实例中安装GRID驱动（Linux）](/cn.zh-CN/实例/选择实例规格/GPU计算型/在vgn6i和vgn5i实例中安装GRID驱动（Linux）.md)。
-   计算：
    -   采用NVIDIA T4 GPU计算加速器
    -   实例包含分片虚拟化后的虚拟GPU
        -   计算能力支持NVIDIA Tesla T4的1/4和1/2
        -   GPU显存支持4 GB和8 GB
    -   处理器与内存配比约为1:5
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8163（Skylake）
-   存储：
    -   I/O优化实例
    -   仅支持SSD云盘和高效云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   云游戏的云端实时渲染
    -   AR和VR的云端实时渲染
    -   AI（DL和ML）推理，适合弹性部署含有AI推理计算应用的互联网业务
    -   深度学习的教学练习环境
    -   深度学习的模型实验环境

vgn6i包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|GPU|GPU显存|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:--|:----|:-----------|:----------|:--|:---|-------|
|ecs.vgn6i-m4.xlarge|4|23.0|NVIDIA T4 \* 1/4|16GB \* 1/4|3.0|50|2|4|10|
|ecs.vgn6i-m8.2xlarge|10|46.0|NVIDIA T4 \* 1/2|16GB \* 1/2|4.0|80|4|5|20|
|ecs.vgn6i-m4-vws.xlarge|4|23.0|NVIDIA T4 \* 1/4|16GB \* 1/4|3.0|50|2|4|10|
|ecs.vgn6i-m8-vws.2xlarge|10|46.0|NVIDIA T4 \* 1/2|16GB \* 1/2|4.0|80|4|5|20|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。

## GPU计算型实例规格族gn6i

gn6i的特点如下：

-   计算：
    -   GPU加速器：T4
        -   创新的Turing架构
        -   单GPU显存16 GB（GPU显存带宽320 GB/s）
        -   单GPU 2560个CUDA Cores
        -   单GPU多达320个Turing Tensor Cores
        -   可变精度Tensor Cores支持65 TFlops FP16、130 INT8 TOPS、260 INT4 TOPS
    -   处理器与内存配比约为1:4
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8163（Skylake）
-   存储：
    -   I/O优化实例
    -   支持ESSD云盘（百万IOPS）、SSD云盘和高效云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   AI（DL和ML）推理，适合计算机视觉、语音识别、语音合成、NLP、机器翻译、推荐系统
    -   云游戏云端实时渲染
    -   AR和VR的云端实时渲染
    -   重载图形计算或图形工作站
    -   GPU加速数据库
    -   高性能计算

gn6i包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|GPU|GPU显存|网络带宽（Gbit/s）|网络收发包PPS（万）|存储IOPS基准（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:--|:----|------------|:----------|-----------|:--|:---|-------|
|ecs.gn6i-c4g1.xlarge|4|15.0|NVIDIA T4 \* 1|16GB \* 1|4.0|50|无|2|2|10|
|ecs.gn6i-c8g1.2xlarge|8|31.0|NVIDIA T4 \* 1|16GB \* 1|5.0|80|无|2|2|10|
|ecs.gn6i-c16g1.4xlarge|16|62.0|NVIDIA T4 \* 1|16GB \* 1|6.0|100|无|4|3|10|
|ecs.gn6i-c24g1.6xlarge|24|93.0|NVIDIA T4 \* 1|16GB \* 1|7.5|120|无|6|4|10|
|ecs.gn6i-c24g1.12xlarge|48|186.0|NVIDIA T4 \* 2|16GB \* 2|15.0|240|无|12|6|10|
|ecs.gn6i-c24g1.24xlarge|96|372.0|NVIDIA T4 \* 4|16GB \* 4|30.0|480|25|24|8|10|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。

## GPU计算型实例规格族gn6e

gn6e的特点如下：

-   计算：
    -   采用NVIDIA V100（32 GB NVLink）GPU计算卡
    -   GPU加速器：V100（SXM2封装）
        -   创新的Volta架构
        -   单GPU显存32 GB HBM2（GPU显存带宽900 GB/s）
        -   单GPU 5120个CUDA Cores
        -   单GPU 640个Tensor Cores
        -   支持6个NVLink链路，每个25 GB/s，总共300 GB/s
    -   处理器与内存配比约为1:8
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8163（Skylake）
-   存储：
    -   I/O优化实例
    -   支持ESSD云盘、SSD云盘和高效云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   深度学习，例如图像分类、无人驾驶、语音识别等人工智能算法的训练、推理应用
    -   科学计算，例如计算流体动力学、计算金融学、分子动力学、环境分析等

gn6e包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|GPU|GPU显存|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:--|:----|:-----------|:----------|:--|:---|-------|
|ecs.gn6e-c12g1.3xlarge|12|92.0|NVIDIA V100 \* 1|32GB \* 1|5.0|80|8|6|10|
|ecs.gn6e-c12g1.12xlarge|48|368.0|NVIDIA V100 \* 4|32GB \* 4|16.0|240|8|8|20|
|ecs.gn6e-c12g1.24xlarge|96|736.0|NVIDIA V100 \* 8|32GB \* 8|32.0|480|16|8|20|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。

## GPU计算型实例规格族gn6v

gn6v的特点如下：

-   计算：
    -   采用NVIDIA V100 GPU计算卡
    -   GPU加速器：V100（SXM2封装）
        -   创新的Volta架构
        -   单GPU显存16 GB HBM2（GPU显存带宽900 GB/s）
        -   单GPU 5120个CUDA Cores
        -   单GPU 640个Tensor Cores
        -   支持6个NVLink链路，每个25 GB/s，总共300 GB/s
    -   处理器与内存配比约为1:4
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8163（Skylake）
-   存储：
    -   I/O优化实例
    -   支持ESSD云盘、SSD云盘和高效云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   深度学习，例如图像分类、无人驾驶、语音识别等人工智能算法的训练、推理应用
    -   科学计算，例如计算流体动力学、计算金融学、分子动力学、环境分析等

gn6v包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|GPU|GPU显存|网络带宽（Gbit/s）|网络收发包PPS（万）|存储IOPS基准（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:--|:----|:-----------|:----------|-----------|:--|:---|-------|
|ecs.gn6v-c8g1.2xlarge|8|32.0|NVIDIA V100 \* 1|16GB \* 1|2.5|80|无|4|4|10|
|ecs.gn6v-c8g1.8xlarge|32|128.0|NVIDIA V100 \* 4|16GB \* 4|10.0|200|无|8|8|20|
|ecs.gn6v-c8g1.16xlarge|64|256.0|NVIDIA V100 \* 8|16GB \* 8|20.0|250|无|16|8|20|
|ecs.gn6v-c10g1.20xlarge|82|336.0|NVIDIA V100 \* 8|16GB \* 8|32.0|450|25|16|8|20|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。

## 轻量级GPU计算型实例规格族vgn5i

vgn5i的特点如下：

-   如果您需要vgn5i实例支持OpenGL图形显示等图形功能，请使用NVIDIA vGPU相关软件，软件License的获取方式和实例镜像类型有关：
    -   vgn5i实例（Windows镜像）：创建实例时在镜像市场中搜索关键词GRID，并选用预装GRID驱动的收费镜像。这些收费镜像带有已经激活License的GRID驱动，不用再手动安装GRID驱动。关于如何选择镜像市场镜像，请参见[创建配备NVIDIA GPU的实例]()。
    -   vgn5i实例（Linux镜像）：请自行向[NVIDIA](https://www.nvidia.com/object/nvidia-enterprise-account.html)购买GRID License，并在创建实例后手动安装GRID驱动和激活License。关于如何安装GRID驱动，请参见[在GPU虚拟化型实例中安装GRID驱动（Linux）](/cn.zh-CN/实例/选择实例规格/GPU计算型/在vgn6i和vgn5i实例中安装GRID驱动（Linux）.md)。
-   计算：
    -   采用NVIDIA P4 GPU计算加速器
    -   实例包含分片虚拟化后的虚拟GPU
        -   计算能力支持NVIDIA Tesla P4的1/8、1/4、1/2和1:1
        -   GPU显存支持1 GB、2 GB、4 GB和8 GB
    -   处理器与内存配比为1:3
    -   处理器：2.5 GHz主频的Intel ® Xeon ® E5-2682 v4（Broadwell）
-   存储：
    -   I/O优化实例
    -   仅支持SSD云盘和高效云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   云游戏的云端实时渲染
    -   AR和VR的云端实时渲染
    -   AI（DL和ML）推理，适合弹性部署含有AI推理计算应用的互联网业务
    -   深度学习的教学练习环境
    -   深度学习的模型实验环境

vgn5i包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|GPU|GPU显存|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:--|:----|:-----------|:----------|:--|:---|-------|
|ecs.vgn5i-m1.large|2|6.0|NVIDIA P4 \* 1/8|8GB \* 1/8|1.0|30|2|2|6|
|ecs.vgn5i-m2.xlarge|4|12.0|NVIDIA P4 \* 1/4|8GB \* 1/4|2.0|50|2|3|10|
|ecs.vgn5i-m4.2xlarge|8|24.0|NVIDIA P4 \* 1/2|8GB \* 1/2|3.0|80|2|4|10|
|ecs.vgn5i-m8.4xlarge|16|48.0|NVIDIA P4 \* 1|8GB \* 1|5.0|100|4|5|20|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。

## GPU计算型实例规格族gn5

gn5的特点如下：

-   计算：
    -   采用NVIDIA P100 GPU计算卡
    -   多种处理器与内存配比
    -   处理器：2.5 GHz主频的Intel ® Xeon ® E5-2682 v4（Broadwell）
-   存储：
    -   配备高性能NVMe SSD本地盘
    -   I/O优化实例
    -   仅支持SSD云盘和高效云盘
-   网络：
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   深度学习
    -   科学计算，例如计算流体动力学、计算金融学、基因组学研究、环境分析
    -   高性能计算、渲染、多媒体编解码及其他服务器端GPU计算工作负载

gn5包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|本地存储（GiB）|GPU|GPU显存|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:--------|:--|:----|:-----------|:----------|:--|:---|-------|
|ecs.gn5-c4g1.xlarge|4|30.0|440|NVIDIA P100 \* 1|16GB \* 1|3.0|30|1|3|10|
|ecs.gn5-c8g1.2xlarge|8|60.0|440|NVIDIA P100 \* 1|16GB \* 1|3.0|40|1|4|10|
|ecs.gn5-c4g1.2xlarge|8|60.0|880|NVIDIA P100 \* 2|16GB \* 2|5.0|100|2|4|10|
|ecs.gn5-c8g1.4xlarge|16|120.0|880|NVIDIA P100 \* 2|16GB \* 2|5.0|100|4|8|20|
|ecs.gn5-c28g1.7xlarge|28|112.0|440|NVIDIA P100 \* 1|16GB \* 1|5.0|100|8|8|20|
|ecs.gn5-c8g1.8xlarge|32|240.0|1760|NVIDIA P100 \* 4|16GB \* 4|10.0|200|8|8|20|
|ecs.gn5-c28g1.14xlarge|56|224.0|880|NVIDIA P100 \* 2|16GB \* 2|10.0|200|14|8|20|
|ecs.gn5-c8g1.14xlarge|54|480.0|3520|NVIDIA P100 \* 8|16GB \* 8|25.0|400|14|8|20|

**说明：**

-   gn5优惠活动详情请参见[异构计算GPU实例活动页](https://promotion.aliyun.com/ntms/act/gpufreetier.html)。
-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。

## GPU计算型实例规格族gn5i

gn5i的特点如下：

-   计算：
    -   采用NVIDIA P4 GPU计算卡
    -   处理器与内存配比为1:4
    -   处理器：2.5 GHz主频的Intel ® Xeon ® E5-2682 v4（Broadwell）
-   存储：
    -   I/O优化实例
    -   仅支持SSD云盘和高效云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   深度学习推理
    -   多媒体编解码等服务器端GPU计算工作负载

gn5i包括的实例规格及指标数据如下：

|实例规格|vCPU|内存（GiB）|GPU|GPU显存|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:--|:----|:-----------|:----------|:--|:---|-------|
|ecs.gn5i-c2g1.large|2|8.0|NVIDIA P4 \* 1|8GB \* 1|1.0|10|2|2|6|
|ecs.gn5i-c4g1.xlarge|4|16.0|NVIDIA P4 \* 1|8GB \* 1|1.5|20|2|3|10|
|ecs.gn5i-c8g1.2xlarge|8|32.0|NVIDIA P4 \* 1|8GB \* 1|2.0|40|4|4|10|
|ecs.gn5i-c16g1.4xlarge|16|64.0|NVIDIA P4 \* 1|8GB \* 1|3.0|80|4|8|20|
|ecs.gn5i-c16g1.8xlarge|32|128.0|NVIDIA P4 \* 2|8GB \* 2|6.0|120|8|8|20|
|ecs.gn5i-c28g1.14xlarge|56|224.0|NVIDIA P4 \* 2|8GB \* 2|10.0|200|14|8|20|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。

