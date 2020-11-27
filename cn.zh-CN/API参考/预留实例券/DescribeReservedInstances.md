# DescribeReservedInstances

调用DescribeReservedInstances查询已经购买的预留实例券。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeReservedInstances&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeReservedInstances|系统规定参数。取值： DescribeReservedInstances |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Tag.N.Key|String|否|TestKey|预留实例券的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。

 使用一个标签过滤资源，查询到该标签下的资源数量不能超过1000个；使用多个标签过滤资源，查询到同时绑定了多个标签的资源数量不能超过1000个。如果资源数量超过1000个，请使用[ListTagResources](~~110425~~)接口进行查询。 |
|Tag.N.Value|String|否|TestValue|预留实例券的标签值。N的取值范围：1~20。一旦传入该值，允许为空字符串。最多支持128个字符，不能以acs:开头，不能包含http://或者https://。 |
|PageNumber|Integer|否|1|预留实例券列表的页码，起始值：1

 默认值：1 |
|PageSize|Integer|否|50|分页查询时的每页行数，最大值：100

 默认值：10 |
|ZoneId|String|否|cn-hangzhou-z|实例所属的可用区编号，当Scope为Zone时必填。更多详情，请参见[DescribeZones](~~25610~~)获取可用区列表。 |
|ReservedInstanceId.N|RepeatList|否|ri-bpzhex2ulpzf53\*\*\*\*|预留实例券ID。N的取值范围：1~100 |
|ReservedInstanceName|String|否|testReservedInstanceName|预留实例券名称。 |
|Status.N|RepeatList|否|Active|预留实例券的状态，N的取值范围：1~100。状态值取值范围：

 -   Creating：正在创建
-   Active：在有效期中
-   Expired：已过期
-   Updating：正在更改预留实例券的属性 |
|LockReason|String|否|security|锁定类型。取值范围：

 -   financial：账号欠费或服务过期
-   security：安全原因 |
|InstanceType|String|否|ecs.g5.large|实例资源的规格。取值请参见[实例规格族](~~25378~~)。 |
|InstanceTypeFamily|String|否|ecs.g5|实例资源的规格族。取值请参见[实例规格族](~~25378~~)。 |
|Scope|String|否|Region|预留实例券的范围。取值范围：

 -   Region：地域级别
-   Zone：可用区级别

 默认值：Region |
|OfferingType|String|否|All Upfront|预留实例券的付款类型。取值范围：

 -   No Upfront：零预付
-   Partial Upfront：部分预付
-   All Upfront：全预付 |
|AllocationType|String|否|Normal|分配类型。取值范围：

 -   Normal：查询当前账号下的预留实例券。
-   Shared：查询当前账号下已经建立主子账号共享的预留实例券。

 默认值：Normal |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|预留实例券列表的页码。 |
|PageSize|Integer|1|输入时设置的每页行数。 |
|RequestId|String|E572643C-6A29-49D6-9D4E-6CFA4E063A3E|请求ID。 |
|ReservedInstances|Array of ReservedInstance| |由ReservedInstance组成的数组格式，返回预留实例券的详细信息。 |
|ReservedInstance| | | |
|AllocationStatus|String|allocated|当AllocationType值为Shared时，该参数表示预留实例券的分配状态。可能值：

 -   allocated：已分配给其他用户的预留实例券。
-   beAllocated：被其他用户分配的预留实例券。 |
|CreationTime|String|2018-12-10T12:07Z|创建时间。 |
|Description|String|testDescription|描述。 |
|ExpiredTime|String|2019-12-10T12:07Z|到期时间。 |
|InstanceAmount|Integer|10|可以匹配同规格按量付费实例的数量。 |
|InstanceType|String|ecs.g5.large|匹配的按量付费实例的规格。 |
|OfferingType|String|All Upfront|付款类型。 |
|OperationLocks|Array of OperationLock| |是否被锁定。 |
|OperationLock| | | |
|LockReason|String|security|锁定原因。 |
|Platform|String|Linux|实例使用的镜像的操作系统类型。可能值：

 -   Windows：Windows Server类型的操作系统。
