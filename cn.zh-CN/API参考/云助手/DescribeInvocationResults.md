# DescribeInvocationResults

调用DescribeInvocationResults查看一条或多条云助手命令的执行结果，即在ECS实例中的实际执行结果。

## 接口说明

-   当您执行命令后，不代表命令一定成功运行，并且一定有预期的命令效果。您需要通过本接口查看实际的具体执行结果，以实际输出结果为准。
-   您可以查询最近2周的执行信息，执行信息的保留上限为10万条。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeInvocationResults&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeInvocationResults|系统规定参数。取值：DescribeInvocationResults |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|InvokeId|String|否|t-hz0jdfwd9f\*\*\*\*|命令执行ID。命令进程执行ID。您可以通过接口[DescribeInvocations](~~64840~~)查询InvokeId。 |
|InstanceId|String|否|i-bp1i7gg30r52z2em\*\*\*\*|实例ID。 |
|CommandId|String|否|c-hz0jdfwcsr\*\*\*\*|命令ID。 |
|InvokeRecordStatus|String|否|Running|命令执行状态。取值范围：

 -   Running：运行中
-   Finished：已完成
-   Failed：失败
-   Stopped：已停止 |
|IncludeHistory|Boolean|否|false|是否返回周期性任务的历史记录。取值范围：

 -   true：表示返回周期性任务的执行结果。当取值为true时，参数`InvokeId`的取值不能为空，且必须为周期性任务的执行ID。
-   false：表示不返回。

 默认值：false |
|ContentEncoding|String|否|PlainText|设置返回数据中`Output`字段的编码方式，取值范围：

 -   PlainText：返回原始脚本内容和输出信息。
-   Base64：返回Base64编码后的脚本内容和输出信息。

 默认值：Base64 |
|PageNumber|Long|否|1|当前页码，起始值：1

 默认值：1 |
|PageSize|Long|否|1|分页查询时设置的每页行数。

 最大值：50

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Invocation|Struct| |命令执行结果的集合。 |
|InvocationResults|Array of InvocationResult| |命令执行结果集。 |
|InvocationResult| | | |
|CommandId|String|c-hz0jdfwcsr\*\*\*\*|命令ID。 |
|Dropped|Integer|0|`Output`字段中文字长度超出24 KB后，截断并丢弃的文字长度。 |
|ErrorCode|String|InstanceNotExists|命令的下发失败或执行失败原因的代码，可能值：

 -   空：命令运行正常。
-   InstanceNotExists：指定的实例不存在或已释放。
-   InstanceReleased：执行任务期间，该实例被释放。
-   InstanceNotRunning：创建任务时，该实例不在运行中。
-   CommandNotApplicable：命令不适用于指定的实例。
-   AccountNotExists：指定的帐号不存在。
-   DirectoryNotExists：指定的目录不存在。
-   BadCronExpression：指定的周期表达式不合法。
-   ClientNotRunning：云助手客户端未运行。
-   ClientNotResponse：云助手客户端无响应。
-   ClientIsUpgrading：云助手客户端正在升级中。
-   ClientNeedUpgrade：云助手客户端需要升级。
-   DeliveryTimeout：发送命令超时。
-   ExecutionTimeout：命令运行超时。
-   ExecutionException：命令运行发生异常。
-   ExecutionInterrupted：命令运行任务中断。
-   ExitCodeNonzero：命令执行结束，退出码非0。 |
|ErrorInfo|String|the specified instance does not exists|命令的下发失败或执行失败原因的详情，可能值：

 -   空：命令运行正常。
-   the specified instance does not exists：指定的实例不存在或已释放。
-   the instance has released when create task：执行任务期间，该实例被释放。
-   the instance is not running when create task：创建任务时，该实例不在运行中。
-   the command is not applicable：命令不适用于指定的实例。
-   the specified account does not exists：指定的帐号不存在。
-   the specified directory does not exists：指定的目录不存在。
-   the cron job expression is invalid：指定的周期表达式不合法。
-   the aliyun service is not running on the instance：云助手客户端未运行。
-   the aliyun service in the instance does not response：云助手客户端无响应。
-   the aliyun service in the instance is upgrading now：云助手客户端正在升级中。
-   the aliyun service in the instance need upgrade：云助手客户端需要升级。
-   the command delivery has been timeout：发送命令超时。
-   the command execution has been timeout：命令运行超时。
-   the command execution got an exception：命令运行发生异常。
-   the command execution has been interrupted：命令运行任务中断。
-   the command execution exit code is not zero：命令执行结束，退出码非0。 |
|ExitCode|Long|0|命令进程的退出码。

 -   Linux实例为Shell进程的退出码。
