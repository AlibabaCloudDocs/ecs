# RunCommand

调用RunCommand在一台或多台ECS实例中执行一段Shell、PowerShell或者Bat类型的脚本。

## 接口说明

不同于通过[CreateCommand](~~64844~~)和[InvokeCommand](~~64841~~)执行脚本，RunCommand只需一次调用即可完成脚本的创建与执行。

调用该接口时，您需要注意：

-   目标实例的网络类型必须是专有网络VPC。
-   目标实例的状态必须为运行中（`Running`）。
-   目标实例必须预先安装云助手客户端（[InstallCloudAssistant](~~85916~~)）。
-   执行类型为PowerShell的脚本时，您需要确保目标ECS Windows实例已经配置了PowerShell模块。
-   周期执行的时间设置基准为UTC +0，且该时间以实例的系统时间为准。ECS实例的时间或者时区必须与您预期的时间一致。更多关于时区的详情，请参见[设置Linux实例时区和NTP服务](~~92803~~)或[设置Windows实例NTP服务](~~51890~~)。
-   您可以通过指定参数`TimeOut`为脚本设置在ECS实例中执行时最大的超时时间，脚本执行超时后，云助手客户端会强制终止进程。
    -   单次执行超时后，脚本的执行状态（[InvokeRecordStatus](~~64845~~)）变为执行失败（Failed）。
    -   周期执行的超时时间对每一次执行记录均有效，上次执行超时不影响下一次执行。某次执行超时后，执行状态（[InvokeRecordStatus](~~64845~~)）变为执行失败（Failed）。
-   脚本可能会因为目标实例的状态异常、网络异常或云助手客户端异常而出现无法执行的情况，无法执行时不会生成执行信息。
-   `EnableParameter=true`时会启用自定义参数功能。在设置`CommandContent`时可以通过`{{parameter}}`的形式表示自定义参数，并在运行脚本时，传入自定义参数键值对。
-   在一个地域下，根据您的使用情况，最多可以保有100-10000条云助手脚本，每天最多可以执行2000-200000条云助手脚本。您可以通过[DescribeAccountAttribute](~~73772~~)查询配额情况，也可以[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)调整保有量配额和调用次数配额。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=RunCommand&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RunCommand|系统规定参数。取值：RunCommand |
|CommandContent|String|是|ZWNobyAxMjM=|脚本的明文内容或者Base64编码后的内容。脚本内容Base64编码后不能超过16KB。

 指定参数`EnableParameter=true`可在脚本内容中启用自定义参数功能：

 -   用`{{}}`包含的方式定义自定义参数，在`{{}}`内参数名前后的空格以及换行符会被忽略。
-   自定义参数个数不能超过20个。
-   自定义参数名允许a-zA-Z0-9-\_的组合，不支持其余字符，参数名不区分大小写。

单个自定义参数键不能超过64字节。 |
|InstanceId.N|RepeatList|是|i-bp185dy2o3o6neg\*\*\*\*|ECS实例ID列表。N的取值范围：1~50

 若指定了多台实例后，其中某台实例不满足执行条件时，您都需要重新选择。 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Type|String|是|RunShellScript|运维脚本的语言类型。取值范围：

 -   RunBatScript：适用于Windows实例的Bat脚本。
-   RunPowerShellScript：适用于Windows实例的PowerShell脚本。
-   RunShellScript：适用于Linux实例Shell脚本。 |
|Name|String|否|testName|脚本名称。支持全字符集，长度不得超过128个字符。 |
|Description|String|否|testDescription|脚本描述。支持全字符集，长度不得超过512个字符。 |
|WorkingDir|String|否|/home/|脚本在ECS实例中的运行目录。

 默认值：

 -   Linux系统实例默认在管理员（root用户）的home目录下，即`/root`。
-   Windows系统实例默认在云助手客户端进程所在目录，例如`C:\Windows\System32`。 |
|Timeout|Long|否|3600|执行脚本的超时时间，单位为秒。

 当因为进程原因、缺失模块、缺失云助手客户端等原因无法运行脚本时，会出现超时现象。超时后，会强制终止脚本进程。

 默认值：60 |
|EnableParameter|Boolean|否|false|脚本中是否包含自定义参数。

 默认值：false |
