# DeleteNetworkInterface

You can call this operation to delete an elastic network interface \(ENI\).

## Description

-   The ENI must be in the Available state.
-   If the ENI is bound to an ECS instance, you must unbind the ENI from the ECS instance \([DetachNetworkInterface](~~58514~~)\) before you can delete the ENI.
-   After an ENI is deleted:
    -   The primary private IP address of the ENI is automatically released.
    -   The ENI is automatically removed from its security groups.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DeleteNetworkInterface&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteNetworkInterface|The operation that you want to perform. Set the value to DeleteNetworkInterface. |
|NetworkInterfaceId|String|Yes|eni-bp14v2sdd3v8htln\*\*\*\*|The ID of the ENI. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the ENI. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|F3CD6886-D8D0-4FEE-B93E-1B73239673DE|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DeleteNetworkInterface
&NetworkInterfaceId=eni-bp14v2sdd3v8htln****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteNetworkInterfaceResponse>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</DeleteNetworkInterfaceResponse>
```

`JSON` format

```
{
    "RequestId": "F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
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

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

