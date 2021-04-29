# DescribeInvocations

调用DescribeInvocations查询云助手命令的执行列表和状态。

## 接口说明

-   当您执行命令后，不代表命令一定成功运行，并且一定有预期的命令效果。您需要通过接口返回值查看实际执行结果，以实际输出结果为准。
-   您可以查询最近2周的执行信息，执行信息的保留上限为10万条。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeInvocations&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeInvocations|系统规定参数。取值：DescribeInvocations |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|InvokeId|String|否|t-hz0jdfwd9f\*\*\*\*|命令执行ID。 |
|CommandId|String|否|c-hz0jdfwcsr\*\*\*\*|命令ID。您可以通过接口[DescribeCommands](~~64843~~)查询所有可用的CommandId。 |
|CommandName|String|否|CommandTestName|命令名称。 |
|CommandType|String|否|RunShellScript|命令类型。 |
|Timed|Boolean|否|true|查询的命令是否在将来会自动执行。取值范围：

 -   true：查询在调用`RunCommand`或`InvokeCommand`执行命令时，`RepeatMod`参数取值为`Period`、`NextRebootOny`或者`EveryReboot`，且处于未被取消的未完成状态命令或者未被停止的未完成状态命令。
-   false：查询以下两种状态的命令：
    -   在调用`RunCommand`或`InvokeCommand`执行命令时，`RepeatMod`参数取值为`Once`。
    -   已被取消、被停止或者已完成执行的命令。

 默认值：false |
|InvokeStatus|String|否|Finished|命令执行的总执行状态。总执行状态取决于创建执行中的一台或多台实例的共同执行状态。取值范围：

 -   Running：
    -   周期执行：未手动停止周期执行命令前，执行状态一直为进行中。
    -   单次执行：一旦有进行中的命令进程，总的执行状态就为进行中。
-   Finished：
    -   周期执行：命令进程不可能为执行完成。
    -   单次执行：所有实例全部完成执行。或者手动停止部分实例的命令进程，其余实例全部执行完成。
-   Failed：
    -   周期执行：命令进程不可能为执行失败。
    -   单次执行：所有实例全部执行失败。
-   PartialFailed：
    -   周期执行：命令进程不可能为部分失败。
    -   单次执行：部分实例有执行失败的命令进程，则总执行状态为部分失败。
-   Stopped：停止命令。

 默认值：Running |
|InstanceId|String|否|i-bp1i7gg30r52z2em\*\*\*\*|实例ID。当您传入了该参数，将查询该实例所有的命令执行记录。 |
|ContentEncoding|String|否|PlainText|设置返回数据中`CommandContent`字段和`Output`字段的编码方式。取值范围：

 -   PlainText：返回原始命令内容和输出信息。
-   Base64：返回Base64编码后的命令内容和输出信息。

 默认值：Base64 |
|IncludeOutput|Boolean|否|false|是否在结果中返回命令运行的输出信息。

 -   true：返回。此时，您至少指定参数`InvokeId`或`InstanceId`。
-   false：不返回。

 默认值：false |
|PageNumber|Long|否|1|当前页码。

 起始值：1

 默认值：1 |
|PageSize|Long|否|10|分页查询时设置的每页行数。

 最大值：50

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Invocations|Array of Invocation| |命令执行记录组成的数组。 |
|Invocation| | | |
|CommandContent|String|cnBtIC1xYSB8IGdyZXAgdnNm\*\*\*\*|命令内容，以Base64编码后传输。 |
|CommandId|String|c-hz0jdfwcsr\*\*\*\*|命令ID。 |
|CommandName|String|CommandTestName|命令名称。 |
|CommandType|String|RunShellScript|命令类型。 |
|CreationTime|String|2020-01-19T09:15:46Z|任务的创建时间。 |
|Frequency|String|0 \*/20 \* \* \* \*|周期执行命令的执行周期。该参数值结构以[Cron表达式](~~64769~~)为准。 |
|InvocationStatus|String|Running|命令执行的总执行状态，总执行状态取决于本次调用的全部实例的共同执行状态，可能值：

 -   Pending：系统正在校验或发送命令。存在至少一台实例的命令执行状态为Pending，则总执行状态为Pending。
