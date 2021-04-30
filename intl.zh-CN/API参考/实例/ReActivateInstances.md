# ReActivateInstances

调用ReActivateInstances重新启动一台已过期或欠费回收的按量付费ECS实例。

## 接口说明

调用该接口时，您需要注意：

-   实例必须处于**已过期**（`Stopped`）的状态。
-   为避免实例会被释放和无法恢复数据，您必须在实例欠费停机后15天内清理账单并重开机实例。无法重开机VPC类型实例时，请间隔一段时间后再试或[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)联系阿里云。
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

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

