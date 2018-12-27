# 为Windows实例配置静态IPv6地址 {#concept_s2s_4fx_yfb .concept}

本文描述了如何通过网络连接管理为 Windows 实例配置静态 IPv6 地址。

## 前提条件 {#section_z1h_2ww_yfb .section}

您已经为实例配置了 IPv6 服务。更多详情，请参阅 [为Windows实例配置IPv6服务](cn.zh-CN/用户指南/配置IPv6地址/为Windows实例配置IPv6服务.md#)。

## 步骤 1：查询实例的 IPv6 地址 {#section_nw4_lww_yfb .section}

您可以通过控制台和实例元数据查看实例分配的 IPv6 地址。

控制台操作请参阅 [创建实例时配置 IPv6 地址](cn.zh-CN/用户指南/配置IPv6地址/创建实例时配置IPv6地址.md#)。

实例元数据请参阅 [实例元数据](cn.zh-CN/用户指南/实例/实例自定义数据和元数据/实例元数据.md#)，并通过以下元数据项获取 IPv6 地址：

-   IPv6 地址：network/interfaces/macs/\[mac\]/ipv6s
-   IPv6 网关：network/interfaces/macs/\[mac\]/ipv6-gateway
-   IPv6 虚拟交换机 CIDR 地址段：network/interfaces/macs/\[mac\]/vswitch-ipv6-cidr-block

**具体操作方式如下：**

打开 **PowerShell**，首先运行如下语句获取 MAC 信息：

```powershell
Invoke-RestMethod http://100.100.100.200/2016-01-01/meta-data/mac
```

例如返回：`00:16:3e:00:24:64` 后续使用 `00:16:3e:00:24:64` 代替 `[mac]`

获取 IPv6 地址和 IPv6 网关：

```powershell
Invoke-RestMethod http://100.100.100.200/2016-01-01/meta-data/network/interfaces/macs/[返回的mac地址]/ipv6s
Invoke-RestMethod http://100.100.100.200/2016-01-01/meta-data/network/interfaces/[返回的mac地址]/00:16:3e:00:24:64/ipv6s
```


## 步骤 2：配置静态 IPv6 地址 {#section_lxr_2jx_yfb .section}

**Windows Server 2008/2012/2016 操作步骤**

本文以 Windows Server 2008 实例为例，为您示范如何加载 IPv6 服务组件。同样的配置流程适用于 Windows Server 2012 和 Windows Server 2016：

1.  远程连接实例。

2.  选择 **控制面板** \> **网络**。

3.  单击当前网络连接名，打开状态界面，再单击 **属性**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154390910433462_zh-CN.png)

4.  选择 **IPv6协议** \> **属性**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/66243/154390910433501_zh-CN.png)

5.  勾选 **使用以下 IPv6 地址**，并填入 IPv6 地址、子网前缀长度和 IPv6 网关，点击 **确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/66243/154390910433502_zh-CN.png)

6.  （可选）绑定多个 IPv6 地址：在Internet 协议版本 6（TCP/IP）属性，点击 **高级** 打开高级设置界面，单击 **添加** 做批量处理。完成后单击 **确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/66243/154390910433503_zh-CN.png)


**Windows Server 2003 操作步骤**

1.  远程连接实例。

2.  选择 **控制面板** \> **网络连接**，查看当前网络连接名，假设为 **本地连接 2**。

3.  打开 Windows 命令处理程序 CMD。

4.  （单个 IPv6 地址）运行以下命令添加 IPv6 地址：

    ```
    netsh interface ipv6 add address "本地连接 2" <IPv6地址>
    ```

5.  （多个 IPv6 地址）运行以下命令添加 IPv6 地址：

    ```
    netsh interface ipv6 add address "本地连接 2" <IPv6地址1>
    netsh interface ipv6 add address "本地连接 2" <IPv6地址2>
    ```

6.  运行以下命令添加默认路由：

```
netsh interface ipv6 add route ::/0 "本地连接 2" <IPv6网关>
```
