# DescribeAutoProvisioningGroups

You can call this operation to query information of one or more auto provisioning groups.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeAutoProvisioningGroups&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAutoProvisioningGroups|The operation that you want to perform. Set the value to DescribeAutoProvisioningGroups. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the auto provisioning group. |
|AutoProvisioningGroupId.N|RepeatList|No|apg-sn54avj8htgvtyh8\*\*\*\*|The ID of auto provisioning group N. Valid values of N: 1 to 20. |
|AutoProvisioningGroupName|String|No|testAutoProvisioningGroupName|The name of the auto provisioning group. |
|PageSize|Integer|No|2|The number of entries to return on each page.

Maximum value: 100.

Default value: 10. |
|PageNumber|Integer|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1. |
|AutoProvisioningGroupStatus.N|RepeatList|No|active|The status of auto provisioning group N. Valid values:

-   submitted: The auto provisioning group is created and has not started to execute scheduling tasks.
-   active: The auto provisioning group is executing scheduling tasks.
-   deleted: The auto provisioning group is deleted.
-   delete-running: The auto provisioning group is being deleted.
-   modifying: The auto provisioning group is being modified. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AutoProvisioningGroups|Array of AutoProvisioningGroup| |Details about the auto provisioning groups. |
|AutoProvisioningGroup| | | |
|AutoProvisioningGroupId|String|apg-sn54avj8htgvtyh8\*\*\*\*|The ID of the auto provisioning group. |
|AutoProvisioningGroupName|String|EcsDocTest|The name of the auto provisioning group. |
|AutoProvisioningGroupType|String|maintain|The delivery type of the auto provisioning group. Valid values:

-   request: one-time delivery. After the auto provisioning group is started, it attempts to deliver an instance cluster once. If the cluster fails to be delivered, the group does not retry the operation.
-   maintain: continuous delivery. After the auto provisioning group is started, it continuously attempts to create and deliver an instance cluster. The auto provisioning group compares the real-time capacity and the target cluster capacity. If the cluster does not meet the target capacity, the group creates instances until the cluster meets the target capacity. |
|CreationTime|String|2019-04-01T15:10:20Z|The time when the auto provisioning group was created. |
|ExcessCapacityTerminationPolicy|String|termination|Indicates whether to stop excess preemptible instances when the target capacity of the auto provisioning group is exceeded. Valid values:

-   no-termination: continues to run excess preemptible instances.
-   termination: stops excess preemptible instances. The action to be performed on these stopped instances is specified by the SpotInstanceInterruptionBehavior parameter.

**Note:** The ExcessCapacityTerminationPolicy parameter is set when the auto provisioning group is created, and cannot be modified. For more information, see [CreateAutoProvisioningGroup](~~122738~~). |
|LaunchTemplateConfigs|Array of LaunchTemplateConfig| |Details about the extended configurations. |
|LaunchTemplateConfig| | | |
|InstanceType|String|ecs.g5.large|The instance type specified in the extended configuration. |
|MaxPrice|Float|3|The maximum price of the instance type specified in the extended configuration. |
|Priority|Float|1|The priority of the instance type specified in the extended configuration. A value of 0 indicates the highest priority. |
|VSwitchId|String|vsw-sn5bsitu4lfzgc5o7\*\*\*\*|The ID of the VSwitch specified in the extended configuration. |
|WeightedCapacity|Float|2|The weight of the instance type specified in the extended configuration. |
|LaunchTemplateId|String|lt-bp1fgzds4bdogu03\*\*\*\*|The ID of the launch template associated with the auto provisioning group. |
|LaunchTemplateVersion|String|1|The version of the launch template associated with the auto provisioning group. |
|MaxSpotPrice|Float|2|The maximum price for preemptible instances in the auto provisioning group.

**Note:** If both the MaxSpotPrice and LaunchTemplateConfig.N.MaxPrice parameters are specified, the maximum price is the lower value of the two parameters.

The LaunchTemplateConfig.N.MaxPrice parameter is set when the auto provisioning group is created, and cannot be modified. |
|PayAsYouGoOptions|Struct| |The policies related to pay-as-you-go instances. |
|AllocationStrategy|String|prioritized|The provisioning policy for pay-as-you-go instances. Valid values:

-   lowest-price: the cost optimization policy. This policy indicates that instance types of the lowest cost are used to create instances.
-   prioritized: the priority-based policy. This policy indicates that instances are created based on the priority specified by the LaunchTemplateConfig.N.Priority parameter.

**Note:** The LaunchTemplateConfig.N.Priority parameter is set when the auto provisioning group is created, and cannot be modified. |
|RegionId|String|cn-hangzhou|The region ID of the auto provisioning group. |
|SpotOptions|Struct| |The policy related to preemptible instances. |
|AllocationStrategy|String|diversified|The provisioning policy for preemptible instances. Valid values:

