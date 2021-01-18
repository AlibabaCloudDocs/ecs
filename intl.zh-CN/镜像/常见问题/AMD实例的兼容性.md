# AMD实例的兼容性

本文主要说明AMD实例与不同版本的操作系统镜像之间的兼容性问题。

## 背景信息

AMD实例是阿里云新推出的重磅产品，基于AMD EPYCTM Zen 2微处理器架构（代号Rome），该架构属于x86架构。AMD实例将大量虚拟化功能卸载到专用硬件，降低虚拟化开销，提供稳定可预期的超高性能。AMD实例规格族目前有以下三种：

-   通用型实例规格族g6a
-   计算型实例规格族c6a
-   内存型实例规格族r6a

更多信息，请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。

AMD实例可以兼容不同版本的操作系统，AMD Zen架构发布于2017年，处理器的部分新特性在旧版操作系统上会出现部分功能支持上的缺陷。请您根据应用的实际情况，自行决定需要使用的操作系统版本。下文列出了各主流操作系统建议使用的版本。

## 各操作系统对AMD Rome处理器支持说明

下表列出了支持AMD Rome处理器的不同操作系统版本。

|操作系统|操作系统版本|官方文档|
|----|------|----|
|Windows|-   Windows Server 2012 R2
-   Windows Server 2016
-   Windows Server 2019

|[Windows Server support and installation instructions for the AMD Rome family of processors](https://support.microsoft.com/en-us/help/4514607/windows-server-support-and-installation-instructions-for-amd-rome-proc)|
|Linux|-   Alibaba Cloud Linux 2
-   CentOS 7.6/7.7/7.8/7.9/8.0/8.1/8.2/8.3
-   Ubuntu 16.04/18.04/20.04

|-   Red Hat Enterprise Linux：[AMD CPUs and Supported Red Hat Enterprise Linux \(RHEL\) Versions](https://access.redhat.com/support/policy/amd)
-   Ubuntu：[AMD EPYC Rome support in Ubuntu Server](https://ubuntu.com/blog/amd-epyc-rome-support-in-ubuntu-server) |

**相关文档**  


[公共镜像发布记录](/intl.zh-CN/镜像/公共镜像/公共镜像发布记录.md)

