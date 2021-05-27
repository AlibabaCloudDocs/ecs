# DescribeCapacityReservationInstances

You can call this operation to query the instances that were created by using a capacity reservation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeCapacityReservationInstances&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeCapacityReservationInstances|The operation that you want to perform. Set the value to DescribeCapacityReservationInstances. |
|PrivatePoolOptions.Id|String|Yes|crp-bp67acfmxazb4\*\*\*\*|The ID of the capacity reservation. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the capacity reservation. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|MaxResults|Integer|No|10|The number of entries to return on each page.

Maximum value: 100

Default value: 10. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the query. The token is obtained from the response of the previous request. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CapacityReservationItem|Array of InstanceIdSet| |Details about the instances that were created by using the capacity reservation. |
|InstanceIdSet| | | |
|InstanceId|String|i-bp67acfmxazb4\*\*\*\*|The ID of the instance. |
|MaxResults|Integer|10|The number of entries returned per page. |
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the next query. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|10|The number of entries that meet the query criteria. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeCapacityReservationInstances
&RegionId=cn-hangzhou
&PrivatePoolOptions.Id=crp-bp67acfmxazb4****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeCapacityReservationInstancesResponse>
      <TotalCount>2</TotalCount>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <NextToken>caeba0bbb2be03f84eb48b699f0a4883</NextToken>
      <MaxResults>10</MaxResults>
      <CapacityReservationItem>
            <InstanceIdSet>
                  <InstanceId>i-bp67acfmxazb4****</InstanceId>
            </InstanceIdSet>
            <InstanceIdSet>
                  <InstanceId>i-bp67acfmxazb5****</InstanceId>
            </InstanceIdSet>
      </CapacityReservationItem>
</DescribeCapacityReservationInstancesResponse>
```

`JSON` format

```
{
    "TotalCount":2,
    "RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "NextToken":"caeba0bbb2be03f84eb48b699f0a4883",
    "MaxResults":10,
    "CapacityReservationItem":
        {"InstanceIdSet":
            [{"InstanceId":"i-bp67acfmxazb4****"},
            {"InstanceId":"i-bp67acfmxazb5****"}]
        }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|The error message returned because the RegionId parameter is not specified.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

