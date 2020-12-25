# DescribeEniMonitorData

You can call this operation to query all monitoring data about traffic on a secondary elastic network interface \(ENI\) over a specific period of time.

## Description

The monitoring data includes traffic sent and received over the internal network, the number of packets sent and received by the secondary ENI, and the number of dropped packets sent and received by the secondary ENI. A portion may be missing from the returned monitoring data. This is because the system cannot obtain the relevant information. For example, if the instance to which the secondary ENI is bound is in the Stopped state, or if the secondary ENI is not bound to an instance and is in the Available state, monitoring data about traffic on the ENI cannot be obtained. When you call this operation, take note of the following items:

-   Up to 400 monitoring data entries can be returned at a time. An error is returned if the value calculated based on the following formula is greater than 400: \(EndTime − StartTime\)/Period.
-   You can only query the monitoring data within the past 30 days. If the value of the StartTime parameter is earlier than 30 days from the time when you call this operation, an error is returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeEniMonitorData&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeEniMonitorData|The operation that you want to perform. Set the value to DescribeEniMonitorData. |
|EndTime|String|Yes|2018-05-21T12:22:00Z|The end time of the retrieved data. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. If the specified value of seconds \(ss\) is not 00, the time is rounded up to the next minute. |
|InstanceId|String|Yes|i-bp1a5zr3u7nq9cx\*\*\*\*|The ID of the instance to which the secondary ENI is bound. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|StartTime|String|Yes|2018-05-21T12:19:00Z|The start time of the retrieved data. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. If the specified value of seconds \(ss\) is not 00, the time is rounded up to the next minute. |
|EniId|String|No|eni-bp19da36d6xdwey\*\*\*\*|The ID of the secondary ENI. By default, all secondary ENIs that are bound to the specified instance are queried. |
|Period|Integer|No|60|The interval at which to retrieve monitoring data. Unit: seconds. Valid values:

-   60
-   600
-   3600

Default value: 60. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|MonitorData|Array of EniMonitorData| |Details about the ENI monitoring data. |
|EniMonitorData| | | |
|DropPacketRx|String|0|The discarded intranet data packets received by the secondary ENI. Unit: packets. |
|DropPacketTx|String|0|The discarded intranet data packets sent by the secondary ENI. Unit: packets. |
|EniId|String|eni-bp19da36d6xdwey\*\*\*\*|The ID of the secondary ENI. |
|IntranetRx|String|0|The internal data traffic received by the secondary ENI. Unit: Kbit/s. |
|IntranetTx|String|0|The internal data traffic sent by the secondary ENI. Unit: Kbit/s. |
|PacketRx|String|0|The intranet data traffic packets received by the secondary ENI. Unit: packets. |
|PacketTx|String|0|The intranet data packets sent by the secondary ENI. Unit: packets. |
|TimeStamp|String|2018-05-21T03:22:00Z|The timestamp of the monitoring data. The time follows the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|4|The total number of returned entries. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeEniMonitorData
&EndTime=2018-05-21T12:22:00Z
&InstanceId=i-bp1a5zr3u7nq9cx****
&RegionId=cn-hangzhou
&StartTime=2018-05-21T12:19:00Z
&EniId=eni-bp19da36d6xdwey****
&Period=60
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeEniMonitorDataResponse>
      <RequestId>5A03C2BA-3BCE-4A87-8076-7DC1629</RequestId>
      <MonitorData>
            <EniMonitorData>
                  <PacketTx>0</PacketTx>
                  <TimeStamp>2018-05-21T03:22:00Z</TimeStamp>
                  <IntranetOut>0</IntranetOut>
                  <DropPacketRx>0</DropPacketRx>
                  <IntranetIn>0</IntranetIn>
                  <EniId>eni-bp19da36d6xdwey4****</EniId>
                  <DropPacketTx>0</DropPacketTx>
                  <PacketRx>0</PacketRx>
            </EniMonitorData>
            <EniMonitorData>
                  <PacketTx>0</PacketTx>
                  <TimeStamp>2018-05-21T03:21:00Z</TimeStamp>
                  <IntranetOut>0</IntranetOut>
                  <DropPacketRx>0</DropPacketRx>
                  <IntranetIn>0</IntranetIn>
                  <EniId>eni-bp19da36d6xdwey3****</EniId>
                  <DropPacketTx>0</DropPacketTx>
                  <PacketRx>0</PacketRx>
            </EniMonitorData>
            <EniMonitorData>
                  <PacketTx>52240</PacketTx>
                  <TimeStamp>2018-05-21T03:19:00Z</TimeStamp>
                  <IntranetOut>73344</IntranetOut>
                  <DropPacketRx>0</DropPacketRx>
                  <IntranetIn>467</IntranetIn>
                  <EniId>eni-bp19da36d6xdwey2****</EniId>
                  <DropPacketTx>0</DropPacketTx>
                  <PacketRx>6603</PacketRx>
            </EniMonitorData>
            <EniMonitorData>
                  <PacketTx>34925</PacketTx>
                  <TimeStamp>2018-05-21T03:20:00Z</TimeStamp>
                  <IntranetOut>48871</IntranetOut>
                  <DropPacketRx>0</DropPacketRx>
                  <IntranetIn>350</IntranetIn>
                  <EniId>eni-bp19da36d6xdwey1****</EniId>
                  <DropPacketTx>0</DropPacketTx>
                  <PacketRx>4888</PacketRx>
            </EniMonitorData>
      </MonitorData>
