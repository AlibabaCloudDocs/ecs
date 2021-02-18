# InvokeCommand

调用InvokeCommand为一台或多台ECS实例触发一条云助手命令。

## 接口说明

-   在一个阿里云地域下，您每天能调用5000次InvokeCommand接口。[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)可以申请调整调用次数配额。
-   对目标ECS实例有如下限制。选择了多台ECS实例后，若其中某台实例不满足执行条件，您需要重新调用接口。
    -   网络类型是[专有网络VPC](~~34217~~)。
    -   状态必须为运行中（`Running`）。
    -   已预先安装[云助手客户端](~~64921~~)。
    -   执行类型为PowerShell的命令时，实例必须已经配置了PowerShell模块。
-   单次执行（`Timed=false`），只执行一次命令。
-   周期执行（`Timed=true`）：
    -   根据参数`Frequency`指定的时间频率定时执行，上次的执行结果不对下一次执行产生任何影响。
    -   时间设置基准为UTC +0，且该时间以实例的系统时间为准。请确保ECS实例的时间或者时区与您预期的时间一致。更多关于时区的详情，Linux实例请参见[设置Linux实例时区和NTP服务](~~92803~~)，Windows实例请参见[设置Windows实例NTP服务](~~51890~~)。
-   命令的执行可能会因为目标实例的状态异常、网络异常或云助手客户端异常而出现无法执行的情况，无法执行时不会生成执行信息。
-   当您创建命令时启用了自定义参数功能，需要在执行命令时传入自定义参数（`Parameters`）。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=InvokeCommand&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|InvokeCommand|系统规定参数。取值：InvokeCommand |
|CommandId|String|是|c-e996287206324975b5fbe1d\*\*\*\*|命令ID。您可以通过接口[DescribeCommands](~~64843~~)查询所有可用的CommandId。 |
|InstanceId.N|RepeatList|是|i-bp185dy2o3o6n\*\*\*\*|需要执行命令的实例列表，最多能指定50台实例ID。N的取值范围：1~50 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Timed|Boolean|否|true|命令是否为周期执行。

 默认值：false |
|Frequency|String|否|0 \*/20 \* \* \* \*|周期执行命令的执行周期，两次周期执行的命令时间间隔不能低于10秒。当参数`Timed`的值为`true`时，`Frequency`为必选参数。

 该参数取值遵循Cron表达式，请参见[设置定时执行命令](~~64769~~)。 |
|Parameters|Json|否|\{"name":"Jack", "accessKey":"LTAIdyv\*\*\*\*\*\*aRY"\}|启用自定义参数功能时，执行命令时传入的自定义参数的键值对。自定义参数的个数范围：0~10

 -   Map的键不允许为空字符串，最多支持64个字符。
-   Map的值允许为空字符串。
-   自定义参数与原始命令内容在Base64编码后，综合长度不能超过16KB。
-   设置的自定义参数名集合必须为创建命令时定义的参数集的子集。对于未传入的参数，您可以使用空字符串代替。

 您可以取消设置该参数从而禁用自定义参数。 |
|Username|String|否|root|在ECS实例中执行命令的用户名称。

 -   Linux系统的ECS实例，默认以root用户执行命令。
-   Windows系统的ECS实例，默认以System用户执行命令。

 您也可以指定实例中已存在的其他用户执行命令，以普通用户执行云助手命令更加安全。更多信息，请参见[设置普通用户执行云助手命令](~~203771~~)。 |
|WindowsPasswordName|String|否|axtSecretPassword|在Windows实例中执行命令的用户的密码名称。

 当您希望以非默认用户（System）在Windows实例中执行命令时，需要同时传入`Username`和该参数。为降低密码泄露的风险，需要将密码明文托管在运维编排服务的参数仓库中，此处仅传入密码的名称。更多信息，请参见[加密参数](~~186828~~)以及[设置普通用户执行云助手命令](~~203771~~)。

 **说明：** 当您使用Linux实例的root用户或Windows实例的System用户执行命令时，不需要传递该参数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|InvokeId|String|t-7d2a745b412b4601b2d47f6a768d\*\*\*\*|命令执行ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=InvokeCommand
&CommandId=c-e996287206324975b5fbe1d****
&InstanceId.1=i-bp185dy2o3o6n****
&RegionId=cn-hangzhou
&Timed=true
&Frequency=0 */20 * * * *
&Parameters={"name":"Jack", "accessKey":"LTAIdyv******aRY"}
&Username=root
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<InvokeCommandResponse>
      <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
      <InvokeId>t-7d2a745b412b4601b2d47f6a768d****</InvokeId>
</InvokeCommandResponse>
```

`JSON`格式

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "InvokeId": "t-7d2a745b412b4601b2d47f6a768d****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|RegionId.ApiNotSupported|The api is not supported in this region.|指定地域下不支持调用API。请检查RegionId参数取值是否正确。|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发送请求时发生错误，请稍后重试。|
|404|InvalidInstance.NotFound|The specified instance does not exist.|指定的实例不存在。|
|403|InvalidInstance.NotMatch|The specified instance type does not match the command.|指定的实例ID不支持执行指定的命令ID。请检查实例的状态是否符合云助手命令的执行条件。|
|404|InvalidCmdId.NotFound|The specified command ID does not exist.|指定的CommandId参数有误，请检查参数值是否正确。您可以通过接口DescribeCommands查询所有可用的CommandId。|
|403|MissingParam.Frequency|The frequency must be specified when you create a timed task.|创建定时任务时必须指定频率。|
|403|InvalidParam.Frequency|The specified frequency is invalid.|指定的Frequency参数无效。请检查参数值是否正确。|
|403|InstanceIds.ExceedLimit|The number of instance IDs exceeds the upper limit.|目标实例数量超过上限。|
|404|Parameter.Disabled|Parameters cannot be passed in when the command customization function is disabled.|当您禁用命令自定义参数功能时，请不要传递自定义参数。|
|403|ParameterCount.ExceedLimit|The maximum number of parameters is exceeded.|参数数量超出最大可设置数量。|
|403|ParameterKey.ExceedLimit|The maximum length of a parameter name is exceeded.|指定的参数Key长度超过可设置的最大长度。|
|403|CmdContent.ExceedLimit|The maximum length of a command is exceeded.|您的命令内容过长，请精简您的命令内容。|
|403|ParameterKey.Duplicate|Parameter names cannot be duplicated.|参数名称不能重复，请确认后重试。|
|403|Parameter.NotMatched|The passed-in parameters do not match the parameters defined when you created the command.|传入的自定义参数与创建命令时定义的自定义参数不匹配。|
|403|Username.ExceedLimit|The length of the username exceeds the upper limit.|用户名长度超过上限。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

