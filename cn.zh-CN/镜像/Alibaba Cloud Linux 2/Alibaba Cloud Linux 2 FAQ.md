# Alibaba Cloud Linux 2 FAQ

本文提供了Alibaba Cloud Linux 2镜像的常见问题与解决方案。

-   [Alibaba Cloud Linux 2与Aliyun Linux有何不同？](#section_imn_fim_626)
-   [Alibaba Cloud Linux 2的多个镜像之间有何不同？](#section_9bw_q66_hep)
-   [如何开始在阿里云上使用Alibaba Cloud Linux 2？](#section_ih8_6n8_aty)
-   [在阿里云ECS中运行Alibaba Cloud Linux 2是否有任何相关成本？](#section_7na_hla_jpe)
-   [Alibaba Cloud Linux 2支持哪些阿里云ECS实例类型？](#section_dja_kr5_fuo)
-   [Alibaba Cloud Linux 2是否支持32位应用程序和库？](#section_esh_mwl_ir7)
-   [Alibaba Cloud Linux 2是否附带图形用户界面（GUI）桌面？](#section_o24_dn0_rae)
-   [是否可以查看Alibaba Cloud Linux 2组件的源代码？](#section_wtr_xdj_ktn)
-   [Alibaba Cloud Linux 2是否与现有版本的Aliyun Linux向后兼容？](#section_a7h_hcy_6ps)
-   [是否可以在本地使用Alibaba Cloud Linux 2？](#section_2go_rnh_810)
-   [Alibaba Cloud Linux 2上支持运行哪些第三方应用程序？](#section_37f_kfg_e2f)
-   [相比其他Linux操作系统，Alibaba Cloud Linux 2有哪些优势？](#section_0hi_2xq_mb4)
-   [Alibaba Cloud Linux 2怎样保证数据安全？](#section_2gz_az0_nd6)
-   [Alibaba Cloud Linux 2是否支持数据加密？](#section_dn9_qtz_eoz)
-   [怎样设置Alibaba Cloud Linux 2的有关权限？](#section_z2y_011_tl5)

## Alibaba Cloud Linux 2与Aliyun Linux有何不同？

Alibaba Cloud Linux 2即为原Aliyun Linux 2，是Aliyun Linux的升级版本。Alibaba Cloud Linux 2和Aliyun Linux之间的主要区别是：

-   Alibaba Cloud Linux 2针对容器场景优化，更好支持云原生应用。
-   Alibaba Cloud Linux 2附带了更新的Linux内核、及用户态软件包版本。

## Alibaba Cloud Linux 2的多个镜像之间有何不同？

Alibaba Cloud Linux 2的镜像发布记录请参见[Alibaba Cloud Linux 2发布记录](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2发布记录.md)。Alibaba Cloud Linux 2包括的镜像之间的关系，请参见[Alibaba Cloud Linux 2镜像](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2概述.md)。

## 如何开始在阿里云上使用Alibaba Cloud Linux 2？

阿里云为Alibaba Cloud Linux 2提供了公共镜像，您可以在创建ECS实例时，选择公共镜像下的Alibaba Cloud Linux 2镜像的版本。

## 在阿里云ECS中运行Alibaba Cloud Linux 2是否有任何相关成本？

没有。运行Alibaba Cloud Linux 2是免费的，您只需支付ECS实例运行的费用。

## Alibaba Cloud Linux 2支持哪些阿里云ECS实例类型？

Alibaba Cloud Linux 2支持大部分阿里云ECS实例类型，包括弹性裸金属服务器。

**说明：** Alibaba Cloud Linux 2不支持使用Xen虚拟机平台的实例。

## Alibaba Cloud Linux 2是否支持32位应用程序和库？

暂不支持。

## Alibaba Cloud Linux 2是否附带图形用户界面（GUI）桌面？

暂不提供官方支持。

## 是否可以查看Alibaba Cloud Linux 2组件的源代码？

Alibaba Cloud Linux 2遵循开源协议。您可以通过yumdownloader工具或者在阿里云开源站点下载源代码包，也可以从Github站点下载Alibaba Cloud Linux 2内核源代码树，详情请参见[Github](https://github.com/alibaba/cloud-kernel)。

## Alibaba Cloud Linux 2是否与现有版本的Aliyun Linux向后兼容？

Alibaba Cloud Linux 2完全兼容Aliyun Linux 17.01。

**说明：** 如果您使用了自行编译的内核模块，可能需要在Alibaba Cloud Linux 2上重新编译才能正常使用。

## 是否可以在本地使用Alibaba Cloud Linux 2？

可以。Alibaba Cloud Linux 2提供了qcow2格式的本地镜像，目前只支持KVM虚拟机，详情请参见[在本地使用Alibaba Cloud Linux 2镜像](/cn.zh-CN/镜像/Alibaba Cloud Linux 2/Alibaba Cloud Linux 2支持的功能和接口/在本地使用Alibaba Cloud Linux 2镜像.md)。

## Alibaba Cloud Linux 2上支持运行哪些第三方应用程序？

当前Alibaba Cloud Linux 2与CentOS 7.6.1810版本二进制兼容，因此所有可以运行在CentOS上的应用程序，均可在Alibaba Cloud Linux 2上流畅运行。

## 相比其他Linux操作系统，Alibaba Cloud Linux 2有哪些优势？

Alibaba Cloud Linux 2与CentOS 7.6.1810发行版保持二进制兼容，在此基础上提供差异化的操作系统功能。

与CentOS及RHEL相比，Alibaba Cloud Linux 2的优势体现在：

-   满足您的操作系统新特性诉求，更快的发布节奏，更新的Linux内核、用户态软件及工具包。
-   开箱即用，最简用户配置，最短时间服务就绪。
-   最大化用户性能收益，与云基础设施联动优化。
-   与RHEL相比没有运行时计费，与CentOS相比有商业支持。

## Alibaba Cloud Linux 2怎样保证数据安全？

Alibaba Cloud Linux 2二进制兼容CentOS 7.6.1810/RHEL 7.6，遵从RHEL的安全规范。具体体现在以下几个方面：

-   使用业内标准的漏洞扫描及安全测试工具，定期做安全扫描。
-   定期评估CentOS 7的CVE补丁，修补OS安全漏洞。
-   与安全团队合作，支持阿里云现有的OS安全加固方案。
-   使用CentOS 7相同的机制，发布用户安全警告及补丁更新。

## Alibaba Cloud Linux 2是否支持数据加密？

Alibaba Cloud Linux 2保留CentOS 7的数据加密工具包，并确保CentOS 7与KMS协同工作的加密方案可以在Alibaba Cloud Linux 2得到支持。

## 怎样设置Alibaba Cloud Linux 2的有关权限？

Alibaba Cloud Linux 2属于与CentOS 7同源的操作系统。CentOS 7的管理员可以无缝地使用完全一致的管理命令做相关的权限设置，Alibaba Cloud Linux 2的缺省权限设置与阿里云CentOS 7镜像完全一致。

