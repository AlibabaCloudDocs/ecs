# 步骤4：配置IPv6地址

本文介绍了如何为Linux实例自动配置IPv6地址和手动配置IPv6地址，推荐您使用更高效的自动配置工具配置IPv6地址。

## 自动配置IPv6地址

ecs-util-ipv6能为已分配IPv6地址的ECS实例一键配置IPv6地址，或者为没有分配IPv6地址的ECS实例一键清理IPv6配置。

ecs-util-ipv6工具下载地址如下所示：

|系列|发行版|下载地址|
|:-|:--|:---|
|RHEL|-   CentOS 5/6/7/8
-   Red Hat 5/6/7

|[下载地址](https://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/rhel/ecs-utils-ipv6)|
|Debian|-   Ubuntu 14/16
-   Debian/8/9

|[下载地址](https://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/debian/ecs-utils-ipv6)|
|SLES|-   SUSE 11/12
-   OpenSUSE 42

|[下载地址](https://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/sles/ecs-utils-ipv6)|
|CoreOS|CoreOS 14/17|[下载地址](https://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/coreos/ecs-utils-ipv6)|
|FreeBSD|FreeBSD 11|[下载地址](https://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/freebsd/ecs-utils-ipv6)|

使用限制如下：

-   ecs-util-ipv6工具仅适用于VPC类型实例，依赖实例元数据服务，使用前请勿将网络禁用或者将相关出口IP端口（100.100.100.200:80）禁用。详情请参见[实例元数据](/cn.zh-CN/实例/管理实例/使用实例元数据/ECS实例元数据概述.md)。
-   ecs-util-ipv6工具运行时会自动重启网卡、网络服务，短时间内网络可能会不可用，请慎重执行。

下载对应系统版本工具到目标系统，赋予执行权限后使用管理员权限执行：

```
chmod +x ./ecs-utils-ipv6
./ecs-utils-ipv6
```

如果当前ECS已绑定IPv6地址，则会自动配置；否则会自动清理原有IPv6地址配置。

命令行参数：

```
ecs-utils-ipv6 --help           # show usage
ecs-utils-ipv6 --version        # show version
ecs-utils-ipv6                  # auto config all dev ipv6
ecs-utils-ipv6 --static [dev] [ip6s] [prefix_len] [gw6] # config dev static ipv6
e.g. ecs-utils-ipv6 --static eth0
       ecs-utils-ipv6 --static eth0 xxx::x1 64 xxx::x0
       ecs-utils-ipv6 --static eth0 "xxx::x1 xxx:x2 xxx:x3" 64 xxx::x0
ecs-utils-ipv6 --enable         # enable ipv6
ecs-utils-ipv6 --disable        # disable ipv6
```

可以开启、禁用、手动配置、自动配置（默认）IPv6。

```
./ecs-utils-ipv6                 #默认可不带参数，自动配置多网卡多IPv6
./ecs-utils-ipv6 --enable    #开启IPv6
./ecs-utils-ipv6 --disable    #禁用IPv6
./ecs-utils-ipv6 --static <dev>      #自动配置网卡IPv6
./ecs-utils-ipv6 --static <dev> <ip6s> <prefix_len> <gw6>     #手动配置网卡IPv6，支持多IPv6，请用""包含，多个IPv6用空格隔开
```

对于需要自动化配置IPv6实例的需求，例如大批量配置，建议您使用云助手或者实例自定义数据配合脚本的方式来调用。详情请参见[云助手](/cn.zh-CN/运维与监控/云助手/云助手概述.md)和[实例自定义数据](/cn.zh-CN/实例/管理实例/使用实例自定义数据/ECS实例自定义数据概述.md)。以下为脚本示例（假设是RHEL系列，Bash Shell脚本）。

```
#!/bin/sh
install_dir=/usr/sbin
install_path="$install_dir"/ecs-utils-ipv6
if [ ! -f "$install_path" ]; then
    tool_url="http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/rhel/ecs-utils-ipv6"
    # download the tool
    if ! wget "$tool_url" -O "$install_path"; then
        echo "[Error] download tool failed, code $?"
        exit "$?"
    fi
fi
# chmod the tool
if ! chmod +x "$install_path"; then
    echo "[Error] chmod tool failed, code $?"
    exit "$?"
fi
# run the tool
"$install_path"
```

## 手动配置IPv6地址（Alibaba Cloud Linux 2操作系统）

Alibaba Cloud Linux 2镜像在`aliyun_2_1903_64_20G_alibase_20190829.vhd`及之前的版本未开启IPv6，从`aliyun_2_1903_x64_20G_alibase_20200221.vhd`版本开始默认开启了IPv6。

请先检查实例是否已开启IPv6服务。

1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
2.  运行命令`ip addr | grep inet6`或者`ifconfig | grep inet6`：
    -   若返回`inet6`相关内容，表示实例已成功开启IPv6服务。您可以跳过本节内容。
    -   若未返回`inet6`相关内容，表示实例未开启IPv6服务，请根据下文开启IPv6服务。

开启IPv6支持配置为暂时或持久。暂时配置将在实例停止或重启时失效；持久配置将不受实例的状态影响。您可以根据实际情况选择配置方式，手动配置操作如下：

-   暂时开启IPv6。
    1.  运行以下命令进入/etc/systemd/network/目录。

        ```
        cd /etc/systemd/network/
        ```

    2.  使用命令`ls`查询该目录下的`.network`文件。

        例如，`50-dhcp.network`文件。

    3.  修改文件50-dhcp.network内容。

        ```
        vi /etc/systemd/network/50-dhcp.network
        ```

    4.  按i键进入编辑模式。

        将`[Network]`下的信息修改为`DHCP=yes`。

        **说明：** 文件内参数`Name=eth*`表示适配所有网络接口，所有网络接口都将通过DHCP配置IP地址与路由。如果只需要配置指定的网络接口，可以修改参数`Name`为指定的网络接口，例如，`Name=eth0`表示只适配`eth0`网络接口。更多关于network的信息请参见[systemd.network](https://www.freedesktop.org/software/systemd/man/systemd.network.html)。

        ```
        [Match]
        Name=eth*
        
        [Network]
        DHCP=yes
        ```

        修改完成后按esc键，并输入`:wq`后按下回车键，保存并退出。

    5.  运行以下命令开启IPv6。
        -   开启所有网络接口。

            ```
            sudo sysctl -w net.ipv6.conf.all.disable_ipv6=0
            sudo sysctl -w net.ipv6.conf.default.disable_ipv6=0
            ```

        -   开启指定网络接口示例。

            ```
            sudo sysctl -w net.ipv6.conf.eth0.disable_ipv6=0
            ```

        -   重启systemd-networkd服务使配置生效。

            ```
            sudo systemctl restart systemd-networkd
            ```

-   持久开启IPv6。
    1.  修改`/etc/sysctl.conf`配置文件。

        ```
        vi /etc/sysctl.conf
        ```

    2.  按i进入编辑模式。使用以下任一方式修改文件内容。
        -   删除下列配置信息。

            ```
            net.ipv6.conf.all.disable_ipv6 = 1
            net.ipv6.conf.default.disable_ipv6 = 1
            net.ipv6.conf.lo.disable_ipv6 = 1
            ```

        -   修改对应的配置信息为如下内容。

            ```
            net.ipv6.conf.all.disable_ipv6 = 0
            net.ipv6.conf.default.disable_ipv6 = 0
            net.ipv6.conf.lo.disable_ipv6 = 0
            ```

            如果需要开启指定网络接口，修改信息示例如下。

            ```
            net.ipv6.conf.eth0.disable_ipv6 = 0
            ```

            修改完成后按esc键，并输入`:wq`后按下回车键，保存并退出。

    3.  验证`/etc/sysctl.conf`配置信息是否与initramfs中的`/etc/sysctl.conf`存在差异。

        ```
        diff -u /etc/sysctl.conf <(lsinitrd -f /etc/sysctl.conf)
        ```

        **说明：** Alibaba Cloud Linux 2配置了initramfs（initram file system）。如果initramfs中的`/etc/sysctl.conf`文件与IPv6的配置文件`/etc/sysctl.conf`存在差异，系统可能会生效新的配置，与您需求的配置混淆。

    4.  如果两个配置文件存在差异，您可以执行以下命令重新生成initramfs。

        ```
        sudo dracut -v -f
        ```

    5.  重启实例。

        ```
        sudo reboot
        ```

    6.  执行`ifconfig`命令判断是否已开启IPv6。

        如果网络配置信息包含以下信息，表示IPv6已开启。

        ```
        inet6 <以fe80::开头的单播地址>
        inet6 <ECS实例的IPv6地址>
        ```


支持多网卡，配置操作如下：

1.  运行以下命令进入/etc/systemd/network/目录。

    ```
    cd /etc/systemd/network/
    ```

2.  使用命令`ls`查询该目录下的`.network`文件。

    例如，`10-eth0.network`文件。

3.  使用命令`cp`复制一个新的配置文件，例如：

    ```
    cp 10-eth0.network 20-dhcp.network
    ```

4.  运行以下命令修改配置文件。

    ```
    sed -i 's/^Name.*$/Name=*/g' /etc/systemd/network/20-dhcp.network
    ```

5.  重启systemd-networkd服务使配置生效。

    ```
    sudo systemctl restart systemd-networkd
    ```


## 手动配置IPv6地址（其它操作系统）

CentOS、Debian、FreeBSD、OpenSUSE、SUSE、Ubuntu系统请完成以下操作，手动配置IPv6地址：

1.  检查实例是否已开启IPv6服务。

    **说明：** CentOS 8、Debian 10.3、Ubuntu 18.04默认开启了IPv6服务。

    1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。

    2.  运行命令`ip addr | grep inet6`或者`ifconfig | grep inet6`：

        -   若返回`inet6`相关内容，表示实例已成功开启IPv6服务。您可以跳过本章内容。
        -   若实例未开启IPv6服务，请根据下文开启IPv6服务。
2.  开启IPv6服务。

    -   CentOS 6的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/modprobe.d/disable_ipv6.conf`，将`options ipv6 disable=1`修改为`options ipv6 disable=0`后保存退出。
        3.  运行`vi /etc/sysconfig/network`，将`NETWORKING_IPV6=no`修改为`NETWORKING_IPV6=yes`后保存退出。
        4.  运行以下命令：

            ```
            modprobe ipv6 -r
            modprobe ipv6
            ```

        5.  运行`lsmod | grep ipv6`，当返回以下内容时，表明IPv6模块已经成功加载：

            ```
            ipv6                  xxxxx  8
            ```

            **说明：** 第三列参数值不能为 0，否则您需要重新设置IPv6服务。

        6.  运行`vi /etc/sysctl.conf`做如下修改：

            ```
            #net.ipv6.conf.all.disable_ipv6 = 1
            #net.ipv6.conf.default.disable_ipv6 = 1
            #net.ipv6.conf.lo.disable_ipv6 = 1
            
            net.ipv6.conf.all.disable_ipv6 = 0
            net.ipv6.conf.default.disable_ipv6 = 0
            net.ipv6.conf.lo.disable_ipv6 = 0
            ```

            修改完成后，保存并退出。

        7.  运行`sysctl -p`使配置生效。
    -   CentOS 7的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/modprobe.d/disable_ipv6.conf`，将`options ipv6 disable=1`修改为`options ipv6 disable=0` 后保存退出。
        3.  运行`vi /etc/sysconfig/network`，将`NETWORKING_IPV6=no`修改为`NETWORKING_IPV6=yes`后保存退出。
        4.  运行`vi /etc/sysctl.conf`做如下修改：

            ```
            #net.ipv6.conf.all.disable_ipv6 = 1
            #net.ipv6.conf.default.disable_ipv6 = 1
            #net.ipv6.conf.lo.disable_ipv6 = 1
            
            net.ipv6.conf.all.disable_ipv6 = 0
            net.ipv6.conf.default.disable_ipv6 = 0
            net.ipv6.conf.lo.disable_ipv6 = 0
            ```

            修改完成后，保存并退出。

        5.  运行`sysctl -p`使配置生效。
    -   CoreOS 14或17的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /usr/share/oem/grub.cfg`，删除`ipv6.disable=1`后保存退出。
        3.  重启实例。
    -   Debian 8或9的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/default/grub`，删除`ipv6.disable=1`后保存退出。
        3.  运行`vi /boot/grub/grub.cfg`，删除`ipv6.disable=1`后保存退出。
        4.  重启实例。
        5.  运行`vi /etc/sysctl.conf`做如下修改：

            ```
            #net.ipv6.conf.all.disable_ipv6 = 1
            #net.ipv6.conf.default.disable_ipv6 = 1
            #net.ipv6.conf.lo.disable_ipv6 = 1
            
            net.ipv6.conf.all.disable_ipv6 = 0
            net.ipv6.conf.default.disable_ipv6 = 0
            net.ipv6.conf.lo.disable_ipv6 = 0
            ```

            修改完成后，保存并退出。

        6.  运行`sysctl -p`使配置生效。
    -   FreeBSD 11的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/rc.conf`，添加`ipv6_activate_all_interfaces="YES"`后保存退出。
        3.  运行`/etc/netstart restart`重启网络。
    -   OpenSUSE 42的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/sysctl.conf`做如下修改：

            ```
            #net.ipv6.conf.all.disable_ipv6 = 1
            #net.ipv6.conf.default.disable_ipv6 = 1
            #net.ipv6.conf.lo.disable_ipv6 = 1
            
            net.ipv6.conf.all.disable_ipv6 = 0
            net.ipv6.conf.default.disable_ipv6 = 0
            net.ipv6.conf.lo.disable_ipv6 = 0
            ```

            修改完成后，保存并退出。

        3.  运行`sysctl -p`使配置生效。
    -   SUSE 11或12的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/modprobe.d/50-ipv6.conf`，删除`install ipv6 /bin/true`后保存退出。
        3.  运行`vi /etc/sysctl.conf`做如下修改：

            ```
            #net.ipv6.conf.all.disable_ipv6 = 1
            #net.ipv6.conf.default.disable_ipv6 = 1
            #net.ipv6.conf.lo.disable_ipv6 = 1
            
            net.ipv6.conf.all.disable_ipv6 = 0
            net.ipv6.conf.default.disable_ipv6 = 0
            net.ipv6.conf.lo.disable_ipv6 = 0
            ```

            修改完成后，保存并退出。

        4.  运行`sysctl -p`使配置生效。
    -   Ubuntu 14或16的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/sysctl.conf`做如下修改：

            ```
            #net.ipv6.conf.all.disable_ipv6 = 1
            #net.ipv6.conf.default.disable_ipv6 = 1
            #net.ipv6.conf.lo.disable_ipv6 = 1
            
            net.ipv6.conf.all.disable_ipv6 = 0
            net.ipv6.conf.default.disable_ipv6 = 0
            net.ipv6.conf.lo.disable_ipv6 = 0
            ```

            修改完成后，保存并退出。

        3.  运行`sysctl -p`使配置生效。
3.  查询实例的IPv6地址。

    您可以通过控制台和实例元数据查看实例分配的IPv6地址。

    -   控制台：请参见[分配 IPv6 地址](/cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤2：分配IPv6地址.md)。
    -   实例元数据：通过以下元数据项获取IPv6地址。详情请参见[实例元数据](/cn.zh-CN/实例/管理实例/使用实例元数据/ECS实例元数据概述.md)。
        -   IPv6 地址：network/interfaces/macs/\[mac\]/ipv6s
        -   IPv6 网关：network/interfaces/macs/\[mac\]/ipv6-gateway
        -   IPv6 虚拟交换机 CIDR 地址段：network/interfaces/macs/\[mac\]/vswitch-ipv6-cidr-block
4.  手动配置IPv6地址。

    -   CentOS 6/7/8 和 Red Hat 6/7 的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/sysconfig/network-scripts/ifcfg-eth0`打开网卡配置文件，`eth0`为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：
            -   单IPv6地址：

                ```
                IPV6INIT=yes
                IPV6ADDR=<IPv6地址>/<子网前缀长度>
                IPV6_DEFAULTGW=<IPv6网关>
                ```

            -   多IPv6地址：

                ```
                IPV6INIT=yes
                IPV6ADDR=<IPv6地址>/<子网前缀长度>
                IPV6ADDR_SECONDARIES="<IPv6地址1>/<子网前缀长度> <IPv6地址2>/<子网前缀长度>"
                IPV6_DEFAULTGW=<IPv6网关>
                ```

                **说明：** 为区分单个IPv6与多个IPv6地址，请在IPV6ADDR\_SECONDARIES 参数中使用列表格式表达多地址格式，使用半角引号（`"`）包含地址，并用空格隔开。

        3.  重启网络服务：
            -   非CentOS 8系统运行`service network restart`或`systemctl restart network`。
            -   CentOS 8系统运行`nmcli c reload`。
    -   Debian/8/9和Ubuntu 14/16的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/network/interfaces`打开网卡配置文件，`eth0`为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：
            -   单 IPv6 地址：

                ```
                auto eth0
                iface eth0 inet6 static
                address <IPv6地址>
                netmask <子网前缀长度>
                gateway <IPv6网关>
                ```

            -   多 IPv6 地址：

                ```
                auto eth0
                iface eth0 inet6 static
                address <IPv6地址>
                netmask <子网前缀长度>
                gateway <IPv6网关>
                
                auto eth0:0
                iface eth0:0 inet6 static
                address <IPv6地址1>
                netmask <子网前缀长度>
                gateway <IPv6网关>
                
                auto eth0:1
                iface eth0:1 inet6 static
                address <IPv6地址2>
                netmask <子网前缀长度>
                gateway <IPv6网关>
                ```

                **说明：** 为区分单个 IPv6 与多个 IPv6 地址，您只需在同一网卡标识符的基础上重复添加地址信息即可。

        3.  重启网络服务：运行`service network restart`或`systemctl restart networking`。
    -   OpenSUSE 42 和 SUSE Linux 11/12的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/sysconfig/network/ifcfg-eth0`打开网卡配置文件，`eth0`为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：
            -   单 IPv6 地址：

                ```
                IPADDR_0=<IPv6地址>
                PREFIXLEN_0=<子网前缀长度>
                ```

            -   多 IPv6 地址：

                ```
                IPADDR_0=<IPv6地址>
                PREFIXLEN_0=<子网前缀长度>
                
                IPADDR_1=<IPv6地址1>
                PREFIXLEN_1=<子网前缀长度>
                
                IPADDR_2=<IPv6地址2>
                PREFIXLEN_2=<子网前缀长度>
                ```

                **说明：** 为区分单个IPv6与多个IPv6地址，请使用不用的IPADDR\_N和PREFIXLEN\_N重复添加地址信息。

        3.  运行`vi /etc/sysconfig/network/routes`打开路由配置文件，添加配置项：

            ```
            default <IPv6网关> - -
            ```

        4.  重启网络服务：运行`service network restart`或`systemctl restart networking`。
    -   CoreOS 14/17的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/systemd/network/10-eth0.network`打开网卡配置文件，`eth0`为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：
            -   单IPv6地址：

                ```
                [Address]
                Address=<IPv6地址>/<子网前缀长度>
                [Route]
                Destination=::/0
                Gateway=<IPv6网关>
                ```

            -   多IPv6地址：

                ```
                [Address]
                Address=<IPv6地址1>/<子网前缀长度>
                [Address]
                Address=<IPv6地址2>/<子网前缀长度>
                [Route]
                Destination=::/0
                Gateway=<IPv6网关>
                ```

                **说明：** 为区分单个IPv6与多个IPv6地址，您只需在同一网卡标识符的基础上重复添加地址信息即可。

        3.  重启网络服务：运行`systemctr restart systemd-networkd`。
    -   FreeBSD 11的操作步骤如下：
        1.  远程连接实例。具体操作，请参见[通过密码认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。
        2.  运行`vi /etc/rc.conf`打开网卡配置文件，`vtnet0`为网卡标识符，您需要修改成实际的标识符。在文件中根据实际信息添加以下配置：
            -   单IPv6地址：

                ```
                ipv6_ifconfig_vtnet0="<IPv6地址>"
                ipv6_defaultrouter="<IPv6网关>"
                ```

            -   多IPv6地址：

                ```
                ipv6_ifconfig_vtnet0="<IPv6地址1>"
                ipv6_ifconfig_vtnet0="<IPv6地址2>"
                ipv6_defaultrouter="<IPv6网关>"
                ```

                **说明：** 为区分单个IPv6与多个IPv6地址，您只需在同一网卡标识符的基础上重复添加地址信息即可。

        3.  重启网络服务：运行`/etc/netstart restart`。