-   Windows实例为Bat或者PowerShell进程的退出码。 |
|FinishedTime|String|2019-12-20T06:15:56Z|命令进程的完成时间。如果命令进程出现超时情况，命令进程的完成时间以[CreateCommand](~~64844~~)中指定的参数TimedOut为准。 |
|InstanceId|String|i-bp1i7gg30r52z2em\*\*\*\*|实例ID。 |
|InvocationStatus|String|Success|单台实例的脚本进度状态，可能值：

 -   Pending：系统正在校验或发送命令。
-   Invalid：指定命令类型或参数有误。
-   Aborted：向实例发送命令失败。实例必须在运行中，且命令可以1分钟内发送完成。
-   Running：命令正在实例上运行。
-   Success：
    -   立即运行的任务：命令执行完成，且退出码为0。
    -   周期运行的任务：上一次运行成功且退出码为0，且指定的周期已结束。
-   Failed：
    -   立即运行的任务：命令执行完成，且退出码非0。
    -   周期运行的任务：上一次运行成功且退出码非0，且指定的周期将中止。
-   Error：命令执行时发生异常无法继续。
-   Timeout：命令执行超时。
-   Cancelled：任务已经取消，命令未曾启动。
-   Stopping：正在停止任务。
-   Terminated：命令运行时被终止。
-   Scheduled：
    -   立即运行的任务：不适用，不会出现。
    -   周期运行的任务：等待运行。 |
|InvokeId|String|t-hz0jdfwd9f\*\*\*\*|命令执行ID。 |
|InvokeRecordStatus|String|Running|命令执行状态。 |
|Output|String|MTU6MzA6MDEK|脚本进程的输出信息。 |
|Repeats|Integer|0|命令在该实例上执行的次数。

 -   若执行方式为立即执行，则值为0或1。
-   若执行方式为周期执行，则值为执行过多少次。 |
|StartTime|String|2019-12-20T06:15:55Z|脚本进程在实例中开始执行的时间。 |
|StopTime|String|2020-01-19T09:15:47Z|若调用了`StopInvocation`，则表示调用的时间。 |
|Username|String|root|在ECS实例中执行脚本的用户名称。 |
|PageNumber|Long|1|当前页码。 |
|PageSize|Long|1|分页查询时设置的每页行数。 |
|TotalCount|Long|1|命令总个数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeInvocationResults
&RegionId=cn-hangzhou
&InstanceId=i-bp1i7gg30r52z2em****
&PageNumber=1
&PageSize=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeInvocationResultsResponse>
      <RequestId>F416C43A-6581-4138-9503-4FBBC4EA1BB7</RequestId>
      <Invocation>
            <InvocationResults>
                  <InvocationResult>
                        <Dropped>0</Dropped>
                        <InvocationStatus>Failed</InvocationStatus>
                        <InstanceId>i-bp1i7gg30r52z2em****</InstanceId>
                        <ExitCode>1</ExitCode>
                        <ErrorInfo>the command execution exit code is not zero.</ErrorInfo>
                        <StartTime>2020-05-11T09:01:40Z</StartTime>
                        <Repeats>1</Repeats>
                        <InvokeRecordStatus>Finished</InvokeRecordStatus>
                        <FinishedTime>2020-05-11T09:01:41Z</FinishedTime>
                        <Output></Output>
                        <CommandId>c-hz0jdfwcsr****</CommandId>
                        <ErrorCode>ExitCodeNonzero</ErrorCode>
                        <InvokeId>t-hz0jdfwd9f****</InvokeId>
                        <StopTime></StopTime>
                  </InvocationResult>
            </InvocationResults>
            <TotalCount>5</TotalCount>
            <PageSize>1</PageSize>
            <PageNumber>1</PageNumber>
      </Invocation>
</DescribeInvocationResultsResponse>
```

`JSON` 格式

```
{
	"RequestId": "F416C43A-6581-4138-9503-4FBBC4EA1BB7",
	"Invocation": {
		"InvocationResults": {
			"InvocationResult": [
				{
					"Dropped": 0,
					"InvocationStatus": "Failed",
					"InstanceId": "i-bp1i7gg30r52z2em****",
					"ExitCode": 1,
					"ErrorInfo": "the command execution exit code is not zero.",
					"StartTime": "2020-05-11T09:01:40Z",
					"Repeats": 1,
					"InvokeRecordStatus": "Finished",
					"FinishedTime": "2020-05-11T09:01:41Z",
					"Output": "",
					"CommandId": "c-hz0jdfwcsr****",
					"ErrorCode": "ExitCodeNonzero",
					"InvokeId": "t-hz0jdfwd9f****",
					"StopTime": ""
				}
			]
		},
		"TotalCount": 5,
		"PageSize": 1,
		"PageNumber": 1
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发送请求时发生错误，请稍后重试。|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|指定的PageNumber参数无效。|
|403|InvalidParam.PageSize|The specified parameter is invalid.|指定的PageSize参数无效。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