-   Scheduled：周期执行的命令已发送，等待运行。存在至少一台实例的命令执行状态为Scheduled，则总执行状态为Scheduled。
-   Running：命令正在实例上运行。存在至少一台实例的命令执行状态为Running，则总执行状态为Running。
-   Success：各个实例上的命令执行状态均为Stopped或Success，且至少一个实例的命令执行状态是Success，则总执行状态为Success。
    -   立即运行的任务：命令执行完成，且退出码为0。
    -   周期运行的任务：最近一次执行成功且退出码为0，且指定的周期已全部完成。
-   Failed：各个实例上的命令执行状态均为Stopped或Failed，则总执行状态为Failed。实例上的命令执行状态一项或多项为以下状态时，返回值均为Failed状态：
    -   命令校验失败（Invalid）
    -   命令发送失败（Aborted）
    -   命令执行完成但退出码非0（Failed）
    -   命令执行超时（Timeout）
    -   命令执行异常（Error）
-   Stopping：正在停止任务。存在至少一台实例的命令执行状态为Stopping，则总执行状态为Stopping。
-   Stopped：任务已停止。所有实例的命令执行状态是Stopped，则总执行状态为Stopped。实例上的命令执行状态为以下状态时，返回值均为Stopped状态：
    -   任务已取消（Cancelled）
    -   任务已终止（Terminated）
-   PartialFailed：部分实例执行成功且部分实例执行失败。各个实例的命令执行状态均为Success、Failed或Stopped，则总执行状态为PartialFailed。

**说明：** 返回参数中的`InvokeStatus`与该参数意义相似，但建议您查看该返回值。 |
|InvokeId|String|t-hz0jdfwd9f\*\*\*\*|命令执行ID。 |
|InvokeInstances|Array of InvokeInstance| |执行目标实例集类型。 |
|InvokeInstance| | | |
|CreationTime|String|2019-12-20T06:15:54Z|命令执行的开始时间。 |
|Dropped|Integer|0|Output字段中文字长度超出24KB后，截断丢弃的文字长度。 |
|ErrorCode|String|InstanceNotExists|命令的下发失败或执行失败原因的代码，可能值：

 -   空：命令运行正常。
-   InstanceNotExists：指定的实例不存在或已释放。
-   InstanceReleased：执行命令期间，该实例被释放。
-   InstanceNotRunning：开始执行命令时，该实例不在运行中。
-   CommandNotApplicable：命令不适用于指定的实例。
-   AccountNotExists：指定的帐号不存在。
-   DirectoryNotExists：指定的目录不存在。
-   BadCronExpression：指定的周期表达式不合法。
-   ClientNotRunning：云助手客户端未运行。
-   ClientNotResponse：云助手客户端无响应。
-   ClientIsUpgrading：云助手客户端正在升级中。
-   ClientNeedUpgrade：云助手客户端需要升级。
-   DeliveryTimeout：发送命令超时。
-   ExecutionTimeout：命令执行超时。
-   ExecutionException：命令执行发生异常。
-   ExecutionInterrupted：命令执行任务中断。
-   ExitCodeNonzero：命令执行结束，退出码非0。 |
|ErrorInfo|String|the specified instance does not exists|命令的下发失败或执行失败原因的详情，可能值：

 -   空：命令运行正常。
