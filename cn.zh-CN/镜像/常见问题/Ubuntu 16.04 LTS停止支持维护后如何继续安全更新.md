# Ubuntu 16.04 LTS停止支持维护后如何继续安全更新

2021年04月，Ubuntu 16.04 LTS（Xenial Xerus）将停止为期5年的标准支持维护，同时阿里云也将停止Ubuntu 16.04 LTS公共镜像的更新。Ubuntu 16.04 LTS后续将过渡到扩展安全维护（ESM）的阶段。您可以参考本文的操作，通过Ubuntu订阅服务（UA-I）为Ubuntu 16.04实例获取ESM更新支持。

当Ubuntu 16.04 LTS处于扩展安全维护（ESM）阶段时，您可以通过Ubuntu订阅服务（UA-I）内的扩展安全维护（ESM），继续获取基础操作系统、关键软件包和基础设置组件的安全更新。更多信息，请参见[Ubuntu Advantage for Infrastructure](https://ubuntu.com/advantage)以及[Extended Security Maintenance](https://ubuntu.com/security/esm)。

如果您需要在Ubuntu 16.04实例中继续获取操作系统的安全更新，请参见以下操作步骤。

## 步骤一：在Ubuntu官网订阅UA-I服务

1.  在本地主机，访问[Ububtu官网](https://ubuntu.com/)（`https//ubuntu.com`）。

2.  在顶部菜单栏，单击**Sign in**。

    您需要使用Ubuntu账号登录，如果您没有Ubuntu账号，需要根据实际的页面提示完成注册并登录Ubuntu官网。

3.  在顶部菜单栏，单击Ubuntu账号的用户名，然后单击**UA subscriptions**。

    ![ubuntu订阅uai](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3411444261/p286706.png)

4.  在**Your free personal subscription**区域，单击**Get your free token**。

    ![get free token](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3411444261/p286709.png)

    您需要自行保存**To attach a machine**后的命令信息。


## 步骤二：在Ubuntu 16.04实例中添加UA-I并进行安全更新

1.  远程连接Ubuntu 16.04实例。

    具体操作，请参见[连接方式概述](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  依次运行以下命令，安装Ubuntu最新的Ubuntu Advantage（UA）客户端。

    1.  升级软件包。

        ```
        sudo apt update
        ```

    2.  安装UA客户端。

        ```
        sudo apt install ubuntu-advantage-tools
        ```

3.  运行步骤一中保存的**To attach a machine**命令。

    命令格式如下所示，您需要将<token\>替换为实际保存的数值。

    ```
    sudo ua attach <token\>
    ```

    如下图所示，表示已启用ESM。

    ![esm-infra](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3411444261/p286721.png)

4.  运行以下命令，启用ESM。

    如果您不确定ESM是否启用，可以运行以下命令确保ESM已启用。

    ```
    sudo ua enable esm-infra
    ```

5.  依次运行以下命令，升级软件包并更新安全补丁。

    1.  升级软件包。

        ```
        sudo apt update
        ```

    2.  更新安全补丁。

        ```
        sudo apt upgrade 
        ```


