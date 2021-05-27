# ModifyElasticityAssurance

调用ModifyElasticityAssurance修改一个弹性保障服务的名称与描述信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyElasticityAssurance&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|ModifyElasticityAssurance|系统规定参数。取值：ModifyElasticityAssurance |
|PrivatePoolOptions.Id|String|是|eap-bp67acfmxazb4\*\*\*\*|弹性保障服务ID。 |
|RegionId|String|是|cn-hangzhou|弹性保障服务所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|PrivatePoolOptions.Name|String|否|eapTestName|弹性保障服务的名称。长度为2~128个英文或中文字符。必须以大小写字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|Description|String|否|This is description.|弹性保障服务的描述信息。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|8455DD10-84F8-43C9-8365-5F448EB169B6|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyElasticityAssurance
&PrivatePoolOptions.Id=eap-bp67acfmxazb4****
&RegionId=cn-hangzhou
&PrivatePoolOptions.Name=eapTestName
&Description=This is description.
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyElasticityAssuranceResponse>
      <RequestId>8455DD10-84F8-43C9-8365-5F448EB169B6</RequestId>
</ModifyElasticityAssuranceResponse>
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

