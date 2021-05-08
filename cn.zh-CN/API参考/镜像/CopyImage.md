# CopyImage

调用CopyImage复制一个地域下的自定义镜像到其他地域。复制镜像可以实现跨地域部署ECS实例、跨地域复制ECS实例等目的。

## 接口说明

您可以在其他地域使用复制后的镜像创建ECS实例（RunInstances），或者更换实例的系统盘（ReplaceSystemDisk）。

调用该接口时，您需要注意：

-   自定义镜像的状态必须为可用（`Available`）。
-   源自定义镜像必须为您账号下的镜像，不能跨账号复制。
-   复制镜像时，您无法删除复制后的镜像（[DeleteImage](~~25537~~)），但是您可以取消复制任务（[CancelCopyImage](~~25539~~)）。
-   同一个地域下同时只能有一个镜像拷贝任务运行，其余任务需要排队等待上一个任务完成后再依次排队执行。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CopyImage&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CopyImage|系统规定参数。取值：CopyImage |
|ImageId|String|是|m-bp1h46wfpjsjastc\*\*\*\*|源自定义镜像的ID。 |
|RegionId|String|是|cn-hangzhou|源自定义镜像的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|DestinationRegionId|String|否|cn-shanghai|复制到目标地域的ID。 |
|DestinationImageName|String|否|YourImageName|复制后的镜像的名称。长度为2~128个字符。必须以大小字母或中文开头，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。可以包含数字、半角句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。

 默认值：空 |
|DestinationDescription|String|否|This is a description example.|复制后的镜像的描述信息。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。

 默认值：空 |
|Encrypted|Boolean|否|false|是否加密复制后的镜像。

 默认值：false |
|Tag.N.Key|String|否|TestKey|复制后的镜像的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |
|Tag.N.Value|String|否|TestValue|复制后的镜像的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以`acs:`开头，不能包含`http://`或者`https://`。 |
|KMSKeyId|String|否|e522b26d-abf6-4e0d-b5da-04b7\*\*\*\*\*\*3c|加密镜像使用的密钥ID。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|复制后的镜像的资源组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ImageId|String|m-bp1h46wfpjsjastd\*\*\*\*|复制后的镜像的ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CopyImage
&ImageId=m-bp1h46wfpjsjastc****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CopyImageResponse>
      <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
      <ImageId>m-bp1h46wfpjsjastd****</ImageId>
</CopyImageResponse>
```

`JSON`格式

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "ImageId": "m-bp1h46wfpjsjastd****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|401|InvalidAliUid.IsNull|The aliUid must not be null|参数aliUid不得为空。|
|400|InvalidImageName.Malformed|The specified Image name is wrongly formed.|镜像名称格式错误。长度为2~128个字符。必须以大小字母或中文开头，不能以aliyun和acs:开头，不能包含http://或者https://。可以包含数字、半角句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。|
|403|Forbbiden|User not authorized to operate on the specified resource.|用户未被授权操作指定的资源。|
|400|InvalidImageName.Malformed|The specified destination Image name is wrongly formed.|镜像名称不合法。限制条件请参见DestinationImageName参数说明。|
|400|InvalidDescription.Malformed|The specified destination description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|400|SourceRegion.NotFound|The source region not found|指定的源镜像的地域不存在。|
|400|DestinationRegion.NotFound|The destination region not found|指定的目标地域不存在。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像ID是否正确。|
|400|IncorrectImageStatus|The image not available.|指定的镜像不可用。|
|400|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|指定的快照不存在，请您检查快照是否正确。|
|400|InvalidImageName.Duplicated|The destination image is exist.|指定的镜像名已存在。|
|403|QuotaExceed.Image|The Image Quota exceeds.|自定义镜像额度已用完。|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|快照额度超过限制，若要存储新快照，在不影响业务的情况下，请您删除已有的老快照。|
|403|OperationDenied.ImageCopying|The Image are coping.|正在复制镜像，请您稍后再试。|
|403|RegionNotSupportCopy|The region not support copy.|指定的目标镜像地域或者源镜像所在地域暂时不支持镜像复制。|
|403|InvalidSnapshot.TooOld|This operation is denied because the specified snapshot is created before 2013-07-15.|该操作被拒绝。因为指定的快照创建于2013-07-15之前。|
|403|OperationDenied|The specified snapshot is not allowed to create image.|指定快照不允许创建镜像。|
|403|IncorrectDestinationRegion|The destination region is not equal the target region.|复制镜像的源地域不能等于目标地域。|
|403|SizeExceed.Image|The image exceeds the maximum size. Please open a ticket to add the account to the white list.|镜像的大小已超过可操作的最大值。|
|403|OperationDeined.EncryptedSnapshot|The image contains encrypted snapshots, which do not support copying.|指定的镜像含有加密快照，不支持复制这种镜像。|
|403|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|OperationDenied.SameRegionOnly|The image shared from others can not be copied to another region directly.|其他人分享的镜像不能复制到另一个地域。|
|403|OperationDenied.NotPublished|The operation is denied because corresponding marketplace image is not published in destination region.|由于目标地域不支持该类型镜像，导致操作被拒绝。|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|加密云盘设置了KMSKeyId后，CMK必须处于启用状态。您可以调用密钥管理服务的DescribeKey接口查询指定CMK的相关信息。|
|404|InvalidParameter.KMSKeyId.NotFound|The specified KMSKeyId does not exist.|指定的参数KMSKeyId不存在。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InvalidRegion.NotSupport|The specified region does not support byok.|该地域不支持BYOK。|
|403|UserNotInTheWhiteList|The user is not in byok white list.|您不在byok白名单中，请加入白名单后重试。|
|400|InvalidParameter.EncryptedIllegal|The specified parameter Encrypted must be true when kmsKeyId is not empty.|设置参数KMSKeyId后，您必须开启加密属性。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

