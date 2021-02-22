# CreateImagePipeline

调用CreateImagePipeline创建一个镜像模板。镜像模板可用于构建镜像。

## 接口说明

您可以通过镜像模版定制镜像内容，并支持跨地域跨账号构建镜像。创建镜像模板前，您需要注意：

-   仅支持创建您自定义的镜像模版。
-   仅支持设置Linux系统的公共镜像、自定义镜像、共享镜像或者镜像族系。
-   通过镜像模版构建镜像时，需要创建中转实例辅助构建镜像，中转实例为按量计费的ECS实例，将收取一定的费用。更多信息，请参见[按量付费](~~40653~~)。

关于构建模板内容`BuildContent`，您需要注意：

-   如果参数`BuildContent`设置了`FROM`命令，则源镜像类型`BaseImageType`和源镜像`BaseImage`设置的值会被`FROM`命令覆盖。
-   如果参数`BuildContent`没有设置`FROM`命令，则系统会自动将源镜像类型`BaseImageType`和源镜像`BaseImage`构成的`FROM`命令添加到模板内容的首行，格式为`<BaseImageType>:<BaseImage>`。
-   一个镜像模板内容可以通过Dockerfile编辑，然后将内容传入`BuildContent`参数。内容大小不能超过16 KB，最大支持127个命令。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateImagePipeline&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateImagePipeline|系统规定参数。取值：CreateImagePipeline |
|BaseImage|String|是|m-bp67acfmxazb4p\*\*\*\*|源镜像。

 -   当`BaseImageType=IMAGE`时，该参数取值为自定义镜像ID。
-   当`BaseImageType=IMAGE_FAMILY`时，该参数取值为镜像族系名称。 |
|BaseImageType|String|是|IMAGE|源镜像类型。取值范围：

 -   IMAGE：自定义镜像。
-   IMAGE\_FAMILY：镜像族系。 |
|RegionId|String|是|cn-hangzhou|所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Tag.N.Key|String|否|TestKey|标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|Tag.N.Value|String|否|TestValue|标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以acs:开头，不能包含http://或者https://。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|企业资源组ID。 |
|Name|String|否|testImagePipeline|模板名称。长度为2~128个字符，必须以大小字母或中文开头，不能以http://和https://开头。可以包含中文、英文、数字、半角冒号（:）、下划线（\_）、英文句号（.）或者短划线（-）。

 **说明：** 不设置`Name`时，默认使用`ImagePipelineId`返回值。 |
|Description|String|否|This is description.|描述信息。长度为2~256个英文或中文字符，不能以http://和https://开头。 |
|ImageName|String|否|testImageName|目标镜像名称前缀。长度为2~64个字符，必须以大小字母或中文开头，不能以http://和https://开头。可以包含中文、英文、数字、半角冒号（:）、下划线（\_）、英文句号（.）或者短划线（-）。

 最终完整的镜像名称由系统自动拼接名称前缀与构建任务ID（ExecutionId），格式为`{ImageName}_{ExecutionId}`。 |
|VSwitchId|String|否|vsw-bp67acfmxazb4p\*\*\*\*|VPC的交换机ID。

 不设置参数值时，默认创建新的VPC与交换机，请确保您账号下VPC资源配额充足，更多信息，请参见[使用限制](~~27750~~)。 |
|InstanceType|String|否|ecs.g6.large|实例规格。您可以调用[DescribeInstanceTypes](~~25620~~)查询不同的实例规格。

 不设置参数值时，默认按vCPU和内存最小的原则，自动设置实例规格，并受实例规格的库存影响。例如，默认选择ecs.g6.large实例规格，如果库存不足，将选择ecs.g6.xlarge实例规格。 |
|SystemDiskSize|Integer|否|40|中转实例的系统盘大小。单位：GiB。取值范围：20~500

 默认值：40 |
|InternetMaxBandwidthOut|Integer|否|0|中转实例的公网出带宽大小。单位：Mbit/s。取值范围：0~100

 默认值：0 |
|DeleteInstanceOnFailure|Boolean|否|true|镜像构建失败后是否释放中转实例。取值范围：

 -   true：释放
-   false：不释放

 默认值：true

 **说明：** 中转实例如果没有成功启动，则实例默认不保留。 |
|BuildContent|String|否|FROM IMAGE:m-bp67acfmxazb4p\*\*\*\*|镜像模板内容。内容大小不能超过16 KB，最大支持127个命令。具体支持的命令请参见接口说明。 |
|AddAccount.N|RepeatList|否|1234567890|目标镜像共享的阿里云账号ID。N的取值范围：1~20 |
|ToRegionId.N|RepeatList|否|cn-hangzhou|目标镜像待分发的地域列表。N的取值范围：1~20

 不设置参数值时，默认只在当前地域创建镜像。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25693~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ImagePipelineId|String|ip-2ze5tsl5bp6nf2b3\*\*\*\*|镜像模板ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateImagePipeline
&BaseImage=m-bp67acfmxazb4p****
&BaseImageType=IMAGE
&RegionId=cn-hangzhou
&Name=testImagePipeline
&BuildContent=FROM IMAGE:m-bp67acfmxazb4p****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateImagePipelineResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ImagePipelineId>ip-2ze5tsl5bp6nf2b3****</ImagePipelineId>
</CreateImagePipelineResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E", 
    "ImagePipelineId": "ip-2ze5tsl5bp6nf2b3****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidImage.NotFound|%s|指定的参数值有误，具体信息请参见错误信息%s占位符的实际返回结果。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

