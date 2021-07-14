---
keyword: [发布更新, ecs, alibaba cloud linux]
---

# Alibaba Cloud Linux 2发布记录

本文以发布时间为顺序，介绍Alibaba Cloud Linux 2镜像的特性更新动态。

## 背景信息

-   如无特殊声明，更新内容适用于云服务器ECS所有可用地域。
-   Alibaba Cloud Linux 2镜像适用于大多数实例规格族，但存在一部分实例规格族不适用。这些实例规格族只能选用指定的公共镜像，详情请参见[仅适用部分实例规格族的镜像发布记录](#section_zai_t2o_j01)。

## 镜像发布记录

|镜像ID|发布时间|发布内容|
|----|----|----|
|aliyun\_2\_1903\_x64\_20G\_alibase\_20210630.vhd|2021-06-30|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像到最新的软件版本。
-   内核更新：
    -   版本更新至kernel-4.19.91-24.al7
    -   修复内核缺陷及重要安全漏洞
    -   支持x86 FSGSBASE特性
    -   支持AMD Milan架构
    -   支持RDMA NET Namespace特性
    -   支持ZSR特性
    -   支持CPU资源隔离Group Identity特性
    -   支持ARM64 MPAM特性
    -   支持Hisilicon、PHYTIUM、Zhaoxin架构
    -   在/proc/<pid\>/status以及/proc/<pid\>/smap中加入了进程的THP使能信息。
-   适用地域：华东1（杭州）、华北1（青岛）、华北2（北京）、西南1（成都）、中国（香港）、新加坡 |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20210325.vhd|2021-03-25|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像到最新的软件版本，兼容最新CentOS 7.9版本，修复软件包安全漏洞
-   修复CVE-2021-3156漏洞，即Linux sudo权限漏洞。更多信息，请参见[漏洞公告 \| Linux sudo权限漏洞（CVE-2021-3156）](/cn.zh-CN/动态与公告/安全公告/漏洞公告 | Linux sudo权限漏洞（CVE-2021-3156）.md)
-   默认的网络配置服务切换为network-scripts
-   增大net.ipv4.tcp\_max\_tw\_buckets参数值
-   在initramfs增加了NVME驱动
-   默认开启Kdump服务
-   内核更新：
    -   版本更新至kernel-4.19.91-23.al7
    -   修复内核缺陷及重要安全漏洞
    -   支持Intel SGX
    -   支持网络诊断工具Ping Trace
    -   支持在单机多实例的场景下轻量级创建cgroup，有效减少cgroup的创建时间
    -   支持Intel IceLake MCA |
|aliyun\_2\_1903\_x64\_20G\_qboot\_alibase\_20210325.vhd|2021-03-25|-   更新`Alibaba Cloud Linux 2.1903 64位 快速启动版`镜像
-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20210325.vhd版本制作
-   适用地域：华东1（杭州）、华北2（北京）、华北3（张家口）、华南1（深圳）、中国（香港）、新加坡、马来西亚（吉隆坡）、美国（弗吉尼亚） |
|aliyun\_2\_1903\_x64\_20G\_dengbao\_alibase\_20210325.vhd|2021-03-25|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位 等保2.0三级版`镜像
-   该镜像是根据*GB/T22239-2019信息安全技术网络安全等级保护基本要求*进行等保加固的镜像，您使用本镜像无需额外配置即可满足以下等保合规要求：

    -   身份鉴别
    -   访问控制
    -   安全审计
    -   入侵防范
    -   恶意代码防范
更多信息，请参见[Alibaba Cloud Linux等保2.0三级版镜像使用说明](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux等保2.0三级版镜像/Alibaba Cloud Linux等保2.0三级版镜像使用说明.md)

-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20210325.vhd版本制作
-   内核版本：kernel-4.19.91-23.al7
-   适用地域：华东1（杭州）、华东2（上海）、华北1（青岛）、华北2（北京）、华北3（张家口）、华北5（呼和浩特）、华北6（乌兰察布）、华南1（深圳）、华南2（河源）、华南3（广州）、西南1（成都）、中国（香港） |
|aliyun\_2\_1903\_x64\_20G\_qboot\_alibase\_20210218.vhd|2021-02-18|-   更新`Alibaba Cloud Linux 2.1903 64位 快速启动版`镜像
-   默认的网络配置服务切换为network-scripts
-   修复CVE-2021-3156漏洞，即Linux sudo权限漏洞。更多信息，请参见[漏洞公告 \| Linux sudo权限漏洞（CVE-2021-3156）](/cn.zh-CN/动态与公告/安全公告/漏洞公告 | Linux sudo权限漏洞（CVE-2021-3156）.md)
-   适用地域：华东1（杭州）、华南1（深圳）、华北2（北京）、华北3（张家口）、中国（香港）、新加坡、马来西亚（吉隆坡）、美国（弗吉尼亚） |
|aliyun\_2\_1903\_x64\_20G\_dengbao\_alibase\_20210218.vhd|2021-02-18|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位 等保2.0三级版`镜像
-   该镜像是根据*GB/T22239-2019信息安全技术网络安全等级保护基本要求*进行等保加固的镜像，您使用本镜像无需额外配置即可满足以下等保合规要求：

    -   身份鉴别
    -   访问控制
    -   安全审计
    -   入侵防范
    -   恶意代码防范
更多信息，请参见[Alibaba Cloud Linux等保2.0三级版镜像使用说明](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux等保2.0三级版镜像/Alibaba Cloud Linux等保2.0三级版镜像使用说明.md)

-   默认的网络配置服务切换为network-scripts
-   修复CVE-2021-3156漏洞，即Linux sudo权限漏洞。更多信息，请参见[漏洞公告 \| Linux sudo权限漏洞（CVE-2021-3156）](/cn.zh-CN/动态与公告/安全公告/漏洞公告 | Linux sudo权限漏洞（CVE-2021-3156）.md)
-   内核版本：kernel-4.19.91-22.2.al7
-   适用地域：华东1（杭州）、华东2（上海）、华北1（青岛）、华北2（北京）、华北3（张家口）、华北5（呼和浩特）、华北6（乌兰察布）、华南1（深圳）、华南2（河源）、华南3（广州）、西南1（成都）、中国（香港） |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20210120.vhd|2021-01-20|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像到最新的软件版本，兼容最新CentOS 7.9版本，修复软件包安全漏洞
-   新增并默认开启update-motd服务
-   默认开启rhel-loadmodules服务
-   增加vring\_force\_dma\_api启动参数
-   内核更新：
    -   版本更新至kernel-4.19.91-22.2.al7
    -   修复内核缺陷及重要安全漏洞
    -   同步社区最新的ext4文件系统，增强稳定性
    -   默认开启RAID支持
    -   增加Dragonfly Enclaves特性支持
    -   增加Intel IceLake PMU Topdown性能调试支持
    -   优化增强IO\_Uring Buffer读能力
    -   优化增强blk-throttle
    -   增加SM2国密算法支持以及SM2-with-SM3的标准X509格式证书支持
    -   增加blk-mq batch request支持
    -   增加PCIe Error recover特性支持
    -   优化Swap，大大提升内存超卖稳定性
    -   增加Alibaba Cloud Linux容器增强技术支持 |
|aliyun\_2\_1903\_x64\_20G\_qboot\_alibase\_20210120.vhd|2021-01-20|-   更新`Alibaba Cloud Linux 2.1903 64位 快速启动版`镜像
-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20210120.vhd版本制作
-   适用地域：华东1（杭州）、华南1（深圳）、华北2（北京）、华北3（张家口）、中国（香港）、新加坡、马来西亚（吉隆坡）、美国（弗吉尼亚） |
|aliyun\_2\_1903\_x64\_20G\_dengbao\_alibase\_20210120.vhd|2021-01-20|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位 等保2.0三级版`镜像
-   该镜像是根据*GB/T22239-2019信息安全技术网络安全等级保护基本要求*进行等保加固的镜像，您使用本镜像无需额外配置即可满足以下等保合规要求：

    -   身份鉴别
    -   访问控制
    -   安全审计
    -   入侵防范
    -   恶意代码防范
更多信息，请参见[Alibaba Cloud Linux等保2.0三级版镜像使用说明](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux等保2.0三级版镜像/Alibaba Cloud Linux等保2.0三级版镜像使用说明.md)

-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20210120.vhd版本制作
-   内核版本：kernel-4.19.91-22.2.al7
-   适用地域：华东1（杭州）、华东2（上海）、华北1（青岛）、华北2（北京）、华北3（张家口）、华北5（呼和浩特）、华北6（乌兰察布）、华南1（深圳）、华南2（河源）、华南3（广州）、西南1（成都）、中国（香港） |
|aliyun\_2\_1903\_x64\_20G\_dengbao\_alibase\_20200925.vhd|2020-09-25|-   新增`Alibaba Cloud Linux 2.1903 LTS 64位 等保2.0三级版`镜像
-   该镜像是根据*GB/T22239-2019信息安全技术网络安全等级保护基本要求*进行等保加固的镜像，您使用本镜像无需额外配置即可满足以下等保合规要求：

    -   身份鉴别
    -   访问控制
    -   安全审计
    -   入侵防范
    -   恶意代码防范
详情请参见[Alibaba Cloud Linux等保2.0三级版镜像使用说明](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux等保2.0三级版镜像/Alibaba Cloud Linux等保2.0三级版镜像使用说明.md)

-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd版本制作
-   内核版本：kernel-4.19.91-21.al7
-   适用地域：华东1（杭州）、华东2（上海）、华北1（青岛）、华北2（北京）、华北3（张家口）、华北5（呼和浩特）、华北6（乌兰察布）、华南1（深圳）、华南2（河源）、华南3（广州）、西南1（成都）、中国（香港） |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd|2020-09-04|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像到最新的软件版本，兼容最新CentOS 7.8版本，修复软件包安全漏洞
-   /etc/redhat-release的信息从Aliyun Linux release 7.2 LTS \(Hunting Beagle\)变更成Alibaba Cloud Linux \(Aliyun Linux\) release 2.1903 LTS \(Hunting Beagle\)
-   优化/etc/image-id标识镜像类型
-   默认开启tuned服务
-   内核更新：
    -   版本更新至kernel-4.19.91-21.al7
    -   修复内核重要缺陷及安全漏洞
    -   修复IO\_Uring缺陷及功能增加
    -   增加THP fork优化，提升大内存进程创建速度
    -   增加AEP设备安全操作支持
    -   增加阿里巴巴自研特性TCP-RT支持
    -   增加virtio-mem特性支持
    -   增强Intel® IceLake处理器电源管理、PCIe Gen4、RAS等功能
    -   增加Intel® Speed Select Technology技术支持 |
|aliyun\_2\_1903\_x64\_20G\_qboot\_alibase\_20200904.vhd|2020-09-04|-   更新`Alibaba Cloud Linux 2.1903 64位 快速启动版`镜像
-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd版本制作
-   适用地域：华东1（杭州）、华南1（深圳）、华北3（张家口）、中国（香港） |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200529.vhd|2020-05-29|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像到最新的软件版本，兼容最新CentOS 7.8版本，修复软件包安全漏洞
-   增加/etc/image-id标识
-   默认关闭tuned服务
-   内核更新：
    -   版本更新至kernel-4.19.91-19.1.al7
    -   开源阿里云内核对调度、内存QoS指标统计内核接口支持，提供调度、内存相关SLI细粒度监控能力
    -   开源阿里云内核memcg OOM（Out-Of-Memory）优先级控制接口支持，增强系统OOM时重要进程保护措施
    -   增加AMD QoS支持
    -   增加virtio pmem驱动支持
    -   增加free page reporting特性支持，增强Hypervisor对Guest OS空闲内存感知能力，高效管理利用物理内存资源
    -   优化Memory compaction，有效缓解内存碎片化，提升系统内存使用效率
    -   修复内核重要缺陷及安全漏洞 |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200324.vhd|2020-03-24|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像到最新的软件版本，兼容最新CentOS 7.8版本，修复软件包安全漏洞
-   新增支持通过yum获取安全漏洞（CVE）更新
-   正式发布Alibaba Cloud Linux 2的LTS版本，并更新/etc/alinux-release为Aliyun Linux release 2.1903 LTS \(Hunting Beagle\)
-   默认开启tuned服务
-   内核更新：
    -   版本更新至kernel-4.19.91-18.al7
    -   增加NVMe设备支持
    -   默认开启THP以提升应用性能
    -   增加IO\_Uring技术
    -   开启Intel\_idle及guest halt polling，以提升guest CPU效能
    -   开启ftrace syscalls以增强bpftrace工具的能力
    -   开源了多个阿里云内部内核优化和缺陷修复，包含调度器、内存、文件系统与块层等多个子系统
    -   修复内核安全漏洞 |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200221.vhd|2020-02-21|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像到最新的软件版本，兼容最新CentOS 7.8版本，修复软件包安全漏洞
-   默认开启IPv6支持
-   内核更新：
    -   版本更新至kernel-4.19.81-17.1.al7
    -   支持Intel Cooper Lake CPU和Ice Lake CPU
    -   完善对AMD CPU和ARM64 CPU架构的支持
    -   支持持久化内存（presistent memory）
    -   支持IO Cost（基于IO消耗模型、按比例分配的blkio cgroup controller），详情请参见[blk-iocost权重限速](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/blk-iocost权重限速.md)
    -   支持基于cgroup v1接口的PSI（pressure stall information）功能，详情请参见[在cgroup v1接口开启PSI功能](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/在cgroup v1接口开启PSI功能.md)
    -   开源了多个阿里云内部内核优化和缺陷修复，包含调度器、内存、文件系统与块层等多个子系统
    -   修复内核安全漏洞 |
|aliyun\_2\_1903\_x64\_20G\_alibase\_20200114.qboot.vhd|2020-01-14|-   新增`Alibaba Cloud Linux 2.1903 64位 快速启动版`镜像
-   内核更新：
    -   版本更新至4.19.81-17.al7.x86\_64
    -   支持qboot快速启动
-   适用地域：华北2（北京）、华东1（杭州）、中国（香港） |
|aliyun\_2\_1903\_64\_20G\_alibase\_20190829.vhd|2019-08-29|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像到最新的软件版本
-   内核更新：
    -   版本更新至kernel-4.19.57-15.1.al7.x86\_64
    -   修复Spectre-V1 SWAPGS问题
    -   修复DM bio splitting问题
    -   修改TCP拥塞控制默认算法为CUBIC
    -   网络配置统一为10-eth0.network |
|aliyun\_2\_1903\_64\_20G\_alibase\_20190619.vhd|2019-06-19|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像到最新的软件版本
-   内核更新：
    -   版本更新至kernel-4.19.43-13.2.al7.x86\_64
    -   支持基于cgroup v1版本接口的cgroup writeback特性
    -   支持策略路由
    -   开启INET\_DIAG内核配置项，以支持iproute2套件的ss命令
    -   支持可配置的内核接口net.ipv4.tcp\_tw\_timeout
    -   修复了以下网络相关缺陷（CVE）：
        -   CVE-2019-11477
        -   CVE-2019-11478
        -   CVE-2019-11479 |
|aliyun-2.1903-x64-20G-alibase-20190507.vhd|2019-05-07|-   更新`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像到最新的软件版本
-   修复启动ECS实例后时间同步延迟的问题
-   内核版本更新至kernel-4.19.34-11.al7.x86\_64，更新系统内核，修复若干问题 |
|aliyun-2.1903-x64-20G-alibase-20190327.vhd|2019-03-27|-   `Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像发布上线
-   初次采用的内核版本为kernel-4.19.24-9.al7.x86\_64 |

## 仅适用部分实例规格族的镜像发布记录

|镜像ID|发布时间|适用实例规格族|发布内容|
|----|----|-------|----|
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20210325.vhd|2021-03-25|可信实例规格族：-   ecs.g6t
-   ecs.c6t

|-   更新`Alibaba Cloud Linux 2.1903 64位 可信版`镜像
-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20210325.vhd版本制作
-   启动切换为UEFI模式，而且仅支持该模式
-   内核更新：版本更新至kernel-4.19.91-23.al7 |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20210325.vhd|2021-03-25|适用以下实例规格族：-   ecs.g7
-   ecs.c7
-   ecs.r7
-   ecs.g7t
-   ecs.c7t
-   ecs.r7t

|-   更新`Alibaba Cloud Linux 2.1903 64位 UEFI版`镜像
-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20210325.vhd版本制作
-   启动切换为UEFI模式，而且仅支持该模式
-   适用地域：华北2（北京）、华东1（杭州）、华东2（上海）、华南1（深圳） |
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20210218.vhd|2021-02-18|可信实例规格族：-   ecs.g6t
-   ecs.c6t

|-   更新`Alibaba Cloud Linux 2.1903 64位 可信版`镜像
-   默认的网络配置服务切换为network-scripts
-   修复CVE-2021-3156漏洞，即Linux sudo权限漏洞。更多信息，请参见[漏洞公告 \| Linux sudo权限漏洞（CVE-2021-3156）](/cn.zh-CN/动态与公告/安全公告/漏洞公告 | Linux sudo权限漏洞（CVE-2021-3156）.md)
-   启动切换为UEFI模式，而且仅支持该模式
-   内核更新：版本更新至kernel-4.19.91-22.2.al7 |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20210218.vhd|2021-02-18|AMD实例规格族：-   ecs.ebmg6a
-   ecs.ebmc6a
-   ecs.ebmr6a
-   ecs.ebmg6a-htoff
-   ecs.ebmc6a-htoff
-   ecs.ebmr6a-htoff

|-   更新`Alibaba Cloud Linux 2.1903 64位 AMD版`镜像到最新的软件版本
-   默认的网络配置服务切换为network-scripts
-   修复CVE-2021-3156漏洞，即Linux sudo权限漏洞。更多信息，请参见[漏洞公告 \| Linux sudo权限漏洞（CVE-2021-3156）](/cn.zh-CN/动态与公告/安全公告/漏洞公告 | Linux sudo权限漏洞（CVE-2021-3156）.md)
-   启动切换为UEFI模式，而且仅支持该模式 |
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20210120.vhd|2021-01-20|可信实例规格族：-   ecs.g6t
-   ecs.c6t

|-   更新`Alibaba Cloud Linux 2.1903 64位 可信版`镜像
-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20210120.vhd版本制作
-   启动切换为UEFI模式，而且仅支持该模式
-   内核更新：版本更新至kernel-4.19.91-22.2.al7 |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20210120.vhd|2021-01-20|AMD实例规格族：-   ecs.ebmg6a
-   ecs.ebmc6a
-   ecs.ebmr6a
-   ecs.ebmg6a-htoff
-   ecs.ebmc6a-htoff
-   ecs.ebmr6a-htoff

|-   更新`Alibaba Cloud Linux 2.1903 64位 AMD版`镜像到最新的软件版本
-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20210120.vhd版本制作
-   启动切换为UEFI模式，而且仅支持该模式 |
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20200904.vhd|2020-09-04|可信实例规格族：-   ecs.g6t
-   ecs.c6t

|-   更新`Alibaba Cloud Linux 2.1903 64位 可信版`镜像到最新的软件版本
-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd版本制作
-   启动切换为UEFI模式，而且仅支持该模式
-   增加可信功能 |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20200904.vhd|2020-09-04|AMD实例规格族：-   ecs.ebmg6a
-   ecs.ebmc6a
-   ecs.ebmr6a
-   ecs.ebmg6a-htoff
-   ecs.ebmc6a-htoff
-   ecs.ebmr6a-htoff

|-   更新`Alibaba Cloud Linux 2.1903 64位 AMD版`镜像到最新的软件版本
-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20200904.vhd版本制作
-   启动切换为UEFI模式，而且仅支持该模式 |
|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20200622.vhd|2020-06-22|可信实例规格族：-   ecs.g6t
-   ecs.c6t

|-   新增`Alibaba Cloud Linux 2.1903 64位 可信版`镜像
-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20200529.vhd版本制作
-   启动切换为UEFI模式，而且仅支持该模式
-   增加可信功能
-   内核更新：
    -   版本更新至kernel-4.19.91-19.2.al7
    -   增加AMD IOMMU支持 |
|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20200616.vhd|2020-06-16|AMD实例规格族：-   ecs.ebmg6a
-   ecs.ebmc6a
-   ecs.ebmr6a
-   ecs.ebmg6a-htoff
-   ecs.ebmc6a-htoff
-   ecs.ebmr6a-htoff

|-   新增`Alibaba Cloud Linux 2.1903 64位 AMD版`镜像
-   该镜像基于`Alibaba Cloud Linux 2.1903 LTS 64位`基础镜像的aliyun\_2\_1903\_x64\_20G\_alibase\_20200529.vhd版本制作
-   启动切换为UEFI模式，而且仅支持该模式
-   内核更新：
    -   版本更新至kernel-4.19.91-19.2.al7
    -   增加AMD IOMMU支持 |

