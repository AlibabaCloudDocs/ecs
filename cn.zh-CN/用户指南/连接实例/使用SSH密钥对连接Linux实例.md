# 使用SSH密钥对连接Linux实例 {#concept_ucj_wrx_wdb .concept}

本文介绍了在以下环境中您如何使用SSH密钥对登录Linux实例。

-   [本地为Windows环境](#windows)
-   [本地为Linux或支持SSH命令的环境](#linux)

**说明：** 您也可以使用用户名密码验证连接Linux实例。具体操作，请参见 [使用用户名密码验证连接 Linux 实例](cn.zh-CN/用户指南/连接实例/使用用户名密码验证连接 Linux 实例.md#) 和 [使用管理终端连接 ECS 实例](cn.zh-CN/用户指南/连接实例/使用管理终端连接 ECS 实例.md#)。

## 本地为Windows环境 {#windows .section}

这里以PuTTY和PuTTYgen为例，说明怎样在Windows环境里使用由阿里云生成的密钥对在SSH远程连接工具中登录Linux实例。

**前提条件**

-   您应该已经下载并安装了PuTTY和PuTTYgen。PuTTY和PuTTYgen的下载地址：

    -   PuTTY：[https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe)
    -   PuTTYgen：[https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe](https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe)
-   您应该已经拥有一台分配了密钥对的Linux实例。您可以在创建ECS实例时分配密钥对，也可以为实例 [绑定 / 解绑 SSH 密钥对](cn.zh-CN/用户指南/密钥对/绑定 / 解绑 SSH 密钥对.md#)。

-   实例所在的安全组必须添加以下安全组规则。具体操作，请参见 [添加安全组规则](cn.zh-CN/用户指南/安全组/添加安全组规则.md#)。

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
    |----|----|----|----|----|----|----|----|---|
    |VPC|不需要配置|入方向|允许|SSH\(22\)|22/22|地址段访问|0.0.0.0/0|1|
    |经典网络|公网|


**操作步骤**

1.  （可选）如果您正在使用阿里云生成的.pem私钥文件，必须先按以下步骤转为.ppk私钥文件。如果您使用的私钥文件本身已经是.ppk文件，可以略过这一步。

    **说明：** 在 [创建 SSH 密钥对](cn.zh-CN/用户指南/密钥对/创建 SSH 密钥对.md#) 时下载.pem私钥文件。

    1.  启动PuTTYgen。本示例中的PuTTYgen版本为 0.68。
    2.  在 **Parameters** \> **Type of key to generate** 中，选中 RSA。

        **说明：** **Number of bits in a generated key** 的值不需要设置，软件会根据导入的私钥信息自动更新。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/5187_zh-CN.png)

    3.  单击 **Load**，选择显示所有类型的文件，找到您的 .pem 文件。

        **说明：** PuTTYgen默认仅显示扩展名为 .ppk 的文件。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/5188_zh-CN.png)

    4.  选择您从阿里云下载的.pem格式的私钥文件，然后单击 **打开**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/5189_zh-CN.png)

    5.  单击 **OK**（确定）关闭确认对话框。
    6.  单击 **Save private key**。PuTTYgen会显示一条关于在没有口令的情况下保存密钥的警告，单击 **是\(Y\)**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/5190_zh-CN.png)

    7.  指定与密钥对相同的私钥名称，保存。PuTTY会自动为文件添加.ppk扩展名。
2.  启动PuTTY。
3.  选择 **Connection** \> **SSH** \> **Auth**，再单击 **Browse…**，选择前面所生成的.ppk文件。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/5191_zh-CN.png)

4.  单击 **Session**。
    -   在 Host Name \(or IP address\) 里输入账号和需要连接的实例公网IP地址，格式为 root@IP 地址。
    -   在 Port 里输入端口号 22。
    -   Connection type 选择 SSH。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/5192_zh-CN.png)

5.  单击 **Open**，开始连接您的Linux实例。

当页面上出现 `Connection established.` 时，说明您已经成功地使用密钥对登录实例。

## 本地为Linux或支持SSH命令的环境 {#linux .section}

这里说明怎样在Linux或其他支持SSH命令的环境（如Windows下的MobaXterm）下使用SSH密钥对登录Linux实例。

**前提条件**

您应该已经拥有一个分配了密钥对的Linux实例。您可以在 [步骤 2：创建ECS实例](../../../../cn.zh-CN/个人版快速入门/步骤 2：创建ECS实例.md#)，也可以为实例[绑定 / 解绑 SSH 密钥对](cn.zh-CN/用户指南/密钥对/绑定 / 解绑 SSH 密钥对.md#)。

实例所在的安全组必须添加以下安全组规则。具体操作，请参见 [添加安全组规则](cn.zh-CN/用户指南/安全组/添加安全组规则.md#)。

|网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
|----|----|----|----|----|----|----|----|---|
|VPC|不需要配置|入方向|允许|SSH\(22\)|22/22|地址段访问|0.0.0.0/0|1|
|经典网络|公网|

**操作步骤**

1.  找到您所下载的.pem私钥文件在本地机上的存储路径，如 /root/xxx.pem。

    **说明：** 在 [创建 SSH 密钥对](cn.zh-CN/用户指南/密钥对/创建 SSH 密钥对.md#) 时下载.pem私钥文件。xxx.pem即为您的私钥文件，下同。

2.  运行命令修改私钥文件的属性：`chmod 400 [.pem私钥文件在本地机上的存储路径]`。例如， `chmod 400 /root/xxx.pem`。
3.  运行命令连接至实例：`ssh -i [.pem私钥文件在本地机上的存储路径] root@[公网IP地址]`。例如， `ssh -i /root/xxx.pem root@10.10.10.100`。

**通过SSH配置简化连接命令**

进入用户根目录的ssh目录，修改其中的config文件如下:

```
Host ecs    // ecs服务器的别名
HostName 192.168.211.218 // ecs服务器的公网地址
Port 1022   // 端口
User root   // 登录账号
IdentityFile ~/.ssh/ecs.pem // .pem私钥在本机的地址
```

保存config后，重启ssh。以后连接ECS服务器只需输入如下命令即可：`ssh [ecs别名]`。例如，`ssh ecs`。





