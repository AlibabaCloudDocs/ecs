# 使用SSH密钥对连接Linux实例

SSH密钥对是一种安全便捷的登录认证方式。在Windows环境和支持SSH命令的环境（例如Linux环境、Windows下的MobaXterm）中，您均可以使用SSH密钥对连接Linux实例。

-   已创建密钥对并下载.pem私钥文件，具体操作请参见[创建SSH密钥对](/intl.zh-CN/安全/SSH密钥对/使用SSH密钥对/创建SSH密钥对.md)。
-   实例处于运行中状态。
-   已为实例绑定密钥对。
-   已为实例分配固定公网IP或EIP。
-   已为实例所在的安全组添加安全组规则，并放行对相应端口（例如SSH协议默认的22端口）的访问，具体操作请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|优先级|授权类型|授权对象|
    |----|----|----|----|----|----|---|----|----|
    |专有网络VPC|无需配置|入方向|允许|SSH\(22\)|22/22|1|IPv4地址段访问|0.0.0.0/0|
    |经典网络|公网|


## 在Windows环境中使用密钥对

本节以PuTTYgen为例介绍如何将私钥文件格式从.pem转换为.ppk，并以PuTTY为例介绍如何使用密钥对连接Linux实例。

1.  下载并安装PuTTYgen和PuTTY。

    下载链接如下：

    -   [PuTTYgen](https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe)
    -   [PuTTY](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe)
2.  将.pem私钥文件转换为.ppk私钥文件。

    1.  启动PuTTYgen。

        本示例中的PuTTYgen版本为0.71。

    2.  选择**Type of key to generate**为**RSA**，然后单击**Load**。

        ![windows_puttygen_1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1904359951/p51179.png)

    3.  选择**All Files**。

        ![windows_puttygen_2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1904359951/p5188.png)

    4.  选择待转换的.pem私钥文件。

    5.  在弹出的对话框中，单击**确定**。

    6.  单击**Save private key**。

    7.  在弹出的对话框中，单击**是**。

    8.  指定.ppk私钥文件的名称，然后单击**保存**。

3.  启动PuTTY。

4.  配置用于身份验证的私钥文件。

    1.  选择**Connection** \> **SSH** \> **Auth**。

    2.  单击**Browse…**。

    3.  选择转换好的.ppk私钥文件。

    ![windows_putty_3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1904359951/p5191.png)

5.  配置连接Linux实例所需的信息。

    1.  单击**Session**。

    2.  在**Host Name \(or IP address\)**中输入登录账号和实例公网IP地址。

        格式为**root@IP 地址**，例如root@10.10.xx.xxx。

    3.  在**Port**中输入端口号**22**。

    4.  选择**Connection type**为**SSH**。

    ![windows_putty_4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1904359951/p5192.png)

6.  单击**Open**。

    当出现以下提示时，说明您已经成功地使用SSH密钥对登录了实例。

    ![windows_putty_5](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1904359951/p51203.png)


## 在支持SSH命令的环境中使用密钥对（通过命令配置信息）

本节介绍如何在支持SSH命令的环境（例如Linux、Windows下的MobaXterm）中通过命令配置所需信息，并通过SSH命令登录Linux实例。

1.  找到.pem私钥文件在本地机上的存储路径，例如~/.ssh/ecs.pem。

    此处路径和文件名称仅为示例，在后续命令中请根据实际情况修改。

2.  运行以下命令修改私钥文件的属性。

    ```
    chmod 400 [.pem私钥文件在本地机上的存储路径]
    ```

    示例如下：

    ```
    chmod 400 ~/.ssh/ecs.pem
    ```

3.  运行以下命令连接至实例。

    ```
    ssh -i [.pem私钥文件在本地机上的存储路径] root@[公网IP地址]
    ```

    示例如下：

    ```
    ssh -i ~/.ssh/ecs.pem root@10.10.xx.xxx
    ```


## 在支持SSH命令的环境中使用密钥对（通过config文件配置信息）

本节介绍如何在支持SSH命令的环境（例如Linux、Windows下的MobaXterm）中通过命令配置所需信息，并通过SSH命令登录Linux实例。

1.  找到.pem私钥文件在本地机上的存储路径，例如~/.ssh/ecs.pem。

    此处路径和文件名称仅为示例，在后续命令中请根据实际情况修改。

2.  运行以下命令修改私钥文件的属性。

    ```
    chmod 400 [.pem私钥文件在本地机上的存储路径]
    ```

    示例如下：

    ```
    chmod 400 ~/.ssh/ecs.pem
    ```

3.  运行以下命令，进入用户主目录下的.ssh目录，并创建config文件。

    ```
    cd ~/.ssh
    vim config
    ```

4.  在`config`配置文件内，按i进入编辑模式，添加如下配置项。

    ```
    # 输入ECS实例的别名，用户SSH远程连接。
    Host ecs
    # 输入ECS实例的公网IP地址。
    HostName 121.196.**.**
    # 输入端口号，默认为22。
    Port 22
    # 输入登录账号。
    User root
    # 输入.pem私钥文件在本机的地址。
    IdentityFile ~/.ssh/ecs.pem
    ```

    如果您有多台ECS实例，也可以通过`config`配置文件，统一进行免密登录的配置。配置两台ECS实例的示例内容如下：

    ```
    # 输入ECS实例的别名，用户SSH远程连接。
    Host ecs1
    # 输入ECS实例的公网IP地址。
    HostName 121.196.**.**
    # 输入端口号，默认为22。
    Port 22
    # 输入登录账号。
    User root
    # 输入.pem私钥文件在本机的地址。
    IdentityFile ~/.ssh/ecs.pem
    
    # 输入ECS实例的别名，用户SSH远程连接。
    Host ecs2
    # 输入ECS实例的公网IP地址。
    HostName 121.196.**.**
    # 输入端口号，默认为22。
    Port 22
    # 输入登录账号。
    User root
    # 输入.pem私钥文件在本机的地址。
    IdentityFile ~/.ssh/ecs.pem
    ```

    添加完成后，按Ecs键，并输入`:wq`保存config文件。

5.  运行以下命令，重启SSH服务。

    ```
    service sshd restart
    ```

6.  运行命令连接至实例。

    ```
    ssh [ECS实例的别名]
    ```

    示例如下：

    ```
    ssh ecs
    ```


