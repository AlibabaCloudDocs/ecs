---
keyword: [阿里云, ecs, 服务器, 弹性计算]
---

# 本地SSD型

本文介绍云服务器ECS本地SSD型实例规格族的特点，并列出了具体的实例规格。

-   推荐
    -   [本地SSD型实例规格族i3g](#section_o4u_ofu_2f5)
    -   [本地SSD型实例规格族i3](#section_ogb_jlc_y4v)
    -   [本地SSD型实例规格族i2](#section_y55_6f0_568)
    -   [本地SSD型实例规格族i2g](#section_0xx_a83_xv8)
    -   [本地SSD型实例规格族i2ne](#section_yum_us8_tq0)
    -   [本地SSD型实例规格族i2gne](#section_lze_1l0_mtl)
-   其他在售（如果售罄，建议使用推荐规格族）

    [本地SSD型实例规格族i1](#section_buh_5lq_frq)


## 本地SSD型实例规格族介绍

本地SSD型实例属于高I/O型本地盘存储实例，适用于对存储I/O性能有极高要求，同时具备应用层高可用架构的业务场景，例如NoSQL非关系型数据库、MPP数据仓库、分布式文件系统等。

本地SSD型实例适合网络游戏、电商、视频直播、媒体等提供在线业务的行业客户，满足I/O密集型应用对块存储的低时延和高I/O性能需求。

本地SSD型实例具有以下特点：

-   在大型数据库业务场景下，具备每秒数万至数十万次低时延随机IOPS读写能力。
-   在大数据、并行计算等大型数据集业务场景下，具备高达数GiB的顺序读写吞吐能力。
-   基于本地NVMe SSD磁盘资源，在提供高达数十万随机I/O读写能力的同时，时延水平保持在μs级别。

使用本地SSD型实例时请注意：

-   不支持变配和宕机迁移。
-   本地盘与特定规格的实例相绑定，本地盘的数量和容量由您选择的实例规格决定。不支持单独购买本地盘，不支持将本地盘卸载并挂载到另一台实例上使用。
-   本地盘不支持快照功能。如果您需要为本地盘实例创建包含系统盘和数据盘的镜像，建议通过组合系统盘快照和数据盘（仅限云盘）快照的方式来创建。
-   不支持基于实例ID创建包含系统盘和数据盘的镜像。
-   支持挂载SSD云盘，挂载的云盘支持扩容。
-   本地盘来自单台物理机，数据可靠性取决于物理机的可靠性，存在单点故障风险。

    **警告：** 使用本地盘存储数据有丢失数据的风险，例如ECS实例所在物理机发生硬件故障时。请勿在本地盘上存储需要长期保存的业务数据。

    -   建议您在应用层做数据冗余，保证数据的可用性。您可以使用部署集将业务涉及到的几台ECS实例分散部署在不同的物理服务器上，保证业务的高可用性和底层容灾能力。具体操作，请参见[创建部署集](/cn.zh-CN/部署与弹性/部署集/创建部署集.md)。
    -   如果您的应用无数据可靠性架构设计，强烈建议您在ECS实例中同时使用云盘或者备份服务，提高数据可靠性。更多信息，请参见[云盘概述](/cn.zh-CN/块存储/块存储介绍/云盘概述.md)或[什么是混合云备份](/cn.zh-CN/产品简介/什么是混合云备份.md)。
-   操作本地盘实例可能对本地盘数据产生影响，详情请参见[实例操作对本地盘数据的影响](/cn.zh-CN/块存储/块存储介绍/本地盘.md)。

## 本地SSD型实例规格族i3g

本实例规格族正在邀测中，如需使用，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。

i3g的特点如下：

-   配备高性能（高IOPS、大吞吐、低访问延迟）NVMe SSD本地盘
-   计算：
    -   处理器与内存配比为1:4，为高性能数据库等场景设计
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8269CY（Cascade Lake ），睿频3.2 GHz，计算性能稳定
-   存储：
    -   I/O优化实例
    -   仅支持ESSD云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   OLTP、高性能关系型数据库
    -   NoSQL数据库（例如Cassandra、MongoDB、HBase等）
    -   Elasticsearch等搜索场景

i3g包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|本地存储（GiB）|网络基础带宽（Gbit/s）|网络突发带宽（Gbit/s）|网络收发包PPS（万）|连接数（万）|多队列|弹性网卡|单网卡私有IP|云盘IOPS（万）|云盘带宽（Gbit/s）|
|:---|:---|:------|:--------|:-------------|--------------|:----------|------|:--|:---|-------|---------|------------|
|ecs.i3g.2xlarge|8|32.0|1 \* 447|3.0|10|175|25|8|4|15|5.25|2.0|
|ecs.i3g.4xlarge|16|64.0|1 \* 894|5.0|10|350|30|8|8|15|8.40|3.0|
|ecs.i3g.8xlarge|32|128.0|2 \* 894|12.0|无|700|60|8|8|30|15.75|5.0|
|ecs.i3g.13xlarge|52|192.0|3 \* 894|16.0|无|1200|90|16|8|30|25.20|8.0|
|ecs.i3g.26xlarge|104|384.0|6 \* 894|32.0|无|2400|180|32|15|30|50.00|16.0|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。
-   SSD本地盘的性能请参见[本地盘](/cn.zh-CN/块存储/块存储介绍/本地盘.md)。

## 本地SSD型实例规格族i3

该实例规格族正在公测中。

i3的特点如下：

-   配备高性能（高IOPS、大吞吐、低访问延迟）NVMe SSD本地盘，并支持在线隔离坏盘
-   计算：
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8269CY（Cascade Lake ），睿频3.2 GHz，计算性能稳定
-   存储：
    -   I/O优化实例
    -   仅支持ESSD云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   OLTP、高性能关系型数据库
    -   NoSQL数据库（例如Cassandra、MongoDB等）
    -   Elasticsearch等搜索场景

i3包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|本地存储（GiB）|网络基础带宽（Gbit/s）|网络突发带宽（Gbit/s）|网络收发包PPS（万）|连接数（万）|多队列|弹性网卡|单网卡私有IP|云盘IOPS（万）|云盘带宽（Gbit/s）|
|:---|:---|:------|:--------|:-------------|--------------|:----------|------|:--|:---|-------|---------|------------|
|ecs.i3.xlarge|4|32.0|1 \* 894|1.5|10|100|25|4|4|15|4|1.5|
|ecs.i3.2xlarge|8|64.0|1 \* 1788|2.5|10|160|25|8|4|15|5|2.0|
|ecs.i3.4xlarge|16|128.0|2 \* 1788|5.0|10|300|30|8|8|30|8|3.0|
|ecs.i3.8xlarge|32|256.0|4 \* 1788|10.0|无|600|60|16|8|30|15|5.0|
|ecs.i3.13xlarge|52|384.0|6 \* 1788|16.0|无|900|90|32|7|30|24|8.0|
|ecs.i3.26xlarge|104|768.0|12 \* 1788|32.0|无|2400|180|32|15|30|48|16.0|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。
-   SSD本地盘的性能请参见[本地盘](/cn.zh-CN/块存储/块存储介绍/本地盘.md)。

## 本地SSD型实例规格族i2

i2的特点如下：

-   配备高性能（高IOPS、大吞吐、低访问延迟）NVMe SSD本地盘
-   计算：
    -   处理器与内存配比为1:8，为高性能数据库等场景设计
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8163（Skylake）
-   存储：
    -   I/O优化实例
    -   仅支持SSD云盘和高效云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   OLTP、高性能关系型数据库
    -   NoSQL数据库（如Cassandra、MongoDB、HBase等）
    -   Elasticsearch等搜索场景

i2包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|本地存储（GiB）|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|云盘带宽（Gbit/s）|
|:---|:---|:------|:--------|:-----------|:----------|:--|:---|-------|------------|
|ecs.i2.xlarge|4|32.0|1 \* 894|1.0|50|2|3|10|最高16|
|ecs.i2.2xlarge|8|64.0|1 \* 1788|2.0|100|2|4|10|最高16|
|ecs.i2.4xlarge|16|128.0|2 \* 1788|3.0|150|4|8|20|最高16|
|ecs.i2.8xlarge|32|256.0|4 \* 1788|6.0|200|8|8|20|最高16|
|ecs.i2.16xlarge|64|512.0|8 \* 1788|10.0|400|16|8|20|最高16|
|ecs.i2d.21xlarge|84|712.0|4 \* 3570|25.0|400|32|16|20|最高16|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。
-   SSD本地盘的性能请参见[本地盘](/cn.zh-CN/块存储/块存储介绍/本地盘.md)。

## 本地SSD型实例规格族i2g

i2g的特点如下：

-   配备高性能（高IOPS、大吞吐、低访问延迟）NVMe SSD本地盘
-   计算：
    -   处理器与内存配比为1:4，为高性能数据库等场景设计
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8163（Skylake）
-   存储：
    -   I/O优化实例
    -   仅支持SSD云盘和高效云盘
-   网络：
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   OLTP、高性能关系型数据库
    -   NoSQL数据库（例如Cassandra、MongoDB、HBase等）
    -   Elasticsearch等搜索场景

i2g包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|本地存储（GiB）|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:--------|:-----------|:----------|:--|:---|-------|
|ecs.i2g.2xlarge|8|32.0|1 \* 894|2.0|100|2|4|10|
|ecs.i2g.4xlarge|16|64.0|1 \* 1788|3.0|150|4|8|20|
|ecs.i2g.8xlarge|32|128.0|2 \* 1788|6.0|200|8|8|20|
|ecs.i2g.16xlarge|64|256.0|4 \* 1788|10.0|400|16|8|20|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。
-   SSD本地盘的性能请参见[本地盘](/cn.zh-CN/块存储/块存储介绍/本地盘.md)。

## 本地SSD型实例规格族i2ne

i2ne的特点如下：

-   配备高性能（高IOPS、大吞吐、低访问延迟）NVMe SSD本地盘
-   计算：
    -   处理器与内存配比为1:8，为高性能数据库等场景设计
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8163（Skylake）
-   存储：
    -   I/O优化实例
    -   仅支持SSD云盘和高效云盘
-   网络：
    -   支持IPv6
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
    -   实例网络带宽最高可达20 Gbit/s
-   适用场景：
    -   OLTP、高性能关系型数据库
    -   NoSQL数据库（如Cassandra、MongoDB、HBase等）
    -   Elasticsearch等搜索场景

i2ne包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|本地存储（GiB）|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|云盘带宽（Gbit/s）|
|:---|:---|:------|:--------|:-----------|:----------|:--|:---|-------|------------|
|ecs.i2ne.xlarge|4|32.0|1 \* 894|1.5|50|2|3|10|最高16|
|ecs.i2ne.2xlarge|8|64.0|1 \* 1788|2.5|100|2|4|10|最高16|
|ecs.i2ne.4xlarge|16|128.0|2 \* 1788|5.0|150|4|8|20|最高16|
|ecs.i2ne.8xlarge|32|256.0|4 \* 1788|10.0|200|8|8|20|最高16|
|ecs.i2ne.16xlarge|64|512.0|8 \* 1788|20.0|400|16|8|20|最高16|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。
-   SSD本地盘的性能请参见[本地盘](/cn.zh-CN/块存储/块存储介绍/本地盘.md)。

## 本地SSD型实例规格族i2gne

i2gne的特点如下：

-   配备高性能（高IOPS、大吞吐、低访问延迟）NVMe SSD本地盘
-   计算：
    -   处理器与内存配比为1:4，为高性能数据库等场景设计
    -   处理器：2.5 GHz主频的Intel ® Xeon ® Platinum 8163（Skylake）
-   存储：
    -   I/O优化实例
    -   仅支持SSD云盘和高效云盘
-   网络：
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
    -   实例网络带宽最高可达20 Gbit/s
-   适用场景：
    -   OLTP、高性能关系型数据库
    -   NoSQL数据库（例如Cassandra、MongoDB、HBase等）
    -   Elasticsearch等搜索场景

i2gne包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|本地存储（GiB）|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:--------|:-----------|:----------|:--|:---|-------|
|ecs.i2gne.2xlarge|8|32.0|1 \* 894|2.5|100|2|4|10|
|ecs.i2gne.4xlarge|16|64.0|1 \* 1788|5.0|150|4|8|20|
|ecs.i2gne.8xlarge|32|128.0|2 \* 1788|10.0|200|8|8|20|
|ecs.i2gne.16xlarge|64|256.0|4 \* 1788|20.0|400|16|8|20|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。
-   SSD本地盘的性能请参见[本地盘](/cn.zh-CN/块存储/块存储介绍/本地盘.md)。

## 本地SSD型实例规格族i1

i1的特点如下：

-   配备高性能（高IOPS、大吞吐、低访问延迟）NVMe SSD本地盘
-   计算：
    -   处理器与内存配比为1:4，为高性能数据库等场景设计
    -   处理器：2.5 GHz主频的Intel ® Xeon ® E5-2682 v4（Broadwell）
-   存储：
    -   I/O优化实例
    -   仅支持SSD云盘和高效云盘
-   网络：
    -   实例网络性能与计算规格对应（规格越高网络性能越强）
-   适用场景：
    -   OLTP、高性能关系型数据库
    -   NoSQL数据库（例如Cassandra、MongoDB等）
    -   Elasticsearch等搜索场景

i1包括的实例规格及指标数据如下表所示。

|实例规格|vCPU|内存（GiB）|本地存储（GiB）|网络带宽（Gbit/s）|网络收发包PPS（万）|多队列|弹性网卡|单网卡私有IP|
|:---|:---|:------|:--------|:-----------|:----------|:--|:---|-------|
|ecs.i1.xlarge|4|16.0|2 \* 104|0.8|20|1|3|10|
|ecs.i1.2xlarge|8|32.0|2 \* 208|1.5|40|1|4|10|
|ecs.i1.3xlarge|12|48.0|2 \* 312|2.0|40|1|6|10|
|ecs.i1.4xlarge|16|64.0|2 \* 416|3.0|50|2|8|20|
|ecs.i1-c5d1.4xlarge|16|64.0|2 \* 1456|3.0|40|2|8|20|
|ecs.i1.6xlarge|24|96.0|2 \* 624|4.5|60|2|8|20|
|ecs.i1.8xlarge|32|128.0|2 \* 832|6.0|80|3|8|20|
|ecs.i1-c10d1.8xlarge|32|128.0|2 \* 1456|6.0|80|3|8|20|
|ecs.i1.14xlarge|56|224.0|2 \* 1456|10.0|120|4|8|20|

**说明：**

-   您可以前往[ECS实例可购买地域](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看实例在各地域的可购情况。
-   指标的含义请参见[实例规格指标说明](/cn.zh-CN/实例/实例规格族.md)。
-   SSD本地盘的性能请参见[本地盘](/cn.zh-CN/块存储/块存储介绍/本地盘.md)。

