# DescribeCapacityReservations

You can call this operation to query the details of one or more capacity reservations.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeCapacityReservations&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeCapacityReservations|The operation that you want to perform. Set the value to DescribeCapacityReservations. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the capacity reservation. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|MaxResults|Integer|No|10|The maximum number of entries to return on each page.

Maximum value: 100.

Default value: 10. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the query. The token is obtained from the response of the previous request. |
|PrivatePoolOptions.Ids|String|No|\["crp-bp67acfmxazb4\*\*\*\*", "crp-bp67acfmxazb5\*\*\*\*"\]|The IDs of the capacity reservations. The value can be a JSON array that consists of up to 100 IDs. Separate multiple IDs with commas \(,\). |
|Platform|String|No|linux|The operating system of instances to be created by using the capacity reservation. Valid values:

-   Windows: queries only capacity reservations that reserve capacity for Windows instances.
-   Linux: queries only capacity reservations that reserve capacity for Linux instances.
-   all: queries all capacity reservations.

Default value: all. |
|InstanceType|String|No|ecs.c6.large|The instance type of instances to be created by using the capacity reservation. |
|ZoneId|String|No|cn-hangzhou-h|The zone ID of the capacity reservation. |
|InstanceChargeType|String|No|PostPaid|The billing method of the instances to be created by using the capacity reservation. Set the value to PostPaid. You can query only capacity reservations that reserve capacity for pay-as-you-go instances.

Default value: PostPaid. |
|Status|String|No|Active|The status of the capacity reservation. Valid values:

-   Preparing: queries capacity reservations that are being prepared.
-   Active: queries capacity reservations that are in effect.
-   Released: queries capacity reservations that have been released manually or automatically upon expiration.

Default value: Active. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CapacityReservationSet|Array of CapacityReservationItem| |Details of capacity reservations. |
|CapacityReservationItem| | | |
|AllocatedResources|Array of AllocatedResource| |Details of allocated resources. |
|AllocatedResource| | | |
|InstanceType|String|ecs.c6.large|The instance type of instances to be created by using the capacity reservation. |
|TotalAmount|Integer|2|The total number of instances reserved for a single instance type. |
|UsedAmount|Integer|2|The number of instances reserved by the capacity reservation that have been used. |
|zoneId|String|cn-hangzhou-h|The zone ID of the capacity reservation. |
|Description|String|This is description.|The description of the capacity reservation. |
|EndTime|String|2021-02-19T03:02Z|The expiration time of the capacity reservation. |
|EndTimeType|String|Unlimited|The release mode of the capacity reservation. Valid values:

-   Limited: The capacity reservation is automatically released at the specified time.
-   Unlimited: The capacity reservation is manually released. You can release capacity reservations at any time. |
|InstanceChargeType|String|PostPaid|The billing method of the instances to be created by using the capacity reservation. |
|Platform|String|linux|The operating system of the instances to be created by using the capacity reservation. Valid values:

-   windows
-   linux |
|PrivatePoolOptionsId|String|cr-bp67acfmxazb4\*\*\*\*|The ID of the capacity reservation. |
|PrivatePoolOptionsMatchCriteria|String|Open|The type of the private pool generated after the capacity reservation takes effect. Valid values:

-   Open: open private pool
-   Target: targeted private pool |
|PrivatePoolOptionsName|String|crpTestName|The name of the capacity reservation. |
|RegionId|String|cn-hangzhou|The region ID of the capacity reservation. |
|StartTime|String|2021-02-19T02:01Z|The effective time of the capacity reservation. |
|Status|String|Active|The status of the capacity reservation. Valid values:

-   Preparing: The capacity reservation is being prepared.
-   Active: The capacity reservation is in effect.
-   Released: The capacity reservation has been released manually or automatically upon expiration. |
|TimeSlot|String|null|**Note:** This parameter is in invitational preview and not available. |
|MaxResults|Integer|10|The maximum number of entries returned per page. |
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the next query. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|10|The total number of entries returned. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeCapacityReservations
&RegionId=cn-hangzhou
&PrivatePoolOptions.Ids=["crp-bp67acfmxazb4****", "crp-bp67acfmxazb5****"]
&InstanceType=ecs.c6.large
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|The error message returned because the required RegionId parameter is not specified.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

