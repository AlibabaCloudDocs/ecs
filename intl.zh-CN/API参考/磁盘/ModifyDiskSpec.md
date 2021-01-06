# ModifyDiskSpec

调用ModifyDiskSpec修改一块ESSD云盘的性能级别。

## 接口说明

修改ESSD云盘性能级别，您需要注意：

-   包年包月ESSD云盘仅支持升级性能级别，按量付费ESSD云盘支持升级和降低性能级别。
-   ESSD云盘的状态必须是**使用中**（In\_Use）状态或者**待挂载**（Available）状态。
-   若ESSD云盘已挂载到ECS实例上，实例必须处于**运行中**（Running）状态或者**已停止**（Stopped）状态，ECS实例不能处于过期或者账号欠费状态。
-   由于ESSD云盘性能级别受容量限制，如果您无法升级性能级别，可以扩容（[ResizeDisk](~~25522~~)）后重新操作。更多详情，请参见[ESSD云盘](~~122389~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyDiskSpec&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDiskSpec|系统规定参数。取值：ModifyDiskSpec |
|DiskId|String|是|d-bp131n0q38u3a4zi\*\*\*\*|云盘的ID。 |
|PerformanceLevel|String|否|PL2|修改一块ESSD云盘的性能级别。取值范围：

 -   PL1（默认）：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。 |
|DryRun|Boolean|否|false|是否只预检此次请求。取值范围：

 -   true：发送检查请求。检查项包括是否填写了必需参数、请求格式、业务限制和ECS库存。如果检查不通过，则返回对应错误。如果检查通过，则返回错误码`DryRunOperation`。
-   false（默认）：发送正常请求，通过检查后返回2XX HTTP状态码并且直接变配云盘或修改ESSD性能等级。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TaskId|String|null|**说明：** 该参数正在邀测中，暂未开放使用。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyDiskSpec
&DiskId=d-bp131n0q38u3a4zi****
&PerformanceLevel=PL2
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyDiskSpecResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyDiskSpecResponse>
```

`JSON` 格式

```
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|403|DiskInArrears|The specified operation is denied as your disk owing fee.|指定的磁盘已欠费。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|指定的磁盘正在创建快照。|
|403|OperationDenied|The type of the disk does not support the operation.|此磁盘种类不支持指定的操作。|
|400|InvalidPerformanceLevel.Malformed|The specified parameter PerformanceLevel is not valid.|指定的参数PerformanceLevel无效。|
|403|OperationDenied.PerformanceLevelNotMatch|The specified PerformanceLevel and disk size do not match.|指定的性能等级与磁盘大小不匹配。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

