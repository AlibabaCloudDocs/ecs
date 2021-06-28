# ModifySecurityGroupAttribute

调用ModifySecurityGroupAttribute修改一个安全组的名称或者描述。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifySecurityGroupAttribute&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifySecurityGroupAttribute|系统规定参数。取值：ModifySecurityGroupAttribute |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|SecurityGroupId|String|是|sg-bp67acfmxazb4p\*\*\*\*|安全组ID。 |
|SecurityGroupName|String|否|SecurityGroupTestName|安全组名称。 长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以`http://`和`https://`开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空 |
|Description|String|否|TestDescription|安全组描述信息。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。

 默认值：空 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifySecurityGroupAttribute
&SecurityGroupId=sg-bp67acfmxazb4p****
&RegionId=cn-hangzhou
&SecurityGroupName=SecurityGroupTestName
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifySecurityGroupAttributeResponse>
       <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</ModifySecurityGroupAttributeResponse>
```

`JSON`格式

```
{
    "RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|指定的安全组在该用户账号下不存在，请您检查安全组ID是否正确。|
|400|InvalidSecurityGroupName.Malformed|Specified security group name is not valid.|指定的安全组名称格式不合法。请您按照规则进行配置：默认值为空，长度为2-128个英文或中文字符，必须以大小字母或中文开头，可包含数字，英文句号（.），下划线（\_）或连字符（-），安全组名称会展示在控制台。不能以http://和https://开头。|
|400|InvalidSecurityGroupDiscription.Malformed|Specified security group description is not valid.|指定的安全组描述不合法。|
|403|InvalidOperation.ResourceManagedByCloudProduct|%s|云产品托管的安全组不支持修改操作。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

