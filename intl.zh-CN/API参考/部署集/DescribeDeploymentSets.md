# DescribeDeploymentSets

调用DescribeDeploymentSets查询一个或多个部署集的属性列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeDeploymentSets&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDeploymentSets|系统规定参数。取值：DescribeDeploymentSets |
|RegionId|String|是|cn-hangzhou|部署集所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|PageNumber|Integer|否|1|部署集列表的页码。

 起始值：1

 默认值：1 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。

 最大值：50

 默认值：10 |
|DeploymentSetIds|String|否|\["ds-bp67acfmxazb4ph\*\*\*\*", "ds-bp67acfmxazb4pi\*\*\*\*", … "ds-bp67acfmxazb4pj\*\*\*\*"\]|部署集ID列表。取值可以由多个部署集ID组成一个JSON数组，最多支持100个ID，ID之间用半角逗号（,）隔开。 |
|DeploymentSetName|String|否|testDeploymentSetName|部署集名称。 |
|Strategy|String|否|Availability|部署策略。仅支持设置高可用策略。取值：Availability

 默认值：空 |
|NetworkType|String|否|null|部署集内实例的网络类型。

 **说明：** 为提高兼容性，请尽量使用其他参数。 |
|Granularity|String|否|null|部署粒度。

 **说明：** 为提高兼容性，请尽量使用其他参数。 |
|Domain|String|否|null|部署域。

 **说明：** 为提高兼容性，请尽量使用其他参数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DeploymentSets|Array of DeploymentSet| |由DeploymentSet组成的数组格式，返回部署集详细信息。 |
|DeploymentSet| | | |
|CreationTime|String|2017-12-05T22:40:00Z|部署集的创建时间。 |
|DeploymentSetDescription|String|testDeploymentSetDescription|部署集的描述信息。 |
|DeploymentSetId|String|ds-bp67acfmxazb4ph\*\*\*\*|部署集ID。 |
|DeploymentSetName|String|testDeploymentSetName|部署集名称。 |
|DeploymentStrategy|String|Availability|部署策略。该返回值对应请求参数`Strategy`的值。 |
|Domain|String|default|部署域。 |
|Granularity|String|Host|部署粒度。 |
|GroupCount|Integer|0|**说明：** 该参数正在邀测，暂未开放使用。 |
|InstanceAmount|Integer|1|部署集内的实例数量。 |
|InstanceIds|List|\["i-bp67acfmxazb4ph\*\*\*\*"\]|部署集内的实例ID列表。 |
|Strategy|String|LooseDispersion|部署策略。 |
|PageNumber|Integer|1|部署集列表的页数。 |
|PageSize|Integer|10|设置的每页行数。 |
|RegionId|String|cn-hangzhou|部署集所处的地域ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|1|查询到的部署集总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeDeploymentSets
&RegionId=cn-hangzhou
&PageSize=1
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeDeploymentSetsResponse>
      <DeploymentSets>
            <DeploymentSet>
                  <CreationTime>2017-12-05T22:40:00Z</CreationTime>
                  <Granularity>switch</Granularity>
                  <DeploymentSetDescription>autogen deploymentset, do not delete</DeploymentSetDescription>
                  <Domain>default</Domain>
                  <InstanceIds>
                        <InstanceId>i-bp67acfmxazb4ph****</InstanceId>
                        <InstanceId>i-bp67acfmxazb4pi****</InstanceId>
                        <InstanceId>i-bp67acfmxazb4pj****</InstanceId>
                  </InstanceIds>
                  <InstanceAmount>0</InstanceAmount>
                  <Strategy>LooseDispersion</Strategy>
                  <DeploymentSetName>hpc-null-deploymentset</DeploymentSetName>
                  <DeploymentStrategy>Availability</DeploymentStrategy>
                  <DeploymentSetId>ds-bp120c8htdzx3869****</DeploymentSetId>
            </DeploymentSet>
      </DeploymentSets>
      <PageNumber>1</PageNumber>
      <TotalCount>5</TotalCount>
      <PageSize>1</PageSize>
      <RegionId>cn-hangzhou</RegionId>
      <RequestId>FB5EF912-FD87-4CF7-91D9-9204974A63F3</RequestId>
</DescribeDeploymentSetsResponse>
```

`JSON`格式

```
{
	"DeploymentSets": {
		"DeploymentSet": [
			{
				"CreationTime": "2017-12-05T22:40:00Z",
				"Granularity": "switch",
				"DeploymentSetDescription": "autogen deploymentset, do not delete",
				"Domain": "default",
				"InstanceIds": {
					"InstanceId": [
                        "i-bp67acfmxazb4ph****",
                        "i-bp67acfmxazb4pi****",
                        "i-bp67acfmxazb4pj****"]
				},
				"InstanceAmount": 0,
				"Strategy": "LooseDispersion",
				"DeploymentSetName": "hpc-null-deploymentset",
				"DeploymentStrategy": "Availability",
				"DeploymentSetId": "ds-bp120c8htdzx3869****"
			}
		]
	},
	"PageNumber": 1,
	"TotalCount": 5,
	"PageSize": 1,
	"RegionId": "cn-hangzhou",
	"RequestId": "FB5EF912-FD87-4CF7-91D9-9204974A63F3"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidDeploymentSetIds.TooManyInput|The parameter DeploymentSets size should less than 100.|指定的DeploymentSets数量大于100。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

