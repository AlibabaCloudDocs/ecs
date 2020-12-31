---
keyword: [多私网IP, 弹性网卡, 绑定弹性网卡, ecs, 阿里云]
---

# 分配辅助私网IP地址

通过在一张弹性网卡（包括主网卡和辅助弹性网卡）上分配一个或多个辅助私网IP地址，能实现专有网络VPC类型ECS实例的高利用率和负载故障时的流量转移。

-   您的实例规格必须支持分配多个辅助私网IP，单块弹性网卡可分配的私有IP数量和绑定的实例规格有关，详情请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。
-   为主弹性网卡分配辅助私网IP地址时，主弹性网卡绑定的实例必须处于**运行中**或者**已停止**状态。

分配辅助私网IP地址适用于以下场景：

-   多应用场景

    如果您的ECS实例托管多个应用，您可以在弹性网卡上分配多个辅助私网IP地址。每个应用对外呈现一个独立的IP地址，提升实例的利用率。

-   故障转移

    当实例发生故障时，您可以重新绑定弹性网卡，将请求流量转移到其他备用实例上，实现故障转移。


分配辅助私网IP地址有如下使用限制：

-   单台专有网络VPC类型的安全组内的私网IP地址个数不能超过2000，主网卡和辅助网卡共享此配额。
-   一张弹性网卡最多可以分配20个私网IP地址，与网卡状态和绑定的实例规格相关。
    -   弹性网卡的状态处于**可用**时，您最多可以分配10个私网IP地址。
    -   弹性网卡的状态处于**已绑定**时，您可以分配的私网IP地址数与实例规格相关。

## 流程说明

本章节步骤同时适用于主网卡和辅助弹性网卡。

