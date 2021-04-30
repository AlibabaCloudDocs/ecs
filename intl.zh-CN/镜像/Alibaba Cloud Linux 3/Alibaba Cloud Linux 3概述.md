---
keyword: [ecs, alibaba cloud linux, alibaba cloud linux 3, linux, 镜像, 操作系统]
---

# Alibaba Cloud Linux 3概述

Alibaba Cloud Linux 3是阿里云官方操作系统的第三代发行版，继承Alibaba Cloud Linux 2功能特性的同时，进一步提升安全性、稳定性和运行时性能，在阿里云上为您提供了更好地操作系统体验。您可以免费使用Alibaba Cloud Linux 3公共镜像，并免费获得阿里云针对该操作系统的长期支持。

## 适用范围

Alibaba Cloud Linux 3适用于下列场景。

-   各种云场景工作负载。例如数据库、云原生容器、数据分析、Web应用程序，以及生产环境中的其他工作负载。
-   多种实例规格族，包括弹性裸金属服务器。详情请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。
    -   支持的实例vCPU范围为1 vCPU~768 vCPU。
    -   支持的实例内存范围为0.5 GiB~12288 GiB。
    -   不支持非I/O优化实例。

**说明：** Alibaba Cloud Linux 3操作系统目前支持华北1（青岛）、华北2（北京）、华东1（杭州）、西南1（成都）、中国（香港）、新加坡地域，地域数量持续增加中。

## 优势

Alibaba Cloud Linux 3继承Alibaba Cloud Linux 2的全部优势，并与其他Linux系统相比，Alibaba Cloud Linux 3具有以下优势：

-   阿里云为Alibaba Cloud Linux 3提供免费的软件维护和技术支持，到2029年04月30日结束。
-   选择Linux kernel 5.10 LTS作为Alibaba Cloud Linux 3的内核，为云上应用程序环境提供Linux社区的最新操作系统增强功能。
-   选择阿里云提供的GCC 10.2、binutils 2.35、glibc 2.32的编译器，增强稳定性并提高与其它软件的兼容性。
-   兼容CentOS 8、RHEL 8软件生态。
-   与阿里云基础设施的结合优化，持续提升系统的启动速度、运行时的性能。
-   对Intel、AMD、ARM等平台进行功能适配、性能调优和稳定性加固，保证操作系统在各平台都能稳定可靠地长期运行。

## Alibaba Cloud Linux 3镜像

|镜像|最新版本镜像ID|说明|
|--|--------|--|
|Alibaba Cloud Linux 3.2104 64位|aliyun\_3\_x64\_20G\_alibase\_20210425.vhd|Alibaba Cloud Linux 3操作系统的默认标准镜像。|

## 费用

Alibaba Cloud Linux 3是免费镜像，但当您选用Alibaba Cloud Linux 3镜像创建ECS实例时，需要支付其他资源产生的费用，如vCPU、内存、存储、公网带宽和快照等。计费详情请参见[计费概述](/intl.zh-CN/产品计费/计费概述.md)。

## 获取Alibaba Cloud Linux 3

您可通过下列方法获取并使用Alibaba Cloud Linux 3。

-   新创建ECS实例时选择**公共镜像**，并选择Alibaba Cloud Linux 3的相应版本。具体操作，请参见[使用向导创建实例](/intl.zh-CN/实例/创建实例/使用向导创建实例.md)。
-   已创建的ECS实例可通过更换系统盘，将现有操作系统更换为Alibaba Cloud Linux 3。具体操作，请参见[更换系统盘（公共镜像）](/intl.zh-CN/块存储/云盘/更换系统盘/更换系统盘（公共镜像）.md)。

## 更新记录

关于Alibaba Cloud Linux 3镜像发布记录的更多信息，请参见[Alibaba Cloud Linux 3镜像发布记录]()。

## 技术支持

阿里云为Alibaba Cloud Linux 3提供如下技术支持：

-   为期8年的长期支持，包括安全更新和问题修复，于2029年04月30日结束版本生命周期。您可以通过以下方式获得免费的技术支持：
    -   [提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)
    -   [GitHub](https://alibaba.github.io/cloud-kernel/os.html?spm=5176.cnalinux.0.0.1f8323d1WpS5ZY&aly_as=32Di8ZOj)
-   每4个月更新一次镜像，更新内容包括新特性支持、安全更新、已知问题修复等。
-   在YUM源提供安全更新（Security Updates），运行yum update命令可更新至新版本。

