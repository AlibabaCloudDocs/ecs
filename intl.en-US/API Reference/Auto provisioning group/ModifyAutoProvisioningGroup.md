# ModifyAutoProvisioningGroup

You can call this operation to modify the configurations of an auto provisioning group.

## Description

Before you call this operation, take note of the following items:

-   If you modify the capacity or capacity-related settings of an auto provisioning group, the group executes the scheduling task once after the group is modified.
-   You cannot modify an auto provisioning group when the group is being deleted.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyAutoProvisioningGroup&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyAutoProvisioningGroup|The operation that you want to perform. Set the value to ModifyAutoProvisioningGroup. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the auto provisioning group. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|AutoProvisioningGroupId|String|No|apg-bp67acfmxazb4ph\*\*\*\*|The ID of the auto provisioning group. |
|ExcessCapacityTerminationPolicy|String|No|no-termination|Specifies whether to release scaled-in instances when the real-time capacity of the auto provisioning group exceeds the target capacity and the group is triggered to scale in. Valid values:

 -   termination: releases the scaled-in instances.
-   no-termination: removes the scaled-in instances from the auto provisioning group but not releases the instances. |
|DefaultTargetCapacityType|String|No|Spot|The billing method of supplemental instances. The target capacity of the auto provisioning group must be at least the sum of the capacity of pay-as-you-go instances specified by the PayAsYouGoTargetCapacity parameter and the capacity of preemptible instances specified by the SpotTargetCapacity parameter. Valid values:

 -   PayAsYouGo: pay-as-you-go
-   Spot: preemptible instance |
|TerminateInstancesWithExpiration|Boolean|No|false|Specifies whether to release instances in the auto provisioning group when the auto provisioning group expires. Valid values:

 -   true: releases instances in the auto provisioning group.
-   false: removes the instances in the group from the auto provisioning group but not releases the instances. |
|MaxSpotPrice|Float|No|0.5|The maximum price of preemptible instances in the auto provisioning group.

 **Note:** If both the MaxSpotPrice and LaunchTemplateConfig.N.MaxPrice parameters are specified, the maximum price is the lower value of the two parameters. The LaunchTemplateConfig.N.MaxPrice parameter is set when the auto provisioning group is created, and cannot be modified. |
|TotalTargetCapacity|String|No|70|The target capacity of the auto provisioning group. The parameter value is a positive integer.

 The target capacity of the auto provisioning group must be at least the sum of the capacity of pay-as-you-go instances specified by the PayAsYouGoTargetCapacity parameter and the capacity of preemptible instances specified by the SpotTargetCapacity parameter. |
|PayAsYouGoTargetCapacity|String|No|30|The target capacity of pay-as-you-go instances in the auto provisioning group. Valid values: Set this parameter to a value smaller than the TotalTargetCapacity value. |
|SpotTargetCapacity|String|No|30|The target capacity of preemptible instances in the auto provisioning group. Valid values: Set this parameter to a value smaller than the TotalTargetCapacity value. |
|AutoProvisioningGroupName|String|No|apg-test|The name of the auto provisioning group. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. The name can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|LaunchTemplateConfig.N.InstanceType|String|No|ecs.g5.large|The instance type of extended configuration N. Valid values of N: 1 to 20. For more information about valid values of this parameter, see [Instance families](~~25378~~). |
|LaunchTemplateConfig.N.MaxPrice|Double|No|3|The maximum price of preemptible instances in extended configuration N. |
|LaunchTemplateConfig.N.VSwitchId|String|No|vsw-sn5bsitu4lfzgc5o7\*\*\*\*|The ID of the vSwitch in extended configuration N. The zone of the ECS instances created from the extended configurations is determined by the vSwitch. |
|LaunchTemplateConfig.N.WeightedCapacity|Double|No|2|The weight of the instance type specified in extended configuration N. A greater weight indicates that a single instance has more computing power, and as a result fewer instances are required. This parameter value must be greater than 0.

 The weight is calculated based on the computing power of the specified instance type and the minimum computing power of a single node of the cluster. For example, if the minimum computing power of a single node is 8 vCPUs and 60 GiB:

 -   The weight of the instance type with 8 vCPUs and 60 GiB can be set to 1.
-   The weight of the instance type with 16 vCPUs and 120 GiB can be set to 2. |
|LaunchTemplateConfig.N.Priority|Integer|No|1|The priority of extended configuration N. A value of 0 indicates the highest priority. This parameter value must be greater than 0. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://ecs.aliyuncs.com/?Action=ModifyAutoProvisioningGroup
&RegionId=cn-hangzhou
&AutoProvisioningGroupId=apg-bp67acfmxazb4ph****
&TotalTargetCapacity=70
&MaxSpotPrice=0.5
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyAutoProvisioningGroupResponse>
    <RequestId>928E2273-5715-46B9-A730-238DC996****</RequestId>
</ModifyAutoProvisioningGroupResponse>
```

`JSON` format

```
{
    "RequestId": "B48A12CD-1295-4A38-A8F0-0E92C937****"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|The error message returned because you are not authorized to manage this resource, or this API operation does not support RAM roles.|
|400|OperationDenied|%s|The error message returned because the operation is denied.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

