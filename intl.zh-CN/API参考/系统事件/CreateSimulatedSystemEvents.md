# CreateSimulatedSystemEvents

调用CreateSimulatedSystemEvents为一台或多台ECS实例预约模拟系统事件。模拟系统事件相当于事件演习，不会真正执行事件，也不会对ECS实例产生影响。

## 接口说明

预约模拟事件后，您可以通过ECS管理控制台、[ECS API](~~63962~~)和云监控服务查看已经预约的模拟系统事件。

下表为模拟系统事件的生命周期：

-   Scheduled（计划中）：预约后，模拟系统事件自动切换为Scheduled状态。
-   Executed（已完成）：在没有人为干预的情况下，模拟系统事件在指定时间点（NotBefore）自动变成Executed状态。
-   Canceled（已取消）：您调用[CancelSimulatedSystemEvents](~~88808~~)取消模拟系统事件后，变成Canceled状态。
-   Avoided（已避免）：对于因系统维护实例重启（SystemMaintenance.Reboot）的模拟系统事件，可以通过在指定时间点前[重启实例](~~25502~~)而变成Avoided状态。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateSimulatedSystemEvents&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateSimulatedSystemEvents|系统规定参数。取值：CreateSimulatedSystemEvents |
|EventType|String|是|SystemMaintenance.Reboot|系统事件的类型。取值范围：

 -   SystemMaintenance.Reboot：因系统维护实例重启
-   SystemFailure.Reboot：因系统错误实例重启
-   InstanceFailure.Reboot：因实例错误实例重启
-   SystemMaintenance.Stop：因系统维护实例停止
-   SystemMaintenance.Redeploy：因系统维护实例重新部署
-   SystemFailure.Redeploy：因系统错误实例重新部署
-   SystemFailure.Stop：因系统错误实例重新停止
-   InstanceFailure.Reboot：因实例错误实例重启 |
|InstanceId.N|RepeatList|是|i-bp1gtjxuuvwj17zr\*\*\*\*|一个或者多个ECS实例ID。N的取值范围：1~100，多个取值使用重复列表的形式。 |
|NotBefore|String|是|2018-12-01T06:32:31Z|事件计划执行的开始时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 **说明：** 对于系统错误或实例错误导致的异常事件，创建后事件处于正在执行（`Executing`）的一个中间状态，此时参数`NotBefore`为事件变为`Executed`状态的时间。 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|EventIdSet|List|" EventId " : \[ " e-bp16helosl7v0ooj\*\*\*\* " \]|模拟事件ID（EventId）列表。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateSimulatedSystemEvents
&EventType=SystemMaintenance.Reboot
&InstanceId.1=i-bp1gtjxuuvwj17zr****
&NotBefore=2018-12-01T06:32:31Z
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateSimulatedSystemEventsResponse>
	  <EventIdSet>
		    <EventId>e-bp191hqye34x****</EventId>
		    <EventId>e-bp191hqye34y****</EventId>
	  </EventIdSet>
          <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</CreateSimulatedSystemEventsResponse>
```

`JSON` 格式

```
{
    "EventIdSet":{
        "EventId":[
            "e-bp191hqye34x****",
            "e-bp191hqye34y****"
        ]
    },
    "RequestId":"679E9056-9B75-4306-8A72-A1DF93EBEF74"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|403|InvalidParameter|%s|无效的参数。|
|403|InvalidNotBefore.Passed|%s|指定的NotBefore不能早于当前时间。|
|404|InvalidInstanceId.NotFound|%s|指定的实例不存在，请确认参数InstanceId是否正确。|
|403|SimulatedEventLimitExceeded|%s|超出模拟事件限制。|
|403|InstanceIdLimitExceeded|%s|指定的InstanceId个数不能超过100个。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