</DescribeEniMonitorDataResponse>
```

`JSON` format

```
{
 "RequestId":"5A03C2BA-3BCE-4A87-8076-7DC1629",
 "MonitorData":{
     "EniMonitorData":[
         {
             "PacketTx":0,
             "TimeStamp":"2018-05-21T03:22:00Z",
             "IntranetOut":0,
             "DropPacketRx":0,
             "IntranetIn":0,
             "EniId":"eni-bp19da36d6xdwey4****",
             "DropPacketTx":0,
             "PacketRx":0
         },
         {
             "PacketTx":0,
             "TimeStamp":"2018-05-21T03:21:00Z",
             "IntranetOut":0,
             "DropPacketRx":0,
             "IntranetIn":0,
             "EniId":"eni-bp19da36d6xdwey3****",
             "DropPacketTx":0,
             "PacketRx":0
         },
         {
             "PacketTx":52240,
             "TimeStamp":"2018-05-21T03:19:00Z",
             "IntranetOut":73344,
             "DropPacketRx":0,
             "IntranetIn":467,
             "EniId":"eni-bp19da36d6xdwey2****",
             "DropPacketTx":0,
             "PacketRx":6603
         },
         {
             "PacketTx":34925,
             "TimeStamp":"2018-05-21T03:20:00Z",
             "IntranetOut":48871,
             "DropPacketRx":0,
             "IntranetIn":350,
             "EniId":"eni-bp19da36d6xdwey1****",
             "DropPacketTx":0,
             "PacketRx":4888
         }
     ]
 }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDiskId.NotFound|The DiskId provided does not exist in our records.|The error message returned because the specified DiskId parameter does not exist. Check whether the disk ID is correct.|
|403|InvalidStartTime.Malformed|The specified parameter "StartTime" is not valid.|The error message returned because the specified StartTime parameter is invalid.|
|403|InvalidEndTime.Malformed|The specified parameter "EndTime" is not valid.|The error message returned because the specified EndTime parameter is invalid.|
|403|InvalidPeriod.ValueNotSupported|The specified parameter "Period" is not valid.|The error message returned because the specified Period parameter is invalid.|
|403|InvalidStartTime.TooEarly|The specified parameter "StartTime" is too early.|The error message returned because the specified StartTime value is earlier than the valid range of time.|
|403|InvalidParameter.TooManyDataQueried|Too many data queried.|The error message returned because the maximum amount of queried monitoring data has been reached.|
|403|Throttling|Request was denied due to request throttling.|The error message returned because the request is denied due to throttling. Try again later.|
|403|InvalidInstanceType.NotSupportCredit|The InstanceType of the specified instance does not support credit.|The error message returned because burstable instances are not supported.|
|403|InvalidParameter.EndTime|The specified parameter EndTime is earlier than StartTime.|The error message returned because the end time is earlier than the start time.|
|4003|InvalidParam.Malformed|The specified parameter "EniId" and "InstanceId" are not valid|The error message returned because the specified EniId and InstanceId parameters are invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

