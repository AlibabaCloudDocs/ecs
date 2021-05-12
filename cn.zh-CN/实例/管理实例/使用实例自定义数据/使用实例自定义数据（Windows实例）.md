# 使用实例自定义数据（Windows实例）

本文介绍如何准备适用于Windows实例的实例自定义数据脚本，以及如何传入实例自定义数据和验证效果。

如果为已有实例修改实例自定义数据，该实例必须处于**已停止**状态。

Windows实例自定义数据功能为Windows实例提供运行初始化脚本的能力，在实例启动时系统首先以管理员权限运行实例自定义数据。

实例自定义数据的使用限制如下：

-   仅网络类型为专有网络VPC的实例支持实例自定义数据功能。
-   实例必须使用公共镜像或基于公共镜像创建的自定义镜像，且必须为以下镜像之一：
    -   Alibaba Cloud Linux、CentOS、Ubuntu、SUSE Linux Enterprise、OpenSUSE、Debian
    -   Windows Server 2008 R2及更高版本
-   在售的实例规格均支持实例自定义数据功能。但已停售的实例规格中，仅I/O优化实例支持实例自定义数据功能，更多信息，请参见[已停售的实例规格](/cn.zh-CN/实例/选择实例规格/已停售的实例规格.md)。
-   执行时的实例自定义数据必须为Base64编码形式，且在进行Base64编码前自定义数据内容的大小不能超过16 KB。

    **说明：** 您可以在控制台输入未经过Base64编码的实例自定义数据，控制台会自动进行Base64编码。如果您不在控制台输入实例自定义数据，请先自行将实例自定义数据进行Base64编码。


## 操作步骤

1.  准备实例自定义数据。

    您可以通过Bat和PowerShell准备Windows实例自定义数据，不同脚本类型的特点以及示例请参见：

    -   [Bat](#section_5lb_6c5_sdf)
    -   [PowerShell](#section_p81_sdk_rnb)
2.  将实例自定义数据传入实例。

    -   创建实例时传入实例自定义数据：在**系统配置**页面中，单击展开**高级选项**区域，然后在**实例自定义数据**区域输入实例自定义数据。如果实例自定义数据已进行Base64编码，请选中**输入已采用Base64编码**。

        向指定文件写入内容的示例如下图所示。

        ![createinstance-powershellsample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4820460261/p272285.png)

    -   为已有实例修改实例自定义数据：在**实例列表**页面中，选择**更多** \> **实例设置** \> **设置用户数据**，然后在**用户数据**区域输入新的实例自定义数据。

        **说明：** 对于按量付费实例，如果您需要在修改自定义数据后立即启动实例，建议停止模式设置为**保留并收费**。

        向指定文件写入内容的示例如下图所示。

        ![modifyinstance-powershellsample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4820460261/p272289.png)

        **说明：** 修改Windows实例自定义数据后，启动实例时不会重新运行新的实例自定义数据。

3.  查看传入实例的内容和运行效果。

    1.  [远程连接实例](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

    2.  通过实例元数据查看内容。

        ```
        Invoke-RestMethod http://100.100.100.200/latest/user-data
        ```

        以查看[步骤2](#step_v0x_9gc_u16)中的创建实例时传入实例自定义数据为例，如下图所示，内容一致表明实例自定义数据已成功传入实例。

        ![view-userdata](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4820460261/p272292.png)

    3.  查看运行效果。

        运行效果和内容有关，向指定文件写入内容的效果如下图所示。

        ![powershell-sample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4820460261/p272280.png)


## Bat

Bat脚本具有以下特点：

-   首行为`[bat]`，且起始位置不能有空格。
-   只能输入半角字符，不能有多余字符。

示例Bat脚本：

```
[bat]
echo "bat test" > C:\userdata_test.txt
```

示例Bat脚本的效果为在实例首次启动时向userdata\_test.txt写入内容`"bat test"`，如下图所示。

![bat-sample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5820460261/p272279.png)

## PowerShell

PowerShell脚本具有以下特点：

-   首行为`[powershell]`，且起始位置不能有空格。
-   只能输入半角字符，不能有多余字符。

示例PowerShell脚本如下：

```
[powershell]
write-output "powershell test" | Out-File C:\userdata_test.txt
```

示例PowerShell的效果为在实例首次启动时向userdata\_test.txt写入内容`powershell test`，如下图所示。

![powershell-sample](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4820460261/p272280.png)

