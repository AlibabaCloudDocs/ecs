# DescribeSecurityGroups

调用DescribeSecurityGroups查询您创建的安全组的基本信息。

## 接口说明

安全组的基本信息包括安全组ID和安全组描述等。返回参数列表按照安全组ID降序排列。

通过阿里云CLI调用API时，不同数据类型的请求参数取值必须遵循一定的格式要求，详情请参见[CLI参数格式说明](~~110340~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeSecurityGroups&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSecurityGroups|系统规定参数。取值：DescribeSecurityGroups |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|VpcId|String|否|vpc-bp67acfmxazb4p\*\*\*\*|安全组所在的专有网络ID。 |
|PageNumber|Integer|否|1|安全组列表的页码。

 起始值：1

 默认值：1 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。

 最大值：50

 默认值：10 |
|SecurityGroupIds|String|否|\["sg-bp67acfmxazb4p\*\*\*\*", "sg-bp67acfmxazb4p\*\*\*\*", "sg-bp67acfmxazb4p\*\*\*\*",....\]|安全组ID列表。一次最多支持100个安全组ID，ID之间用半角逗号（,）隔开，格式为JSON数组。 |
|Tag.N.value|String|否|testvalue|安全组的标签值。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Value参数。 |
|Tag.N.key|String|否|testkey|安全组的标签键。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Key参数。 |
|Tag.N.Key|String|否|TestKey|安全组的标签键。N的取值范围：1~20

 使用一个标签过滤资源，查询到该标签下的资源数量不能超过1000个；使用多个标签过滤资源，查询到同时绑定了多个标签的资源数量不能超过1000个。如果资源数量超过1000个，请使用[ListTagResources](~~110425~~)接口进行查询。 |
|Tag.N.Value|String|否|TestValue|安全组的标签值。N的取值范围：1~20 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|安全组所在的企业资源组ID。使用该参数过滤资源时，资源数量不能超过1000个。 |
|NetworkType|String|否|vpc|安全组的网络类型。取值范围：

 -   vpc
-   classic |
|SecurityGroupId|String|否|sg-bp67acfmxazb4p\*\*\*\*|安全组ID。 |
|SecurityGroupName|String|否|SGTestName|安全组名称。 |
|SecurityGroupType|String|否|normal|安全组类型。取值范围：

 -   normal：普通安全组
-   enterprise：企业安全组

**说明：** 当不为该参数传值时，表示查询所有类型的安全组。 |
|DryRun|Boolean|否|false|是否只预检此次请求。取值范围：

 -   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码DryRunOperation。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

 默认值：false |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|1|每页行数。 |
|RegionId|String|cn-hangzhou|安全组所属地域ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|SecurityGroups|Array of SecurityGroup| |安全组信息集合。 |
|SecurityGroup| | | |
|AvailableInstanceAmount|Integer|0|**说明：** 该参数正在邀测中，暂未开放使用。 |
|CreationTime|String|2017-12-05T22:40:00Z|创建时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC时间。格式为：yyyy-MM-ddThh:mmZ。 |
|Description|String|TestDescription|安全组描述信息。 |
|EcsCount|Integer|0|**说明：** 该参数正在邀测中，暂未开放使用。 |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|安全组所在的企业资源组ID。 |
|SecurityGroupId|String|sg-bp67acfmxazb4p\*\*\*\*|安全组ID。 |
|SecurityGroupName|String|SGTestName|安全组名称。 |
|SecurityGroupType|String|normal|安全组类型。可能值：

 -   normal：普通安全组
-   enterprise：企业安全组 |
|ServiceID|Long|12345678910|安全组对应的虚商ID。 |
|ServiceManaged|Boolean|true|安全组的使所有者是否为云产品或虚商。 |
|Tags|Array of Tag| |安全组的标签。 |
|Tag| | | |
|TagKey|String|TestKey|安全组的标签键。 |
|TagValue|String|TestValue|安全组的标签值。 |
|VpcId|String|vpc-bp67acfmxazb4p\*\*\*\*|安全组所属的专有网络。 |
|TotalCount|Integer|49|安全组的总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeSecurityGroups
&RegionId=cn-hangzhou
&PageSize=1
&PageNumber=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeSecurityGroupsResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>49</TotalCount>
      <PageSize>1</PageSize>
      <RegionId>cn-hangzhou</RegionId>
      <RequestId>A1707FC0-430C-423A-B624-284046B20399</RequestId>
      <SecurityGroups>
            <SecurityGroup>
                  <CreationTime>2019-11-01T06:08:46Z</CreationTime>
                  <SecurityGroupId>sg-bp67acfmxazb4p****</SecurityGroupId>
                  <Description></Description>
                  <SecurityGroupName>SGTestName</SecurityGroupName>
                  <ResourceGroupId></ResourceGroupId>
                  <SecurityGroupType>normal</SecurityGroupType>
                  <VpcId>vpc-bp67acfmxazb4p****</VpcId>
            </SecurityGroup>
      </SecurityGroups>
</DescribeSecurityGroupsResponse>
```

`JSON` 格式

```
{
	"PageNumber": 1,
	"TotalCount": 49,
	"PageSize": 1,
	"RegionId": "cn-hangzhou",
	"RequestId": "A1707FC0-430C-423A-B624-284046B20399",
	"SecurityGroups": {
		"SecurityGroup": [
			{
				"CreationTime": "2019-11-01T06:08:46Z",
				"Tags": {
					"Tag": []
				},
				"SecurityGroupId": "sg-bp67acfmxazb4p****",
				"Description": "",
				"SecurityGroupName": "SGTestName",
				"ResourceGroupId": "",
				"SecurityGroupType": "normal",
				"VpcId": "vpc-bp67acfmxazb4p****"
			}
		]
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

