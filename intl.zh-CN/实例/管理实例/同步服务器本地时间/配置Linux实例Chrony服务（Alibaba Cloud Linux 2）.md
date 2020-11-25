# 配置Linux实例Chrony服务（Alibaba Cloud Linux 2）

本文以Alibaba Cloud Linux 2.1903 LTS 64位系统为例介绍如何修改Linux系统的ECS实例的时区，以及如何开启、配置及使用Chrony服务，保证实例本地时间精确同步。

已在实例安全组的入方向添加安全组规则并放行UDP 123端口。具体操作请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

目前，所有地域下ECS实例默认采用CST（China Standard Time）时区，您也可以根据自己的业务需求为ECS实例设置或者修改时区。

Alibaba Cloud Linux 2系统中使用Chrony工具实现本地时间与标准时间同步。Chrony包含了两个核心程序：

-   chronyd是后台运行的守护进程。用于调整内核中运行的系统时钟和时钟服务器同步。它确定计算机增减时间的比率，并对此进行修正。
-   chronyc提供了一个用户界面，用于监控性能并进行多样化的配置。它可以在chronyd控制的服务器上工作；也可以在一台不同的远程服务器上工作。

更多详情请参见[Chrony](https://chrony.tuxfamily.org/index.html)。

## 修改Linux系统实例时区

1.  远程连接Linux实例。具体操作，请参见[通过VNC远程连接登录Linux实例](/intl.zh-CN/实例/连接实例/连接Linux实例/通过VNC远程连接登录Linux实例.md)。

2.  运行以下命令查看时区列表。

    ```
    ls /usr/share/zoneinfo/<时区文件夹名称>
    ```

    例如，运行以下命令可以在时区列表中查看到`Hong_Kong`时区。

    ```
    ls /usr/share/zoneinfo/Asia
    ```

3.  运行以下命令修改时区。

    ```
    ln -sf /usr/share/zoneinfo/Asia/Hong-Kong /etc/localtime
    ```

4.  运行以下命令更新硬件时钟（RTC）。

    ```
    hwclock -w
    ```

5.  运行以下命令查看时区。

    ```
    timedatectl status
    ```

    查询结果如下所示，时区已修改为`Hong_Kong`。

    ```
          Local time: 一 2020-09-14 08:00:04 UTC
      Universal time: 一 2020-09-14 08:00:04 UTC
            RTC time: 一 2020-09-14 08:00:04
           Time zone: Asia/Hong-Kong (UTC, +0000)
    ```


## 启用Chrony服务

1.  远程连接Linux实例。具体操作，请参见[通过VNC远程连接登录Linux实例](/intl.zh-CN/实例/连接实例/连接Linux实例/通过VNC远程连接登录Linux实例.md)。

2.  运行以下命令启动chronyd服务并设置开机自启动。

    ```
    systemctl start chronyd.service
    systemctl enable chronyd.service
    ```

3.  运行以下命令查看本机时间同步状态，用于验证服务是否已启动。

    ```
    chronyc tracking
    ```

4.  运行以下命令查看时间同步服务器列表。

    ```
    chronyc -n sources -v
    ```


## 配置Chrony服务

1.  远程连接Linux实例。具体操作，请参见[通过VNC远程连接登录Linux实例](/intl.zh-CN/实例/连接实例/连接Linux实例/通过VNC远程连接登录Linux实例.md)。

2.  运行以下命令打开chrony配置文件。

    ```
    vim /etc/chrony.conf
    ```

3.  找到`server <NTP服务器> minpoll 4 maxpoll 10 iburst`的信息后，按i键开始编辑文件，给您暂时不需要的NTP服务器句首加上`#`隐藏起来。

4.  新添加一行NTP服务器信息，格式为：`server <需要添加的NTP服务器> minpoll 4 maxpoll 10 iburst`。完成编辑后按Esc键并输入`:wq`保存退出。

    NTP服务器信息请参见[阿里云NTP服务器](/intl.zh-CN/实例/管理实例/同步服务器本地时间/阿里云NTP服务器.md)。

5.  运行以下命令启动chronyd服务并设置开机自启动。

    ```
    systemctl start chronyd.service
    systemctl enable chronyd.service
    ```

6.  运行以下命令查看时间同步服务器列表。

    ```
    chronyc -n sources -v
    ```


## 配置Chrony服务

1.  远程连接Linux实例。具体操作，请参见[通过VNC远程连接登录Linux实例](/intl.zh-CN/实例/连接实例/连接Linux实例/通过VNC远程连接登录Linux实例.md)。

2.  运行以下命令打开chrony配置文件。

    ```
    vim /etc/chrony.conf
    ```

3.  找到`server <NTP服务器> minpoll 4 maxpoll 10 iburst`的信息后，按i键开始编辑文件，给您暂时不需要的NTP服务器句首加上`#`隐藏起来。

4.  新添加一行NTP服务器信息，格式为：`server <需要添加的NTP服务器> minpoll 4 maxpoll 10 iburst`。完成编辑后按Esc键并输入`:wq`保存退出。

    NTP服务器信息请参见[阿里云NTP服务器](/intl.zh-CN/实例/管理实例/同步服务器本地时间/阿里云NTP服务器.md)。

5.  运行以下命令启动chronyd服务并设置开机自启动。

    ```
    systemctl start chronyd.service
    systemctl enable chronyd.service
    ```

6.  运行以下命令查看时间同步服务器列表。

    ```
    chronyc -n sources -v
    ```


## 使用Chrony手动同步时钟

1.  运行以下命令进入Chrony工具。

    ```
    chronyc
    ```

2.  在Chrony工具内，运行以下命令同步时钟。

    ```
    makestep
    ```

    **说明：** 您可以运行命令help获取Chrony常用命令的使用说明。


