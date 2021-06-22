# ModifyDiskSpec

调用ModifyDiskSpec变更一块云盘类型，或者修改一块ESSD云盘的性能级别。

## 接口说明

请确保在使用该接口前，您已充分了解云盘的计费方式和[价格](https://www.aliyun.com/price/product#/disk/detail)。

调用该接口完成以下操作时，您需要注意：

-   修改ESSD云盘性能级别：
    -   包年包月ESSD云盘仅支持升级性能级别。
    -   按量付费ESSD云盘支持升级和降低性能级别，但不支持降配到PL0。
    -   ESSD云盘的状态必须是**使用中**（In\_Use）状态或者**待挂载**（Available）状态。
    -   若ESSD云盘已挂载到ECS实例上，实例必须处于**运行中**（Running）状态或者**已停止**（Stopped）状态，ECS实例不能处于过期或者账号欠费状态。
    -   由于ESSD云盘性能级别受容量限制，如果您无法升级性能级别，可以扩容（[ResizeDisk](~~25522~~)）后重新操作。更多信息，请参见[ESSD云盘](~~122389~~)。
-   变更一块云盘类型的注意事项，请参见[变更云盘类型](~~161980~~)中的限制条件章节。
-   开启多重挂载特性的云盘不支持云盘变配。

调用接口后，新的云盘类型立即生效，阿里云按照新的云盘类型及云盘性能级别单价计算消费账单。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyDiskSpec&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDiskSpec|系统规定参数。取值：ModifyDiskSpec |
|DiskId|String|是|d-bp131n0q38u3a4zi\*\*\*\*|云盘的ID。 |
|DiskCategory|String|否|cloud\_essd|变更一块云盘的类型。取值范围：

 -   cloud\_essd：ESSD云盘
-   cloud\_ssd：SSD云盘
-   cloud\_efficiency：高效云盘

 默认值：空，表示不变配云盘。

 **说明：** 以上有效取值按云盘性能降序排列。如果指定的云盘是包年包月云盘，则不允许降配云盘。 |
|PerformanceLevel|String|否|PL2|修改一块ESSD云盘的性能级别。取值范围：

 -   PL0：单盘最高随机读写IOPS 1万。
-   PL1：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。

 默认值：PL1 |
|DryRun|Boolean|否|false|是否只预检此次请求。取值范围：

 -   true：发送检查请求。检查项包括是否填写了必需参数、请求格式、业务限制和ECS库存。如果检查不通过，则返回对应错误。如果检查通过，则返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并且直接变配云盘或修改ESSD性能等级。

 默认值：false |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|20413515388\*\*\*\*|生成的订单ID。

 **说明：** 仅在变更或修改包年包月云盘时会返回订单ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TaskId|String|t-bp67acfmxazb4p\*\*\*\*|变配云盘的任务ID。

 **说明：** 如果您只修改了一块ESSD云盘的性能级别，则不会返回该参数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyDiskSpec
&DiskId=d-bp131n0q38u3a4zi****
&PerformanceLevel=PL2
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyDiskSpecResponse>
    <TaskId>t-bp67acfmxazb4p****</TaskId>
    <RequestId>5B38289D-88AB-42BD-B021-12FC6942F099</RequestId>
    <OrderId>20413515388****</TaskId>
</ModifyDiskSpecResponse>
```

`JSON`格式

```
{
  "TaskId": "t-bp67acfmxazb4p****",
  "RequestId": "5B38289D-88AB-42BD-B021-12FC6942F099",
  "OrderId": "20413515388****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidPerformanceLevel.Malformed|The specified parameter PerformanceLevel is not valid.|指定的参数PerformanceLevel无效。|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|指定的SystemDisk.Category参数有误。|
|403|DiskInArrears|The specified operation is denied as your disk owing fee.|指定的磁盘已欠费。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|指定的磁盘正在创建快照。|
|403|OperationDenied|The type of the disk does not support the operation.|此磁盘种类不支持指定的操作。|
|403|OperationDenied.PerformanceLevelNotMatch|The specified PerformanceLevel and disk size do not match.|指定的性能等级与磁盘大小不匹配。|
|403|InvalidInstanceType.NotSupportDiskCategory|The instanceType of the specified instance does not support this disk category.|指定的实例规格（InstanceType）不支持当前实例的云盘类别。请尝试更换其它实例规格。关于实例规格支持的云盘类型，请参见实例规格族文档。|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|库存不足。|
|403|InvalidOperation.MultiAttachDisk|Multi attach disk does not support this operation.|开启多重挂载特性的云盘不支持该操作。|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

