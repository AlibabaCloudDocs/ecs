# 在云助手命令中使用OOS参数仓库

在云助手命令中使用自定义参数，可以更加灵活地编写脚本，提高命令的复用性。同时，运维编排服务OOS提供参数仓库功能，支持普通参数和加密参数。您可以在云助手命令中结合OOS的参数仓库功能，更为方便和安全地管理自定义参数。

-   目标ECS实例必须满足以下条件：
    -   实例处于**运行中**（`Running`）状态。
    -   实例已安装云助手客户端。具体操作，请参见[安装云助手客户端](/intl.zh-CN/运维与监控/云助手/配置云助手客户端/安装云助手客户端.md)。
-   已开通运维编排服务（OOS）。更多信息，请参见[什么是运维编排服务]()。
-   如果需要使用加密参数，需要开通密钥管理服务（KMS）。更多信息，请参见[什么是密钥管理服务](/intl.zh-CN/产品简介/什么是密钥管理服务.md)。

在云助手命令中，您可以直接使用`{{parameterName}}`方式表示自定义参数。例如云助手命令`adduser {{username}}`，表示为Linux实例添加用户名。此时，username表示一个自定义参数，您可以在[RunCommand](/intl.zh-CN/API参考/云助手/RunCommand.md)或[InvokeCommand](/intl.zh-CN/API参考/云助手/InvokeCommand.md)的Parameters参数中传入具体的取值。

通过引用运维编排服务参数仓库中的参数，您可以以更灵活的方式使用参数。参数仓库定义的参数分为普通参数和加密参数，云助手分别以`{{oos:}}`和`{{oos-secret:}}`的方式定义普通参数和加密参数。