-   the specified instance does not exists：指定的实例不存在或已释放。
-   the instance has released when create task：执行命令期间，该实例被释放。
-   the instance is not running when create task：开始执行命令时，该实例不在运行中。
-   the command is not applicable：命令不适用于指定的实例。
-   the specified account does not exists：指定的帐号不存在。
-   the specified directory does not exists：指定的目录不存在。
-   the cron job expression is invalid：指定的周期表达式不合法。
-   the aliyun service is not running on the instance：云助手客户端未运行。
-   the aliyun service in the instance does not response：云助手客户端无响应。
-   the aliyun service in the instance is upgrading now：云助手客户端正在升级中。
-   the aliyun service in the instance need upgrade：云助手客户端需要升级。
-   the command delivery has been timeout：发送命令超时。
-   the command execution has been timeout：命令执行超时。
-   the command execution got an exception：命令执行发生异常。
-   the command execution has been interrupted：命令执行任务中断。
-   the command execution exit code is not zero：命令执行结束，退出码非0。 |
|ExitCode|Long|0|命令进程的退出代码。可能值：

 -   Linux实例为Shell进程的退出码。
-   Windows实例为Bat或者PowerShell进程的退出码。 |
|FinishTime|String|2019-12-20T06:15:56Z|命令进程的结束时间。 |
|InstanceId|String|i-bp1i7gg30r52z2em\*\*\*\*|实例ID。 |
|InstanceInvokeStatus|String|Finished|**说明：** 不推荐查看该返回值，推荐您查看`InvocationStatus`的返回值。 |
|InvocationStatus|String|Success|单台实例的命令进度状态，可能值：

 -   Pending：系统正在校验或发送命令。
-   Invalid：指定命令类型或参数有误。
-   Aborted：向实例发送命令失败。实例必须在运行中，且命令可以1分钟内发送完成。
-   Running：命令正在实例上运行。
-   Success：
    -   单次执行的命令：命令执行完成，且退出码为0。
    -   周期执行的命令：上一次运行成功且退出码为0，且指定的周期已结束。
-   Failed：
    -   单次执行的命令：命令执行完成，且退出码非0。
    -   周期执行的命令：上一次运行成功且退出码非0，且指定的周期将中止。
-   Error：命令执行时发生异常无法继续。
-   Timeout：命令执行超时。
-   Cancelled：命令的执行动作已经取消，命令未曾启动。
-   Stopping：正在停止任务。
-   Terminated：命令运行时被终止。
-   Scheduled：
    -   单次执行的命令：不适用，不会出现。
    -   周期执行的命令：等待运行。 |
|Output|String|OutPutTestmsg|命令的输出信息。 |
|Repeats|Integer|0|命令在该实例上执行的次数。

 -   若执行方式为单次执行，则值为0或1。
-   若执行方式为周期执行，则值为执行过多少次。 |
|StartTime|String|2019-12-20T06:15:55Z|命令在实例中开始执行的时间。 |
|StopTime|String|2020-01-19T09:15:47Z|若调用了`StopInvocation`，表示调用的时间。 |
|Timed|Boolean|false|查询的命令是否在将来会自动执行。 |
|UpdateTime|String|2020-01-19T09:15:47Z|命令状态的更新时间。 |
|InvokeStatus|String|Finished|命令总的执行状态。

 **说明：** 不推荐查看该返回值，推荐您查看`InvocationStatus`的返回值。 |
|Parameters|String|\{\}|命令中的自定义参数。 |
|RepeatMode|String|Once|命令执行的方式。可能值：

 -   Once：立即执行命令。
