# RebootInstance

当一台ECS实例处于运行中（Running）状态时，调用RebootInstance可以重启这台实例。

## 接口说明

-   您只能重启状态为**运行中**（`Running`）的ECS实例。
-   重启ECS实例后进入**启动中**（`Starting`）状态。
-   支持强制重启（`ForceStop`），强制重启等同于传统服务器的断电重启，可能丢失实例操作系统中未写入磁盘的数据。
-   被安全锁定的ECS实例的`OperationLocks`参数包含"LockReason": "security"时，不能重启实例。更多信息，请参见[安全锁定时的API行为](~~25695~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=RebootInstance&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RebootInstance|系统规定参数。取值：RebootInstance |
|InstanceId|String|是|i-bp67acfmxazb4ph\*\*\*\*|指定实例的ID。 |
|ForceStop|Boolean|否|false|重启ECS实例前，是否强制关机。取值范围：

 -   true：强制关机。相当于典型的断电操作，所有未写入存储设备的缓存数据会丢失。
-   false（默认）：正常关机。 |
|DryRun|Boolean|否|false|是否只预检此次请求。取值范围：

 -   true：发送检查请求，不会重启实例。检查项包括是否填写了必选参数、请求格式、业务限制和ECS库存。如果检查不通过，则返回对应错误。如果检查通过，则返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后直接重启实例。

 默认值：false |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=RebootInstance
&InstanceId=i-bp67acfmxazb4ph****
&ForceStop=false
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RebootInstanceResponse>
      <RequestId>F2E2C40D-AB09-45A1-B5C5-EB9F5C4E4E4A</RequestId>
</RebootInstanceResponse>
```

`JSON` 格式

```
{
    "RequestId": "F2E2C40D-AB09-45A1-B5C5-EB9F5C4E4E4A"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|DiskError|IncorrectDiskStatus.|指定的磁盘状态不合法。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|IncorrectInstanceStatus|%s|当前实例的状态不支持此操作。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

