# DescribeCommands

调用DescribeCommands查询您手动创建的云助手命令或者阿里云提供的公共命令。

## 接口说明

只输入参数`Action`和`RegionId`，不输入其他任何请求参数，则默认查询您手动创建的所有可用的命令（`CommandId`）。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeCommands&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeCommands|系统规定参数。取值：DescribeCommands |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Provider|String|否|AlibabaCloud|公共命令的提供者。参数值的具体说明如下：

 -   当该参数不传值时，默认查询您手动创建的所有云助手命令。
-   当该参数取值为`AlibabaCloud`时，查询由阿里云提供的所有公共命令。
-   当该参数的取值为具体的公共命令提供者时，查询该提供者提供的所有公共命令。例如：
    -   当`Provider=AlibabaCloud.ECS.GuestOS`时，查询`AlibabaCloud.ECS.GuestOS`提供的公共命令。
    -   当`Provider=AlibabaCloud.ECS.GuestOSDiagnose`时，查询`AlibabaCloud.ECS.GuestOSDiagnose`提供的公共命令。

 默认值：空 |
|CommandId|String|否|c-hz01272yr52\*\*\*\*|命令ID。 |
|Name|String|否|testName|命令的名称，暂不支持模糊查询。 |
|Description|String|否|testDescription|命令描述。 |
|Type|String|否|RunShellScript|命令的类型。取值范围：

 -   RunBatScript：命令为在Windows实例中运行的Bat脚本。
-   RunPowerShellScript：命令为在Windows实例中运行的PowerShell脚本。
-   RunShellScript：命令为在Linux实例中运行的Shell脚本。 |
|ContentEncoding|String|否|PlainText|设置返回数据中`CommandContent`字段和`Output`字段的编码方式。取值范围：

 -   PlainText：返回原始脚本内容和输出信息。
-   Base64：返回Base64编码后的脚本内容和输出信息。

 默认值：Base64 |
|PageNumber|Long|否|1|当前页码。起始值：1

 默认值：1 |
|PageSize|Long|否|10|分页查询时设置的每页行数。最大值：50

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Commands|Array of Command| |命令数据集类型。 |
|Command| | | |
|Category|String|阿里云-云服务器-实例系统|公共命令的类目。 |
|CommandContent|String|Y2QgL3Jvb3Q=|命令内容，以Base64编码后传输。 |
|CommandId|String|c-hz01272yr52\*\*\*\*|命令ID。 |
|CreationTime|String|2020-11-17T06:52Z|命令创建时间。 |
|Description|String|testDescription|命令描述。 |
|EnableParameter|Boolean|true|该命令是否启用自定义参数。 |
|InvokeTimes|Integer|2|使用该命令创建的任务数。 |
|Latest|Boolean|true|公共命令是否是最新版本。如果多个命令属于同一个`Provider`，且名称与类目相同，则这些命令属于同一个命令的不同版本。您手动创建的云助手命令不会返回该值。 |
|Name|String|testName|命令名称。 |
|ParameterNames|List|\['parameter1','parameter2'\]|通过创建命令时的CommandContent解析出的自定义参数名列表，以列表（List）的形式返回。如未使用自定义参数功能，则返回空值列表。 |
|Provider|String|AlibabaCloud.ECS.GuestOS|公共命令的提供者。 |
|Timeout|Long|3600|超时时间。 |
|Type|String|RunShellScript|命令类型。 |
|Version|Integer|1|公共命令的版本。如果多个命令属于同一个`Provider`，且名称与类目相同，则这些命令属于同一个命令的不同版本。您手动创建的云助手命令不会返回该值。 |
|WorkingDir|String|/home/|执行路径。 |
|PageNumber|Long|1|命令列表页码。 |
|PageSize|Long|10|每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Long|5|命令总个数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeCommands
&RegionId=cn-hangzhou
&CommandId=c-hz01272yr52****
&PageNumber=1
&PageSize=10
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeCommandsResponse>
      <TotalCount>1</TotalCount>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
      <Commands>
            <Command>
                  <Category></Category>
                  <Description>test1</Description>
                  <ParameterNames></ParameterNames>
                  <Timeout>3600</Timeout>
                  <Name>testName</Name>
                  <Provider></Provider>
                  <CommandContent>Y2QgL3Jvb3Q=</CommandContent>
                  <WorkingDir></WorkingDir>
                  <Type>RunShellScript</Type>
                  <InvokeTimes>2</InvokeTimes>
                  <CreationTime>2020-11-17T06:52Z</CreationTime>
                  <EnableParameter>false</EnableParameter>
                  <CommandId>c-hz01272yr52****</CommandId>
            </Command>
      </Commands>
</DescribeCommandsResponse>
```

`JSON`格式

```
{
	"TotalCount": 1,
	"RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"PageSize": 10,
	"PageNumber": 1,
	"Commands": {
		"Command": [
			{
				"Category": "",
				"Description": "test1",
				"ParameterNames": {
					"ParameterName": []
				},
				"Timeout": 3600,
				"Name": "testName",
				"Provider": "",
				"CommandContent": "Y2QgL3Jvb3Q=",
				"WorkingDir": "",
				"Type": "RunShellScript",
				"InvokeTimes": 2,
				"CreationTime": "2020-11-17T06:52Z",
				"EnableParameter": false,
				"CommandId": "c-hz01272yr52****"
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