-   Period：定时执行命令。
-   NextRebootOnly：当实例下一次启动时，自动执行命令。
-   EveryReboot：实例每一次启动都将自动执行命令。 |
|Timed|Boolean|false|查询的命令是否在将来会自动执行。 |
|Username|String|root|ECS实例中执行命令的用户名称。 |
|PageNumber|Long|1|查询结果的页码。 |
|PageSize|Long|10|每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Long|1|命令总个数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeInvocations
&RegionId=cn-hangzhou
&InvokeId=t-hz0jdfwd9f****
&CommandId=c-hz0jdfwcsr****
&CommandName=CommandTestName
&CommandType=RunShellScrip
&Timed=true
&InvokeStatus=Finished
&InstanceId=i-bp1i7gg30r52z2em****
&PageNumber=1
&PageSize=10
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeInvocationsResponse>
      <TotalCount>1</TotalCount>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
      <Invocations>
            <Invocation>
                  <InvocationStatus>Running</InvocationStatus>
                  <Parameters>{}</Parameters>
                  <Timed>false</Timed>
                  <InvokeInstances>
                        <InvokeInstance>
                              <Dropped>0</Dropped>
                              <InvocationStatus>Success</InvocationStatus>
                              <InstanceId>i-bp1i7gg30r52z2em****</InstanceId>
                              <Timed>false</Timed>
                              <InstanceInvokeStatus>Finished</InstanceInvokeStatus>
                              <ExitCode>0</ExitCode>
                              <ErrorInfo></ErrorInfo>
                              <StartTime>2019-12-20T06:15:55Z</StartTime>
                              <Repeats>0</Repeats>
                              <FinishTime>2019-12-20T06:15:56Z</FinishTime>
                              <Output>OutPutTestmsg</Output>
                              <CreationTime>2019-12-20T06:15:54Z</CreationTime>
                              <UpdateTime>2020-01-19T09:15:47Z</UpdateTime>
                              <ErrorCode></ErrorCode>
                              <StopTime>2020-01-19T09:15:47Z</StopTime>
                        </InvokeInstance>
                  </InvokeInstances>
                  <CommandContent>cnBtIC1xYSB8IGdyZXAgdnNm****</CommandContent>
                  <RepeatMode>Once</RepeatMode>
                  <InvokeStatus>Finished</InvokeStatus>
                  <CommandType>RunShellScript</CommandType>
                  <Username>root</Username>
                  <CreationTime>2020-01-19T09:15:46Z</CreationTime>
                  <Frequency></Frequency>
                  <CommandId>c-hz0jdfwcsr****</CommandId>
                  <CommandName>CommandTestName</CommandName>
                  <InvokeId>t-hz0jdfwd9f****</InvokeId>
            </Invocation>
      </Invocations>
</DescribeInvocationsResponse>
```

`JSON`格式

```
{
  "TotalCount": 1,
  "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
  "PageSize": 10,
  "PageNumber": 1,
  "Invocations": {
    "Invocation": [
      {
        "InvocationStatus": "Running",
        "Parameters": "{}",
        "Timed": false,
        "InvokeInstances": {
          "InvokeInstance": [
            {
              "Dropped": 0,
              "InvocationStatus": "Success",
              "InstanceId": "i-bp1i7gg30r52z2em****",
              "Timed": false,
              "InstanceInvokeStatus": "Finished",
              "ExitCode": 0,
              "ErrorInfo": "",
              "StartTime": "2019-12-20T06:15:55Z",
              "Repeats": 0,
              "FinishTime": "2019-12-20T06:15:56Z",
              "Output": "OutPutTestmsg",
              "CreationTime": "2019-12-20T06:15:54Z",
              "UpdateTime": "2020-01-19T09:15:47Z",
              "ErrorCode": "",
              "StopTime": "2020-01-19T09:15:47Z"
            }
          ]
        },
        "CommandContent": "cnBtIC1xYSB8IGdyZXAgdnNm****",
        "RepeatMode": "Once",
        "InvokeStatus": "Finished",
        "CommandType": "RunShellScript",
        "Username": "root",
        "CreationTime": "2020-01-19T09:15:46Z",
        "Frequency": "",
        "CommandId": "c-hz0jdfwcsr****",
        "CommandName": "CommandTestName",
        "InvokeId": "t-hz0jdfwd9f****"
      }
    ]
  }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|RegionId.ApiNotSupported|The api is not supported in this region.|指定地域下不支持调用API。请检查RegionId参数取值是否正确。|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发送请求时发生错误，请稍后重试。|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|指定的PageNumber参数无效。|
|403|InvalidParam.PageSize|The specified parameter is invalid.|指定的PageSize参数无效。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

