# 辅助网卡配置IPv6地址最佳实践

本文通过示例操作，介绍不同VPC下的实例如何通过辅助网卡IPv6实现互通。

辅助网卡是一种可以绑定到专有网络VPC类型ECS实例上的虚拟网卡。更多信息，请参见[弹性网卡概述](/cn.zh-CN/网络/弹性网卡/弹性网卡概述.md)。

辅助网卡配置IPv6地址的使用限制如下：

-   目前支持辅助网卡配置IPv6地址的地域为华北2（北京）、华北5（呼和浩特）、华东2（上海）、华南1（深圳）、中国（香港）。
-   可用（Available）状态的辅助网卡默认能分配1个IPv6地址。
-   已分配（InUse）状态的辅助网卡能分配的IPv6个数受实例规格限制，可通过[DescribeInstanceTypes](/cn.zh-CN/API参考/实例/DescribeInstanceTypes.md)接口查询。目前在支持IPv6的实例规格中，最多只支持分配1个IPv6地址。
-   配置IPv6地址的辅助网卡必须绑定在支持IPv6的实例上。实例是否支持IPv6，请参见[实例规格族](/cn.zh-CN/实例/实例规格族.md)。
-   辅助网卡已经分配IPv6的实例不能变配到不支持IPv6的实例规格。
-   单台专有网络VPC类型的安全组内的私网IP地址（包含IPv6地址）个数不能超过2000，主网卡和辅助网卡共享此配额。
-   暂不支持创建网卡的同时分配IPv6。
-   暂不支持创建实例时为附带的网卡分配IPv6。

## 示例一：不同账号下的实例通过辅助网卡IPv6实现互通

本示例适用于两个不同的账号（服务账号和资源账号）下实例互通的场景。在服务账号下创建RAM用户作为用户账号，用户账号和资源账号分别创建各自的VPC、实例等相关资源，然后为资源账号授予用户账号的STS（阿里云临时安全令牌）权限。此时用户账号创建网卡后，资源账号能够跨账号将用户账号下的网卡绑定到实例上，从而实现两台实例的跨账号互通。

前提条件：

-   已存在两个阿里云账号作为服务账号和资源账号，并在服务账号下已创建了RAM用户作为用户账号。创建RAM用户的具体操作，请参见[创建RAM用户](/cn.zh-CN/用户管理/创建RAM用户.md)。
-   已为资源账号授予用户账号的STS（阿里云临时安全令牌）权限。具体操作，请参见[跨阿里云账号的资源授权](/cn.zh-CN/教程/跨阿里云账号的资源授权.md)。
-   为保证网络连通性，两个账号创建的资源必须在同一地域可用区。

本示例云资源名称使用情况如下表所示。

|云资源|资源账号|用户账号|
|---|----|----|
|专有网络名称|`test-vpc-1`|`test-vpc-2`|
|交换机名称|`test-vsw-1`|`test-vsw-2`|
|安全组名称|`test-group-1`|`test-group-2`|
|实例名称|`test-ecs-ipv6-1`|`test-ecs-ipv6-2`|
|弹性网卡名称|无|`test-eni-ipv6-2`|

资源账号和用户账号均需要进行的操作如下：

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  创建专有网络VPC和交换机。

    1.  在ECS管理控制台的左侧导航栏，选择**网络与安全** \> **专有网络VPC**跳转至专有网络控制台。

    2.  在顶部菜单栏处，选择地域。

        **说明：** 请选择支持辅助网卡配置IPv6地址的地域。

    3.  单击**创建专有网络**。

        分别创建专有网络和交换机，并且**IPv6网段**选择**分配**。具体操作，请参见[步骤一：创建专有网络和交换机](/cn.zh-CN/快速入门/搭建IPv6专有网络.md)。

3.  创建安全组。

    1.  在ECS管理控制台的左侧导航栏，选择**网络与安全** \> **安全组**。

    2.  在顶部菜单栏处，选择地域。

        **说明：** 选择地域与已创建的专有网络地域保持一致。

    3.  单击**创建安全组**。

        创建安全组，并且**网络**选择对应已创建好的专有网络。具体操作，请参见[创建安全组](/cn.zh-CN/安全/安全组/创建安全组.md)。

