# DescribeInstanceMonitorData

You can call this operation to query the monitoring data about an ECS instance. The returned monitoring data about an ECS instance includes the vCPU utilization, CPU credits of the burstable instance, received data traffic, sent data traffic, and average bandwidth.

## Description

When you call this operation, take note of the following items:

-   Up to 400 monitoring data entries can be returned at a time. An error is returned if the value calculated based on the formula of `(EndTime - StartTime)/Period` is greater than 400.
-   You can query the monitoring data of the last 30 days. If the value of StartTime is more than 30 days earlier than the current time, an error is returned.
-   A portion may be missing from the returned monitoring data. This is because the system cannot obtain the relevant information in some scenarios, such as when the instance is in the Stopped state.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceMonitorData&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInstanceMonitorData|The operation that you want to perform. Set the value to DescribeInstanceMonitorData. |
|InstanceId|String|Yes|i-bp1a36962lrhj4ab\*\*\*\*|The ID of the instance. |
|StartTime|String|Yes|2014-10-29T23:00:00Z|The beginning of the time range to query. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. If the value of seconds \(`ss`\) is not `00`, the time is rounded up to the next minute. |
|EndTime|String|Yes|2014-10-30T08:00:00Z|The end of the time range to query. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. If the value of seconds \(`ss`\) is not `00`, the time is rounded up to the next minute. |
|Period|Integer|No|60|The period in which to retrieve monitoring data. Unit: seconds. Valid values:

-   60
-   600
-   3600

Default value: 60. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|MonitorData|Array of InstanceMonitorData| |The collection of monitoring data about the instance. |
|InstanceMonitorData| | | |
|BPSRead|Integer|1000|The read bandwidth of the system disk. Unit: Byte/s. |
|BPSWrite|Integer|13585|The write bandwidth of the system disk. Unit: Byte/s. |
|CPU|Integer|2|The vCPU utilization of the instance. Unit: percent \(%\). |
|CPUAdvanceCreditBalance|Float|0.4|The overdrawn CPU credits of the burstable instance. |
|CPUCreditBalance|Float|120|The total CPU credits of the burstable instance. |
|CPUCreditUsage|Float|30|The number of CPU credits consumed by the burstable instance. |
|CPUNotpaidSurplusCreditUsage|Float|0.5|The unpaid excess credits. |
|IOPSRead|Integer|1000|The number of read I/O operations per second on the system disk. |
|IOPSWrite|Integer|200|The number of write I/O operations per second on the system disk. |
|InstanceId|String|i-bp1a36962lrhj4\*\*\*\*|The ID of the instance. |
|InternetBandwidth|Integer|10|The public bandwidth of the instance. Unit: Kbit/s. |
|InternetRX|Integer|122|The public data traffic received by the instance during the period specified by the Period parameter, which starts from the time specified by the TimeStamp parameter. Unit: Kbit/s. |
|InternetTX|Integer|343|The public data traffic sent by the instance during the period specified by the Period parameter, which starts from the time specified by the TimeStamp parameter. Unit: Kbit/s. |
|IntranetBandwidth|Integer|10|The internal bandwidth of the instance. Unit: Kbit/s. |
|IntranetRX|Integer|122|The internal data traffic received by the instance during the period specified by the Period parameter, which starts from the time specified by the TimeStamp parameter. Unit: Kbit/s. |
|IntranetTX|Integer|343|The internal data traffic sent by the instance during the period specified by the Period parameter, which starts from the time specified by the TimeStamp parameter. Unit: Kbit/s. |
|TimeStamp|String|2014-10-30T05:00:00Z|The timestamp of monitoring data query. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceMonitorData
&EndTime=2014-10-30T08:00:00Z
&InstanceId=i-bp1a36962lrhj4ab****
&StartTime=2014-10-29T23:00:00Z
&Period=3600
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeInstanceMonitorDataResponse>
      <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
      <MonitorData>
            <InstanceMonitorData>
                  <InstanceId>i-bp1a36962lrhj4ab****</InstanceId>
                  <CPU>2</CPU>
                  <IntranetRX>122</IntranetRX>
                  <IntranetTX>343</IntranetTX>
                  <IntranetFlow>675</IntranetFlow>
                  <IntranetBandwidth>10</IntranetBandwidth>
                  <InternetRX>122</InternetRX>
                  <InternetTX>343</InternetTX>
                  <InternetFlow>675</InternetFlow>
                  <InternetBandwidth>10</InternetBandwidth>
                  <IOPSRead>1000</IOPSRead>
                  <IOPSWrite>200</IOPSWrite>
                  <BPSRead>1000</BPSRead>
                  <BPSWrite>13585</BPSWrite>
                  <TimeStamp>2014-10-30T05:00:00Z</TimeStamp>
            </InstanceMonitorData>
      </MonitorData>
</DescribeInstanceMonitorDataResponse>
```

`JSON` format

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "MonitorData": {
        "InstanceMonitorData": [
            {
                "InstanceId": "i-bp1a36962lrhj4ab****",
                "CPU": 0,
                "IntranetRX": 122,
                "IntranetTX": 343,
                "IntranetFlow": 675,
                "IntranetBandwidth": 10,
                "InternetRX": 122,
                "InternetTX": 343,
                "InternetFlow": 675,
                "InternetBandwidth": 10,
                "IOPSRead": 1000,
                "IOPSWrite": 13585,
                "BPSRead": 1000,
                "BPSWrite": 200,
                "TimeStamp": "2014-10-30T05:00:00Z"
            }
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|400|InvalidStartTime.Malformed|The specified parameter "StartTime" is not valid.|The error message returned because the specified StartTime parameter is invalid.|
|400|InvalidEndTime.Malformed|The specified parameter "EndTime" is not valid.|The error message returned because the specified EndTime parameter is invalid.|
|400|InvalidPeriod.ValueNotSupported|The specified parameter "Period" is not valid.|The error message returned because the specified Period parameter is invalid.|
|400|InvalidStartTime.TooEarly|The specified parameter "StartTime" is too early.|The error message returned because the specified StartTime parameter is more than 30 days earlier than the current time.|
|400|InvalidParameter.TooManyDataQueried|Too many data queried.|The error message returned because the amount of queried monitoring data has reached the upper limit.|
|400|Throttling|Request was denied due to request throttling.|The error message returned because the request is denied due to throttling. Try again later.|
|400|InvalidStartTime.ValueNotSupported|The specified parameter StartTime is later than EndTime.|The error message returned because the specified EndTime value is earlier than the specified StartTime value.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

