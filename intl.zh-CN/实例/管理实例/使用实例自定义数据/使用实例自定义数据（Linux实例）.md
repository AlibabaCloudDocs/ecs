# 使用实例自定义数据（Linux实例）

本文介绍如何准备适用于Linux实例的实例自定义数据，以及如何传入实例自定义数据和验证效果。

如果为已有实例修改实例自定义数据，该实例必须处于**已停止**状态。

Linux实例自定义数据功能采用开源的cloud-init架构。通过控制台或API等方式将实例自定义数据传入实例后，可以通过实例元数据查看内容，cloud-init也以实例元数据为来源自动化配置Linux实例。在实例启动时系统首先以管理员或者root权限运行实例自定义数据。

实例自定义数据的使用限制如下：

-   仅网络类型为专有网络VPC的实例支持实例自定义数据功能。
-   实例必须使用公共镜像或基于公共镜像创建的自定义镜像，且必须为以下镜像之一：
    -   Alibaba Cloud Linux、CentOS、Ubuntu、SUSE Linux Enterprise、OpenSUSE、Debian
    -   Windows Server 2008 R2及更高版本
-   在售的实例规格均支持实例自定义数据功能。但已停售的实例规格中，仅I/O优化实例支持实例自定义数据功能，更多信息，请参见[已停售的实例规格](/intl.zh-CN/实例/选择实例规格/已停售的实例规格.md)。
-   执行时的实例自定义数据必须为Base64编码形式，且在进行Base64编码前自定义数据内容的大小不能超过16 KB。

    **说明：** 您可以在控制台输入未经过Base64编码的实例自定义数据，控制台会自动进行Base64编码。如果您不在控制台输入实例自定义数据，请先自行将实例自定义数据进行Base64编码。


## 操作步骤

