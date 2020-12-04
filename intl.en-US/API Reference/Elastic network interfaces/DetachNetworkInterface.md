# DetachNetworkInterface

You can call this operation to unbind an elastic network interface \(ENI\) from an ECS instance.

## Description

When you call this operation, take note of the following items:

-   The primary ENIs of ECS instances cannot be unbound.
-   The ENI must be in the Detaching \(Detaching\) or InUse \(InUse\) state.
-   The instance must be in the Running \(Running\) or Stopped \(Stopped\) state.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DetachNetworkInterface&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DetachNetworkInterface|The operation that you want to perform. Set the value to DetachNetworkInterface. |
|InstanceId|String|Yes|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|NetworkInterfaceId|String|Yes|eni-bp67acfmxazb4p\*\*\*\*|The ID of the ENI. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the ENI. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DetachNetworkInterface
&InstanceId=i-bp67acfmxazb4p****
&NetworkInterfaceId=eni-bp67acfmxazb4p****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DetachNetworkInterfaceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachNetworkInterfaceResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|InvalidUserType.NotSupported|%s|The error message returned because your account does not support this operation.|
|403|Abs.InvalidAccount.NotFound|%s|The error message returned because your Alibaba Cloud account does not exist or your AccessKey pair has expired.|
|400|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|403|Forbidden.NotSupportRAM|%s|The error message returned because RAM users are not authorized to perform this operation.|
|400|UnsupportedParameter|%s|The error message returned because a specific parameter is not supported.|
|403|Forbidden.SubUser|%s|The error message returned because you are not authorized to manage this resource. Contact the owner of the Alibaba Cloud account for authorization.|
|400|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|400|InvalidInstanceID.Malformed|%s|The error message returned because the specified InstanceId parameter is invalid.|
|400|InvalidOperation.InvalidRegion|%s|The error message returned because the specified RegionId parameter is invalid.|
|400|InvalidOperation.InvalidEcsState|%s|The error message returned because the operation is not supported while the instance is in the current state.|
|400|InvalidOperation.InvalidEniState|%s|The error message returned because the operation is not supported while the ENI is in the current state.|
|400|InvalidOperation.DetachPrimaryEniNotAllowed|%s|The error message returned because you cannot unbind the primary ENI from the instance.|
|404|InvalidEcsId.NotFound|%s|The error message returned because the specified instance ID does not exist.|
|404|InvalidEniId.NotFound|%s|The error message returned because the specified NetworkInterfaceId parameter does not exist.|
|404|InvalidVSwitchId.NotFound|%s|The error message returned because the specified vSwitch ID does not exist.|
|404|InvalidSecurityGroupId.NotFound|%s|The error message returned when the specified security group ID does not exist.|
|403|MaxEniCountExceeded|%s|The error message returned because the maximum number of ENIs that can be managed has been reached.|
|403|EniPerInstanceLimitExceeded|%s|The error message returned because the maximum number of ENIs that can be bound to the specified instance has been reached.|
|403|InvalidOperation.AvailabilityZoneMismatch|%s|The error message returned because the operation is invalid.|
|403|InvalidOperation.VpcMismatch|%s|The error message returned because the operation is invalid. Check whether the VPC in the operation corresponds to other parameters.|
|403|SecurityGroupInstanceLimitExceed|%s|The error message returned because the maximum number of instances in the specified security group has been reached.|
|403|InvalidSecurityGroupId.NotVpc|%s|The error message returned because the specified SecurityGroupId parameter is invalid and the security group is not of the VPC type.|
|403|InvalidOperation.InvalidEniType|%s|The error message returned because the ENI type does not support this operation.|
|400|Forbidden.RegionId|%s|The error message returned because the service is unavailable in the current region.|
|400|InvalidParams.EniId|%s|The error message returned because the specified NetworkInterfaceId parameter is invalid.|
|403|InvalidOperation.EniServiceManaged|%s|The error message returned because the operation is invalid.|
|403|InvalidOperation.EniLinked|%s|The error message returned because the operation is not supported while the ENI is linked to another ENI. You must disassociate the EIP before you can unbind the EIP from an instance.|
|403|InvalidInstanceId.NotFound|%s|The error message returned because the specified InstanceId parameter does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

