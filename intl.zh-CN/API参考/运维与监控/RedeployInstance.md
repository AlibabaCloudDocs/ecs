# RedeployInstance

当ECS实例收到系统事件通知时，调用RedeployInstance可以重新部署这台ECS实例。

## 接口说明

RedeployInstance为异步调用接口，会重启并迁移实例。重新部署成功后，实例进入运行中（`Running`）状态。重新部署失败时，实例返回原有的物理服务器，并恢复到重新部署前的状态。

调用该接口时，您需要注意：

-   目标实例必须处于运行中或者已停止状态，调用接口后的实例状态变化：
    -   处于运行中（`Running`）的实例会进入停止中（`Stopping`）状态。
    -   处于已停止（`Stopped`）的实例会进入启动中（`Starting`）状态。
-   不支持重新部署专有宿主机上的实例。
-   被安全控制的实例的`OperationLocks`中标记了`"LockReason": "security"`时，不支持重新部署。
-   不支持响应通过CreateSimulatedSystemEvent创建的模拟事件。
-   在隔离本地盘的系统事件流程中，受损本地盘已隔离但尚未发出**因系统维护计划重启并重新初始化坏盘**事件（SystemMaintenance.RebootAndReInitErrorDisk）时，也可以调用RedeployInstance。更多详情，请参见[本地盘实例系统事件概述](~~107693~~)。

RedeployInstance能响应系统事件类型及事件状态请参见下表。

|事件名称及参数

|事件状态 |
|---------|------|
|因系统维护实例重启（SystemMaintenance.Reboot）

|Inquiring、Scheduled |
|因系统维护实例重新部署（SystemMaintenance.Redeploy）

|Inquiring、Scheduled |
|因系统维护重启并更换坏盘（SystemMaintenance.RebootAndIsolateErrorDisk）

|Inquiring |
|因系统维护重启并重新初始化坏盘（SystemMaintenance.RebootAndReInitErrorDisk）

|Inquiring |
|因系统错误实例重新部署（SystemFailure.Redeploy）

|Inquiring、Scheduled |
|仅限使用了本地盘的ECS实例：因系统错误实例重新启动（SystemFailure.Reboot）

|Executing |
|因系统维护隔离坏盘（SystemMaintenance.IsolateErrorDisk）

|Inquiring |
|因系统维护重新初始化坏盘（SystemMaintenance.ReInitErrorDisk）

|Inquiring |

**说明：** 重新部署本地盘实例会重新初始化本地盘，存储设备的数据被清空。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=RedeployInstance&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RedeployInstance|系统规定参数。取值：RedeployInstance |
|InstanceId|String|是|i-bp1azkttqpldxgted\*\*\*\*|处于运行中或者已停止状态的实例ID。 |
|ForceStop|Boolean|否|false|是否强制停止运行中（Running）的实例。

 默认值：false

 **说明：** 强制停止等同于典型的服务器断电关机，实例操作系统中暂未写入存储设备的数据会丢失。建议您尽量对已停止实例做重新部署操作。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TaskId|String|t-bp10e8orkp8x\*\*\*\*|重新部署的任务ID。

 您可以使用[DescribeTasks](~~25622~~)接口查询迁移结果。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=RedeployInstance
&InstanceId=i-bp1azkttqpldxgted****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<RedeployInstanceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <TaskId>t-bp10e8orkp8x****</TaskId>
</RedeployInstanceResponse>
```

`JSON` 格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "TaskId": "t-bp10e8orkp8x****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|The InstanceId provided does not exist in our records.|指定的实例不存在，请您检查实例ID是否正确。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|DiskError|IncorrectDiskStatus.|指定的磁盘状态不合法。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|IncorrectInstanceStatus|%s|当前实例的状态不支持此操作。|
|403|InvalidOperation.RedeployInstance|%s|操作无效。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

