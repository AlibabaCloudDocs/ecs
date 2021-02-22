# CreateImageComponent

调用CreateImageComponent创建一个镜像组件。镜像组件用于存储您在构建镜像时，常用的构建模板命令。

## 接口说明

创建镜像组件前，您需要注意：

-   仅支持创建您自定义的镜像组件。
-   仅支持Linux系统，即`SystemType=Linux`。
-   仅支持设置为镜像构建组件类型，即`ComponentType=Build`。
-   镜像组件的内容可以通过Dockerfile编辑，然后将内容传入`Content`参数。内容大小不能超过16 KB，不支持`FROM`命令，一个镜像组件最大支持127个命令。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateImageComponent&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateImageComponent|系统规定参数。取值：CreateImageComponent |
|RegionId|String|是|cn-hangzhou|所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Tag.N.Key|String|否|TestKey|标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|Tag.N.Value|String|否|TestValue|标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以acs:开头，不能包含http://或者https://。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|企业资源组ID。 |
|Name|String|否|testComponent|组件名称。长度为2~128个字符，必须以大小字母或中文开头，不能以http://和https://开头。可以包含中文、英文、数字、半角冒号（:）、下划线（\_）、英文句号（.）或者短划线（-）。

 **说明：** 不设置`Name`时，默认使用`ImageComponentId`返回值。 |
|Description|String|否|This is description.|描述信息。长度为2~256个英文或中文字符，不能以http://和https://开头。 |
|SystemType|String|否|Linux|组件支持的操作系统。目前仅支持Linux系统。取值：Linux

 默认值：Linux |
|ComponentType|String|否|Build|组件类型。目前仅支持镜像构建组件。取值：Build

 默认值：Build |
|Content|String|否|RUN yum update -y|组件内容。由多条命令组成，命令最大条数不能超过127条。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25693~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ImageComponentId|String|ic-bp67acfmxazb4p\*\*\*\*|镜像组件ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateImageComponent
&RegionId=cn-hangzhou
&Name=testComponent
&Description=This is description.
&SystemType=Linux
&ComponentType=Build
&Content=RUN yum update -y
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateImageComponentResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ImageComponentId>ic-bp67acfmxazb4p****</ImageComponentId>
</CreateImageComponentResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E", 
    "ImageComponentId": "ic-bp67acfmxazb4p****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