-   如果您的参数不涉及敏感数据，建议使用普通参数。操作示例，请参见[在云助手命令中使用普通参数](#section_cdy_0u6_hbo)。
-   如果您的参数涉及敏感数据（例如密码等），建议使用加密参数。操作示例，请参见[在云助手命令中使用加密参数](#section_1m4_3wb_7s1)。

## 在云助手命令中使用普通参数

如果您使用RAM用户执行云助手命令，需要为RAM用户配置策略。具体操作，请参见[创建自定义策略](/intl.zh-CN/权限策略管理/自定义策略/创建自定义策略.md)和[为RAM用户授权](/intl.zh-CN/用户管理/为RAM用户授权.md)。允许RAM用户使用普通参数执行云助手命令，需要使用云助手和参数仓库相关的API权限。具体RAM权限策略如下：

```
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:DescribeInstances",
                "ecs:DescribeTagKeys",
                "ecs:DescribeTags",
                "ecs:CreateCommand",
                "ecs:DescribeCommands",
                "ecs:InvokeCommand",
                "ecs:RunCommand",
                "ecs:DeleteCommand",
                "ecs:DescribeInvocations",
                "ecs:DescribeInvocationResults",
                "ecs:StopInvocation",
                "ecs:DescribeCloudAssistantStatus",
                "ecs:InstallCloudAssistant",
                "oos:GetParameters",
                "oos:GetParameter"
            ],
            "Resource": "*"
        }
    ],
    "Version": "1"
}
```

如果您的命令不涉及敏感数据，可以使用普通参数。本节以在Linux实例中增加新用户为例，介绍如何在云助手命令中使用OOS参数仓库的普通参数。

1.  通过运维编排服务OOS的参数仓库创建普通参数。具体操作，请参见[普通参数]()。

    以下示例表示在普通参数中新增一个username参数，取值为user01，您可以根据实际情况修改。

    |名称|示例值|
    |--|---|
    |**参数名称**|username|
    |**参数类型**|String|
    |**值**|user01|

2.  通过Java SDK调用[RunCommand](/intl.zh-CN/API参考/云助手/RunCommand.md)，执行云助手命令。

    以下示例表示通过云助手命令为Linux实例创建一个新用户，命令内容为`adduser {{oos:username}}`。其中，`{{oos:username}}`表示新用户名由OOS参数仓库的普通参数username定义。

    ```
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.IAcsClient;
    import com.aliyuncs.ecs.model.v20140526.RunCommandRequest;
    import com.aliyuncs.ecs.model.v20140526.RunCommandResponse;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.exceptions.ServerException;
    import com.aliyuncs.profile.DefaultProfile;
    import com.google.gson.Gson;
    
    import java.util.ArrayList;
    import java.util.List;
    
    public class addUserName {
        public static void main(String[] args) {
            # 设置地域和账号AccessKey信息。
            DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<accessKeyId>", "<accessSecret>");
            IAcsClient client = new DefaultAcsClient(profile);
    
            RunCommandRequest request = new RunCommandRequest();
            # 设置实例所在的地域。
            request.setRegionId("cn-hangzhou");
            # 设置云助手命令的语言类型，示例表示使用shell语言。
            request.setType("RunShellScript");
            # 设置云助手命令内容，示例表示为Linux新增一个用户，用户名由OOS参数仓库的普通参数username决定。
            request.setCommandContent("adduser {{oos:username}}");
    
            List<String> instanceIdList = new ArrayList<String>();
            # 设置运行云助手命令的实例ID。
            instanceIdList.add("i-bp1dktddjsg7oh11****");
            request.setInstanceIds(instanceIdList);
            # 设置云助手命令支持自定义参数。
            request.setEnableParameter(true);
    
            try {
                RunCommandResponse response = client.getAcsResponse(request);
                System.out.println(new Gson().toJson(response));
            } catch (ServerException e) {
                e.printStackTrace();
            } catch (ClientException e) {
                System.out.println("ErrCode:" + e.getErrCode());
                System.out.println("ErrMsg:" + e.getErrMsg());
                System.out.println("RequestId:" + e.getRequestId());
            }
        }
    }
    ```

    执行结果如下所示：

    ```
    {
        "requestId": "67D1BD1A-0D08-42C3-AFD9-A3397CD67CD1",
        "commandId": "c-hz01hkgs19i****",
        "invokeId": "t-hz01hkgs19s****"
    }
    ```

3.  检查云助手命令执行结果。

    您可以登录ECS实例检查云助手命令是否生效。以下示例表示在Linux实例中检查是否新增用户user01。

    1.  登录ECS实例。具体操作，请参见[通过密码认证登录Linux实例](/intl.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。

    2.  运行以下命令查看是否已经新增user01用户。

        ```
        cat /etc/passwd |grep user01
        ```

        以下结果表示已经成功新增user01用户。

        ![新增user01](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3931009161/p266512.png)


## 在云助手命令中使用加密参数

如果您使用RAM用户执行云助手命令，需要为RAM用户配置策略。具体操作，请参见[创建自定义策略](/intl.zh-CN/权限策略管理/自定义策略/创建自定义策略.md)和[为RAM用户授权](/intl.zh-CN/用户管理/为RAM用户授权.md)。允许RAM用户使用加密参数执行云助手命令，需要使用云助手、参数仓库及KMS相关的API权限。具体RAM权限策略如下：

```
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:DescribeInstances",
                "ecs:DescribeTagKeys",
                "ecs:DescribeTags",
                "ecs:CreateCommand",
                "ecs:DescribeCommands",
                "ecs:InvokeCommand",
                "ecs:RunCommand",
                "ecs:DeleteCommand",
                "ecs:DescribeInvocations",
                "ecs:DescribeInvocationResults",
                "ecs:StopInvocation",
                "ecs:DescribeCloudAssistantStatus",
                "ecs:InstallCloudAssistant",
                "oos:GetParameters",
                "oos:GetSecretParameters",
                "oos:GetParameter",
                "oos:GetSecretParameter",
                "kms:GetSecretValue"
            ],
            "Resource": "*"
        }
    ],
    "Version": "1"
}
```

如果您的命令涉及敏感数据（例如服务器密码、数据库密码等），建议使用加密参数，以提高命令的安全性。本节以在Linux实例中修改用户密码为例，介绍如何在云助手命令中使用OOS参数仓库的加密参数。

**说明：** 执行以下操作前，实例中需要已经创建目标用户。关于如何为Linux实例添加新用户，请参见[在云助手命令中使用普通参数](#section_cdy_0u6_hbo)。

1.  通过运维编排服务OOS的参数仓库创建加密参数和普通参数。具体操作，请参见[加密参数]()和[普通参数]()。

    以下示例表示在OOS参数仓库中创建用户名参数username和密码参数password。

    -   在普通参数中新增一个用户名参数username，取值为user01，您可以根据实际情况修改。

        |名称|示例值|
        |--|---|
        |**参数名称**|username|
        |**参数类型**|String|
        |**值**|user01|

    -   在加密参数中新增一个密码参数password，取值为MyPassword01，您可以根据实际情况修改。

        |名称|示例值|
        |--|---|
        |**参数名称**|password|
        |**KMS密钥ID**|Default Service CMK|
        |**值**|MyPassword01**说明：** 此密码仅做示例，请不要在线上环境使用。 |

2.  为目标实例设置RAM角色。

    1.  创建RAM角色。具体操作，请参见[创建可信实体为阿里云服务的RAM角色](/intl.zh-CN/角色管理/创建RAM角色/创建可信实体为阿里云服务的RAM角色.md)。

        相关配置示例如下所示。

        |名称|示例|
        |--|--|
        |**当前可信实体类型**|选择**阿里云服务**。|
        |**角色类型**|选择**普通服务角色**。|
        |**角色名称**|AxtParametersRamRole|
        |**选择受信服务**|下拉栏中选择**云服务器**。|

    2.  创建RAM角色相关权限策略。具体操作，请参见[创建自定义策略](/intl.zh-CN/权限策略管理/自定义策略/创建自定义策略.md)。

        策略名称为AxtParametersRamPolicy，策略内容如下所示，表示允许调用KMS和OOS的相关API（GetSecretValue、GetParameters、GetSecretParameters、GetParameter和GetSecretParameter）。

        ```
        {
            "Version": "1",
            "Statement": [
                {
                    "Action": [
                        "kms:GetSecretValue"
                    ],
                    "Resource": "*",
                    "Effect": "Allow"
                },
                {
                    "Action": [
                        "oos:GetParameters",
                        "oos:GetSecretParameters",
                        "oos:GetParameter",
                        "oos:GetSecretParameter"
                    ],
                    "Effect": "Allow",
                    "Resource": "*"
                }
            ]
        }
        ```

    3.  为RAM角色（AxtParametersRamRole）设置策略权限（AxtParametersRamPolicy）。具体操作，请参见[为RAM角色授权](/intl.zh-CN/角色管理/为RAM角色授权.md)。

    4.  为目标ECS实例设置RAM角色（AxtParametersRamRole）。具体操作，请参见[授予实例RAM角色](/intl.zh-CN/安全/实例RAM角色/授予实例RAM角色.md)。

3.  通过Java SDK调用[RunCommand](/intl.zh-CN/API参考/云助手/RunCommand.md)，执行云助手命令。

    以下示例表示通过云助手命令为Linux实例修改用户密码，命令内容如下所示：

    ```
    echo '{{oos-secret:password}}' | passwd '{{oos:username}}' --stdin"
    ```

    其中，`{{oos-secret:password}}`表示用户新密码由OOS参数仓库的加密参数password定义；`{{oos:username}}`表示用户名由OOS参数仓库的普通参数username定义。

    ```
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.IAcsClient;
    import com.aliyuncs.ecs.model.v20140526.RunCommandRequest;
    import com.aliyuncs.ecs.model.v20140526.RunCommandResponse;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.exceptions.ServerException;
    import com.aliyuncs.profile.DefaultProfile;
    import com.google.gson.Gson;
    
    import java.util.ArrayList;
    import java.util.List;
    
    public class changePassword {
        public static void main(String[] args) {
            # 设置地域和账号AccessKey信息。
            DefaultProfile profile = DefaultProfile.getProfile("cn-hangzhou", "<accessKeyId>", "<accessSecret>");
            IAcsClient client = new DefaultAcsClient(profile);
    
            RunCommandRequest request = new RunCommandRequest();
            # 设置实例所在的地域。
            request.setRegionId("cn-hangzhou");
            # 设置云助手命令的语言类型，示例表示使用shell语言。
            request.setType("RunShellScript");
            # 设置云助手命令内容，示例表示为Linux的用户（用户名为username取值）修改密码（密码为password取值）。
            request.setCommandContent(
                    "echo '{{oos-secret:password}}' | passwd '{{oos:username}}' --stdin");
    
            List<String> instanceIdList = new ArrayList<String>();
            instanceIdList.add("i-bp1dktddjsg7oh11****");
            request.setInstanceIds(instanceIdList);
            request.setEnableParameter(true);
    
            try {
                RunCommandResponse response = client.getAcsResponse(request);
                System.out.println(new Gson().toJson(response));
            } catch (ServerException e) {
                e.printStackTrace();
            } catch (ClientException e) {
                System.out.println("ErrCode:" + e.getErrCode());
                System.out.println("ErrMsg:" + e.getErrMsg());
                System.out.println("RequestId:" + e.getRequestId());
            }
        }
    
    }
    ```

    执行结果如下所示：

    ```
    {
        "requestId": "C73D7B90-6503-4DB4-844C-9412AC55ECC5",
        "commandId": "c-hz01hnyd4e8****",
        "invokeId": "t-hz01hnyd4ed****"
    }
    ```

4.  检查云助手命令执行结果。

    您可以使用修改后的密码远程登录ECS实例，确认云助手命令是否生效。具体操作，请参见[通过密码认证登录Linux实例](/intl.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。