1.  准备实例自定义数据。

    您可以通过多种脚本准备Linux实例自定义数据，不同脚本类型的特点以及示例请参见：

    -   [User-Data脚本](#section_lu5_puw_zsj)
    -   [Cloud Config数据](#section_7gb_rtg_ouq)
    -   [Include文件](#section_t34_b33_6gz)
    -   [Gzip压缩内容](#section_esq_lq8_ra7)
    -   [Upstart Job](#section_7ug_631_wrv)
    **说明：** 如果您采用Include文件或Gzip压缩内容的方式，需要使用存储服务进行上传脚本获取脚本链接、设置链接有效期等操作。推荐您使用阿里云对象存储OSS，具体操作请参见OSS文档[上传文件](/intl.zh-CN/快速入门/控制台快速入门/上传文件.md)和[设置生命周期规则](/intl.zh-CN/控制台用户指南/存储空间管理/基础设置/设置生命周期规则.md)。您也可以阅读cloud-init文档了解更多准备实例自定义数据的方式，请参见[User-Data Formats](http://cloudinit.readthedocs.io/en/latest/topics/format.html)。

2.  将实例自定义数据传入实例。

    -   创建实例时传入实例自定义数据：在**系统配置**页面中，单击展开**高级选项**区域，然后在**实例自定义数据**区域输入实例自定义数据。如果实例自定义数据已进行Base64编码，请选中**输入已采用Base64编码**。

        实例首次启动时向指定文件写入系统时间的示例如下图所示。

        ![createinstance-userdata](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5446060261/p271700.png)

    -   为已有实例修改实例自定义数据：在**实例列表**页面中，选择**更多** \> **实例设置** \> **设置用户数据**，然后在**用户数据**区域输入新的实例自定义数据。

        **说明：** 对于按量付费实例，如果您需要在修改自定义数据后立即启动实例，建议停止模式设置为**保留并收费**。

        实例每次启动时向指定文件写入最新系统时间的示例如下图所示。

        ![modifyinstance-userdata](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4820460261/p271925.png)

        修改Linux实例自定义数据后，启动实例时是否会重新运行新的实例自定义数据由脚本类型和模块类型决定。例如：

        -   User-Data脚本：都不会重新运行。
        -   Cloud Config数据：如果配置的对象是Byobu、Set Passwords等模块，不会重新运行。
        -   Cloud Config数据：如果配置的对象是Bootcmd、Update Etc Hosts、Yum Add Repo等模块，会重新运行。
        模块类型的特点，请参见[Modules](http://cloudinit.readthedocs.io/en/latest/topics/modules.html)中各模块（Module）的模块频率（Module Frequency）。

3.  查看传入实例的内容和运行效果。

    1.  [远程连接实例](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

    2.  通过实例元数据查看内容。

        ```
        curl http://100.100.100.200/latest/user-data
        ```

        以查看[步骤2](#step_7v1_zjw_1b8)中的创建实例时传入实例自定义数据为例，如下图所示，内容一致表明实例自定义数据已成功传入实例。

        ![view-user-data](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4820460261/p272240.png)

    3.  查看运行效果。

        运行效果和内容有关，向指定文件写入系统时间的效果如下图所示。

        ![view-result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4820460261/p272241.png)


## User-Data脚本

User-Data脚本传入Linux实例后直接作为Shell脚本执行。User-Data脚本具有以下特点：

-   首行以`#!`开头。
-   仅在实例首次启动时运行一次。

示例User-Data脚本：

```
#!/bin/sh
echo "Hello World. The time is now $(date -R)!" | tee /root/userdata_test.txt
```

示例User-Data脚本的效果为在实例首次启动时向userdata\_test.txt写入系统时间。

## Cloud Config数据

以Cloud Config数据的形式编写内容可以方便地为实例预先配置一些服务，例如更新yum源、导入SSH密钥、安装依赖包等。Cloud Config数据具有以下特点：

-   首行为`#cloud-config`，且起始位置不能有空格。
-   必须遵循YAML语法编写内容。
-   实例自定义数据的运行频率由您配置的模块决定。例如，Apt配置每台实例仅运行一次，Bootcmd则实例每次启动时都会运行一次。

示例Cloud Config数据：

```
#cloud-config
apt:
primary:
- arches: [default]
uri: http://us.archive.ubuntu.com/ubuntu/
bootcmd:
- echo "Hello World. The time is now $(date -R)!" | tee /root/userdata_test.txt
```

示例Cloud Config数据的效果为修改默认的软件源，并在实例每次启动时向userdata\_test.txt写入最新的系统时间。

## Include文件

Include文件包含一个或多个脚本链接，脚本链接按行分隔。实例启动时，cloud-init会逐个读取脚本链接以及脚本的内容。如果在读取某一个脚本的内容时出错，则停止读取剩余的脚本。Include文件具有以下特点：

-   首行为`#include`，且起始位置不能有空格。
-   每个脚本内容的大小在Base64编码前不能超过16 KB。
-   实例自定义数据的运行频率由脚本类型和模块类型决定。

示例Include文件：

```
#include
http://ecs-image-test.oss-cn-hangzhou.aliyuncs.com/userdata/myscript.sh
```

示例Include文件包含一个脚本链接，运行频率由脚本的类型决定。例如该脚本为User-Data脚本，则仅在实例首次启动时运行一次。

## Gzip压缩内容

如果您的User-Data脚本、Cloud Config数据和Include文件内容的大小可能超过16 KB，可以采用Gzip压缩内容（`.gz`格式）并做成链接，然后以Include文件的形式输入。cloud-init会自动解压Gzip压缩内容，运行解压后内容的效果和直接传入后运行没有区别。Gzip压缩内容具有以下特点：

-   首行为`#include`，且起始位置不能有空格。
-   每个压缩内容的大小在Base64编码前不能超过16 KB。
-   实例自定义数据的运行频率由脚本类型和模块类型决定。

示例Gzip压缩内容：

```
#include
http://ecs-image-test.oss-cn-hangzhou.aliyuncs.com/userdata/myscript.gz
```

示例Include文件包含一个Gzip压缩内容链接，cloud-init读取该Gzip压缩内容后会自动解压并运行，运行频率由脚本的类型决定。例如该Gzip压缩内容由User-Data脚本压缩得到，则仅在实例首次启动时运行一次。

## Upstart Job

Upstart Job将内容存放到/etc/init目录下的文件中。Upstart Job具有以下特点：

-   首行为`#upstart-job`，且起始位置不能有空格。
-   实例每次启动时都会运行。

**说明：** 如需使用Upstart Job，您需要为实例安装upstart服务，支持采用upstart服务管理启动行为的操作系统有CentOS 6、Ubuntu 10/12/14以及Debian 6/7。

示例Upstart Job内容：

```
#upstart-job
description "upstart test"
start on runlevel [2345] #在运行级别2、3、4、5执行
stop on runlevel [!2345] #在运行级别2、3、4、5以外不执行
exec echo "Hello World. The time is now $(date -R)!" | tee /root/output.txt
```

## 示例一：使用User-Data脚本自定义yum源、NTP服务和DNS服务

系统会在实例启动时自动配置默认的yum源、NTP服务和DNS服务，您可以使用实例自定义数据更改默认的yum源、NTP服务和DNS服务，但请注意：

-   如果您自定义了yum源，阿里云官方不再提供yum源相关支持。
-   如果您自定义了NTP服务，阿里云官方不再提供相关时间同步服务。

适用于CentOS 7.2的示例User-Data脚本如下：

```
#!/bin/sh
# Modify DNS
echo "nameserver 8.8.8.8" | tee /etc/resolv.conf
# Modify yum repo and update
rm -rf /etc/yum.repos.d/*
touch myrepo.repo
echo "[base]" | tee /etc/yum.repos.d/myrepo.repo
echo "name=myrepo" | tee -a /etc/yum.repos.d/myrepo.repo
echo "baseurl=http://mirror.centos.org/centos" | tee -a /etc/yum.repos.d/myrepo.repo
echo "gpgcheck=0" | tee -a /etc/yum.repos.d/myrepo.repo
echo "enabled=1" | tee -a /etc/yum.repos.d/myrepo.repo
yum update -y
# Modify NTP Server
echo "server ntp1.aliyun.com" | tee /etc/ntp.conf
systemctl restart ntpd.service
```

**说明：**

-   其中的URL仅为示例，请按您的实际需要替换。
-   您也可以使用Cloud Config数据更改yum源，但是不够灵活，不能适配阿里云已对部分yum源进行预配置的情况，建议使用User-Data脚本。

在创建实例时传入实例自定义数据，启动后登录实例查看效果，确认实例的yum源、NTP服务和DNS服务配置符合预期，如下图所示。

![custom-yum-dns-ntp](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4820460261/p272130.png)

## 示例二：使用User-Data脚本自定义管理员账号

Linux实例默认使用root用户作为管理员，您可以使用实例自定义数据使用其他用户作为管理员。

适用于CentOS 7.2的示例User-Data脚本如下：

```
#!/bin/sh
useradd test
echo "test   ALL=(ALL)        NOPASSWD:ALL" | tee -a /etc/sudoers
mkdir /home/test/.ssh
touch /home/test/.ssh/authorized_keys
echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCRnnUveAis****" | tee -a /home/test/.ssh/authorized_keys
```

**说明：** 请使用您的公钥替换示例中的公钥ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCRnnUveAis\*\*\*\*。

示例User-Data脚本的效果如下：

-   创建名为test的用户，并作为管理员账号使用。
-   仅允许该用户使用SSH密钥对远程连接实例，不能使用用户密码。
-   如果该用户执行需要管理员权限的操作，通过sudo命令提权即可，无需输入密码。

在创建实例时传入实例自定义数据，启动后可以通过test用户和SSH密钥对远程连接实例，如果尝试使用密码登录会报错。连接实例后，可以通过sudo命令提权执行需要管理员权限的操作，如下图所示。

![test-admin-sample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4820460261/p272158.png)

