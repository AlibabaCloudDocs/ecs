---
keyword: [阿里云, Alibaba Cloud Linux, ecs, 原生linux]
---

# Alibaba Cloud Linux 2概述

Alibaba Cloud Linux 2（原Aliyun Linux 2）是阿里云官方操作系统，在全面兼容CentOS 7生态的同时，为云上应用程序提供安全、稳定、高性能的定制化运行环境，并针对云基础设施进行了深度优化，为您打造更好的运行时体验。您可以免费使用Alibaba Cloud Linux 2公共镜像，并免费获得阿里云针对该操作系统的长期支持。

更多详情，请访问[Alibaba Cloud Linux 2产品详情页](https://www.aliyun.com/product/alinux)。

## 适用范围

Alibaba Cloud Linux 2适用于下列场景。

-   各种云场景工作负载。例如数据库、云原生容器、数据分析、Web应用程序，以及生产环境中的其他工作负载。
-   多种实例规格族，包括弹性裸金属服务器。详情请参见[实例规格族](/cn.zh-CN/实例/实例规格族.md)。
    -   支持的实例vCPU范围为1 vCPU~768 vCPU。
    -   支持的实例内存范围为0.5 GiB~12288 GiB。
    -   不支持非I/O优化实例。

## 优势

与其他Linux系统相比，Alibaba Cloud Linux 2具有以下优势。

-   阿里云官方为Alibaba Cloud Linux 2提供长期免费的软件维护和技术支持。
-   与阿里云基础设施的结合优化，持续提升系统的启动速度、运行时的性能。此外，Alibaba Cloud Linux 2经过海量阿里巴巴经济体应用打磨，提供了最佳的稳定性体验。
-   通过更新Linux内核、用户态软件及工具包，为云上应用程序环境提供Linux社区的最新操作系统增强功能。
-   精简内核，减少潜在安全隐患。提供安全漏洞监控与修复策略，持续保证系统安全。

## Alibaba Cloud Linux 2特性

-   默认搭载并启用最新版本阿里云云内核，新版云内核提供了以下特性。
    -   基于内核社区长期支持（LTS）的4.19定制而成，增加适用于云场景的新特性、改进内核性能并修复重大缺陷，详情请参见[Alibaba Cloud Linux 2发布记录](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2发布记录.md)。
    -   提供针对ECS实例环境定制优化的内核启动参数和系统配置参数。
    -   提供操作系统崩溃后的内核转储（Kdump）能力，您可根据需要在线打开或者关闭该功能，无需重启操作系统。
    -   提供内核热补丁升级（Live Patch）能力。
-   软件包预装和更新说明。
    -   用户态软件包保持与最新版CentOS 7兼容，该版本用户态软件包可直接在Alibaba Cloud Linux 2使用。
    -   默认搭载阿里云CLI。
    -   网络服务从network.service切换为systemd-networkd。
    -   软件包安全漏洞（CVE）修复在Alibaba Cloud Linux 2版本支持期限内会持续更新，详情请参见[Alibaba Cloud Linux 2 CVE更新记录](http://mirrors.aliyun.com/alinux/cve/alinux2.xml)。Alibaba Cloud Linux 2提供自动化修复方案，详情请参见[基于YUM的安全更新操作](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/基于YUM的安全更新操作.md)。
-   大幅优化开机启动速度，提升运行时的系统性能，并增强系统稳定性。
    -   针对ECS实例环境大幅优化启动速度，在实际测试中，相比其他操作系统约减少60%的启动时间。
    -   优化调度、内存、IO及网络等子系统，在部分的开源基准测试（benchmark）中，相比其他操作系统约提升10%~30%性能。
    -   持续增强系统稳定性，在宕机数据统计结果中，相比其他操作系统减少约50%的宕机率。

## Alibaba Cloud Linux 2镜像

|镜像|最新版本镜像ID|说明|
|--|--------|--|
|Alibaba Cloud Linux 2.1903 LTS 64位|aliyun\_2\_1903\_x64\_20G\_alibase\_20210325.vhd|Alibaba Cloud Linux 2操作系统的默认标准镜像。|
|Alibaba Cloud Linux 2.1903 64位 快速启动版|aliyun\_2\_1903\_x64\_20G\_qboot\_alibase\_20210325.vhd|该镜像支持Qboot（quick boot）快速启动，基于Alibaba Cloud Kernel，并直接从内核引导虚拟机启动的定制化镜像。使用该镜像创建的ECS实例相比其它镜像创建的ECS实例，启动速度得到了极大的提升，并且默认运行时与标准镜像完全一致。快速启动版镜像的相关说明如下：

-   只对实例的初次启动加速，后续启动实例的速度将保持正常水准。
-   优化加速内存初始化的过程，模块化了启动耗时的鼠标等设备，加速内核引导速度。
-   使用最新的AliyunInit服务替代了CloudInit服务，降低了操作系统的初始化耗时。
-   该镜像的内核版本无法修改内核启动参数。
-   不支持的实例规格族：GPU计算型、GPU虚拟化型、FPGA计算型、NPU计算型、异构服务型、超级计算集群（SCC）、安全增强型等。
-   支持的地域：华东1（杭州）、华南1（深圳）、华北2（北京）、华北3（张家口）、中国（香港）。 |
|Alibaba Cloud Linux 2.1903 64位 等保2.0三级版|aliyun\_2\_1903\_x64\_20G\_dengbao\_alibase\_20210325.vhd|基于默认标准镜像进行等保加固的镜像版本，该镜像符合等保2.0三级安全保护的基本要求。使用说明请参见[Alibaba Cloud Linux等保2.0三级版镜像使用说明](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux等保2.0三级版镜像/Alibaba Cloud Linux等保2.0三级版镜像使用说明.md)。|
|Alibaba Cloud Linux 2.1903 LTS 64位 AMD版|aliyun\_2\_1903\_x64\_20G\_uefi\_alibase\_20210218.vhd|基于默认标准镜像支持阿里云AMD实例的镜像版本，仅支持UEFI启动模式。 **说明：** 仅阿里云AMD弹性裸金属实例可以使用该镜像。更多信息，请参见[仅适用部分实例规格族的镜像发布记录](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2发布记录.mdsection_zai_t2o_j01)。 |
|Alibaba Cloud Linux 2.1903 64位 可信版|aliyun\_2\_1903\_x64\_20G\_secured\_alibase\_20210325.vhd|基于默认标准镜像支持阿里云可信实例的镜像版本。 **说明：** 仅阿里云可信实例可以使用该镜像。更多信息，请参见[仅适用部分实例规格族的镜像发布记录](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2发布记录.mdsection_zai_t2o_j01)。 |

## 费用

Alibaba Cloud Linux 2是免费镜像，但当您选用Alibaba Cloud Linux 2镜像创建ECS实例时，需要支付其他资源产生的费用，如vCPU、内存、存储、公网带宽和快照等。计费详情请参见[计费概述](/cn.zh-CN/产品计费/计费概述.md)。

## 获取Alibaba Cloud Linux 2

您可通过下列方法获取并使用Alibaba Cloud Linux 2。

-   ECS实例
    -   新创建ECS实例时选择**公共镜像**，并选择Alibaba Cloud Linux 2的相应版本。
        -   创建ECS实例的具体操作请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。
        -   Alibaba Cloud Linux 2多个版本的区别请参见[Alibaba Cloud Linux 2的多个镜像之间有何不同？](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2 FAQ.md)。
    -   已创建的ECS实例可通过更换系统盘，将现有操作系统更换为Alibaba Cloud Linux 2。详情请参见[更换系统盘（公共镜像）](/cn.zh-CN/块存储/云盘基础操作/更换系统盘/更换系统盘（公共镜像）.md)。
-   本地环境（基于KVM技术的虚拟化环境）

    直接下载Alibaba Cloud Linux 2虚拟机镜像并安装启动。详情请参见 [在本地使用Alibaba Cloud Linux 2镜像](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/在本地使用Alibaba Cloud Linux 2镜像.md)。


## 使用Alibaba Cloud Linux 2

-   查看或修改系统参数

    Alibaba Cloud Linux 2在配置文件/etc/sysctl.d/50-aliyun.conf中更新了下列内核配置参数，运行sysctl命令，可查看或修改Alibaba Cloud Linux 2运行时的系统参数。

    |系统参数|说明|
    |----|--|
    |`kernel.hung_task_timeout_secs = 240`|延长内核hung\_task超时秒数，避免频繁的hung\_task提示|
    |`kernel.panic_on_oops = 1`|允许内核发生Oops错误时抛出Kernel Panic异常，如果配置了Kdump则可自动捕获崩溃详情|
    |`kernel.watchdog_thresh = 50`|延长hrtimer、NMI、Soft Lockup以及Hard Lockup等事件的阈值，避免可能出现的内核误报|
    |`kernel.hardlockup_panic = 1`|允许内核发生Hard Lockup错误时抛出Kernel Panic异常，如果配置了Kdump则可自动捕获崩溃详情|

-   查看内核参数

    Alibaba Cloud Linux 2更新了下列内核参数，运行`cat /proc/cmdline`命令，可查看Alibaba Cloud Linux 2运行时的内核参数。

    |内核参数|说明|
    |----|--|
    |`crashkernel=0M-2G:0M,2G-8G:192M,8G-:256M`|为内核转储（Kdump）功能预留的内存空间|
    |`cryptomgr.notests`|关闭crypto在内核启动时的自检行为，加快启动速度|
    |`cgroup.memory=nokmem`|关闭Memory Cgroup的内核内存统计功能，避免出现潜在的内核不稳定问题|
    |`rcupdate.rcu_cpu_stall_timeout=300`|延长RCU CPU Stall Detector的超时阈值为300秒，避免内核误报|

-   开启或关闭内核转储（Kdump）功能

    Alibaba Cloud Linux 2提供了Kdump服务。开启该服务后可捕获内核错误，方便您分析内核崩溃现象。

    **说明：** 所选实例规格的内存小于或等于2GiB时，无法使用Kdump服务。

    -   依次运行以下命令可以开启Kdump服务。

        ```
        # 先开启Kdump服务
        sudo systemctl enable kdump.service
        # 重启Kdump服务
        sudo systemctl restart kdump.service
        ```

    -   依次运行以下命令可以将Kdump服务预留的内存地址空间归还给操作系统，并彻底关闭Kdump服务。

        ```
        # 先更改/sys/kernel/kexec_crash_size文件配置
        sudo sh -c 'echo 0 > /sys/kernel/kexec_crash_size'
        # 关闭Kdump服务
        sudo systemctl disable kdump.service
        # 停止Kdump服务
        sudo systemctl stop kdump.service
        ```

        **说明：** Kdump服务预留的内存地址空间归还给操作系统后，必须重启操作系统才可再次开启Kdump服务。

-   配置网络

    Alibaba Cloud Linux 2默认使用systemd-networkd配置网络，DHCP或静态IP的配置文件位于/etc/systemd/network/目录。

    ```
    # 该命令可以重启网络服务
    sudo systemctl restart systemd-networkd
    ```

-   获取Debuginfo包和源码包
    -   依次运行以下命令可以获取Debuginfo包。

        ```
        # 先安装yum-utils
        sudo yum install -y yum-utils
        # 安装Debuginfo包，其中<packageName>为您预期安装的软件包名称
        sudo debuginfo-install -y <packageName>
        ```

    -   依次运行以下命令可以获取源码包。

        ```
        # 先安装源码
        sudo yum install -y alinux-release-source
        # 安装yum-utils
        sudo yum install -y yum-utils
        # 安装源码包，其中<sourcePackageName>为您预期安装的软件包名称
        sudo yumdownloader --source <sourcePackageName>
        ```

-   使用试验性支持的软件包

    试验性支持的软件包指由阿里云官方提供，但未经严格测试，不保证质量的软件包。Alibaba Cloud Linux 2提供了普通试验性软件包和SCL插件方式支持的试验性软件包。

    -   普通试验性软件包

        -   `Golang 1.12`
        -   `Golang 1.13`
        依次运行以下命令可以安装软件包。

        ```
        # 先开启YUM仓库支持
        sudo yum install -y alinux-release-experimentals
        # 安装普通试验性软件包，其中<packageName>为您预期安装的软件包名称
        sudo yum install -y <packageName>
        ```

    -   SCL插件方式支持的开发工具包

        -   基于`GCC-7.3.1`的开发工具包（devtoolset-7）
        -   基于`GCC-8.2.1`的开发工具包（devtoolset-8）
        -   基于`GCC-9.1.1`的开发工具包（devtoolset-9）
        依次运行以下命令可以安装软件包。

        ```
        # 先安装`scl-utils`
        sudo yum install -y scl-utils
        # 打开YUM仓库支持
        sudo yum install -y alinux-release-experimentals
        # 从YUM源安装您需要的软件包，以下示例命令同时安装了SCL插件方式支持的所有开发工具包
        sudo yum install -y devtoolset-7-gcc devtoolset-7-gdb devtoolset-7-binutils devtoolset-7-make
        sudo yum install -y devtoolset-8-gcc devtoolset-8-gdb devtoolset-8-binutils devtoolset-8-make
        sudo yum install -y devtoolset-9-gcc devtoolset-9-gdb devtoolset-9-binutils devtoolset-9-make
        ```

        安装成功后，您即可使用高版本的GCC以及相关工具。示例代码如下：

        ```
        # 先查看现有的SCL，需要指定库名，本示例代码中，库名为devtoolset-7
        scl -l devtoolset-7
        # 运行相关的SCL软件
        scl enable devtoolset-7 'gcc --version'
        ```


## 更新记录

-   Alibaba Cloud Linux 2镜像发布记录请参见[Alibaba Cloud Linux 2发布记录](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2发布记录.md)。
-   Alibaba Cloud Linux 2 CVE更新记录请参见[Alibaba Cloud Linux 2 CVE更新记录](http://mirrors.aliyun.com/alinux/cve/alinux2.xml)。

## 技术支持

阿里云为Alibaba Cloud Linux 2提供如下技术支持：

-   为期5年的长期支持，包括安全更新和问题修复，于2024年3月31日结束版本生命周期。您可以通过以下方式获得免费的技术支持：
    -   [提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)
    -   [阿里云开发者社区](https://developer.aliyun.com/ask/?spm=a2c6h.13524658#/?_k=npz51r)
    -   [GitHub](https://alibaba.github.io/cloud-kernel/os.html?spm=5176.cnalinux.0.0.1f8323d1WpS5ZY&aly_as=32Di8ZOj)
-   每4个月更新一次镜像，更新内容包括新特性支持、安全更新、已知问题修复等。
-   在YUM源提供安全更新（Security Updates），运行yum update命令可更新至新版本。

