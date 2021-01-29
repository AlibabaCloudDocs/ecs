# DescribeInstanceMaintenanceAttributes

调用DescribeInstanceMaintenanceAttributes查询实例的维护属性。

## 接口说明

查询已设定的维护策略，策略中主要包括两个维护属性。

-   维护时间窗口：您指定的一个时间段，运维只会在该时间内进行。
-   维护动作：您指定的实例宕机处理策略。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceMaintenanceAttributes&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeInstanceMaintenanceAttributes|系统规定参数。取值：DescribeInstanceMaintenanceAttributes |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|InstanceId.N|RepeatList|否|i-bp67acfmxazb4p\*\*\*\*|实例ID。N的取值范围为：1~100 |
|PageNumber|Long|否|1|维护属性列表的页码。

 起始值：1

 默认值：1 |
|PageSize|Long|否|10|单页返回的条数。取值范围：1~100

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|MaintenanceAttributes|Array of MaintenanceAttribute| |运维属性的集合。 |
|MaintenanceAttribute| | | |
|ActionOnMaintenance|Struct| |实例的运维动作属性。 |
|DefaultValue|String|AutoRecover|维护动作，默认的值。 |
|SupportedValues|List|"SupportedValue": \["Stop", "AutoRecover"\]|由维护动作组成的数组格式，返回支持的运维动作值。 |
|Value|String|Stop|维护动作，当前生效的值。可能值：

 -   Stop: 停止状态（即宕机）。
-   AutoRecover：自动恢复。
-   AutoRedeploy：宕机迁移，数据盘有损。 |
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|实例ID。 |
|MaintenanceWindows|Array of MaintenanceWindow| |运维窗口实例的列表。 |
|MaintenanceWindow| | | |
|EndTime|String|18:00:00|维护时间窗口结束时间。 |
|StartTime|String|02:00:00|维护时间窗口开始时间。 |
|NotifyOnMaintenance|Boolean|false|实例宕机运维前是否发送事件通知。 |
|PageNumber|Integer|1|维护属性列表的页码。 |
|PageSize|Integer|10|单页返回的条数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|100|查询到的维护属性总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com?Action=DescribeMaintenanceProperty
&InstanceId.1=i-bp67acfmxazb4p****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeInstanceMaintenanceAttributesResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <TotalCount>100</TotalCount>
      <InstanceMaintenanceAttributes>
            <InstanceMaintenanceAttribute>
                  <InstanceId>i-bp67acfmxazb4ph***</InstanceId>
                  <NotifyOnMaintenance>false</NotifyOnMaintenance>
                  <MaintenanceWindows>
                        <MaintenanceWindow>
                              <StartTime>02:00:00</StartTime>
                              <EndTime>18:00:00</EndTime>
                        </MaintenanceWindow>
                  </MaintenanceWindows>
                  <ActionOnMaintenance>
                        <Value>Stop</Value>
                        <DefaultValue>AutoRecover</DefaultValue>
                        <SupportedValues>
                              <SupportedValue>Stop</SupportedValue>
                              <SupportedValue>AutoRecover</SupportedValue>
                        </SupportedValues>
                  </ActionOnMaintenance>
            </InstanceMaintenanceAttribute>
      </InstanceMaintenanceAttributes>
</DescribeInstanceMaintenanceAttributesResponse>
```

`JSON`格式

```
{
	"RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"PageNumber": 1,
	"PageSize": 10,
	"TotalCount": 100,
	"InstanceMaintenanceAttributes": {
		"InstanceMaintenanceAttribute": [{
			"InstanceId": "i-bp67acfmxazb4ph***",
            "NotifyOnMaintenance": false,
			"MaintenanceWindows ": {
				"MaintenanceWindow": [{
					"StartTime": "02:00:00",
					"EndTime": "18:00:00"
				}]
			},
			"ActionOnMaintenance": {
				"Value": "Stop",
				"DefaultValue": "AutoRecover",
				"SupportedValues": {
					"SupportedValue": ["Stop", "AutoRecover"]
				}
			}
		}]
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|403|InvalidParameter|%s|无效的参数。|
|403|InstanceIdLimitExceeded|%s|指定的InstanceId个数不能超过100个。|
|403|OperationDenied.NotInWhiteList|%s|该操作无效，请先加入白名单。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