4.  创建ECS实例。

    1.  在ECS管理控制台左侧导航栏，选择**实例与镜像** \> **实例**。

    2.  在顶部菜单栏处，选择地域。

        **说明：** 选择地域与已创建的专有网络地域保持一致。

    3.  单击**创建实例**。

        本示例中请参见以下信息配置。未说明的配置详情，请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。

        -   选用实例规格ecs.g6.large。
        -   选用公共镜像CentOS 7.3 64位（此镜像支持网卡自动配置）。
        -   选择对应专有网络。
        -   分配公网IPv4地址。
        -   设置自定义密码，后续用于登录实例。

以上操作完成后，需要分别登录两个账号进行操作。具体操作步骤如下：

1.  使用用户账号创建网卡。

    1.  在ECS管理控制台左侧导航栏，选择**网络与安全** \> **弹性网卡**。

    2.  在顶部菜单栏处，选择地域。

        **说明：** 选择地域与已创建的专有网络地域保持一致。

    3.  单击**创建弹性网卡**。

        本示例中创建名称为`test-eni-ipv6-2`弹性网卡，配置信息如下：

        -   选择对应的`test-vpc-2`专有网络。
        -   选择对应的`test-vsw-2`交换机。
        -   选择对应的`test-group-2`安全组。
2.  使用资源账号跨云账号将弹性网卡`test-eni-ipv6-2`绑定到实例`test-ecs-ipv6-2`。

3.  使用资源账号配置网卡。

    本示例中创建了CentOS 7.3 64位系统的实例，支持网卡自动配置。如果创建实例时选用的镜像不支持网卡自动配置，则需要手动配置网卡，详情请参见[配置弹性网卡](/cn.zh-CN/网络/弹性网卡/配置弹性网卡.md)。

4.  使用资源账号给网卡分配IPv6地址。

    1.  在**网卡列表**中，找到网卡**操作**列，并单击**管理辅助私网IP**。

    2.  在**IPv6 地址**区域，单击**分配新IP**。

5.  分别在两个账号的实例上执行以下操作，配置IPv6地址。

    1.  远程连接实例。

        连接方式请参见[通过Workbench远程连接Linux实例](/cn.zh-CN/实例/连接实例/连接Linux实例/通过Workbench远程连接Linux实例.md)。

    2.  运行命令wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/rhel/ecs-utils-ipv6下载自动配置文件ecs-utils-ipv6。

        该命令下载的文件适用于CentOS 7.3镜像，不同镜像的下载地址，请参见[自动配置IPv6地址](/cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤4：配置IPv6地址.md)。

        **说明：** 您可以将文件下载到本地，然后使用如下方式上传至实例。

        -   使用FTP服务器上传文件。具体操作，请参见[手动搭建FTP站点（CentOS 7）](/cn.zh-CN/建站教程/搭建应用/搭建FTP站点/手动搭建FTP站点（CentOS 7）.md)。
        -   使用远程连接工具连接实例，并通过上传功能将文件上传至实例。例如，FinalShell工具。
    3.  运行命令chmod +x ./ecs-utils-ipv6为文件授予权限。

    4.  运行命令./ecs-utils-ipv6自动配置网卡的IPv6地址。

        配置成功的返回示例如下：

        ```
        [Info]  ECS Utils IPv6 1.0.2.
        [Info]  IPv6 Auto Config Begin...
        [Warn]  get [00:16:3e:01:**:**] ipv6 metadata null
        [Warn]  get [00:16:3e:01:**:**] prefix len metadata null
        [Warn]  get [00:16:3e:01:**:**] ipv6 gateway metadata null
        [Info]  Config eth0...
        [Info]  Config eth1...
        [Done]  IPv6 Auto Config Finished.
        ```

    5.  运行命令ifconfig查看`inet6`后的IPv6地址。

