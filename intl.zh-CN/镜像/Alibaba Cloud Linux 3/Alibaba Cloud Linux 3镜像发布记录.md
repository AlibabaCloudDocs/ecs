# Alibaba Cloud Linux 3镜像发布记录

本文以发布时间为顺序，介绍Alibaba Cloud Linux 3镜像的特性更新动态。

## 背景信息

-   如无特殊声明，更新内容适用于云服务器ECS所有可用地域。
-   Alibaba Cloud Linux 3镜像适用于大多数实例规格族，但存在一部分镜像仅适用于部分实例规格族。更多信息，请参见[仅适用部分实例规格族的镜像发布记录](#section_gb2_fnv_vbn)。

## 镜像发布记录

|镜像ID|发布时间|发布内容|
|----|----|----|
|aliyun\_3\_x64\_20G\_alibase\_20210425.vhd|2021-04-25|-   更新`Alibaba Cloud Linux 3.2104 64位`基础镜像
-   内核更新：版本更新至5.10.23-5.al8.x86\_64 |
|aliyun\_3\_x64\_20G\_alibase\_20210415.vhd|2021-04-16|-   `Alibaba Cloud Linux 3.2104 64位`基础镜像发布上线
-   内核说明：
    -   基于Linux社区主线长期支持的5.10内核版本，初次采用的内核版本为5.10.23-4.al8.x86\_64
    -   ARM64架构支持PV-Panic、PV-Unhalt、PV-Preempt特性
    -   ARM64架构支持内核热补丁
    -   支持TCP-RT功能
    -   支持Memcg后台异步回收
    -   cgroup v1接口支持memcg QoS及PSI功能
    -   支持cgroup writeback功能
    -   增强Block IO限流监控统计能力
    -   优化ext4的JBD2的接口
    -   优化阿里巴巴开源内核并修复缺陷，包括调度器、内存、文件系统与块层等多个子系统
-   镜像说明：
    -   兼容CentOS 8、RHEL 8软件生态，修复软件包安全漏洞
    -   支持GCC 10.2.1、glibc 2.32
    -   支持Python 3.6、Python 2.7
    -   支持Appstream新机制
-   适用地域：华东1（杭州） |

## 仅适用部分实例规格族的镜像发布记录

|镜像ID|发布时间|适用实例规格族|发布内容|
|----|----|-------|----|
|aliyun\_3\_x64\_20G\_uefi\_alibase\_20210425.vhd|2021-04-25|-   ecs.c7
-   ecs.g7
-   ecs.r7
-   ecs.c7t
-   ecs.g7t
-   ecs.r7t

|-   新增`Alibaba Cloud Linux 3.2104 64位 UEFI版`镜像
-   该镜像基于`Alibaba Cloud Linux 3.2104 64位`基础镜像的aliyun\_3\_x64\_20G\_alibase\_20210425.vhd版本制作
-   启动切换为UEFI模式，而且仅支持该模式
-   适用地域：华北2（北京）、华东1（杭州）、华东2（上海）、华南1（深圳） |

