# DetachDisk

调用DetachDisk从一台ECS实例上卸载一块按量付费数据盘，或者卸载一块系统盘。

## 接口说明

调用该接口时，请注意：

-   云盘必须已经挂载到实例上，状态为使用中（`In_Use`\)。
-   卸载数据盘时，所挂载的实例必须处于**运行中**（`Running`）或者**已停止**（`Stopped`）状态。
-   卸载系统盘时，所挂载的实例必须处于**已停止**（`Stopped`）状态。
-   所挂载的实例被安全控制后，`OperationLocks`中不能标记为`"LockReason" : "security"`的锁定状态。
-   DetachDisk是异步操作，调用接口成功后等待一分钟左右才能完成卸载。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DetachDisk&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DetachDisk|系统规定参数。取值：DetachDisk |
|DiskId|String|是|d-bp67acfmxazb4p\*\*\*\*|待卸载的云盘ID。 |
|InstanceId|String|是|i-bp67acfmxazb4p\*\*\*\*|待卸载的ECS实例ID。 |
|DeleteWithInstance|Boolean|否|false|卸载系统盘时，设置自动释放属性。表示释放ECS实例时，是否同时释放该系统盘。

 -   true：释放。
-   false：不释放。云盘被转换为按量付费数据盘被保留下来。

 默认值：true

 您需要注意：

 -   开启多重挂载特性的云盘，不支持设置该参数。
-   如果卸载的是数据盘，默认值为`false`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DetachDisk
&DiskId=d-bp67acfmxazb4p****
&InstanceId=i-bp67acfmxazb4p****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DetachDiskResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachDiskResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter|The input parameter is mandatory for processing this request is empty.|参数不能为空。|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|指定的RegionId不合法。|
|400|InvalidOperation.InstanceTypeNotSupport|The instance type of the specified instance does not support hot detach disk.|磁盘挂载的实例不支持磁盘热插拔操作。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|DiskNotPortable|The specified disk is not a portable disk.|指定的磁盘不是可卸载的磁盘，Portable为false的磁盘无法卸载。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|DependencyViolation|The specified disk has not been attached on the specified instance.|资源有其它依赖无法执行操作，请先将依赖取消关联。如：指定磁盘没有挂载在指定的实例上；指定安全组内有实例时无法删除安全组等。|
|403|DiskTypeViolation|The specified disk is a system disk and cannot support the operation.|指定的云盘是系统盘，不能卸载。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|UserNotInTheWhiteList|The user is not in disk white list.|您不在磁盘白名单中，请加入白名单后重试。|
|403|InvalidInstance.ImageCategory|The image category of the specified instance does not support detaching system disk.|指定实例的镜像状态不支持卸载指定的系统盘。可能原因：创建实例时使用的镜像被删除。|
|403|DeleteWithInstance.Conflict|Multi attach disk cannot be set to DeleteWithInstance attribute.|开启多重挂载特性的云盘不支持设置DeleteWithInstance。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|404|InvalidDisk.AlreadyDetached|The specified disk has been detached.|指定的磁盘已分离。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

