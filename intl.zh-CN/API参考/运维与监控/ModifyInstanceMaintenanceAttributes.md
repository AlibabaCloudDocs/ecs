# ModifyInstanceMaintenanceAttributes

调用ModifyInstanceMaintenanceAttributes修改实例的维护属性。

## 接口说明

修改实例的维护策略，策略中包含两个维护属性。

-   维护时间窗口：您指定的一段时间，运维只会在该时间内进行。
-   维护动作：您指定的实例宕机处理策略。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceMaintenanceAttributes&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyInstanceMaintenanceAttributes|系统规定参数。取值：ModifyInstanceMaintenanceAttributes |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|InstanceId.N|RepeatList|否|i-bp67acfmxazb4ph\*\*\*\*|实例ID。N的取值范围为：1~100 |
|MaintenanceWindow.N.StartTime|String|否|02:00:00|维护时间窗口开始时间。必须为整小时，不允许设置分、秒。开始时间和结束时间必须同时设置，并且结束时间与开始时间需要间隔1~23个整小时。采用UTC +8时区，格式为`HH:mm:ss`。N的取值为1，只支持设置1个时间窗口。 |
|MaintenanceWindow.N.EndTime|String|否|18:00:00|维护时间窗口结束时间。必须为整小时，不允许设置分、秒。开始时间和结束时间必须同时设置，并且结束时间与开始时间需要间隔1~23个整小时。采用UTC +8时区，格式为`HH:mm:ss`。N的取值为1，只支持设置1个时间窗口。 |
|ActionOnMaintenance|String|否|AutoRecover|维护动作。取值范围：

 -   Stop：停止状态（即宕机）。
-   AutoRecover：自动恢复。
-   AutoRedeploy：宕机迁移，数据盘有损。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com?Action=ModifyInstanceMaintenanceAttributes
&InstanceId.1=i-bp67acfmxazb4ph****
&ActionOnMaintenance=AutoRecover
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyInstanceMaintenanceAttributesResponse>    
    <RequestId>E69FF3CC-94DD-42EF-8836-F33C45EDF9945ED</RequestId>
<ModifyInstanceMaintenanceAttributesResponse>
```

`JSON` 格式

```
{
	"RequestId": "E69FF3CC-94DD-42EF-8836-F33C45EDF9945ED"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|%s|指定的实例不存在，请确认参数InstanceId是否正确。|
|403|InvalidParameter|%s|无效的参数。|
|403|OperationDenied.NotInWhiteList|%s|该操作无效，请先加入白名单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