-   lowest-price: the cost optimization policy. This policy indicates that instance types of the lowest cost are used to create instances.
-   diversified: the distribution balancing policy. This policy indicates that instances are created evenly across multiple zones specified in the extended configuration. |
|InstanceInterruptionBehavior|String|stop|The action to be performed after the excess preemptible instances are stopped. Valid values:

-   stop: retains the excess preemptible instances in the stopped state.
-   terminate: releases the excess preemptible instances. |
|InstancePoolsToUseCount|Integer|2|The number of instances that the auto provisioning group used the instance type of the lowest cost to create.

**Note:** This parameter is set when the auto provisioning group is created, and cannot be modified. |
|State|String|fulfilled|The overall status of instance scheduling of the auto provisioning group. Valid values:

-   fulfilled: Scheduling is complete and the instance cluster is delivered.
-   pending-fulfillment: The instances are being created.
-   pending-termination: The instances are being removed.
-   error: An exception has occurred during scheduling and the instance cluster was not delivered. |
|Status|String|submitted|The status of the auto provisioning group. Valid values:

-   submitted: The auto provisioning group is created and has not started to execute scheduling tasks.
-   active: The auto provisioning group is executing scheduling tasks.
-   deleted: The auto provisioning group is deleted.
-   delete-running: The auto provisioning group is being deleted.
-   modifying: The auto provisioning group is being modified. |
|TargetCapacitySpecification|Struct| |The settings of the target capacity of the auto provisioning group. |
|DefaultTargetCapacityType|String|Spot|The type of supplemental instances. The target capacity of the auto provisioning group must be at least the sum of the capacity of pay-as-you-go instances specified by the PayAsYouGoTargetCapacity parameter and the capacity of preemptible instances specified by the SpotTargetCapacity parameter. Valid values:

-   PayAsYouGo: pay-as-you-go
-   Spot: preemptible instance |
|PayAsYouGoTargetCapacity|Float|30|The target capacity of pay-as-you-go instances in the auto provisioning group. |
|SpotTargetCapacity|Float|20|The target capacity of preemptible instances in the auto provisioning group. |
|TotalTargetCapacity|Float|60|The target capacity of the auto provisioning group. The capacity consists of the following three parts:

-   PayAsYouGoTargetCapacity
-   SpotTargetCapacity
-   The supplemental capacity besides instance capacities specified by the PayAsYouGoTargetCapacity and SpotTargetCapacity parameters |
|TerminateInstances|Boolean|false|Indicates whether instances are released together with the auto provisioning group to which the instances belong. |
|TerminateInstancesWithExpiration|Boolean|true|Indicates whether the preemptible instances are stopped when the auto provisioning group expires. Valid values:

-   true: The preemptible instances are stopped. The action to be performed on these stopped instances is specified by the SpotInstanceInterruptionBehavior parameter.
-   false: The preemptible instances continue to run.

