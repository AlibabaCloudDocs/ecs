---
keyword: [阿里云, ecs, 时间校对, 时区]
---

# 配置Linux实例NTP服务（CentOS 6）

本文以Centos 6.5为例介绍如何修改Linux实例时区，以及开启和配置Linux NTP服务，保证实例本地时间精确同步。

NTP服务的通信端口为UDP 123，设置NTP服务之前请确保您已经打开UDP 123端口。您可以通过`netstat -nupl`命令查看实例是否开通UDP 123端口。如何放行UDP 123端口，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

目前，所有地域下ECS实例默认采用CST（China Standard Time）时区，您也可以根据自己的业务需求为ECS实例设置或者修改时区。

NTP 服务能保证 ECS 实例的本地时间与标准时间同步。在Linux系统中，您可以通过ntpdate和ntpd两种命令方式实现NTP时间同步。此处提供标准NTP服务配置和自定义NTP服务配置，您可以根据需要选择性地配置。关于更多NTP服务信息，请参见[内网和公共NTP服务器](/cn.zh-CN/实例/管理实例/同步服务器本地时间/阿里云NTP服务器.md)。

-   `ntpdate`为断点更新。对新购实例，您可以使用`ntpdate`同步时间。
-   `ntpd`为步进式地逐渐调整时间。对已经承载有运行中业务的实例，建议您使用`ntpd`同步时间。

## 修改Linux实例时区

1.  远程连接 Linux 实例。具体操作，请参见[连接方式概述](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

    **说明：** 您需要以root身份打开并编辑时区配置文件，所以此处使用`sudo`命令。

2.  执行命令`sudo rm /etc/localtime`删除系统里的当地时间链接。

3.  执行命令`sudo vi /etc/sysconfig/clock`，打开并编辑配置文件/etc/sysconfig/clock。

4.  输入`i`添加时区城市。例如添加`Zone=Asia/Shanghai`，按下Esc键退出编辑并输入`:wq`保存并退出。

    可执行命令`ls /usr/share/zoneinfo`查询时区列表，`Shanghai`为列表条目之一。

5.  执行命令`sudo ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`更新时区修改内容。

6.  执行命令`hwclock -w`更新硬件时钟（RTC）。

7.  执行命令`sudo reboot`重启实例。

8.  执行命令`date -R`查看时区信息是否生效，未生效可按照上述步骤重新操作一遍。


## 启动标准NTP服务

1.  远程连接Linux实例。具体操作，请参见[连接方式概述](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  执行命令`sudo service ntpd start`启动NTP服务。

3.  执行命令`chkconfig ntpd on`设置开机自启动NTP服务。

4.  执行命令`ntpstat`查看是否启动了NTP服务。

5.  执行命令`ntpq -p`可查看NTP服务对等端的列表信息；执行命令`sudo chkconfig --list ntpd`可查看NTP服务的运行级别。


## 配置自定义NTP服务

1.  远程连接Linux实例。具体操作，请参见[连接方式概述](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  执行命令`sudo vi /etc/ntp.conf`打开并编辑NTP服务配置文件。

3.  找到`server ntp 服务器 iburst`的信息后，输入`i`开始编辑文件，给您暂时不需要的NTP服务器句首加上`#`隐藏起来。

4.  新添加一行NTP服务器信息，格式为：`server 您需要添加的NTP服务器 iburst`。完成编辑后按下Esc键并输入`:wq`保存退出。

5.  执行命令`sudo service ntpd start`启动自定义的NTP服务。

6.  执行命令`chkconfig ntpd on`设置开机自启动NTP服务。

7.  执行命令`ntpstat`查看是否启动了NTP服务。


**相关文档**  


[阿里云NTP服务器](/cn.zh-CN/实例/管理实例/同步服务器本地时间/阿里云NTP服务器.md)

[配置Windows实例NTP服务](/cn.zh-CN/实例/管理实例/同步服务器本地时间/配置Windows实例NTP服务.md)

