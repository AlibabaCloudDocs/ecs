# Alibaba Cloud Linux 2功能和接口概述

本文汇总了Alibaba Cloud Linux 2已支持的功能和内核接口。

## Alibaba Cloud Linux 2镜像的使用

镜像相关的操作说明请参见下表。

|文档链接|说明|
|----|--|
|[在本地使用Alibaba Cloud Linux 2镜像](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/在本地使用Alibaba Cloud Linux 2镜像.md)|Alibaba Cloud Linux 2镜像支持下载至本地KVM虚拟机中使用。|
|[基于YUM的安全更新操作](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/基于YUM的安全更新操作.md)|您可以使用yum查询、检查以及安装Alibaba Cloud Linux 2操作系统的安全更新。|
|[开启或关闭IPv6](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/开启或关闭IPv6.md)|Alibaba Cloud Linux 2提供了暂时开启或关闭IPv6；持久开启或关闭IPv6两种操作方式。|
|[订阅Alibaba Cloud Linux 2安全漏洞（CVE）公告](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/订阅Alibaba Cloud Linux 2安全漏洞（CVE）公告.md)|软件包安全漏洞（CVE）修复在Alibaba Cloud Linux 2版本支持期限内会持续更新，您可以利用浏览器插件，订阅Alibaba Cloud Linux 2 CVE公告，方便快捷地查看CVE更新情况。|

## Alibaba Cloud Linux 2内核系统支持的功能接口

如果您对Linux的内核系统有一定的了解，并且有需求需要使用Linux内核功能，您可以依据下表提供的Alibaba Cloud Linux 2的内核功能与接口进行相关操作。

|文档链接|说明|
|----|--|
|[增强容器资源可见性](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/增强容器资源可见性.md)|Alibaba Cloud Linux 2在内核层面提供了容器资源视图功能的相关接口，实现对容器资源的可见性增强。|
|[启用cgroup writeback功能](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/启用cgroup writeback功能.md)|Alibaba Cloud Linux 2在内核版本4.19.36-12.al7中，对内核接口cgroup v1新增了控制群组回写（cgroup writeback）功能。该功能使您在使用内核接口cgroup v1时，可以对缓存异步I/O \(Buffered I/O\) 进行限速。|
|[blk-iocost权重限速](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/blk-iocost权重限速.md)|Alibaba Cloud Linux 2在内核版本4.19.81-17.al7.x86\_64开始支持基于成本模型（cost model）的权重限速功能，即blk-iocost功能。该功能是对内核中IO子系统（blkcg）基于权重的磁盘限速功能的进一步完善。|
|[在cgroup v1接口开启PSI功能](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/在cgroup v1接口开启PSI功能.md)|Alibaba Cloud Linux 2在内核版本4.19.81-17.al7中为cgroup v1接口提供了PSI功能。PSI（Pressure Stall Information）是一个可以监控CPU、内存及IO性能异常的内核功能。|
|[修改TCP TIME-WAIT超时时间](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/修改TCP TIME-WAIT超时时间.md)|在Linux的内核中，TCP/IP协议的TIME-WAIT状态持续60秒且无法修改。但在某些场景下，例如TCP负载过高时，适当调小该值有助于提升网络性能。因此Alibaba Cloud Linux 2在内核版本4.19.43-13.al7新增内核接口，用于修改TCP TIME-WAIT超时时间。|
|[Block IO限流增强监控接口](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/Block IO限流增强监控接口.md)|为了更方便地监控Linux block IO限流，Alibaba Cloud Linux 2在内核版本4.19.81-17.al7增加相关接口，用于增强block IO限流的监控统计能力。|
|[JBD2优化接口](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/JBD2优化接口.md)|JBD2作为ext4文件系统的内核线程，在使用过程中常会遇到影子状态（BH\_Shadow），影响系统性能。为解决使用JBD2过程中出现的异常，Alibaba Cloud Linux 2在内核版本4.19.81-17.al7对JBD2进行了优化。|
|[跨目录配额创建硬链接](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/跨目录配额创建硬链接.md)|默认情况下，ext4文件系统中存在约束，不允许跨目录配额创建硬链接。但在实际中，某些特定场景有创建硬链接的需求，因此Alibaba Cloud Linux 2提供定制接口，该接口能够绕过ext4文件系统中的约束，实现跨目录配额创建硬链接。|
|[追踪IO时延](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/追踪IO时延.md)|Alibaba Cloud Linux 2优化了IO时延分析工具iostat的原始数据来源/proc/diskstats接口，增加了对设备侧的读、写及特殊IO（discard）等耗时的统计，此外还提供了一个方便追踪IO时延的工具bcc。|
|[检测文件系统和块层的IO hang](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/检测文件系统和块层的IO hang.md)|IO hang是指在系统运行过程中，因某些IO耗时过长而引起的系统不稳定甚至宕机。为了准确检测出IO hang，Alibaba Cloud Linux 2扩展核心数据结构，增加了在较小的系统开销下，快速定位并检测IO hang的功能。|
|[Memcg全局最低水位线分级](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/Memcg全局最低水位线分级.md)|Alibaba Cloud Linux 2新增了memcg全局最低水位线分级功能。在global wmark\_min的基础上，将资源消耗型任务的global wmark\_min上移，使其提前进入直接内存回收。将时延敏感型业务的global wmark\_min下移，使其尽量避免直接内存回收。这样当资源消耗型任务瞬间申请大量内存的时候，会通过上移的global wmark\_min将其短时间抑制，避免时延敏感型业务发生直接内存回收。等待全局kswapd回收一定量的内存后，再解除资源消耗型任务的短时间抑制。|
|[Memcg后台异步回收](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/Memcg后台异步回收.md)|Alibaba Cloud Linux 2增加了memcg粒度的后台异步回收功能。该功能的实现不同于全局kswapd内核线程的实现，并没有创建对应的memcg kswapd内核线程，而是采用了workqueue机制来实现。|
|[cgroup v1接口支持memcg QoS功能](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/cgroup v1接口支持memcg QoS功能.md)|内存子系统服务质量（memcg QoS）可以用来控制内存子系统（memcg）的内存使用量的保证（锁定）与限制。Alibaba Cloud Linux 2在4.19.91-18.al7内核版本，新增cgroup v1接口支持memcg QoS的相关功能。|
|[Memcg Exstat功能](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/Memcg Exstat功能.md)|Alibaba Cloud Linux 2在4.19.91-18.al7内核版本开始支持的Memcg Exstat（Extend/Extra）功能。|
|[TCP-RT功能的配置说明](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/TCP-RT功能的配置说明.md)|Alibaba Cloud Linux 2在内核版本kernel-4.19.91-21.al7开始支持TCP层的服务监控功能（TCP-RT）。|

