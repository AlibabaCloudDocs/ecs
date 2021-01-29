# 设置网卡MTU值

最大传输单元MTU（Maximum Transmission Unit）决定了单次可传输数据包的最大尺寸，本文介绍如何使用ecs-utils-jumboframe脚本为ECS实例的网卡设置MTU值。

建议将网络MTU值与本地MTU值设置为一致，可以充分利用单次传输数据包大小的上限，同时避免因数据包过大而必须拆分数据包导致的额外时间消耗。

**说明：** ecs-utils-jumboframe脚本中没有直接调用重启网卡或者网络服务的指令，但不同系统中可能使用不同类型的网络服务和网卡驱动，不能完全排除出现瞬时网络断流的可能。如果您的业务严格要求实时网络不能中断，请参考脚本内容慎重评估后再决定是否使用。

## 使用限制

-   仅VPC实例支持使用ecs-utils-jumboframe脚本，且ecs-utils-jumboframe脚本依赖实例元数据服务检测实例规格是否支持Jumbo Frame特性。使用该脚本前请勿禁用网络和实例元数据服务相关端口（100.100.100.200:80）。
-   目前仅7代高主频实例（hfg7、hfc7、hfr7）支持Jumbo Frame特性，允许设置的网卡MTU值上限为8500。ecs-utils-jumboframe脚本会根据实例规格判断允许设置的MTU值上限，您也可以使用该脚本为其它实例规格设置网卡MTU值，但上限为1500。
-   Jumbo Frame特性仅限同VPC内7代高主频实例之间使用TCP协议直接通信的场景，不支持经过SLB等其他中间节点。

## 在Linux实例中设置网卡MTU值

确保Linux实例的镜像为以下版本之一：

-   CentOS 6.x、CentOS 7.x、CentOS 8.x
-   Debian 9.x、Debian 10.x
-   SUSE Linux Enterprise Server 15
-   Ubuntu 16.x、18.x、20.x

1.  [远程连接ECS实例](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  下载ecs-utils-jumboframe-linux.sh脚本。

    ```
    wget https://ecs-image-tools.oss-cn-hangzhou.aliyuncs.com/jumboframe/ecs-utils-jumboframe-linux.sh
    ```

3.  赋予脚本可执行权限。

    ```
    chmod +x ./ecs-utils-jumboframe-linux.sh
    ```

    您可以执行`./ecs-utils-jumboframe-linux.sh -h`查看帮助信息。

    ![help](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0438201161/p225163.png)

4.  查看系统网卡设备列表和网卡的当前MTU值。

    ```
    ip addr show
    ```

    ![origin-mtu](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2880881161/p225866.png)

5.  设置网卡MTU值。

    -   临时设置MTU值：如果您需要临时测试Jumbo Frame特性，可以临时设置网卡MTU值，重启ECS实例后网卡MTU值会恢复默认设置。格式如下：

        ```
        ./ecs-utils-jumboframe-linux.sh <网卡> <目标MTU值>
        ```

        例如，将eth0网卡的MTU值临时设置为8500：

        ```
        ./ecs-utils-jumboframe-linux.sh eth0 8500
        ```

    -   永久设置MTU值：如果您需要永久启用Jumbo Frame特性，在设置网卡MTU值时指定模式即可。永久设置完成后，重启ECS实例后网卡MTU值仍保持您设置的值。格式如下：

        ```
        ./ecs-utils-jumboframe-linux.sh -p <网卡> <目标MTU值>
        ```

        例如，将eth0网卡的MTU值永久设置为8500：

        ```
        ./ecs-utils-jumboframe-linux.sh -p eth0 8500
        ```

    设置完成后，您可以执行`ip addr show`查看网卡信息，eth0网卡的MTU值已变为8500。

    ![view-mtu-setting](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2880881161/p225168.png)


## 在Windows实例中设置网卡MTU值

确保Windows实例满足以下要求：

-   镜像为Windows Server 2012或以上版本。
-   已安装PowerShell。

1.  [远程连接ECS实例](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  下载ecs-utils-jumboframe-windows.ps1脚本。

    在浏览器中访问[下载链接](https://ecs-image-tools.oss-cn-hangzhou.aliyuncs.com/jumboframe/ecs-utils-jumboframe-windows.ps1)即可。

3.  打开PowerShell。

4.  切换至脚本所在目录。

    以脚本位于桌面为例：

    ```
    cd C:\Users\Administrator\Desktop
    ```

    您可以执行`Get-Help .\ecs-utils-jumboframe-windows.ps1`查看帮助信息。

    ![get-help](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0438201161/p225498.png)

5.  查看系统网卡设备列表。

    ```
    Get-NetAdapter
    ```

    ![get-netadapter](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2880881161/p225500.png)

6.  设置网卡MTU值。

    **说明：** Windows实例中仅支持永久设置MTU值。永久设置后，重启ECS实例后网卡MTU值仍保持您设置的值。

    格式如下：

    ```
    .\ecs-utils-jumboframe-windows.ps1 -NetworkAdapter <"网卡名称"> -NewMTUValue <目标MTU值>
    ```

    例如，将以太网网卡的MTU值设置为8500：

    ```
    .\ecs-utils-jumboframe-windows.ps1 -NetworkAdapter "以太网" -NewMTUValue 8500
    ```

    设置完成后，您可以执行`Get-NetAdapterAdvancedProperty -Name "以太网" -RegistryKeyword "MTU"`查看以太网网卡的MTU信息，MTU值已变为8500。

    ![view-mtu](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0438201161/p225503.png)


