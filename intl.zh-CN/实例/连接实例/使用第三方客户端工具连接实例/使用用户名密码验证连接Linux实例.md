---
keyword: [远程连接, ssh, linux, 登录, ecs, shell]
---

# 使用用户名密码验证连接Linux实例

在Windows、Linux、MacOS、Android、iOS等环境中，您可以使用用户名密码验证的方式远程连接Linux实例。

-   已创建实例。
-   已为实例设置登录密码。
-   已为实例分配固定公网IP或绑定EIP。
-   实例处于运行中状态。
-   为实例所在的安全组添加安全组规则，放行对相应端口的访问，具体操作请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|优先级|授权类型|授权对象|
    |----|----|----|----|----|----|---|----|----|
    |专有网络VPC|无需配置|入方向|允许|SSH（22）|22/22|1|IPv4地址段访问|0.0.0.0/0|
    |经典网络|公网|


根据本地设备的操作系统，您可以通过不同的方式使用用户名密码远程连接Linux实例：

-   [在Windows环境中使用用户名密码验证](#section_k1p_o74_bwm)
-   [在Linux或Mac OS X环境中使用用户名密码验证](#section_zo7_ddd_8yk)
-   [在Android或iOS环境中使用用户名密码验证](#section_x5j_164_ejd)

## 在Windows环境中使用用户名密码验证

下面以PuTTY为例介绍如何使用用户名密码验证连接Linux实例。

1.  下载并安装PuTTY。

    下载链接：[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)。

2.  启动PuTTY。

3.  配置连接Linux实例所需的信息。

    -   **Host Name \(or IP address\)**：输入实例的固定公网IP或EIP。
    -   **Port**：输入**22**。
    -   **Connection Type**：选择**SSH**。
    -   （可选）**Saved Sessions**：输入一个便于识别的名称，然后单击**Save**即可保存会话，下次登录时无需输入公网IP等信息。

        ![Saved Session](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2904359951/p5249.gif)

4.  单击**Open**。

    首次连接时会出现**PuTTY Security Alert**警告，表示PuTTY无法确认远程服务器的真实性，只能提供服务器的公钥指纹。选择**是**，表示您信任该服务器，PuTTY会将公钥指纹加入到本地设备的注册表中。

    **说明：** 如果后续登录时再次弹出**PuTTY Security Alert**警告，表示实例可能遭受了[中间人攻击](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)。更多警告相关信息，请参见[PuTTY官网文档](https://the.earth.li/~sgtatham/putty/0.70/htmldoc/Chapter2.html#gs-hostkey)。

    ![PuTTY无法确认远程服务器（实例）的真实性](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3904359951/p5251.png)

5.  输入用户名（默认为root），然后按回车键。

6.  输入实例登录密码，然后按回车键。

    输入完成后按回车键即可，登录Linux实例时界面不会显示密码的输入过程。

    如果出现`Welcome to Alibaba Cloud Elastic Compute Service !`，表示成功连接到实例。


## 在Linux或Mac OS X环境中使用用户名密码验证

1.  输入SSH命令。

    ```
    ssh root@<实例的固定公网IP或EIP>
    ```

    示例如下：

    ```
    ssh root@47.99.XX.XX
    ```

2.  输入实例登录密码。

    如果出现`Welcome to Alibaba Cloud Elastic Compute Service !`，表示成功连接到实例。


## 在Android或iOS环境中使用用户名密码验证

具体操作请参见[在移动设备上连接Linux实例](/intl.zh-CN/实例/连接实例/使用Workbench连接实例/在移动设备上连接Linux实例.md)。

