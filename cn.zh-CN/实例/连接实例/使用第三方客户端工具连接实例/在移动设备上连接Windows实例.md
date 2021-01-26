---
keyword: [阿里云, ecs, 服务器, 弹性计算]
---

# 在移动设备上连接Windows实例

本文以微软公司发行的Microsoft Remote Desktop为例，介绍如何在Android设备上连接Windows系统ECS实例。

在连接实例之前，您需要确认以下事项：

-   实例处于**运行中**状态。
-   实例拥有公网IP地址，允许公网访问。
-   您已经设置了实例的登录密码。如果您遗忘了密码，请参见[重置实例登录密码](/cn.zh-CN/实例/管理实例/重置实例登录密码.md)。
-   您已经安装了Microsoft Remote Desktop。如需下载软件，请访问[微软官方网站](https://www.microsoft.com/en-us/p/microsoft-remote-desktop/9wzdncrfj3ps)。
-   您已经为实例所在的安全组添加如下安全组规则。具体操作，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
    |:---|:---|:---|:---|:---|:---|:---|:---|:--|
    |VPC 网络|不需要配置|入方向|允许|RDP \(3389\)|3389/3389|地址段访问|0.0.0.0/0|1|
    |经典网络|公网|

-   如果使用非管理员用户登录Windows实例，该用户必须属于Remote Desktop Users组。

1.  启动RD Client。

2.  在**远程桌面**页面右上角，单击**+**图标。

    ![远程桌面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3014359951/p5327.png)

3.  在**Add New**页面，选择**桌面**。

    ![Add New](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3014359951/p5329.png)

4.  在**编辑桌面**页面，设置连接信息后，单击**保存**。

    需要设置的Windows实例的连接信息包括：

    -   **PC 名称**：公网IP地址。
    -   **用户帐户**：用户名（例如**administrator**）以及实例登录密码。

        ![编辑桌面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3014359951/p5330.png)

5.  在**远程桌面**页面，单击需要连接的Windows实例图标。

    ![远程桌面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3014359951/p5331.png)

6.  在验证确认页面，确认信息后，单击**接受**。

    ![验证确认页面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3014359951/p5332.png)


您成功连接到Windows实例。

![成功连接到Windows实例](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3014359951/p5333.png)

**相关文档**  


[连接方式概述](/cn.zh-CN/实例/连接实例/连接方式概述.md)

