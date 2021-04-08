# ModifyImageAttribute

调用ModifyImageAttribute修改一份自定义镜像的名称、描述信息、状态或镜像族系。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyImageAttribute&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyImageAttribute|系统规定参数。取值：ModifyImageAttribute |
|ImageId|String|是|m-bp18ygjuqnwhechc\*\*\*\*|自定义镜像的ID。 |
|RegionId|String|是|cn-hangzhou|自定义镜像所在的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ImageName|String|否|testImageName|自定义镜像的名称。长度为2~128个字符。必须以大小字母或中文开头，不能以`aliyun`或`acs:`开头，不能包含`http://`或者`https://`。可以包含数字、半角句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。

 默认值：空，表示保持原有名称不变。 |
|Status|String|否|Deprecated|镜像状态，取值范围：

 -   Deprecated：将镜像设置为弃用状态。如果您已经共享的自定义镜像，必须先取消共享才能修改为弃用状态。对处于弃用状态镜像，不能共享和复制镜像。但是可以使用镜像创建实例或更换系统盘。
-   Available：将镜像设置为可用状态。您可以将弃用状态的镜像恢复可用。

 **说明：** 如果您需要回滚镜像族系中的自定义镜像至上一个版本，可以将最新可用的自定义镜像设置为弃用状态，但如果该镜像为镜像族系中唯一一个可用状态的自定义镜像，则弃用镜像以后该镜像族系将无可用状态自定义镜像用来创建实例，因此请谨慎操作。 |
|ImageFamily|String|否|hangzhou-daily-update|镜像族系名称。长度为2~128个字符。必须以大小字母或中文开头，不能以`aliyun`或`acs:`开头，不能包含`http://`或者`https://`。可以包含数字、半角句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。

 默认值：空 |
|BootMode|String|否|BIOS|修改镜像的启动模式。取值范围：

 -   BIOS：BIOS启动模式。
-   UEFI：UEFI启动模式。

 **说明：** 您需要了解指定的镜像支持的启动模式，当通过该参数修改启动模式后，必须与镜像本身支持的启动模式匹配，实例才能正常启动。 |
|Description|String|否|testDescription|自定义镜像的描述信息。长度为2~256个字符。不能以`http://`或`https://`开头。

 默认值：空，表示保持原有描述信息不变。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyImageAttribute
&ImageId=m-bp18ygjuqnwhechc****
&RegionId=cn-hangzhou
&ImageName=testImageName
&Description=testDescription
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyImageAttributeResponse>
      <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</ModifyImageAttributeResponse>
```

`JSON`格式

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidImageName.Malformed|The specified Image name is wrongly formed.|镜像名称格式错误。长度为2~128个字符。必须以大小字母或中文开头，不能以aliyun和acs:开头，不能包含http://或者https://。可以包含数字、半角句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。|
|400|MissingParameter|The input parameter "RegionId" that is mandatory for processing this request is not supplied.|RegionId不得为空。|
|400|InvalidImageName.Duplicated|The specified Image name has already bean used.|镜像名称已经重复。|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像ID是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

