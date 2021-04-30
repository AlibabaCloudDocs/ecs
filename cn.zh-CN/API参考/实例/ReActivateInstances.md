# ReActivateInstances

调用ReActivateInstances重新启动一台已过期或欠费回收的按量付费ECS实例。

## 接口说明

调用该接口时，您需要注意：

-   实例必须处于**已过期**（`Stopped`）或者**欠费回收中**（`Stopped`）的状态。
-   您必须在实例欠费停机后15天内结清账单并重开机实例。结清欠费账单后如果没有重开机，实例在欠费之日起15天后自动释放，数据无法恢复。当重开机VPC类型的按量付费实例时，可能会重开机失败。请间隔一段时间后再试或[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)。
-   结清欠费后，您的阿里云账户余额（即现金余额）和代金券的总值不得小于100.00元人民币，否则无法重新启动实例。更多业务限制，请参见[重开机实例](~~34374~~)。
-   接口调用成功后实例进入**启动中**（`Starting`）状态。
-   被安全锁定的ECS实例的`OperationLocks`参数包含`"LockReason": "security"`时，不支持调用该接口。详情请参见[安全锁定时的API行为](~~25695~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ReActivateInstances&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ReActivateInstances|系统规定参数。取值：ReActivateInstances |
|InstanceId|String|是|i-bp67acfmxazb4p\*\*\*\*|需要重开机的实例ID。 |
|RegionId|String|否|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|51AB7717-6E1A-4D1D-A44D-54CB123ABC|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ReActivateInstances
&RegionId=cn-hangzhou
&InstanceId=i-bp67acfmxazb4p****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ReActivateInstancesResponse>
      <RequestId>51AB7717-6E1A-4D1D-A44D-54CB123ABC</RequestId>
</ReActivateInstancesResponse>
```

`JSON`格式

```
{
	"RequestId": "51AB7717-6E1A-4D1D-A44D-54CB123ABC"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidPayType.NotSupport|The specified pre pay instance not support.|包年包月实例不支持该操作。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|InsufficientBalance|Your account does not have enough balance.|账户余额不足，请先充值再操作。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|ReopenInstance.InstanceStatusNotValid|Instance status is not Expired, ImageExpired or EcsAndImageExpired.|实例重启失败，原因是实例或镜像未过期。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