1.  在ECS管理控制台为弹性网卡分配辅助私网IP地址，具体步骤请参见[分配辅助私网IP地址](#section_bam_ihj_gsy)。

2.  在实例内部配置已分配的辅助私网IP地址。

    **说明：** 如果操作的是辅助弹性网卡，且还未绑定到ECS实例。请先完成绑定后再在实例内部配置已分配的辅助私网IP地址，绑定的操作步骤请参见[绑定弹性网卡](/intl.zh-CN/网络/弹性网卡/绑定弹性网卡.md)。

    -   Windows实例：请参见[为Windows实例配置辅助私网IP地址](#section_y4b_krk_ggb)。
    -   Linux实例：请参见[为Linux实例配置辅助私网IP地址](#section_b2x_hlb_3gb)。

## 分配辅助私网IP地址

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，单击**网络与安全** \> **弹性网卡**。

3.  在顶部菜单栏左上角处，选择地域。

4.  在网卡列表页面，找到目标弹性网卡，在**操作**列，单击**管理辅助私网IP**。

5.  在管理辅助私网IP页面，单击**分配新 IP**。

    -   自动分配：保持默认，系统会从**IPv4 私网网段**中随机分配IP地址。
    -   手动分配：手动输入辅助私网IP地址，取值在**IPv4 私网网段**内即可。
    **说明：** 完成1个IP地址的分配后，您可以再次单击**分配新 IP**进行分配。

    ![输入辅助私网IP地址](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2645459951/p47047.png)

6.  单击**确定**完成分配。


**说明：** 如果您选择了自动分配辅助私网IP地址，在**操作**列，单击**管理辅助私网IP**，可查看系统分配的辅助私网IP地址。

## 为Windows实例配置辅助私网IP地址

1.  远程连接ECS实例。连接方式请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

2.  查询ECS实例的子网掩码和默认网关。

    1.  打开**命令提示符**或**Windows PowerShell**工具。

    2.  输入`ipconfig`命令，查询ECS实例的子网掩码和默认网关。

        ```
        PS C:\Users\Administrator> ipconfig
        Windows IP 配置
        以太网适配器 以太网:
           连接特定的 DNS 后缀 . . . . . . . :
           本地链接 IPv6 地址. . . . . . . . : fe80::6c64:1601:****:****
           IPv4 地址 . . . . . . . . . . . . : 172.**.**.133
           子网掩码  . . . . . . . . . . . . : 255.255.**.**
           默认网关. . . . . . . . . . . . . : 172.**.**.253
        ```

3.  打开网络和共享中心。

4.  单击**更改适配器设置**。

5.  双击当前网络连接名，单击**属性**。

6.  双击**Internet 协议版本4（TCP/IPv4）**。

7.  选择**使用下面的IP地址**，单击**高级**。

8.  在**高级TCP/IP设置**对话框中，设置IP地址。

    1.  在**IP地址**区域，单击**添加**，输入已分配的**IP地址**和查询获取的**子网掩码**。

        您可以为同一网卡适配器重复添加多个IP地址。

        ![添加IP地址](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3645459951/p47049.png)

    2.  在**默认网关**区域，单击**添加**，输入查询获取的**默认网关**。

9.  单击**确定**。


**说明：**

如果Windows实例配置辅助私网IP地址后无法访问公网，请参见[为什么我的Windows实例设置辅助私网IP后，无法访问公网环境？](/intl.zh-CN/网络/网络FAQ.md)。

## 为Linux实例配置辅助私网IP地址

以下步骤均以主弹性网卡eth0为操作示例，如果您使用的是辅助弹性网卡，请根据实际情况修改网卡标识符。

1.  远程连接ECS实例。连接方式请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

2.  使用`ifconfig`命令查询ECS实例的子网掩码和默认网关。

    ```
    [root@ecs ~]# ifconfig
    eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 172.16.**.**  netmask 255.255.**.**  broadcast 172.16.**.**
            inet6 fe80::216:3eff:****:****  prefixlen 64  scopeid 0x20<link>
            ether 00:16:3e:0e:**:**  txqueuelen 1000  (Ethernet)
            RX packets 27146  bytes 39146111 (37.3 MiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 6038  bytes 509398 (497.4 KiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    ```

    **说明：** 如果部分Linux发行版不支持`ifconfig`命令，可以使用`ip addr show`命令。

3.  根据实例操作系统，选择配置辅助私网IP地址的方式。

    -   RHEL系列：CentOS 6/7、Red Hat 6/7、Alibaba Cloud Linux 2
        1.  打开网络配置文件。
            -   单IP地址运行`vi /etc/sysconfig/network-scripts/ifcfg-eth0:0`命令，添加如下配置项。

                ```
                DEVICE=eth0:0
                TYPE=Ethernet
                BOOTPROTO=static
                ONBOOT=yes
                IPADDR=<IPv4地址1>
                NETMASK=<IPv4掩码>
                GATEWAY=<IPv4网关>
                ```

            -   多IP地址运行`vi /etc/sysconfig/network-scripts/ifcfg-eth0:1`命令，添加如下配置项。

                ```
                DEVICE=eth0:1
                TYPE=Ethernet
                BOOTPROTO=static
                ONBOOT=yes
                IPADDR=<IPv4地址2>
                NETMASK=<IPv4掩码>
                GATEWAY=<IPv4网关>
                ```

        2.  运行`service network restart`或`systemctl restart network`命令重启网络服务。
    -   Debian系列：Ubuntu 14/16、Debian/8/9
        1.  运行`vi /etc/network/interfaces`命令打开网络配置文件，添加如下配置项。

            ```
            auto eth0:0
            iface eth0:0 inet static
            address <IPv4地址1>
            netmask <IPv4掩码>
            gateway <IPv4网关>
            
            auto eth0:1
            iface eth0:1 inet static
            address <IPv4地址2>
            netmask <IPv4掩码>
            gateway <IPv4网关>
            ```

        2.  运行`service networking restart`或`systemctl restart networking`命令重启网络服务。
    -   SLES系列：SUSE 11/12、OpenSUSE 42
        1.  运行`vi /etc/sysconfig/network/ifcfg-eth0`命令打开网络配置文件，添加如下配置项：

            ```
            IPADDR_0=<IPv4地址1>
            NETMASK_0=<子网前缀长度>
            LABEL_0='0'
            
            IPADDR_1=<IPv4地址2>
            NETMASK_1=<子网前缀长度>
            LABEL_1='1'
            ```

        2.  运行`service network restart`或`systemctl restart network`命令重启网络服务。

**相关文档**  


[AssignPrivateIpAddresses](/intl.zh-CN/API参考/弹性网卡/AssignPrivateIpAddresses.md)

