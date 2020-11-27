# DescribeStorageCapacityUnits

调用DescribeStorageCapacityUnits查询一个或多个存储容量单位包SCU的详细信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeStorageCapacityUnits&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeStorageCapacityUnits|系统必选参数。取值：DescribeStorageCapacityUnits |
|RegionId|String|是|cn-hangzhou|SCU所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|PageNumber|Integer|否|1|SCU列表的页码。

 起始值：1

 默认值：1 |
|PageSize|Integer|否|1|分页查询时的每页行数。

 最大值：100

 默认值：10 |
|Name|String|否|testScuName|SCU的名称。 |
|Capacity|Integer|否|20|SCU容量大小，单位为GiB。取值范围：\{20, 40, 100, 200, 500, 1024, 2048, 5120, 10240, 20480, 51200\}

 默认值：无 |
|StorageCapacityUnitId.N|RepeatList|否|scu-bp67acfmxazb4p\*\*\*\*|一个或多个SCU ID。N的取值范围：1~100 |
|Status.N|RepeatList|否|Active|一个或多个SCU的状态值，N取值范围为1~4。状态的取值范围：

 -   Creating：创建中
-   Active：启用中
-   Expired：已过期
-   Pending：待生效

 默认值：无 |
|AllocationType|String|否|Normal|分配类型。取值范围：

 -   Normal：查询当前帐号下的SCU。
-   Shared：查询已经建立主子账号共享的SCU。

 默认值：Normal |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|SCU列表的页码。 |
|PageSize|Integer|1|分页查询时的每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|StorageCapacityUnits|Array of StorageCapacityUnit| |由StorageCapacityUnits组成的数组格式，返回SCU的详细信息。 |
|StorageCapacityUnit| | | |
|AllocationStatus|String|allocated|当AllocationType值为Shared时，该参数表示SCU的分配状态。可能值：

 -   allocated：已分配给其他用户的SCU。
-   beAllocated：被其他用户分配的SCU。 |
|Capacity|Integer|20|SCU的容量。 |
|CreationTime|String|2019-09-25T02:12:00Z|SCU的创建时间。 |
|Description|String|testScuDescription|SCU的描述信息。 |
|ExpiredTime|String|2019-09-25T02:12:00Z|SCU的到期时间。 |
|Name|String|testScuName|SCU的名称。 |
|RegionId|String|cn-hangzhou|SCU的所属地域ID。 |
|StartTime|String|2019-09-25T02:00:00Z|SCU的开始生效时间。 |
|Status|String|Active|SCU的状态。 |
|StorageCapacityUnitId|String|scu-bp67acfmxazb4p\*\*\*\*|SCU的ID。 |
|TotalCount|Integer|4|SCU总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeStorageCapacityUnits
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeStorageCapacityUnitsResponse>
      <PageNumber>1</PageNumber>
      <PageSize>1</PageSize>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <StorageCapacityUnits>
            <StorageCapacityUnit>
                  <Capacity>20</Capacity>
                  <CreationTime>2019-09-25T02:12:00Z</CreationTime>
                  <Description>testScuDescription</Description>
                  <ExpiredTime>2019-09-25T02:12:00Z</ExpiredTime>
                  <Name>testScuName</Name>
                  <OfferingType>All Upfront</OfferingType>
                  <RegionId>cn-hangzhou</RegionId>
                  <StartTime>2019-09-25T02:00:00Z</StartTime>
                  <Status>Active</Status>
                  <AllocationStatus></AllocationStatus>
                  <StorageCapacityUnitId>scu-bp67acfmxazb4p****</StorageCapacityUnitId>
            </StorageCapacityUnit>
      </StorageCapacityUnits>
      <TotalCount>4</TotalCount>
</DescribeStorageCapacityUnitsResponse>
```

`JSON` 格式

```
{
    "PageNumber": "1",
    "PageSize": "1",
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "StorageCapacityUnits": {
        "StorageCapacityUnit": [{
            "Capacity": "20",
            "CreationTime": "2019-09-25T02:12:00Z",
            "Description": "testScuDescription",
            "ExpiredTime": "2019-09-25T02:12:00Z",
            "Name": "testScuName",
            "OfferingType": "All Upfront",
            "RegionId": "cn-hangzhou",
            "StartTime": "2019-09-25T02:00:00Z",
            "Status": "Active",
            "AllocationStatus": "",
            "StorageCapacityUnitId": "scu-bp67acfmxazb4p****"
    
        }] 
    },    
    "TotalCount": "4"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|RegionId是必选参数。|
|400|InvalidParameter.Name|The specified Name is invalid.|指定的Name参数无效。|
|400|InvalidParameter.CapacityExceed|The specified Capacity exceeds the limitation of quota.|指定的Capacity参数超出了最大有效取值。|
|400|InvalidAllocationType.ValueNotSupported|The specified AllocationType is not supported.|指定的分配类型无效。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

