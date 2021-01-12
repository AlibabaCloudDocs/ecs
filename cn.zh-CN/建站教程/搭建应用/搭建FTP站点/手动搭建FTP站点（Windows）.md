# 手动搭建FTP站点（Windows）

本文介绍了如何使用Windows实例搭建FTP站点。此方法适用于Windows Server 2008及以上系统，本文以Windows Server 2012 R2为例。

-   使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。

-   已创建ECS实例，本教程中使用的资源信息如下。
    -   实例规格：ecs.c6.large
    -   操作系统：Windows Server 2012 R2 64位

## 操作步骤

Windows实例搭建FTP站点的具体操作步骤如下：

1.  [步骤一：添加IIS以及FTP服务角色](#section_qx9_w5k_gvc)
2.  [步骤二：创建FTP用户名及密码](#section_ztx_c4b_edr)
3.  [步骤三：设置共享文件的权限](#section_jd9_tsn_noi)
4.  [步骤四：添加及设置FTP站点](#section_0gy_5s5_oku)
5.  [步骤五：设置安全组及防火墙](#section_ovb_r91_w7d)
6.  [步骤六：客户端测试](#section_xex_vgd_epn)

## 步骤一：添加IIS以及FTP服务角色

在创建FTP站点前，首先需要安装IIS及FTP服务。

1.  远程连接Windows实例。具体操作，请参见[在本地客户端上连接Windows实例](/cn.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md)。

2.  在底部任务栏，单击**服务器管理器**图标。

    ![ftp0](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3512649951/p92900.png)

3.  在顶部导航栏，单击**管理** \> **添加角色和功能**。

    ![ftp1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3512649951/p92893.png)

4.  在弹出的对话框中，默认单击**下一步**到选择服务器角色界面。

5.  选中**Web 服务器（IIS）**，在弹出的对话框中单击**添加功能**，然后单击**下一步**。

    ![ftp2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3512649951/p92895.png)

6.  在选择角色服务界面。选中**IIS管理控制台**以及**FTP 服务器**，单击**下一步**。

    ![ftp3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3512649951/p92899.png)

7.  单击**安装**。


## 步骤二：创建FTP用户名及密码

完成以下操作，创建Windows用户名和密码，用于FTP使用。如果您希望匿名用户可以访问，可省略此步骤。

1.  在底部任务栏，单击**开始**图标。

2.  单击**管理工具**，然后双击**计算机管理**。

3.  在左侧导航栏单击**本地用户和组** \> **用户**。

    ![ftp4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3512649951/p92902.png)

4.  在中间空白处单击鼠标右键，并选择**新用户**。

    本示例中用户名使用ftptest。

    **说明：** 密码必须包括大写字母、小写字母和数字。否则会显示无法通过密码策略。

    ![ftp5](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3512649951/p92906.png)


## 步骤三：设置共享文件的权限

您需要为在FTP站点共享给用户的文件夹设置访问和修改等权限。

1.  在服务器磁盘上创建一个供FTP使用的文件夹。右键单击文件夹，选择**属性**。

    本示例中，在C盘下创建一个名为ftp的文件夹。

2.  单击**安全**页签，然后单击**编辑**。

3.  单击**添加**。

4.  在弹出的对话框中，输入对象名称ftptest，然后单击**确定**。

5.  在**组或用户名**区域，单击刚刚添加的用户名**ftptest**，然后根据需要，选择**ftptest**的权限，并单击**确定**。

    本示例中允许所有权限。

    ![username](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3512649951/p126888.png)


## 步骤四：添加及设置FTP站点

安装FTP，设置好共享文件夹权限后，您需要创建FTP站点。

1.  在底部任务栏，单击**服务器管理器**图标。

2.  在顶部导航栏，单击**工具** \> **Internet Information Services\(IIS\)管理器**。

    ![ftp8](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3512649951/p92919.png)

3.  在左侧导航栏右键单击**网站**，并单击**添加FTP站点...**。

    ![ftp9](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3512649951/p92920.png)

4.  在弹出的对话框中，填写**FTP站点名称**与共享文件夹的**物理路径**，然后单击**下一步**。

    本示例中**FTP 站点名称**设置为ftptest，**物理路径**请选择在[步骤三：设置共享文件的权限](#section_jd9_tsn_noi)中创建的FTP文件夹路径。

    ![10](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4512649951/p92932.png)

5.  **IP 地址**默认选择**全部未分配**。端口号可自行设置，FTP默认端口号为21。

6.  选择SSL设置，然后单击**下一步**。

    -   **允许**：允许FTP服务器支持与客户端的非SSL和SSL连接。
    -   **需要**：需要对FTP服务器和客户端之间的通信进行SSL加密。
    -   **无**：不需要SSL加密。
    ![ftp11](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4512649951/p92936.png)

7.  选择要使用的一种或多种身份验证方法。

    -   **匿名**：允许任何仅提供用户名**anonymous**或**ftp**的用户访问内容。
    -   **基本**：需要用户提供有效用户名和密码才能访问内容。由于基本身份验证通过网络传输未加密的密码，因此请仅在清楚客户端和FTP服务器之间的连接是安全的情况下（例如，使用安全套接字层SSL时）使用此身份验证方法。
8.  从**允许访问**列表中，选择以下选项之一：

    -   **所有用户**：所有用户（不论是匿名用户还是已标识的用户）均可访问相应内容。
    -   **匿名用户**：匿名用户可访问相应内容。
    -   **指定角色或用户组**：仅特定角色或用户组的成员才能访问相应内容。请在对应的文本框中输入角色或用户组。
    -   **指定用户**：仅指定用户才能访问相应内容。请在对应的文本框中输入用户名。
9.  选中经过授权的用户的**读取**和**写入**权限。然后单击**完成**。

    ![12](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4512649951/p92937.png)


完成后可以看到搭建的FTP站点。

![13](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4512649951/p92938.png)

## 步骤五：设置安全组及防火墙

1.  搭建好FTP站点后，您需要在实例安全组的入方向添加规则，放行FTP服务器21端口及FTP服务器被动1024/65535端口。

    具体步骤请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)，具体配置请参见[安全组应用案例](/cn.zh-CN/安全/安全组/安全组应用案例.md)和[常用端口](/cn.zh-CN/安全/安全组/常用端口.md)。

2.  服务器防火墙默认为关闭状态。如果您的防火墙为开启状态，则需要放行TCP 21与1024/65535端口用于FTP服务。

    具体操作，请参见[设置 ECS 实例远程连接防火墙](http://help.aliyun.com/document_detail/40858.html)。

    其他防火墙设置请参见[微软官方文档](https://technet.microsoft.com/zh-cn/library/hh831655(v=ws.11).aspx#Step4)。


## 步骤六：客户端测试

FTP工具、Windows命令行工具或浏览器均可用来测试FTP服务器。本教程以Google Chrome浏览器为例，介绍FTP服务器的访问步骤。

1.  打开客户端的Google Chrome浏览器，访问`ftp://实例公网IP地址:21`（如果不填端口则默认访问21端口）。

    **说明：** 使用浏览器访问FTP服务器出错时，建议您清除浏览器缓存后再尝试。

2.  在弹出的对话框中，输入用户名**ftptest**和对应的密码，即可对FTP文件进行相应权限的操作。

    浏览器中只能对文件进行读取操作，因此建议您使用FTP工具进行操作，例如，FileZilla。

    **说明：** 此步骤仅适用于基本身份验证，匿名用户无需输入用户名和密码即可登录FTP服务器。


您可以对FTP服务进行安全加固。详情请参见[安全加固方案](https://help.aliyun.com/knowledge_detail/37452.html)。

如果您想基于FTP协议来管理存储在OSS上的文件，您可以安装OSS FTP。具体操作，请参见[安装OSS FTP](/cn.zh-CN/常用工具/ossftp/概述.md)。OSS FTP接收普通FTP请求后，将对文件、文件夹的操作映射为对OSS的操作。