|Timed|Boolean|否|true|是否周期执行脚本。取值范围：

 -   true：根据参数`Frequency`设置的时间频率定时执行。上次的执行结果不对下一次执行产生任何影响。
-   false：只执行一次。

 默认值：false |
|Frequency|String|否|0 \*/20 \* \* \* \*|周期任务的执行周期。当参数Timed的值为True时，参数Frequency为必需参数。两次周期任务的时间间隔不能低于10秒。

 该参数取值遵循Cron表达式，请参见[设置定时执行脚本](~~64769~~)。 |
|Parameters|Json|否|\{"name":"Jack", "accessKey":"LTAIdyvdIqaRY\*\*\*\*"\}|脚本中包含自定义参数时，执行脚本时传入的自定义参数的键值对。例如，脚本内容为`echo {{name}}`，则可以通过`Parameter`参数传入键值对`{"name":"Jack"}`。自定义参数将自动替换变量值`name`，得到一条新的脚本，实际执行的是`echo Jack`。

 自定义参数的个数范围：0~10

 -   键不允许为空字符串，最多支持64个字符。
-   值允许为空字符串。
-   自定义参数与原始脚本内容在Base64编码后，综合长度不能超过16KB。
-   设置的自定义参数名集合必须为创建脚本时定义的参数集的子集。对于未传入的参数，您可以使用空字符串代替。

默认值：空，表示取消设置该参数从而禁用自定义参数。 |
|KeepCommand|Boolean|否|false|执行完该脚本后，是否保留下来。取值范围：

 -   true：保留。可以通过InvokeCommand再次执行。会占用云助手脚本的保有量配额。
-   false：不保留。执行完成后自动删除，不占用云助手脚本的保有量配额。

 默认值：false |
|ContentEncoding|String|否|Base64|脚本内容（`CommandContent`）的编码方式。取值范围（不区分大小写）：

 -   PlainText：不编码，采用明文传输。
-   Base64：Base64编码。

 默认值：PlainText，乱填或错填该取值会当作PlainText处理。 |
|Username|String|否|root|在ECS实例中执行脚本的用户名称。目前仅支持Linux系统的ECS实例，默认以root用户执行脚本。您也可以指定实例中已存在的其它用户执行脚本。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|CommandId|String|c-7d2a745b412b4601b2d47f6a768d\*\*\*\*|脚本ID。 |
|InvokeId|String|t-7d2a745b412b4601b2d47f6a768d\*\*\*\*|脚本执行ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
http(s)://ecs.aliyuncs.com/?Action=RunCommand
&CommandContent='echo hello'
&InstanceId.1=i-bp185dy2o3o6neg****
&Name=Test
&RegionId=cn-hangzhou
&Type=RunShellScript
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RunCommandResponse>
        <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
        <CommandId>c-7d2a745b412b4601b2d47f6a768d****</CommandId>
        <InvokeId>t-7d2a745b412b4601b2d47f6a768d****</InvokeId>
</RunCommandResponse>
```

`JSON` 格式

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "CommandId": "c-7d2a745b412b4601b2d47f6a768d****",
    "InvokeId": "t-7d2a745b412b4601b2d47f6a768d****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发送请求时发生错误，请稍后重试。|
|403|InvalidCmdType.NotFound|The specified command type does not exist.|指定的命令类型不存在。|
|403|CmdName.ExceedLimit|The length of the command name exceeds the upper limit.|命令名称长度超过上限。|
|403|CmdDesc.ExceedLimit|The length of the command description exceeds the upper limit.|命令描述长度超过上限。|
|403|CmdCount.ExceedQuota|The total number of commands in the current region exceeds the quota.|当前地域下的云助手命令数量已超出限。|
|404|InvalidInstance.NotFound|The specified instance does not exist.|指定的实例不存在。|
|403|MissingParam.Frequency|The frequency must be specified when you create a timed task.|创建定时任务时必须指定频率。|
|403|InstanceIds.ExceedLimit|The number of instance IDs exceeds the upper limit.|目标实例数量超过上限。|
|403|Username.ExceedLimit|The length of the username exceeds the upper limit.|用户名长度超过上限。|
|403|Username.NotSupportWindows|Running as specified user has not supported for Windows yet.|指定用户执行暂不支持Windows实例。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