**Note:** The SpotInstanceInterruptionBehavior parameter is set when the auto provisioning group is created, and cannot be modified. |
|ValidFrom|String|2019-04-01T15:10:20Z|The time when the auto provisioning group was started. The period of time between this point in time and the point in time specified by the `ValidUntil` parameter is the effective time period of the auto provisioning group. |
|ValidUntil|String|2019-06-01T15:10:20Z|The time when the auto provisioning group expires. The period of time between this point in time and the point in time specified by the `ValidFrom` parameter is the effective time period of the auto provisioning group. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|745CEC9F-0DD7-4451-9FE7-8B752F39\*\*\*\*|The ID of the request. |
|TotalCount|Integer|10|The number of queried auto provisioning groups. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeAutoProvisioningGroups
&AutoProvisioningGroupId.1=apg-sn54avj8htgvtyh8****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeAutoProvisioningGroups>
    <PageNumber>1</PageNumber>
    <TotalCount>1</TotalCount>
    <PageSize>10</PageSize>
    <RequestId>85331AC9-82C0-4604-9A14-048865BE****</RequestId>
    <AutoProvisioningGroups>
        <AutoProvisioningGroup>
            <TerminateInstancesWithExpiration>false</TerminateInstancesWithExpiration>
            <TerminateInstances>false</TerminateInstances>
            <ValidFrom>2019-06-17T15:22Z</ValidFrom>
            <AutoProvisioningGroupType>maintain</AutoProvisioningGroupType>
            <PayAsYouGoOptions>
                <AllocationStrategy>lowest-price</AllocationStrategy>
            </PayAsYouGoOptions>
            <AutoProvisioningGroupName>test61****</AutoProvisioningGroupName>
            <CreationTime></CreationTime>
            <ExcessCapacityTerminationPolicy>no-termination</ExcessCapacityTerminationPolicy>
            <Status>active</Status>
            <MaxSpotPrice>5</MaxSpotPrice>
            <LaunchTemplateVersion>1</LaunchTemplateVersion>
            <ValidUntil>2100-01-01T07:59Z</ValidUntil>
            <TargetCapacitySpecification>
                <SpotTargetCapacity>180</SpotTargetCapacity>
                <TotalTargetCapacity>300</TotalTargetCapacity>
                <PayAsYouGoTargetCapacity>120</PayAsYouGoTargetCapacity>
                <DefaultTargetCapacityType>PayAsYouGo</DefaultTargetCapacityType>
            </TargetCapacitySpecification>
            <State>fulfilled</State>
            <LaunchTemplateId>lt-uf657o6auob6aivd****</LaunchTemplateId>
            <RegionId>cn-shanghai</RegionId>
            <AutoProvisioningGroupId>apg-uf6c7pl7b30t4m98****</AutoProvisioningGroupId>
            <SpotOptions>
                <InstancePoolsToUseCount>1</InstancePoolsToUseCount>
                <InstanceInterruptionBehavior>terminate</InstanceInterruptionBehavior>
                <AllocationStrategy>lowest-price</AllocationStrategy>
            </SpotOptions>
            <LaunchTemplateConfigs>
                <LaunchTemplateConfig>
                    <MaxPrice>3</MaxPrice>
                    <WeightedCapacity>1</WeightedCapacity>
                    <VSwitchId>vsw-uf6qbjwokzl67uqqf****</VSwitchId>
                    <Priority>1</Priority>
                    <InstanceType>ecs.c5.xlarge</InstanceType>
                </LaunchTemplateConfig>
                <LaunchTemplateConfig>
                    <MaxPrice>2</MaxPrice>
                    <WeightedCapacity>2</WeightedCapacity>
                    <VSwitchId>vsw-uf6n6iy1ib39eqvph****</VSwitchId>
                    <Priority>1</Priority>
                    <InstanceType>ecs.g5.large</InstanceType>
                </LaunchTemplateConfig>
                <LaunchTemplateConfig>
                    <MaxPrice>1</MaxPrice>
                    <WeightedCapacity>3</WeightedCapacity>
                    <VSwitchId>vsw-uf6gs8uerj5osels4****</VSwitchId>
                    <Priority>1</Priority>
                    <InstanceType>ecs.hfc5.large</InstanceType>
                </LaunchTemplateConfig>
            </LaunchTemplateConfigs>
        </AutoProvisioningGroup>
    </AutoProvisioningGroups>
</DescribeAutoProvisioningGroups>
```

`JSON` format

```
{
    "PageNumber": 1,
    "TotalCount": 1,
    "PageSize": 10,
    "RequestId": "85331AC9-82C0-4604-9A14-048865BE****",
    "AutoProvisioningGroups": {
        "AutoProvisioningGroup": {
            "TerminateInstancesWithExpiration": false,
            "TerminateInstances": false,
            "ValidFrom": "2019-06-17T15:22Z",
            "AutoProvisioningGroupType": "maintain",
            "PayAsYouGoOptions": {
                "AllocationStrategy": "lowest-price"
            },
            "AutoProvisioningGroupName": "test61****",
            "CreationTime": "",
            "ExcessCapacityTerminationPolicy": "no-termination",
            "Status": "active",
            "MaxSpotPrice": 5,
            "LaunchTemplateVersion": 1,
            "ValidUntil": "2100-01-01T07:59Z",
            "TargetCapacitySpecification": {
                "SpotTargetCapacity": 180,
                "TotalTargetCapacity": 300,
                "PayAsYouGoTargetCapacity": 120,
                "DefaultTargetCapacityType": "PayAsYouGo"
            },
            "State": "fulfilled",
            "LaunchTemplateId": "lt-uf657o6auob6aivd****",
            "RegionId": "cn-shanghai",
            "AutoProvisioningGroupId": "apg-uf6c7pl7b30t4m98****",
            "SpotOptions": {
                "InstancePoolsToUseCount": 1,
                "InstanceInterruptionBehavior": "terminate",
                "AllocationStrategy": "lowest-price"
            },
            "LaunchTemplateConfigs": {
                "LaunchTemplateConfig": [
                    {
                        "MaxPrice": 3,
                        "WeightedCapacity": 1,
                        "VSwitchId": "vsw-uf6qbjwokzl67uqqf****",
                        "Priority": 1,
                        "InstanceType": "ecs.c5.xlarge"
                    },
                    {
                        "MaxPrice": 2,
                        "WeightedCapacity": 2,
                        "VSwitchId": "vsw-uf6n6iy1ib39eqvph****",
                        "Priority": 1,
                        "InstanceType": "ecs.g5.large"
                    },
                    {
                        "MaxPrice": 1,
                        "WeightedCapacity": 3,
                        "VSwitchId": "vsw-uf6gs8uerj5osels4****",
                        "Priority": 1,
                        "InstanceType": "ecs.hfc5.large"
                    }
                ]
            }
        }
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParamter.RegionId|The regionId should not be null.|The error message returned because the required RegionId parameter is not specified.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

