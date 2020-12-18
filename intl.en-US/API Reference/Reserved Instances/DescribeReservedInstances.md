# DescribeReservedInstances

You can call this operation to query purchased reserved instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeReservedInstances&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeReservedInstances|The operation that you want to perform. Set the value to DescribeReservedInstances. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the reserved instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the reserved instance. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 128 characters in length. It cannot start with aliyun or acs: or contain http:// or https://.

If a single tag is specified to query resources, up to 1,000 resources that are bound with this tag can be displayed in the response. If multiple tags are specified to query resources, up to 1,000 resources that are bound with all these tags can be displayed in the response. To query more than 1,000 resources that are bound with specified tags, call the [ListTagResources](~~110425~~) operation. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the reserved instance. Valid values of N: 1 to 20. The tag value can be an empty string. It can be up to 128 characters in length. It cannot start with acs: or contain http:// or https://. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1. |
|PageSize|Integer|No|50|The number of entries to return on each page. Maximum value: 100.

Default value: 10. |
|ZoneId|String|No|cn-hangzhou-z|The zone ID of the reserved instance. This parameter is required when Scope is set to Zone. You can call the [DescribeZones](~~25610~~) operation to query the most recent zone list. |
|ReservedInstanceId.N|RepeatList|No|ri-bpzhex2ulpzf53\*\*\*\*|The ID of reserved instance N. Valid values of N: 1 to 100. |
|ReservedInstanceName|String|No|testReservedInstanceName|The name of the reserved instance. |
|Status.N|RepeatList|No|Active|The status of reserved instance N. Valid values of N: 1 to 100. Valid values:

-   Creating
-   Active
-   Expired
-   Updating |
|LockReason|String|No|security|The reason why the reserved instance is locked. Valid values:

-   financial: You have an overdue payment in your account or the reserved instance has expired.
-   security: The reserved instance is locked for security reasons. |
|InstanceType|String|No|ecs.g5.large|The instance type of the reserved instance. For more information about the valid values, see [Instance families](~~25378~~). |
|InstanceTypeFamily|String|No|ecs.g5|The instance family of the reserved instance. For more information about the valid values, see [Instance families](~~25378~~). |
|Scope|String|No|Region|The scope of the reserved instance. Valid values:

-   Region: regional
-   Zone: zonal

Default value: Region. |
|OfferingType|String|No|All Upfront|The payment option of the reserved instance. Valid values:

-   No Upfront
-   Partial Upfront
-   All Upfront |
|AllocationType|String|No|Normal|The allocation type. Valid values:

-   Normal: queries all reserved instances that belong to the current account.
-   Shared: queries reserved instances that are shared between the main account and linked accounts.

Default value: Normal. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|1|The number of entries returned per page. |
|RequestId|String|E572643C-6A29-49D6-9D4E-6CFA4E063A3E|The ID of the request. |
|ReservedInstances|Array of ReservedInstance| |Details about the reserved instances. |
|ReservedInstance| | | |
|AllocationStatus|String|allocated|Indicates the sharing status of the reserved instance when the AllocationType parameter is set to Shared. Valid values:

-   allocated: The reserved instance is allocated to another account.
-   beAllocated: The reserved instance is allocated by another account. |
|CreationTime|String|2018-12-10T12:07Z|The time when the reserved instance was created. |
|Description|String|testDescription|The description of the reserved instance. |
|ExpiredTime|String|2019-12-10T12:07Z|The time when the reserved instance expires. |
|InstanceAmount|Integer|10|The number of pay-as-you-go instances that are of the same instance type as the reserved instance and can be matched to the reserved instance. |
|InstanceType|String|ecs.g5.large|The instance type of the pay-as-you-go instances that can be matched to the reserved instance. |
|OfferingType|String|All Upfront|The payment option of the reserved instance. |
|OperationLocks|Array of OperationLock| |Details about the lock status of the reserved instance. |
|OperationLock| | | |
|LockReason|String|security|The reason why the reserved instance was locked. |
|Platform|String|Linux|The operating system of the reserved instance. Valid values:

-   Windows: Windows Server operating systems
-   Linux: Linux and Unix-like operating systems |
|RegionId|String|cn-hangzhou|The region ID of the reserved instance. |
|ReservedInstanceId|String|ri-bpzhex2ulpzf53\*\*\*\*|The ID of the reserved instance. |
|ReservedInstanceName|String|riZbpzhex2ulpzf53\*\*\*\*|The name of the reserved instance. |
|ResourceGroupId|String|EcsDocTest|The ID of the resource group. |
|Scope|String|region|The scope of the reserved instance. |
|StartTime|String|2018-12-10T12:00Z|The time when the reserved instance took effect. |
|Status|String|Active|The status of the reserved instance. |
|Tags|Array of Tag| |Details about the tags of the reserved instance. |
|Tag| | | |
|TagKey|String|TestKey|The tag key of the reserved instance. |
|TagValue|String|TestValue|The tag value of the reserved instance. |
|ZoneId|String|cn-hangzhou-z|The zone ID of the reserved instance. |
|TotalCount|Integer|1|The total number of reserved instances. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeReservedInstances
&RegionId=cn-hangzhou
&Scope=Region
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParamter.RegionId|The regionId should not be null.|The error message returned because the RegionId parameter is not specified.|
|400|InvalidRegion.NotFound|The specified parameter RegionId is not valid.|The error message returned because the specified RegionId parameter is invalid.|
|400|InvalidZone.NotFound|The specified parameter ZoneId is not valid.|The error message returned because the specified ZoneId parameter is invalid.|
|400|InvalidEndTime.ValueNotSupported|The specified endTime is out of the permitted range.|The error message returned because the value of the specified EndTime parameter is out of range.|
|400|InvalidAllocationType.ValueNotSupported|The specified AllocationType is not supported.|The error message returned because the specified AllocationType parameter is invalid.|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist in our records.|The error message returned because the specified RegionId parameter does not exist. Check whether the reserved instance service is available in the region.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