6.  检查网络连通性。

    使用资源账号在实例`test-ecs-ipv6-1`中运行命令ping6 -I <IPv6地址\>。

    操作结果如下所示。

    ![ping](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3562755951/p127833.png)


## 示例二：不同VPC下的实例通过辅助网卡IPv6的公网带宽实现互通

本示例中，将使用同一个账号分别创建两个不同VPC，并在对应VPC下分别创建实例，通过开通辅助网卡IPv6的公网带宽实现两个实例间的互通。

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  创建两个专有网络VPC和交换机。

    1.  在ECS管理控制台的左侧导航栏，选择**网络与安全** \> **专有网络VPC**跳转至专有网络控制台。

    2.  在顶部菜单栏处，选择地域。

        **说明：** 请选择支持辅助网卡配置IPv6地址的地域。

    3.  单击**创建专有网络**。

        本示例中分别创建名称为`test-vpc-1`和`test-vpc-2`两个专有网络，`test-vsw-1`和`test-vsw-2`两个交换机，并且**IPv6网段**选择**分配**。具体操作，请参见[步骤一：创建专有网络和交换机](/cn.zh-CN/快速入门/搭建IPv6专有网络.md)。

3.  创建两个安全组。

    1.  在ECS管理控制台的左侧导航栏，选择**网络与安全** \> **安全组**。

    2.  在顶部菜单栏处，选择地域。

        **说明：** 选择地域与已创建的专有网络地域保持一致。

    3.  单击**创建安全组**。

        1.  本示例中分别创建名称为`test-group-1`和`test-group-2`两个安全组，并且**网络**选择对应已创建好的`test-vpc-1`和`test-vpc-2`专有网络。
        2.  在**访问规则**区域，入方向手动添加规则，放行所有的IPv6地址。添加完成后如下所示。

            ![安全组规则](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3562755951/p127420.png)

            放行所有IPv6地址是为了互相能够ping通公网IPv6地址，您也可以根据实际需求进行规则配置。具体操作，请参见[创建安全组](/cn.zh-CN/安全/安全组/创建安全组.md)及[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

4.  创建两台ECS实例。

    1.  在ECS管理控制台左侧导航栏，选择**实例与镜像** \> **实例**。

    2.  在顶部菜单栏处，选择地域。

        **说明：** 选择地域与已创建的专有网络地域保持一致。

    3.  单击**创建实例**。

        本示例中分别创建名称为`test-ecs-ipv6-1`和`test-ecs-ipv6-2`两台实例，请参见以下信息配置。未说明的配置详情，请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。

        -   选用实例规格ecs.g6.large。
        -   选用公共镜像CentOS 7.3 64位（此镜像支持网卡自动配置）。
        -   分别选择对应的`test-vpc-1`和`test-vpc-2`专有网络。
        -   分配公网IPv4地址。
        -   设置自定义密码，后续登录实例时使用。
5.  创建两块网卡并挂载至实例。

    1.  在ECS管理控制台左侧导航栏，选择**网络与安全** \> **弹性网卡**。

    2.  在顶部菜单栏处，选择地域。

        **说明：** 选择地域与已创建的专有网络地域保持一致。

    3.  单击**创建弹性网卡**。

        本示例中分别创建名称为`test-eni-ipv6-1`和`test-eni-ipv6-2`两块弹性网卡，配置信息如下：

        -   分别选择对应的`test-vpc-1`和`test-vpc-2`专有网络。
        -   分别选择对应的`test-vsw-1`和`test-vsw-2`交换机。
        -   分别选择对应的`test-group-1`和`test-group-2`安全组。
    4.  将网卡`test-eni-ipv6-1`和`test-eni-ipv6-2`分别绑定到对应的实例`test-ecs-ipv6-1`和`test-ecs-ipv6-2`。

    5.  配置辅助网卡。

        本示例中创建了CentOS 7.3 64位系统的实例，支持网卡自动配置。如果创建实例时选用的镜像不支持网卡自动配置，则需要手动配置网卡。具体操作，请参见[配置弹性网卡](/cn.zh-CN/网络/弹性网卡/配置弹性网卡.md)。

    6.  在**网卡列表**中，分别找到两个辅助网卡**操作**列，并单击**管理辅助私网IP**。

    7.  在**IPv6 地址**区域，单击**分配新IP**。

    8.  开通IPv6公网带宽。

        默认IPv6地址只具备私网通信能力，您需要分别为两个IPv6地址开通IPv6公网带宽。具体操作，请参见[步骤三：开通IPv6公网带宽](/cn.zh-CN/快速入门/搭建IPv6专有网络.md)。

6.  分别在两台实例上执行以下操作，配置IPv6地址。

    1.  远程连接实例。

        具体操作，请参见[通过Workbench远程连接Linux实例](/cn.zh-CN/实例/连接实例/连接Linux实例/通过Workbench远程连接Linux实例.md)。

    2.  运行命令wget http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/rhel/ecs-utils-ipv6下载自动配置文件ecs-utils-ipv6。

        该命令下载的文件适用于CentOS 7.3镜像。不同镜像的下载地址，请参见[自动配置IPv6地址](/cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤4：配置IPv6地址.md)。

        **说明：** 您可以将文件下载到本地，然后使用如下方式上传至实例。

        -   使用FTP服务器上传文件。具体操作，请参见[手动搭建FTP站点（CentOS 7）](/cn.zh-CN/建站教程/搭建应用/搭建FTP站点/手动搭建FTP站点（CentOS 7）.md)。
        -   使用远程连接工具连接实例，并通过上传功能将文件上传至实例。例如，FinalShell工具。
    3.  运行命令chmod +x ./ecs-utils-ipv6为文件授予权限。

    4.  运行命令./ecs-utils-ipv6自动配置网卡的IPv6地址。

        配置成功的返回示例如下：

        ```
        [Info]  ECS Utils IPv6 1.0.2.
        [Info]  IPv6 Auto Config Begin...
        [Warn]  get [00:16:3e:01:**:**] ipv6 metadata null
        [Warn]  get [00:16:3e:01:**:**] prefix len metadata null
        [Warn]  get [00:16:3e:01:**:**] ipv6 gateway metadata null
        [Info]  Config eth0...
        [Info]  Config eth1...
        [Done]  IPv6 Auto Config Finished.
        ```

    5.  运行命令ifconfig查看`inet6`后的IPv6地址。

7.  检查网络连通性。

    在任意一台实例内ping另一台实例。

    本示例中在`test-ecs-ipv6-1`实例内运行命令ping6 -I <IPv6地址\>。

    操作结果如下所示。

    ![ping](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3562755951/p127835.png)


## 相关操作

-   分配IPv6地址。
    -   控制台操作，请参见[分配IPv6地址](/cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤2：分配IPv6地址.md)。
    -   调用OpenAPI，请参见[AssignIpv6Addresses](/cn.zh-CN/API参考/弹性网卡/AssignIpv6Addresses.md)。
-   回收IPv6地址。
    -   控制台操作，请参见[删除IPv6地址](/cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤7：（可选）删除IPv6地址.md)。
    -   调用OpenAPI，请参见[UnassignIpv6Addresses](/cn.zh-CN/API参考/弹性网卡/UnassignIpv6Addresses.md)。
-   配置IPv6地址的安全组规则。
    -   控制台操作，请参见[添加IPv6安全组规则](/cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤5：添加IPv6安全组规则.md)。
    -   调用OpenAPI，请参见：
        -   [AuthorizeSecurityGroup](/cn.zh-CN/API参考/安全组/AuthorizeSecurityGroup.md)。
        -   [AuthorizeSecurityGroupEgress](/cn.zh-CN/API参考/安全组/AuthorizeSecurityGroupEgress.md)。
        -   [RevokeSecurityGroup](/cn.zh-CN/API参考/安全组/RevokeSecurityGroup.md)。
        -   [RevokeSecurityGroupEgress](/cn.zh-CN/API参考/安全组/RevokeSecurityGroupEgress.md)。

