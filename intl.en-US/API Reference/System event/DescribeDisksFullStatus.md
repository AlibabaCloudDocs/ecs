# DescribeDisksFullStatus

You can call this operation to query the full status information of one or more Elastic Block Storage \(EBS\) devices.

## Description

-   The full status information of an EBS device includes the lifecycle status specified by the `Status` parameter, health status specified by the `HealthStatus` parameter, and event type specified by the `EventType` parameter of the EBS device.
-   EBS device events occur only when EBS devices are exceptional. The release time, scheduled execution time, and actual execution time of each EBS device event are the same. If you specify a period of time by using the `EventTime.Start` and `EventTime.End` parameters, all events that occurred during this period are queried. You can query events that occurred up to last seven days.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeDisksFullStatus&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDisksFullStatus|The operation that you want to perform. Set the value to DescribeDisksFullStatus. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the EBS device. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|DiskId.N|RepeatList|No|d-bp67acfmxazb4p\*\*\*\*|The ID of EBS device N. Valid values of N: 1 to 100. |
|EventId.N|RepeatList|No|e-bp67acfmxazb4p\*\*\*\*|The ID of event N. Valid values of N: 1 to 100. |
|Status|String|No|Available|The lifecycle status of the EBS device. For more information, see [Disk status](~~25689~~). Valid values:

-   In\_Use
-   Available
-   Attaching
-   Detaching
-   Creating
-   ReIniting |
|HealthStatus|String|No|Warning|The health status of the EBS device. Valid values:

-   Impaired: The EBS device is damaged.
-   Warning: The performance of the EBS device may be degraded.
-   Initializing: The EBS device is being initialized.
-   InsufficientData: The status cannot be determined due to insufficient data.
-   NotApplicable: The EBS device cannot be used. |
|EventType|String|No|Stalled|The event type. Valid values:

-   Degraded: The performance of the EBS device is degraded.
-   SeverelyDegraded: The performance of the EBS device is severely degraded.
-   Stalled: The performance of the EBS device is severely affected.
-   ErrorDetected: The local disk is damaged. |
|EventTime.Start|String|No|2018-05-06T02:43:10Z|The beginning of the time range to query.

Specify the time in the [ISO 8601](~~25696~~) standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC. |
|EventTime.End|String|No|2018-05-08T02:48:52Z|The end of the time range to query.

Specify the time in the [ISO 8601](~~25696~~) standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1. |
|PageSize|Integer|No|10|The number of entries to return on each page. Valid values: 1 to 100.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DiskFullStatusSet|Array of DiskFullStatusType| |The collection of full status information of the EBS devices. |
|DiskFullStatusType| | | |
|Device|String|null|The device name of the EBS device that is attached to an instance. Example: /dev/xvdb.

This parameter has a value only when the value of `Status` is `In_use`.

**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|DiskEventSet|Array of DiskEventType| |The events about the EBS device. |
|DiskEventType| | | |
|EventEndTime|String|2018-05-06T02:48:52Z|The time when the event ended. |
|EventId|String|e-bp67acfmxazb4p\*\*\*\*|The ID of the event. |
|EventTime|String|2018-05-08T02:43:10Z|The time when the event started. |
|EventType|Struct| |The event type. |
|Code|Integer|7|The code of the event type. |
|Name|String|Stalled|The name of the event type. Valid values:

