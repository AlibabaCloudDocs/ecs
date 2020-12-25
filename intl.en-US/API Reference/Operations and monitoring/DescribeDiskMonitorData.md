# DescribeDiskMonitorData

You can call this operation to query the monitoring data of a disk over a specific period of time.

## Description

The monitoring data includes read IOPS, write IOPS, read bandwidth \(byte/s\), write bandwidth \(byte/s\), read latency \(μs\), and write latency \(μs\) of the disk.

When you call this operation, take note of the following items:

-   You can query the monitoring data only of the disks that are in the In Use \(`In_Use`\) state. For more information, see [Basic cloud disk status table](~~25689~~).

**Note:** Some portion of information may be missing from the monitoring data. This is because the system cannot obtain the relevant information, for example, when the disk is not in the In Use \(`In_Use`\) state.

-   A maximum of 400 entries of data can be returned at a time. That means the value of the following formula cannot be greater than 400: `(EndTime-StartTime)/Period`.
-   You can query only the monitoring data within the past 30 days. That means the specified `StartTime` parameter cannot be 30 days later than the current time.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeDiskMonitorData&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDiskMonitorData|The operation that you want to perform. Set the value to DescribeDiskMonitorData. |
|DiskId|String|Yes|d-bp1bq5g3dxxo1x4o\*\*\*\*|The ID of the disk. |
|EndTime|String|Yes|2014-07-23T12:09:00Z|The end time of the time range to query. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. If the specified number of seconds \(ss\) is not 00, the time is automatically rounded up to the next minute. |
|StartTime|String|Yes|2014-07-23T12:07:00Z|The start time of the time range to query. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. If the specified number of seconds \(ss\) is not 00, the time is automatically rounded up to the next minute. |
|Period|Integer|No|60|The interval at which to retrieve monitoring data. Unit: seconds. Valid values:

-   60
-   600
-   3600

Default value: 60. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|MonitorData|Array of DiskMonitorData| |Details about the disk monitoring data. |
|DiskMonitorData| | | |
|BPSRead|Integer|0|The read bandwidth of the system disk. Unit: Byte/s. |
|BPSTotal|Integer|204|The total read and write bandwidth of the system disk. Unit: Byte/s. |
|BPSWrite|Integer|204|The write bandwidth of the system disk. Unit: Byte/s. |
|DiskId|String|d-bp1bq5g3dxxo1x4o\*\*\*\*|The ID of the disk. |
|IOPSRead|Integer|0|The number of read I/O operations per second on the system disk. |
|IOPSTotal|Integer|0|The total number of read and write I/O operations per second on the system disk. |
|IOPSWrite|Integer|0|The number of write I/O operations per second on the system disk. |
|LatencyRead|Integer|0|The read latency of the disk. Unit: μs. |
|LatencyWrite|Integer|0|The write latency of the disk. Unit: μs. |
|TimeStamp|String|2014-07-23T12:07:00Z|The timestamp of monitoring data query. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|3|The total number of returned monitoring data entries. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeDiskMonitorData
&DiskId=d-bp1bq5g3dxxo1x4o****
&EndTime=2014-07-23T12:09:00Z
&StartTime=2014-07-23T12:07:00Z
&Period=60
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDiskMonitorDataResponse>
          <MonitorData>
                    <DiskMonitorData>
                              <BPSRead>0</BPSRead>
                              <BPSTotal>0</BPSTotal>
                              <BPSWrite>0</BPSWrite>
                              <DiskId>d-bp1bq5g3dxxo1x4o****</DiskId>
                              <IOPSRead>0</IOPSRead>
                              <IOPSTotal>0</IOPSTotal>
                              <IOPSWrite>0</IOPSWrite>
                              <TimeStamp>2014-07-23T12:07:00Z</TimeStamp>
                    </DiskMonitorData>
                    <DiskMonitorData>
                              <BPSRead>0</BPSRead>
                              <BPSTotal>204</BPSTotal>
                              <BPSWrite>204</BPSWrite>
                              <DiskId>d-bp1bq5g3dxxo1x4o****</DiskId>
                              <IOPSRead>0</IOPSRead>
                              <IOPSTotal>0</IOPSTotal>
                              <IOPSWrite>0</IOPSWrite>
                              <TimeStamp>2014-07-23T12:08:00Z</TimeStamp>
                    </DiskMonitorData>
                    <DiskMonitorData>
                              <BPSRead>0</BPSRead>
                              <BPSTotal>819</BPSTotal>
                              <BPSWrite>819</BPSWrite>
                              <DiskId>d-bp1bq5g3dxxo1x4o****</DiskId>
                              <IOPSRead>0</IOPSRead>
                              <IOPSTotal>0</IOPSTotal>
                              <IOPSWrite>0</IOPSWrite>
                              <TimeStamp>2014-07-23T12:09:00Z</TimeStamp>
                    </DiskMonitorData>
          </MonitorData>
          <RequestId>BF666447-B171-4076-BCBA-48437C18FD76</RequestId>
          <TotalCount>3</TotalCount>
</DescribeDiskMonitorDataResponse>
```

`JSON` format

```
{
    "MonitorData": {
        "DiskMonitorData": [
            {
                "BPSRead": 0,
                "BPSTotal": 0,
                "BPSWrite": 0,
                "DiskId": "d-bp1bq5g3dxxo1x4o****",
                "IOPSRead": 0,
                "IOPSTotal": 0,
                "IOPSWrite": 0,
                "TimeStamp": "2014-07-23T12:07:00Z"
            },
            {
                "BPSRead": 0,
                "BPSTotal": 204,
                "BPSWrite": 204,
                "DiskId": "d-bp1bq5g3dxxo1x4o****",
                "IOPSRead": 0,
                "IOPSTotal": 0,
                "IOPSWrite": 0,
                "TimeStamp": "2014-07-23T12:08:00Z"
            },
            {
                "BPSRead": 0,
                "BPSTotal": 819,
                "BPSWrite": 819,
                "DiskId": "d-bp1bq5g3dxxo1x4o****",
                "IOPSRead": 0,
                "IOPSTotal": 0,
                "IOPSWrite": 0,
                "TimeStamp": "2014-07-23T12:09:00Z"
            }
        ]
    },
    "RequestId": "A48A0A77-34F5-4C33-9066-9E8D2DA0D8E2",
    "TotalCount": 3
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDiskId.NotFound|The DiskId provided does not exist in our records.|The error message returned because the specified DiskId parameter does not exist. Check whether the disk ID is correct.|
|400|InvalidStartTime.Malformed|The specified parameter "StartTime" is not valid.|The error message returned because the specified StartTime parameter is invalid.|
|400|InvalidEndTime.Malformed|The specified parameter "EndTime" is not valid.|The error message returned because the specified EndTime parameter is invalid.|
|400|InvalidPeriod.ValueNotSupported|The specified parameter "Period" is not valid.|The error message returned because the specified Period parameter is invalid.|
|400|InvalidStartTime.TooEarly|The specified parameter "StartTime" is too early.|The error message returned because the specified StartTime value is earlier than the valid range of time.|
|400|InvalidParameter.TooManyDataQueried|Too many data queried.|The error message returned because the maximum amount of queried monitoring data has been reached.|
|400|Throttling|Request was denied due to request throttling.|The error message returned because the request is denied due to throttling. Try again later.|
|400|InvalidInstanceType.NotSupportCredit|The InstanceType of the specified instance does not support credit.|The error message returned because burstable instances are not supported.|
|400|InvalidParameter.EndTime|The specified parameter EndTime is earlier than StartTime.|The error message returned because the end time is earlier than the start time.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

