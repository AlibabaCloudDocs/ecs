# CreateDeploymentSet

调用CreateDeploymentSet在指定的地域内创建一个部署集。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateDeploymentSet&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDeploymentSet|系统规定参数。取值：CreateDeploymentSet |
|RegionId|String|是|cn-hangzhou|部署集所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|OnUnableToRedeployFailedInstance|String|否|CancelMembershipAndStart|部署集内实例宕机迁移后，缺乏可供打散的实例库存的紧急处理方案。取值范围：

 -   CancelMembershipAndStart（默认）：将实例移出部署集，宕机迁移后即刻启动实例。
-   KeepStopped：维持实例的部署集属性，实例保持停止状态。 |
|Description|String|否|testDescription|部署集描述信息。长度为2~256个英文或中文字符，不能以http://和https://开头。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|DeploymentSetName|String|否|testDeploymentSetName|部署集名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|Strategy|String|否|Availability|部署策略。仅支持设置高可用策略。取值：Availability |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DeploymentSetId|String|ds-bp1frxuzdg87zh4pzq\*\*\*\*|部署集ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateDeploymentSet
&RegionId=cn-hangzhou
&DeploymentSetName=testDeploymentSetName
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateDeploymentSetResponse>
	  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
	  <DeploymentSetId>ds-bp1frxuzdg87zh4pzq****</DeploymentSetId>
</CreateDeploymentSetResponse>
```

`JSON` 格式

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "DeploymentSetId": "ds-bp1frxuzdg87zh4pzq****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|The input parameter RegionId that is mandatory for processing this request is not supplied.|参数RegionId不得为空。|
|400|InvalidDeploymentSetName.Malformed|Specified deployment set name is not valid.|指定的参数DeploymentSetName不合法。|
|400|InvalidDescription.Malformed|The specified parameter Description is not valid.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|400|InvalidParameter.Domain|The specified parameter Domain is not valid.|指定的Domain参数不合法。|
|400|InvalidParameter.Strategy|The specified parameter Strategy is not valid|指定的Strategy不合法。|
|400|InvalidParameter.granularity|The specified parameter Granularity is not valid.|指定的Granularity参数不合法。|
|400|DependencyViolation.domain.granularity|The DeploymentSet domain and granularity is violation.|部署集域与数据粒度冲突。|
|400|DependencyViolation.strategy.granularity|The DeploymentSet strategy and granularity is violation.|部署集策略与数据粒度冲突。|
|400|DEPLOYMENTSET.QUOTA\_FULL|The deploymentSet quota is full|部署集配额已满，请您减少部署集数量。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

