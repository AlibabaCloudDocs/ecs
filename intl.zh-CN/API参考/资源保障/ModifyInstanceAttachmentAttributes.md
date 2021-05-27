# ModifyInstanceAttachmentAttributes

调用ModifyInstanceAttachmentAttributes修改实例的私有池的属性。

## 接口说明

私有池是弹性保障服务或容量预定服务在创建后生成的，关联了与私有池匹配的实例信息。您可以在创建实例时设置是否使用私有池启动，实例将会与弹性保障服务或容量预定服务进行匹配。

-   调用该接口修改实例的私有池的属性后，实例不需要重启。
-   当您调用以下接口时，系统会重新匹配实例的私有池。如果实例已匹配了指定的私有池，可能因私有池容量已用完或私有池失效等原因造成调用失败的问题。如果出现调用失败的问题，请先调用ModifyInstanceAttachmentAttributes接口将私有池的匹配模式修改为`Open`。
    -   StartInstance重启停机不收费的实例
    -   ReActivateInstances
    -   ModifyInstanceChargeType
    -   ModifyPrepayInstanceSpec
    -   ReplaceSystemDisk

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceAttachmentAttributes&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyInstanceAttachmentAttributes|系统规定参数。取值：ModifyInstanceAttachmentAttributes |
|RegionId|String|是|cn-hangzhou|私有池所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|PrivatePoolOptions.MatchCriteria|String|是|Open|修改实例的私有池匹配模式。取值范围：

 -   Open：开放模式。该模式下系统自动为实例匹配开放的私有池。
-   Target：指定模式。该模式下必须同时指定`PrivatePoolOptions.Id`参数，设置指定的私有池ID。
-   None：不使用。该模式下实例正常启动，不使用私有池。 |
|InstanceId|String|是|i-bp67acfmxazb4\*\*\*\*|需要修改私有池匹配属性的实例ID。 |
|PrivatePoolOptions.Id|String|否|eap-bp67acfmxazb4\*\*\*\*|私有池ID，即弹性保障服务ID或者容量预定服务ID。

 -   当`PrivatePoolOptions.MatchCriteria`取值为`Target`时，该参数为必填项。
-   当`PrivatePoolOptions.MatchCriteria`取值为`Open`或`None`时，该参数不传值。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceAttachmentAttributes
&RegionId=cn-hangzhou
&InstanceId=i-bp67acfmxazb4****
&PrivatePoolOptions.MatchCriteria=Open
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyInstanceAttachmentAttributesResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceAttachmentAttributesResponse>
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
|400|MissingParameter.RegionId|The specified RegionId should not be null.|RegionId是必选参数。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

