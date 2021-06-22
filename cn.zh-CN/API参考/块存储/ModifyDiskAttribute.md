# ModifyDiskAttribute

调用ModifyDiskAttribute修改一个或多个块存储的名称、描述、是否随实例释放等属性。

## 接口说明

-   当您调用该接口时设置了不随实例释放（DeleteWithInstance=false）属性，一旦磁盘挂载的ECS实例被安全锁定且OperationLocks中标记了`"LockReason" : "security"`的锁定状态，释放实例时会忽略磁盘的DeleteWithInstance属性而被同时释放。
-   您可以调用`DiskIds.N`参数批量修改多个块存储的名称、描述、是否随实例释放等属性。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyDiskAttribute&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDiskAttribute|系统规定参数。取值：ModifyDiskAttribute |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|DiskId|String|否|d-bp1famypsnar20bv\*\*\*\*|待修改明细的磁盘ID。

 **说明：** `DiskId`和`DiskIds.N`两个参数不能同时被调用，请您根据需求任选其一传值。 |
|DiskName|String|否|MyDiskName|磁盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以`http://`和`https://`开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|Description|String|否|TestDescription|磁盘描述。 长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。 |
|DeleteWithInstance|Boolean|否|false|磁盘是否随实例释放。默认值：无，无表示不改变当前的值。

 开启多重挂载特性的云盘，不支持设置该参数。

 在下列两种情况下，将参数`DeleteWithInstance`设置成`false`时会报错。

 -   磁盘的种类（category）为本地盘（ephemeral）时。
-   磁盘的种类（category）为普通云盘（cloud），且不可以卸载（Portable=false）时。 |
|DeleteAutoSnapshot|Boolean|否|false|删除磁盘时，是否同时删除其自动快照。默认值：无，无表示不改变当前的值。 |
|EnableAutoSnapshot|Boolean|否|true|云盘是否启用自动快照策略功能。

 -   ture：启用
-   false：关闭

 默认值：无，表示不改变当前的值。

 **说明：** 创建后的云盘默认启用自动快照策略功能。您只需要为云盘绑定自动快照策略即可正常使用。 |
|DiskIds.N|RepeatList|否|d-bp1famypsnar20bv\*\*\*\*|待修改明细的多个磁盘ID。N的取值范围：0 ~ 100

 **说明：** `DiskId`和`DiskIds.N`两个参数不能同时被调用，请您根据需求任选其一传值。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyDiskAttribute
&RegionId=cn-hangzhou
&DiskId=d-bp1famypsnar20bv****
&DiskName=MyDiskName
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyDiskAttributeResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyDiskAttributeResponse>
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
|400|InvalidDiskName.Malformed|The specified disk name is wrongly formed.|磁盘名称格式不正确。长度为2-128个字符，以英文字母或中文开头，可包含数字，点号（.），下划线（\_）或连字符（-）。 不能以http://和https://开头。|
|400|NoAttributeToModify|No attribute to be modified in this request.|没有任何属性被修改。|
|400|IncompleteParamter|Some fields can not be null in this request.|请求中缺失参数。|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|指定的RegionId不合法。|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|快照额度超过限制，若要存储新快照，在不影响业务的情况下，请您删除已有的老快照。|
|403|DiskNotPortable|The specified disk is not a portable disk.|指定的磁盘不是可卸载的磁盘，Portable为false的磁盘无法卸载。|
|403|IncorrectDiskStatus|The operation is not supported in this status.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|UserNotInTheWhiteList|The user is not in disk white list.|您不在磁盘白名单中，请加入白名单后重试。|
|403|DeleteWithInstance.Conflict|Multi attach disk cannot be set to DeleteWithInstance attribute.|开启多重挂载特性的云盘不支持设置DeleteWithInstance。|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|404|InvalidInstanceId.NotFound|Specified attached instance does not exist.|指定的实例不存在，请您检查实例ID是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

