---
keyword: [阿里云, ecs, 服务器, 弹性计算]
---

# FPGA实例概述

本文介绍云服务器ECS FPGA计算型实例规格族的特点，并列出了具体的实例规格。

-   推荐

    [FPGA计算型实例规格族f3](#section_9xy_ea1_wz9)

-   其他在售（如果售罄，建议使用推荐规格族）

    [FPGA计算型实例规格族f1](#section_3f4_xet_8t8)


## FPGA计算型实例规格族f3

f3的特点如下：

-   采用Xilinx 16nm Virtex UltraScale+器件VU9P
-   计算：
    -   处理器与内存配比为 1:4
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8163（Skylake）
-   存储：
    -   I/O优化实例
    -   仅支持SSD云盘和高效云盘
-   网络：
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   深度学习推理
    -   基因组学研究
    -   数据库加速
    -   图片转码，例如JPEG转WebP
    -   实时视频处理，例如H.265视频压缩

f3包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|FPGA|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:---|:-----------|:----------|:--|:---|-------|
|ecs.f3-c4f1.xlarge|4|16.0|1 \* Xilinx VU9P|1.5|30|2|3|10|
|ecs.f3-c8f1.2xlarge|8|32.0|1 \* Xilinx VU9P|2.5|50|4|4|10|
|ecs.f3-c16f1.4xlarge|16|64.0|1 \* Xilinx VU9P|5.0|100|4|8|20|
|ecs.f3-c16f1.8xlarge|32|128.0|2 \* Xilinx VU9P|10.0|200|8|8|20|
|ecs.f3-c16f1.16xlarge|64|256.0|4 \* Xilinx VU9P|20.0|250|16|8|20|
|ecs.f3-c22f1.22xlarge|88|336.0|4 \* Xilinx VU9P|30.0|450|16|8|20|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/intl.zh-CN/实例/实例规格族.md)。

## FPGA计算型实例规格族f1

f1的特点如下：

-   采用Intel ® ARRIA ® 10 GX 1150计算卡
-   计算：
    -   处理器：2.5 GHz主频的Intel ® Xeon ® E5-2682 v4（Broadwell）
    -   处理器与内存配比为 1:7.5
-   存储：
    -   I/O优化实例
    -   仅支持SSD云盘和高效云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   深度学习推理
    -   基因组学研究
    -   金融分析
    -   图片转码
    -   实时视频处理及安全等计算工作负载

f1包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|FPGA|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:---|:-----------|:----------|:--|:---|-------|
|ecs.f1-c8f1.2xlarge|8|60.0|Intel ARRIA 10 GX 1150|3.0|40|4|4|10|
|ecs.f1-c8f1.4xlarge|16|120.0|2 \* Intel ARRIA 10 GX 1150|5.0|100|4|8|20|
|ecs.f1-c28f1.7xlarge|28|112.0|Intel ARRIA 10 GX 1150|5.0|200|8|8|20|
|ecs.f1-c28f1.14xlarge|56|224.0|2 \* Intel ARRIA 10 GX 1150|10.0|200|14|8|20|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/intl.zh-CN/实例/实例规格族.md)。

