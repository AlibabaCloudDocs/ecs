---
keyword: [阿里云, ecs, 时间校对, 时区]
---

# 配置Windows实例NTP服务

本文介绍如何开启和配置Windows NTP服务，保证实例本地时间精确同步。

目前，所有地域下ECS实例默认采用CST（China Standard Time）时区，您也可以根据自己的业务需求为ECS实例设置或者修改时区。

本文以Windows Server 2012 R2数据中心版64位为例，介绍如何使用NTP服务同步Windows实例的本地时间。

## 开启NTP服务

Windows Server操作系统默认开启Windows Time服务。为了保证NTP服务配置成功后能正常同步时间，实例中必须开启NTP服务。请按以下步骤检查并开启NTP服务：

1.  远程连接Windows实例。具体操作，请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

2.  单击开始图标![开始](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2952954061/p179485.png)，在底部单击下拉按钮，然后单击**运行**，在运行对话框中执行命令`services.msc`。

3.  在服务对话框中，找到并双击**Windows Time**服务。

4.  在Windows Time的属性（本地计算机）对话框中，执行以下操作：

    1.  将**启动类型**设置为**自动**。

    2.  确认**服务状态**为**正在运行**。如果不是，单击**启动**。

        ![shuxing](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7214359951/p86273.png)

    3.  单击**应用**，并单击**确定**。


## 修改默认NTP服务器地址

Windows Server操作系统默认配置微软NTP服务器（time.windows.com），但是可能经常同步出错。使用阿里云ECS实例时，您可以将默认NTP服务器更换成阿里云提供的内网NTP服务器。请按以下步骤修改默认NTP服务器地址。

1.  远程连接Windows实例。具体操作，请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

2.  在任务栏的通知区域，单击日期和时间，并单击**更改日期和时间设置**。

3.  在日期和时间对话框里，单击**Internet 时间**选项卡，并单击**更改设置**。

4.  在Internet 时间设置对话框里，选择**与Internet时间服务器同步**，填写一个阿里云内网NTP服务器地址，并单击**立即更新**。详细的服务器地址，请参见[使用阿里云NTP服务器](/intl.zh-CN/实例/管理实例/同步服务器本地时间/阿里云NTP服务器.md)。


## 修改NTP服务时间同步间隔

NTP服务的时间同步间隔默认是5分钟，您可以根据业务需求自定义同步间隔。请按以下步骤修改时间同步间隔：

1.  远程连接Windows实例。具体操作，请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

2.  单击开始图标![开始](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2952954061/p179485.png)，在底部单击下拉按钮，然后单击**运行**，在运行对话框中执行命令`regedit`。

3.  在注册表编辑器的左侧目录树中，选择**HKEY\_LOCAL\_MACHINE** \> **SYSTEM** \> **CurrentControlSet** \> **Services** \> **W32Time** \> **TimeProviders** \> **NtpClient**，并双击**SpecialPollInterval**键值。

4.  在编辑 DWORD （32 位）值对话框中，在**基数**栏里选择**十进制**，并按需要填写**数值数据**。填入的数值即是您需要的同步时间间隔（单位为秒）。

5.  单击**确定**，完成修改操作。

6.  重启实例使配置生效。

    您可以直接重启实例使配置生效。如果您的业务需求导致不方便重启实例，您也可以选择重启服务使配置生效。具体操作如下：

    1.  单击开始图标![开始](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2952954061/p179485.png)，在底部单击下拉按钮，然后单击**运行**，在运行对话框中执行命令`services.msc`。

    2.  在服务对话框中，找到并双击**Windows Time**服务。

    3.  在Windows Time的属性（本地计算机）对话框中，单击**停止**。

    4.  等待服务状态变更为**已停止**后，单击**启动**。

    5.  单击**确定**，完成重启服务的操作。


**相关文档**  


[阿里云NTP服务器](/intl.zh-CN/实例/管理实例/同步服务器本地时间/阿里云NTP服务器.md)

[配置Linux实例NTP服务（CentOS 6）](/intl.zh-CN/实例/管理实例/同步服务器本地时间/配置Linux实例NTP服务.md)

[配置Linux实例Chrony服务（CentOS 7）](/intl.zh-CN/实例/管理实例/同步服务器本地时间/配置Linux实例Chrony服务（CentOS 7）.md)

[配置Linux实例Chrony服务（Alibaba Cloud Linux 2）](/intl.zh-CN/实例/管理实例/同步服务器本地时间/配置Linux实例Chrony服务（Alibaba Cloud Linux 2）.md)