-   Linux：Linux及类Unix类型的操作系统。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|ReservedInstanceId|String|ri-bpzhex2ulpzf53\*\*\*\*|预留实例券ID。 |
|ReservedInstanceName|String|riZbpzhex2ulpzf53\*\*\*\*|名称。 |
|ResourceGroupId|String|EcsDocTest|资源组。 |
|Scope|String|region|范围。 |
|StartTime|String|2018-12-10T12:00Z|生效时间。 |
|Status|String|Active|状态。 |
|Tags|Array of Tag| |预留实例券的标签对信息。 |
|Tag| | | |
|TagKey|String|TestKey|预留实例券的标签键。 |
|TagValue|String|TestValue|预留实例券的标签值。 |
|ZoneId|String|cn-hangzhou-z|可用区ID。 |
|TotalCount|Integer|1|预留实例券的总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeReservedInstances
&RegionId=cn-hangzhou
&Scope=Region
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeReservedInstancesResponse>
      <ReservedInstances>
            <ReservedInstance>
                  <CreationTime>2018-12-10T12:07Z</CreationTime>
                  <ExpiredTime>2019-12-10T16:00Z</ExpiredTime>
                  <InstanceAmount>1</InstanceAmount>
                  <ReservedInstanceId>ri-0xzhex2ulpzf53****</ReservedInstanceId>
                  <InstanceType>ecs.g5.large</InstanceType>
                  <OfferingType>All Upfront</OfferingType>
                  <RegionId>cn-hangzhou-test-307</RegionId>
                  <ReservedInstanceName>riZ0xzhex2ulpzf53****</ReservedInstanceName>
                  <Scope>region</Scope>
                  <StartTime>2018-12-10T12:00Z</StartTime>
                  <Status>Active</Status>
                  <Tags>
                        <Tag>
                              <TagKey>TestKey</TagKey>
                              <TagValue>TestValue</TagValue>
                        </Tag>
                  </Tags>
            </ReservedInstance>
      </ReservedInstances>
      <RequestId>E572643C-6A29-49D6-9D4E-6CFA4E063A3E</RequestId>
      <PageNumber>1</PageNumber>
      <PageSize>50</PageSize>
      <Total>1</Total>
</DescribeReservedInstancesResponse>
```

`JSON` 格式

```
{
    "ReservedInstances":{
        "ReservedInstance":[
            {
                "CreationTime":"2018-12-10T12:07Z",
                "ExpiredTime":"2019-12-10T16:00Z",
                "InstanceAmount":1,
                "ReservedInstanceId":"ri-0xzhex2ulpzf53****",
                "InstanceType":"ecs.g5.large",
                "OfferingType":"All Upfront",
                "RegionId":"cn-hangzhou-test-307",
                "ReservedInstanceName":"riZ0xzhex2ulpzf53****",
                "Scope":"region",
                "StartTime":"2018-12-10T12:00Z",
                "Status":"Active",
				"Tags": {
					"Tag": [
						{
							"TagKey": "TestKey",
							"TagValue": "TestValue"
						}
					]
				}
            }
        ]
    },
    "RequestId":"E572643C-6A29-49D6-9D4E-6CFA4E063A3E",
    "PageNumber":1,
    "PageSize":50,
    "Total":1
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParamter.RegionId|The regionId should not be null.|参数RegionId不得为空。|
|400|InvalidRegion.NotFound|The specified parameter RegionId is not valid.|RegionId参数不合法。|
|400|InvalidZone.NotFound|The specified parameter ZoneId is not valid.|指定的ZoneId不合法。|
|400|InvalidEndTime.ValueNotSupported|The specified endTime is out of the permitted range.|指定的EndTime超过限制。|
|400|InvalidAllocationType.ValueNotSupported|The specified AllocationType is not supported.|指定的分配类型无效。|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist in our records.|指定的RegionId不存在，请您检查此产品在该地域是否可用。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

