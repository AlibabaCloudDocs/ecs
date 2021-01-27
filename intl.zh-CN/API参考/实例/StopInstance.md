# StopInstance

调用StopInstance停止一台运行中（Running）的ECS实例。成功调用接口后，实例从停止中（Stopping）变成已停止（Stopped）状态。

## 接口说明

-   被安全锁定的ECS实例的`OperationLocks`参数包含"LockReason": "security"时，不能停止实例。更多信息，请参见[安全锁定时的API行为](~~25695~~)。
-   停止本地SSD型实例规格族：
    -   搭载了[本地盘](~~63138~~)的[i1规格族](~~25378#i1~~)实例，`ConfirmStop`为必选参数，取值为`true`后接口调用才会成功，否则会返回错误码。
    -   成功调用接口后，本地盘上的数据会被清空，您需要通过应用层的数据冗余保证数据可用性。
    -   ECS自动忽略其他实例规格族的`ConfirmStop`请求参数。
-   开通默认VPC内实例停机不收费功能后，您可以通过设置`StoppedMode=KeepCharging`保持停机收费，ECS实例停止后会继续计费，并为您保留ECS实例规格库存和公网IP地址。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=StopInstance&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|StopInstance|系统规定参数。取值：StopInstance |
|InstanceId|String|是|i-bp67acfmxazb4ph\*\*\*\*|指定的实例ID。 |
|StoppedMode|String|否|KeepCharging|停止按量付费ECS实例后，是否继续计费。取值：

 -   StopCharging：停止计费。有关`StopCharging`生效的条件，请参见[按量付费实例停机不收费](~~63353~~)的停机不收费开启条件章节。
-   KeepCharging：继续计费。

 默认值：如果您在ECS控制台上开启了VPC类型实例默认停机不收费（详情请参见[开启按量付费实例停机不收费](~~63353#default~~)），并符合开启条件，则默认为`StopCharging`。否则，默认为`KeepCharging`。 |
|ConfirmStop|Boolean|否|true|是否确认关机。仅对i1型实例规格族生效，且为i1型的实例规格族的必选参数。

 默认值：false |
|ForceStop|Boolean|否|false|停止实例时的是否强制关机策略。取值范围：

 -   true：强制关机。
-   false：正常关机流程。

 默认值：false |
|DryRun|Boolean|否|true|是否只预检此次请求。取值范围：

 -   true：发送检查请求，不会停止实例。检查项包括是否填写了必选参数、请求格式、业务限制和ECS库存。如果检查不通过，则返回对应错误。如果检查通过，则返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后直接停止实例。

 默认值：false |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1C488B66-B819-4D14-8711-C4EAAA13AC01|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=StopInstance
&InstanceId=i-bp67acfmxazb4ph****
&ConfirmStop=true
&ForceStop=false
&StoppedMode=KeepCharging
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<StopInstanceResponse>
      <RequestId>1C488B66-B819-4D14-8711-C4EAAA13AC01</RequestId>
</StopInstanceResponse>
```

`JSON` 格式

```
{
    "RequestId": "1C488B66-B819-4D14-8711-C4EAAA13AC01"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|DiskError|IncorrectDiskStatus|指定的磁盘状态不合法。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InstanceType.ParameterMismatch|The input parameter ConfirmStop must be true when an instance have localstorage.|当实例使用本地存储时，输入参数ConfirmStop必须为Ture。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|InvalidInstanceId.NotSupport|Classic network Instance does not support this operation.|经典网络类型的实例不支持此操作。|
|403|InvalidInstanceId.NotSupport|Pre pay instance does not support this operation.|包年包月实例不支持该操作。|
|403|InvalidInstanceId.NotSupport|Local disk instance does not support this operation.|本地盘实例不支持该操作。|
|403|InvalidInstanceId.NotSupport|Spot instance does not support this operation.|抢占式实例不支持该操作。|
|403|IncorrectInstanceStatus|%s|当前实例的状态不支持此操作。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

