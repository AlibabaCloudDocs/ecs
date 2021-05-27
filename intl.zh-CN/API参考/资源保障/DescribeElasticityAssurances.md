# DescribeElasticityAssurances

调用DescribeElasticityAssurances查询弹性保障服务的详细信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeElasticityAssurances&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeElasticityAssurances|系统规定参数。取值：DescribeElasticityAssurances |
|RegionId|String|是|cn-hangzhou|弹性保障服务所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|MaxResults|Integer|否|10|分页查询时每页行数。

 最大值：100

 默认值：10 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0a4883|弹性保障服务查询起始标志。由上一次的请求结果中获取。 |
|PrivatePoolOptions.Ids|String|否|\["eap-bp67acfmxazb4\*\*\*\*", "eap-bp67acfmxazb5\*\*\*\*"\]|弹性保障服务ID列表。取值可以由多个ID组成一个JSON数组，最多支持100个ID，ID之间用半角逗号（,）隔开。 |
|InstanceType|String|否|ecs.c6.large|实例规格。 |
|ZoneId|String|否|cn-hangzhou-h|弹性保障服务所属地域下的可用区ID。 |
|InstanceChargeType|String|否|PostPaid|实例的计费方式。取值：PostPaid，目前仅支持按量付费。

 默认值：PostPaid |
|Status|String|否|Active|弹性保障服务的状态。取值范围：

 -   Preparing：准备中。
-   Active：正常。
-   Released：已释放。

 默认值：Active |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ElasticityAssuranceSet|Array of ElasticityAssuranceItem| |弹性保障服务详细信息组成的集合。 |
|ElasticityAssuranceItem| | | |
|AllocatedResources|Array of AllocatedResource| |资源分配详情。 |
|AllocatedResource| | | |
|InstanceType|String|ecs.c6.large|实例规格。 |
|TotalAmount|Integer|2|在一个实例规格内，需要预留的实例的总数量。 |
|UsedAmount|Integer|2|已使用的实例的数量。 |
|zoneId|String|cn-hangzhou-h|可用区ID。 |
|Description|String|This is description.|弹性保障服务描述。 |
|EndTime|String|2021-10-30T06:32:00Z|弹性保障服务失效时间。 |
|LatestStartTime|String|0|**说明：** 该参数暂未开放使用。 |
|PrivatePoolOptionsId|String|eap-bp67acfmxazb4\*\*\*\*|弹性保障服务ID。 |
|PrivatePoolOptionsMatchCriteria|String|Open|弹性保障服务的匹配模式。可能值：

 -   Open：开放模式的弹性保障服务。
-   Target：指定模式的弹性保障服务。 |
|PrivatePoolOptionsName|String|eapTestName|弹性保障服务名称。 |
|RegionId|String|cn-hangzhou|弹性保障服务所属地域ID。 |
|StartTime|String|2020-10-30T06:32:00Z|弹性保障服务生效时间。 |
|Status|String|Active|弹性保障服务的状态。可能值：

 -   Preparing：准备中。
-   Active：正常。
-   Released：已释放。 |
|TotalAssuranceTimes|String|Unlimited|弹性保障服务的总次数。 |
|UsedAssuranceTimes|Integer|0|**说明：** 该参数暂未开放使用。 |
|MaxResults|Integer|10|弹性保障服务每页显示行数。 |
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|弹性保障服务下一个查询起始标志。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|10|符合查询条件的记录条数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeElasticityAssurances
&RegionId=cn-hangzhou
&PrivatePoolOptions.Ids=["eap-bp67acfmxazb4****", "eap-bp67acfmxazb5****"]
&InstanceType=ecs.c6.large
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeElasticityAssurancesResponse>
      <ElasticityAssuranceSet>
            <ElasticityAssuranceItem>
                  <TotalAssuranceTimes>Unlimited</TotalAssuranceTimes>
                  <Status>Active</Status>
                  <UsedAssuranceTimes>0</UsedAssuranceTimes>
                  <Description>This is description.</Description>
                  <EndTime>2021-09-29T16:00Z</EndTime>
                  <PrivatePoolOptionsName>eapTestName</PrivatePoolOptionsName>
                  <LatestStartTime></LatestStartTime>
                  <StartTime>2020-09-29T08:00Z</StartTime>
                  <RegionId>cn-hangzhou</RegionId>
                  <PrivatePoolOptionsMatchCriteria>Open</PrivatePoolOptionsMatchCriteria>
                  <AllocatedResources>
                        <AllocatedResource>
                              <UsedAmount>0</UsedAmount>
                              <zoneId>cn-hangzhou-i</zoneId>
                              <TotalAmount>3</TotalAmount>
                              <InstanceType>ecs.c6.xlarge</InstanceType>
                        </AllocatedResource>
                  </AllocatedResources>
                  <PrivatePoolOptionsId>eap-bp1boncv6mbmv6wi****</PrivatePoolOptionsId>
            </ElasticityAssuranceItem>
      </ElasticityAssuranceSet>
      <TotalCount>1</TotalCount>
      <RequestId>45BF0929-A08F-49CA-A053-6FA3EC66B1BD</RequestId>
      <NextToken>caeba0bbb2be03f84eb48b699f0a4883</NextToken>
      <MaxResults>10</MaxResults>
</DescribeElasticityAssurancesResponse>
```

`JSON`格式

```
{
"ElasticityAssuranceSet":
    {
    "ElasticityAssuranceItem":
        [{  
        "TotalAssuranceTimes":"Unlimited",
        "Status":"Active",
        "UsedAssuranceTimes":0,
        "Description":"This is description.",
        "EndTime":"2021-09-29T16:00Z",
        "PrivatePoolOptionsName":"eapTestName",
        "LatestStartTime":"",
        "StartTime":"2020-09-29T08:00Z",
        "RegionId":"cn-hangzhou",
        "PrivatePoolOptionsMatchCriteria":"Open",
        "AllocatedResources":
            {
            "AllocatedResource":[
                {"UsedAmount":0,
                "zoneId":"cn-hangzhou-i",
                "TotalAmount":3,
                "InstanceType":"ecs.c6.xlarge"}
                ]
            },
        "PrivatePoolOptionsId":"eap-bp1boncv6mbmv6wi****"
        }]
    },
    "TotalCount":1,
    "RequestId":"45BF0929-A08F-49CA-A053-6FA3EC66B1BD",
    "NextToken":"caeba0bbb2be03f84eb48b699f0a4883",
    "MaxResults":10
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|RegionId是必选参数。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

