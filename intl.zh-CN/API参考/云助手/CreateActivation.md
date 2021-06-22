# CreateActivation

调用CreateActivation创建一个激活码。该激活码用于将非阿里云服务器注册为阿里云托管实例。

## 接口说明

通过激活码将非阿里云服务器注册为阿里云托管实例后，您可以在托管实例中使用阿里云提供的多种在线服务（例如云助手、运维编排和云效等服务）。

非阿里云服务器的操作系统需要符合以下版本，且服务器可以访问公网，才可以注册为阿里云托管实例。

-   Alibaba Cloud Linux 2
-   CentOS 6/7/8及更高版本
-   Debian 8/9/10及更高版本
-   Ubuntu 12/14/16/18及更高版本
-   CoreOS
-   OpenSUSE
-   RedHat 5/6/7及更高版本
-   SUSE Linux Enterprise Server 11/12/15及更高版本
-   Window Server 2012/2016/2019及更高版本

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateActivation&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateActivation|系统规定参数。取值：CreateActivation |
|InstanceName|String|是|test-InstanceName|默认的实例名称前缀。支持1~50个字符，且必须以字母开头，不能以特殊字符及数字开头，只可包含特殊字符中的英文句号（.）、下划线（\_）、短划线（-）和半角冒号（:），不可以使用`http://`或`https://`开头。

 使用该接口创建的激活码注册的实例，将使用该名称作为前辍，生成有序的实例名。您也可以在注册托管实例时，指定新的实例名称以覆盖此默认值。

 注册托管实例时，如果未指定实例名称，将会生成名称`<InstanceName>-001`，其中编号`001`的数字的位数取决于`InstanceCount`数值的位数。 |
|RegionId|String|是|cn-hangzhou|地域ID。目前仅支持华东1（杭州）、华北2（北京）、华东2（上海）。 |
|Description|String|否|This is description.|激活码对应的描述。支持1~100个字符，不可以使用`http://`或`https://`开头。 |
|InstanceCount|Integer|否|10|激活码用于注册托管实例的使用次数上限。取值范围：1~1000

 默认值：10 |
|TimeToLiveInHours|Long|否|4|激活码的有效使用时间，过期后将不能用于注册新的实例。单位：小时。取值范围：1~24

 默认值：4 |
|IpAddressRange|String|否|0.0.0.0/0|允许使用该激活码的主机IP。取值为对应的IPv4地址、IPv6地址或CIDR地址段。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ActivationCode|String|a-hz0ch3SwhOlE1234+Xo32lAZC\*\*\*\*|激活码的代码。该代码仅在调用接口时返回一次，后续无法被查询。因此，请您务必妥善保存返回值。 |
|ActivationId|String|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|激活码ID。 |
|RequestId|String|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateActivation
&InstanceName=test-InstanceName
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateActivationResponse>
      <RequestId>4ECEEE12-56F1-4FBC-9AB1-890F1234****</RequestId>
      <ActivationId>4ECEEE12-56F1-4FBC-9AB1-890F1234****</ActivationId>
      <ActivationCode>a-hz0ch3SwhOlE1234+Xo32lAZC****</ActivationCode>
</CreateActivationResponse>
```

`JSON`格式

```
{
	"RequestId": "4ECEEE12-56F1-4FBC-9AB1-890F1234****",
	"ActivationId": "4ECEEE12-56F1-4FBC-9AB1-890F1234****",
	"ActivationCode": "a-hz0ch3SwhOlE1234+Xo32lAZC****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|RegionId.ApiNotSupported|The api is not supported in this region.|指定地域下不支持调用API。请检查RegionId参数取值是否正确。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

