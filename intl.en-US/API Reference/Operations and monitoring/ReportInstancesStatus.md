# ReportInstancesStatus

You can call this operation to report the exception on one or more ECS instances. You can report the same exception on multiple ECS instances or the same exception on multiple disks of one ECS instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ReportInstancesStatus&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ReportInstancesStatus|The operation that you want to perform. Set the value to ReportInstancesStatus. |
|InstanceId.N|RepeatList|Yes|i-bp165p6xk2tmdhj0\*\*\*\*|The ID of ECS instance N. Valid values of N: 1 to 100. Specify multiple values in the repeated list format. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Description|String|Yes|The local disk is unavailable, the mount point is inaccessible, or files cannot be loaded.|The detailed description of the exception. |
|Reason|String|No|abnormal-local-disk|The reason why the exception occurs to the ECS instance. Valid values:

-   instance-hang: The instance is unavailable or cannot be connected.
-   instance-stuck-in-status: The instance is stuck in a state such as Starting or Stopping.
-   abnormal-network: The instance has a network exception.
-   abnormal-local-disk: A local disk attached to the instance has an exception.
-   abnormal-cloud-disk: A disk or a Shared Block Storage device attached to the instance has an exception.
-   others: other exception types. If the exception is not of the preceding types, you can set `Reason` to others and specify the `Description` parameter. |
|IssueCategory|String|No|hardware-cpu-error|The category of the exception. This parameter is applicable only to ECS bare metal instances. Valid values:

-   hardware-cpu-error: CPU failure
-   hardware-motherboard-error: motherboard failure
-   hardware-mem-error: memory failure
-   hardware-power-error: power failure
-   hardware-disk-error: disk failure
-   hardware-networkcard-error: network interface controller \(NIC\) failure
-   hardware-raidcard-error: SAS/RAID card failure
-   hardware-fan-error: fan failure
-   others: other failures |
|DiskId.N|RepeatList|No|d-bp1aeljlfad7x6u1\*\*\*\*|The ID of disk N that has the exception. If you are using an ECS bare metal instance, enter the serial number of the disk on the instance.

Valid values of N: 1 to 100. Specify multiple values in the repeated list format.

**Note:** When the value of the `Reason` parameter is `abnormal-local-disk` or `abnormal-cloud-disk`, or the value of the `IssueCategory` parameter is `hardware-disk-error`, you must specify this parameter. |
|Device.N|RepeatList|No|/dev/xvdb|The device name of disk N on an instance that has the exception. If you are using an ECS bare metal instance, enter the slot number of disk N on the instance.

Valid values of N: 1 to 100. Specify multiple values in the repeated list format.

**Note:** For ECS Bare Metal Instance Instance, when the value of the `Reason` parameter is `abnormal-local-disk` or `abnormal-cloud-disk`, or the value of the `IssueCategory` parameter is `hardware-disk-error`, you must specify this parameter. |
|StartTime|String|No|2017-11-30T06:32:31Z|The start time of the instance exception. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|EndTime|String|No|2017-11-31T06:32:31Z|The end time of the instance exception. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ReportInstancesStatus
&InstanceId.1=i-bp165p6xk2tmdhj0****
&Reason=abnormal-local-disk
&DiskId.1=d-bp1aeljlfad7x6u1****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ReportInstancesStatusResponse>
    <RequestId>4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D</RequestId>
</ReportInstancesStatusResponse>
```

`JSON` format

```
{
    "RequestId":"4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|403|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|403|InstanceIdLimitExceeded|%s|The error message returned because the value of N in the InstanceId.N parameter is greater than 100.|
|403|DiskIdLimitExceeded|%s|The error message returned because the value of N in the DiskId.N parameter is greater than 100.|
|403|InvalidInstanceId.NotFound|%s|The error message returned because the specified instance does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