-   Degraded: The performance of the EBS device was degraded.
-   SeverelyDegraded: The performance of the EBS device was severely degraded.
-   Stalled: The performance of the EBS device was severely affected.
-   ErrorDetected: The local disk was damaged. |
|ImpactLevel|String|100|The impact level of the event. |
|DiskId|String|d-bp67acfmxazb4p\*\*\*\*|The ID of the EBS device. |
|HealthStatus|Struct| |The health status of the EBS device. |
|Code|Integer|128|The code of the health status of the EBS device. |
|Name|String|Impaired|The name of the health status of the EBS device. |
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|Status|Struct| |The lifecycle status of the EBS device. |
|Code|Integer|129|The code of the lifecycle status of the EBS device. |
|Name|String|Available|The name of the lifecycle status of the EBS device. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|2|The total number of EBS devices for which full status information is returned. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeDisksFullStatus
&RegionId=cn-hangzhou
&DiskId.1=d-bp13pl2v34qj0xg0****
&EventId.1=e-uf64yvznlao4jl2c****
&Status=Available
&HealthStatus=Warning
&EventType=Stalled
&EventTime.Start=2018-05-06T02:43:10Z
&EventTime.End=2018-05-08T02:48:52Z
&PageNumber=1
&PageSize=10
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDisksFullStatusResponse>
      <DiskFullStatusSet>
            <DiskFullStatusType>
                  <DiskEventSet>
                        <DiskEventType>
                              <EventId>e-bp67acfmxazb4p****</EventId>
                              <EventType>
                                    <Code>7</Code>
                                    <Name>Stalled</Name>
                              </EventType>
                              <EventTime>2018-05-08T02:43:10Z</EventTime>
                        </DiskEventType>
                  </DiskEventSet>
                  <DiskId>d-bp67acfmxazb4p****</DiskId>
                  <InstanceId>i-bp67acfmxazb4p****</InstanceId>
                  <Device>/dev/xvda</Device>
                  <HealthStatus>
                        <Code>128</Code>
                        <Name>Impaired</Name>
                  </HealthStatus>
                  <Status>
                        <Code>129</Code>
                        <Name>Available</Name>
                  </Status>
            </DiskFullStatusType>
            <DiskFullStatusType>
                  <DiskEventSet>
                        <DiskEventType>
                              <EventId>e-bp67acfmxazb4p****</EventId>
                              <EventType>
                                    <Code>1</Code>
                                    <Name>Degraded</Name>
                              </EventType>
                              <EventTime>2018-05-06T02:43:10Z</EventTime>
                              <EventEndTime>2018-05-06T02:48:52Z</EventEndTime>
                        </DiskEventType>
                  </DiskEventSet>
                  <DiskId>d-disk2</DiskId>
                  <InstanceId>i-instance2</InstanceId>
                  <Device>/dev/xvdb</Device>
                  <HealthStatus>
                        <Code>64</Code>
                        <Name>Warning</Name>
                  </HealthStatus>
                  <Status>
                        <Code>0</Code>
                        <Name>Ok</Name>
                  </Status>
            </DiskFullStatusType>
      </DiskFullStatusSet>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <RequestId>1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211</RequestId>
      <TotalCount>2</TotalCount>
</DescribeDisksFullStatusResponse>
```

`JSON` format

```
{
    "DiskFullStatusSet": {
        "DiskFullStatusType": [
            {
                "DiskEventSet": {
                    "DiskEventType": [
                        {
                            "EventId": "e-bp67acfmxazb4p****",
                            "EventType": {
                                "Code": "7",
                                "Name": "Stalled"
                            },
                            "EventTime": "2018-05-08T02:43:10Z"
                        }
                    ]
                },
                "DiskId": "d-bp67acfmxazb4p****",
                "InstanceId": "i-bp67acfmxazb4p****",
                "Device": "/dev/xvda",
                "HealthStatus": {
                    "Code": 128,
                    "Name": "Impaired"
                },
                "Status": {
                    "Code": 129,
                    "Name": "Available"
                }
            },
            {
                "DiskEventSet": {
                    "DiskEventType": [
                        {
                            "EventId": "e-bp67acfmxazb4p****",
                            "EventType": {
                                "Code": "1",
                                "Name": "Degraded"
                            },
                            "EventTime": "2018-05-06T02:43:10Z",
                            "EventEndTime": "2018-05-06T02:48:52Z"
                        }
                    ]
                },
                "DiskId": "d-disk2",
                "InstanceId": "i-instance2",
                "Device": "/dev/xvdb",
                "HealthStatus": {
                    "Code": 0,
                    "Name": "Ok"
                },
                "Status": {
                    "Code": 129,
                    "Name": "Available"
                }
            }
        ]
    },
    "PageNumber": 1,
    "PageSize": 10,
    "RequestId": "1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211",
    "TotalCount": 2
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|403|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|403|DiskIdLimitExceeded|%s|The error message returned because more than 100 EBS device IDs are specified.|
|403|EventIdLimitExceeded|%s|The error message returned because more than 100 events are specified.|
|403|InvalidParameter.TimeEndBeforeStart|%s|The error message returned because the specified parameter is invalid. Check whether the end time is earlier than the start time.|
|403|OperationDenied.NotInWhiteList|%s|The error message returned because you are not authorized to perform this operation. Try again when you are in the whitelist.|
|403|TooManyDiskEvent.DiskIdRequired|%s|The error message returned because the system cannot process this number of requests for the specified resource. Try again later.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

