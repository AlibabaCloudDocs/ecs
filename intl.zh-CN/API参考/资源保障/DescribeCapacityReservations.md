# DescribeCapacityReservations

调用DescribeCapacityReservations查询一个或多个容量预定服务的详细信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeCapacityReservations&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeCapacityReservations|系统规定参数。取值：DescribeCapacityReservations |
|RegionId|String|是|cn-hangzhou|容量预定服务所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|MaxResults|Integer|否|10|分页查询时每页行数。

 最大值：100

 默认值：10 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0a4883|容量预定服务查询起始标志。由上一次的请求结果中获取。 |
|PrivatePoolOptions.Ids|String|否|\["crp-bp67acfmxazb4\*\*\*\*", "crp-bp67acfmxazb5\*\*\*\*"\]|容量预定服务ID列表。取值可以由多个ID组成一个JSON数组，最多支持100个ID，ID之间用半角逗号（,）隔开。 |
|Platform|String|否|linux|实例的操作系统。取值范围：

 -   windows：仅查询windows系统的容量预定服务。
-   linux：仅查询linux系统的容量预定服务。
-   all：查询所有容量预定服务。

 默认值：all |
|InstanceType|String|否|ecs.c6.large|实例规格。 |
|ZoneId|String|否|cn-hangzhou-h|容量预定服务所属地域下的可用区ID。 |
|InstanceChargeType|String|否|PostPaid|实例的计费方式。取值：PostPaid，目前仅支持按量付费。

 默认值：PostPaid |
|Status|String|否|Active|容量预定服务的状态。取值范围：

 -   Preparing：准备中。
-   Active：生效中。
-   Released：已释放，包括手动释放与到期自动释放。

 默认值：Active |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|CapacityReservationSet|Array of CapacityReservationItem| |容量预定服务详细信息组成的集合。 |
|CapacityReservationItem| | | |
|AllocatedResources|Array of AllocatedResource| |资源分配详情。 |
|AllocatedResource| | | |
|InstanceType|String|ecs.c6.large|实例规格。 |
|TotalAmount|Integer|2|在一个实例规格内，需要预留的实例的总数量。 |
|UsedAmount|Integer|2|已使用的实例的数量。 |
|zoneId|String|cn-hangzhou-h|可用区ID。 |
|Description|String|This is description.|容量预定服务描述。 |
|EndTime|String|2021-02-19T03:02Z|容量预定服务的失效时间。 |
|EndTimeType|String|Unlimited|容量预定服务的失效方式。可能值：

 -   Limited：指定时间释放。
-   Unlimited：手动释放。不限制时间。 |
|InstanceChargeType|String|PostPaid|容量预定服务中实例的付费类型。 |
|Platform|String|linux|匹配的实例的操作系统。可能值：

 -   windows
-   linux |
|PrivatePoolOptionsId|String|cr-bp67acfmxazb4\*\*\*\*|容量预定服务ID。 |
|PrivatePoolOptionsMatchCriteria|String|Open|容量预定服务生效后生成的私有资源池的类型。可能值：

 -   Open：开放模式。
-   Target：专用模式。 |
|PrivatePoolOptionsName|String|crpTestName|容量预定服务名称。 |
|RegionId|String|cn-hangzhou|容量预定服务所属地域ID。 |
|StartTime|String|2021-02-19T02:01Z|容量预定服务生效时间。 |
|Status|String|Active|容量预定服务的状态。可能值：

 -   Preparing：准备中。
-   Active：生效中。
-   Released：已释放，包括手动释放与到期自动释放。 |
|TimeSlot|String|null|**说明：** 该参数正在邀测中，暂未开放使用。 |
|MaxResults|Integer|10|容量预定服务每页显示行数。 |
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|容量预定服务下一个查询起始标志。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|10|符合查询条件的记录条数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeCapacityReservations
&RegionId=cn-hangzhou
&PrivatePoolOptions.Ids=["crp-bp67acfmxazb4****", "crp-bp67acfmxazb5****"]
&InstanceType=ecs.c6.large
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeCapacityReservationsResponse>
      <TotalCount>10</TotalCount>
      <NextToken>caeba0bbb2be03f84eb48b699f0a4883</NextToken>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <MaxResults>10</MaxResults>
      <CapacityReservationSet>
            <CapacityReservationItem>
                  <Status>Active</Status>
                  <Description>This is description.</Description>
                  <Platform>linux</Platform>
                  <EndTimeType>Unlimited</EndTimeType>
                  <EndTime>2021-02-19T03:02Z</EndTime>
                  <PrivatePoolOptionsName>crpTestName</PrivatePoolOptionsName>
                  <InstanceChargeType>PostPaid</InstanceChargeType>
                  <StartTime>2021-02-19T02:01Z</StartTime>
                  <PrivatePoolOptionsMatchCriteria>Open</PrivatePoolOptionsMatchCriteria>
                  <RegionId>cn-hangzhou</RegionId>
                  <TimeSlot></TimeSlot>
                  <PrivatePoolOptionsId>cr-bp67acfmxazb4****</PrivatePoolOptionsId>
                  <AllocatedResources>
                        <AllocatedResource>
                              <UsedAmount>2</UsedAmount>
                              <zoneId>cn-hangzhou-h</zoneId>
                              <TotalAmount>2</TotalAmount>
                              <InstanceType>ecs.c6.large</InstanceType>
                        </AllocatedResource>
                  </AllocatedResources>
            </CapacityReservationItem>
      </CapacityReservationSet>
</DescribeCapacityReservationsResponse>
```

`JSON`格式

```
{
    "TotalCount": "10", 
    "NextToken": "caeba0bbb2be03f84eb48b699f0a4883", 
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E", 
    "MaxResults": "10", 
    "CapacityReservationSet": {
        "CapacityReservationItem": [
            {
                "Status": "Active", 
                "Description": "This is description.", 
                "Platform": "linux", 
                "EndTimeType": "Unlimited", 
                "EndTime": "2021-02-19T03:02Z", 
                "PrivatePoolOptionsName": "crpTestName", 
                "InstanceChargeType": "PostPaid", 
                "StartTime": "2021-02-19T02:01Z", 
                "PrivatePoolOptionsMatchCriteria": "Open", 
                "RegionId": "cn-hangzhou", 
                "TimeSlot": "", 
                "PrivatePoolOptionsId": "cr-bp67acfmxazb4****", 
                "AllocatedResources": {
                    "AllocatedResource": [
                        {
                            "UsedAmount": "2", 
                            "zoneId": "cn-hangzhou-h", 
                            "TotalAmount": "2", 
                            "InstanceType": "ecs.c6.large"
                        }
                    ]
                }
            }
        ]
    }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|RegionId是必选参数。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

