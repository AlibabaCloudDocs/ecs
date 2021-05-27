# ModifyCapacityReservation

调用ModifyCapacityReservation修改一个容量预定服务的部分信息，包括容量预定服务的名称、描述信息、失效方式以及预留的实例总数量。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyCapacityReservation&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|ModifyCapacityReservation|系统规定参数。取值：ModifyCapacityReservation |
|RegionId|String|是|cn-hangzhou|容量预定服务所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|PrivatePoolOptions.Id|String|是|crp-bp67acfmxazb4\*\*\*\*|容量预定服务ID。 |
|PrivatePoolOptions.Name|String|否|eapTestName|容量预定服务的名称。长度为2~128个英文或中文字符。必须以大小写字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|Description|String|否|This is description.|容量预定服务的描述信息。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。 |
|StartTime|String|否|Now|容量预定服务的生效方式。目前仅支持设置为立即生效，且参数无需传值。

 **说明：** 该参数不传值即表示设置为立即生效。 |
|EndTimeType|String|否|Unlimited|容量预定服务的失效方式。取值范围：

 -   Limited：指定时间释放。必须同时指定`EndTime`参数。
-   Unlimited：手动释放。不限制时间。 |
|EndTime|String|否|2021-10-30T06:32:00Z|容量预定服务的失效时间，仅`EndTimeType=Limited`时该参数生效。时间格式以ISO8601为标准，并需要使用UTC +0时间，格式为`yyyy-MM-ddTHH:mm:ssZ`。更多信息，请参见[ISO8601](~~25696~~)。 |
|Platform|String|否|Linux|实例使用的镜像的操作系统类型。取值范围：

 -   Windows：Windows Server类型的操作系统。
-   Linux：Linux及类Unix类型的操作系统。

 **说明：** 该参数暂未开放使用。 |
|InstanceAmount|Integer|否|100|容量预定服务需要预留的实例总数量。取值范围：已使用的实例数量~1000

 **说明：** 扩充实例总数量时，可能因库存不足导致扩充失败。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|8455DD10-84F8-43C9-8365-5F448EB169B6|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyCapacityReservation
&PrivatePoolOptions.Id=crp-bp67acfmxazb4****
&RegionId=cn-hangzhou
&PrivatePoolOptions.Name=eapTestName
&Description=This is description.
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyCapacityReservationResponse>
      <RequestId>8455DD10-84F8-43C9-8365-5F448EB169B6</RequestId>
</ModifyCapacityReservationResponse>
```

`JSON`格式

```
{
	"RequestId": "8455DD10-84F8-43C9-8365-5F448EB169B6"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|401|InvalidUser.Unauthorized|The user is not authorized|您当前使用的账号无权限。|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|库存不足。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

