# ModifyCommand

调用ModifyCommand修改一条云助手命令相关参数以及命令内容。

## 接口说明

命令执行期间也允许修改，修改命令后，后续执行会按照新的命令内容执行。

您不能修改命令的类型，例如，如果命令是Shell命令（RunShellScript），则不能修改为Bat命令（RunBatScript）。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyCommand&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyCommand|系统规定参数。取值：ModifyCommand |
|CommandId|String|是|c-hz01272yr52\*\*\*\*|命令ID。您可以通过接口[DescribeCommands](~~64843~~)查询所有可用的CommandId。 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Name|String|否|test-CommandName|命令名称。支持全字符集，长度不得超过128个字符。 |
|Description|String|否|This is description.|命令描述。支持全字符集，长度不得超过512个字符。 |
|WorkingDir|String|否|/home/|执行路径。 |
|Timeout|Long|否|120|您创建的命令在ECS实例中执行时最大的超时时间，单位为秒。当无法在配置的时间内运行并完成您创建的命令时，会出现超时现象。超时后，会强制终止命令进程，即取消命令的PID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|0DE9B41E-EF0D-40A0-BB43-37749C5BDA9C|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyCommand
&CommandId=c-hz01272yr52****
&RegionId=cn-hangzhou
&Name=test-CommandName
&Description=This is description.
&CommandContent=c2VydmljZSB0b21jYXQgc3RhcnQ=
&WorkingDir=/home/
&Timeout=120
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyCommandResponse>
      <RequestId>0DE9B41E-EF0D-40A0-BB43-37749C5BDA9C</RequestId>
</ModifyCommandResponse>
```

`JSON`格式

```
{
    "RequestId": "0DE9B41E-EF0D-40A0-BB43-37749C5BDA9C"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidCmdId.NotFound|The specified command ID does not exist.|指定的CommandId参数有误，请检查参数值是否正确。您可以通过接口DescribeCommands查询所有可用的CommandId。|
|404|InvalidCmdType.NotFound|The specified command type does not exist.|指定的命令类型不存在。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

