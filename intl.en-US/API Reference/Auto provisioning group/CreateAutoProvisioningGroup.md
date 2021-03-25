# CreateAutoProvisioningGroup

You can call this operation to create an auto provisioning group.

## Description

-   Auto Provisioning is a service that allows quick deployment of an instance cluster that consists of preemptible and pay-as-you-go instances. Auto Provisioning supports one-click deployment of instance clusters that are of specific billing methods and instance families across zones.
-   Auto Provisioning uses auto provisioning groups to schedule and maintain computing resources. You can use auto provisioning groups to provide stable computing power. This alleviates the instability problem caused by reclaiming preemptible instances.
-   Auto Provisioning is free to use. However, you are charged for instance resources created in auto provisioning groups. For more information about billing, see [Preemptible instances](~~52088~~) and [Pay-as-you-go](~~40653~~).
-   When you specify both the `LaunchTemplateId` and `LaunchConfiguration.*` parameters, the LaunchTemplateId parameter is preferentially used.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateAutoProvisioningGroup&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateAutoProvisioningGroup|The operation that you want to perform. Set the value to CreateAutoProvisioningGroup. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the auto provisioning group. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|TotalTargetCapacity|String|Yes|60|The total target capacity of the auto provisioning group. The value must be a positive integer.

The total target capacity of the auto provisioning group must be at least the sum of the target capacity of pay-as-you-go instances specified by the `PayAsYouGoTargetCapacity` parameter and the target capacity of preemptible instances specified by the `SpotTargetCapacity` parameter. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which to add the auto provisioning group. |
|AutoProvisioningGroupName|String|No|apg-test|The name of the auto provisioning group. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|AutoProvisioningGroupType|String|No|maintain|The delivery type of the auto provisioning group. Valid values:

-   request: one-time asynchronous delivery. After the auto provisioning group is started, the auto provisioning group attempts to deliver an instance cluster only once. If the cluster fails to be delivered, the group does not retry the operation.
-   instant: one-time synchronous delivery. The auto provisioning group creates instances on system startup and returns the list of created instances and the causes of creation failures in the response.
-   maintain: continuous delivery. After the auto provisioning group is started, the auto provisioning group continuously attempts to create and deliver an instance cluster. The auto provisioning group compares the real-time capacity and target capacity of the cluster. If the cluster does not meet the target capacity, the group creates instances till the cluster meets the expected capacity.

Default value: maintain. |
|SpotAllocationStrategy|String|No|diversified|The policy for creating preemptible instances. Valid values:

-   lowest-price: cost optimization policy. Auto Provisioning attempts to create instances of the lowest-priced instance type.
-   diversified: balanced distribution policy. Auto Provisioning attempts to create instances in zones that are specified by extended configurations and then distributes the instances across the zones.
-   capacity-optimized: capacity-optimized distribution policy. Auto Provisioning attempts to create instances that are of the optimal instance types and across the optimal zones based on the resource availability.

Default value: lowest-price. |
|SpotInstanceInterruptionBehavior|String|No|terminate|The action to take on the excess preemptible instances after the instances are stopped. Valid values:

-   stop: retains the instances in the stopped state.
-   terminate: releases the preemptible instances.

Default value: stop. |
|SpotInstancePoolsToUseCount|Integer|No|2|The number of preemptible instances of the lowest-priced instance type that Auto Provisioning creates. This parameter takes effect when the `SpotAllocationStrategy` parameter is set to `lowest-price`.

The parameter value must be less than N specified in the `LaunchTemplateConfig.N` parameter. |
|PayAsYouGoAllocationStrategy|String|No|prioritized|The policy for creating pay-as-you-go instances. Valid values:

-   lowest-price: cost optimization policy. Auto Provisioning attempts to create instances of the lowest-priced instance type.
-   prioritized: priority policy. Auto Provisioning attempts to create instances based on the priority specified by the `LaunchTemplateConfig.N.Priority` parameter.

Default value: lowest-price. |
|ExcessCapacityTerminationPolicy|String|No|termination|Specifies whether to stop excess preemptible instances when the target capacity of the auto provisioning group is exceeded. Valid values:

-   no-termination: continues to run excess preemptible instances.
-   termination: stops excess preemptible instances. The action to be taken on the stopped instances is specified by the `SpotInstanceInterruptionBehavior` parameter.

Default value: no-termination. |
|ValidFrom|String|No|2019-04-01T15:10:20Z|The time when to start the auto provisioning group. The period of time between this point in time and the point in time specified by the `ValidUntil` parameter is the effective time period of the auto provisioning group.

Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

By default, an auto provisioning group is immediately started after it is created. |
|ValidUntil|String|No|2019-06-01T15:10:20Z|The time when the auto provisioning group expires. The period of time between this point in time and the point in time specified by the `ValidFrom` parameter is the effective time period of the auto provisioning group.

Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

By default, an auto provisioning group is immediately started after it is created. |
|TerminateInstancesWithExpiration|Boolean|No|true|Specifies whether to stop preemptible instances when the auto provisioning group expires. Valid values:

-   true: stops preemptible instances. The action to be taken on the stopped instances is specified by the `SpotInstanceInterruptionBehavior` parameter.
-   false: continues to run preemptible instances.

Default value: false. |
|TerminateInstances|Boolean|No|true|Specifies whether to release instances in the auto provisioning group when the auto provisioning group is deleted.

Default value: false. |
|MaxSpotPrice|Float|No|2|The maximum price of preemptible instances in the auto provisioning group.

**Note:** When the `MaxSpotPrice` and `LaunchTemplateConfig.N.MaxPrice` parameters are both specified, the maximum price is the lower one of the two parameter values. |
|PayAsYouGoTargetCapacity|String|No|30|The target capacity of pay-as-you-go instances in the auto provisioning group. Valid values: The value of this parameter must be smaller than that of `TotalTargetCapacity`. |
|SpotTargetCapacity|String|No|20|The target capacity of preemptible instances in the auto provisioning group. Valid values: The value of this parameter must be smaller than that of `TotalTargetCapacity`. |
|DefaultTargetCapacityType|String|No|Spot|The billing method of the capacity difference when the sum value of the `PayAsYouGoTargetCapacity` and `SpotTargetCapacity` parameters is smaller than the value of the `TotalTargetCapacity` parameter. Valid values:

-   PayAsYouGo: pay-as-you-go instances.
-   Spot: preemptible instances.

Default value: Spot. |
|LaunchTemplateId|String|No|lt-bp1fgzds4bdogu03\*\*\*\*|The ID of the instance launch template associated with the auto provisioning group. You can call the [DescribeLaunchTemplates](~~73759~~) operation to query available instance launch templates. When you specify both this parameter and the `LaunchConfiguration.*` parameter, this parameter is preferentially used. |
|LaunchTemplateVersion|String|No|1|The version of the instance launch template associated with the auto provisioning group. You can call the [DescribeLaunchTemplateVersions](~~73761~~) operation to query the versions of available instance launch templates.

Default value: the default version of the instance launch template. |
|LaunchTemplateConfig.N.InstanceType|String|No|ecs.g5.large|The instance type of extended configuration N. Valid values of N: 1 to 20. For more information about valid values of this parameter, see [Instance families](~~25378~~). |
|LaunchTemplateConfig.N.MaxPrice|Double|No|3|The maximum price of preemptible instances in extended configuration N.

**Note:** If you specify the `LaunchTemplateConfig` parameter, you must also specify the `LaunchTemplateConfig.N.MaxPrice` parameter. |
|LaunchTemplateConfig.N.VSwitchId|String|No|vsw-sn5bsitu4lfzgc5o7\*\*\*\*|The ID of the vSwitch in extended configuration N. The zone of the ECS instances created from the extended configurations is determined by the vSwitch.

**Note:** If you specify the `LaunchTemplateConfig` parameter, you must also specify the `LaunchTemplateConfig.N.VSwitchId` parameter. |
|LaunchTemplateConfig.N.WeightedCapacity|Double|No|2|The weight of the instance type specified in extended configuration N. A greater weight indicates that a single instance has more computing power, and as a result fewer instances are required. The value of this parameter must be greater than 0.

The weight is calculated based on the computing power of the specified instance type and the minimum computing power of a single node of the cluster. For example, if the minimum computing power of a single node is 8 vCPUs and 60 GiB:

-   The weight of the instance type that has 8 vCPUs and 60 GiB can be set to 1.
-   The weight of the instance type that has 16 vCPUs and 120 GiB can be set to 2. |
|LaunchTemplateConfig.N.Priority|Integer|No|1|The priority of extended configuration N. A value of 0 indicates the highest priority. Valid values: 0 to ∞. |
|Description|String|No|testDescription|The description of the auto provisioning group. |
|ClientToken|String|No|0c593ea1-3bea-11e9-b96b-88e9fe637760|The client token that is used to guarantee the idempotence of the request. You can use the client to generate the value, and you must make sure that it is unique among different requests. Only ASCII characters are allowed. The token can contain up to 64 ASCII characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|LaunchConfiguration.ImageId|String|No|m-bp1g7004ksh0oeuc\*\*\*\*|The ID of the image. The image that you select when you create an instance. You can call the [DescribeImages](~~25534~~) operation to query available image resources. When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg\*\*\*\*|The ID of the security group to which the instance belongs. When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.IoOptimized|String|No|optimized|Specifies whether the instance is I/O optimized. Valid values:

-   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized.

For instances of phased-out instance types, the default value is none. For other instances, the default value is optimized.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.DataDisk.N.Size|Integer|No|20|The size of data disk N. Valid values of N: 1 to 16. Unit: GiB. Valid values:

-   Valid values when LaunchConfiguration.DataDisk.N.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when LaunchConfiguration.DataDisk.N.Category is set to cloud\_ssd: 20 to 32768
-   Valid values when LaunchConfiguration.DataDisk.N.Category is set to cloud\_essd: 20 to 32768
-   Valid values when LaunchConfiguration.DataDisk.N.Category is set to cloud: 5 to 2000

**Note:** The parameter value must be greater than or equal to the size of the snapshot specified by the `LaunchConfiguration.DataDisk.N.SnapshotId` parameter.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.DataDisk.N.Category|String|No|cloud\_ssd|The category of data disk N. Valid values of N: 1 to 16. Valid values:

-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\)
-   cloud: basic disk

For I/O optimized instances, the default value is cloud\_efficiency. For non-I/O optimized instances, the default value is cloud.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.DataDisk.N.PerformanceLevel|String|No|PL1|The performance level of the ESSD used as data disk N. The value of N must be the same as that of N in the `LaunchConfiguration.DataDisk.N.Category` parameter. Default value: PL1. Valid values:

-   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

For more information about ESSD performance levels, see [ESSDs](~~122389~~).

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.DataDisk.N.Device|String|No|/dev/vd1|The mount point of data disk N. When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.DataDisk.N.SnapshotId|String|No|s-bp17441ohwka0yuh\*\*\*\*|The ID of the snapshot used to create data disk N. Valid values of N: 1 to 16.

After this parameter is specified, the `LaunchConfiguration.DataDisk.N.Size` parameter is ignored. The size of data disk N is the same as that of the snapshot specified by this parameter. Use snapshots created after July 15, 2013. Otherwise, an error message is returned and your request is rejected.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.DataDisk.N.DeleteWithInstance|Boolean|No|true|Specifies whether to release data disk N when its attached instance is released. Valid values:

-   true: Data disk N is released together with the instance.
-   false: Data disk N is not released together with the instance.

Default value: true.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.DataDisk.N.Encrypted|Boolean|No|false|Specifies whether to encrypt data disk N. Valid values:

-   true: Data disk N is encrypted.
-   false: Data disk N is not encrypted.

Default value: false.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.DataDisk.N.KmsKeyId|String|No|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|The ID of the KMS key used by data disk N. When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.DataDisk.N.DiskName|String|No|cloud\_ssdData|The name of data disk N. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`. It can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).

This parameter is empty by default.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.DataDisk.N.Description|String|No|DataDisk\_Description|The description of data disk N. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.InternetChargeType|String|No|PayByTraffic|The billing method for network usage. Valid values:

-   PayByBandwidth
-   PayByTraffic

**Note:** When the pay-by-traffic billing method is used, the maximum inbound and outbound bandwidths are both the upper limits of bandwidths and for reference only. In the event of resource contention, these maximum bandwidths cannot be guaranteed. If you want guaranteed bandwidths for your instance, use the pay-by-bandwidth billing method.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.InternetMaxBandwidthIn|Integer|No|10|The maximum inbound public bandwidth. Unit: Mbit/s. Valid values:

-   If the purchased outbound public bandwidth is less than or equal to 10 Mbit/s, valid values of this parameter are 1 to 10, and the default value of this parameter is 10.
-   If the purchased outbound public bandwidth is greater than 10 Mbit/s, valid values of this parameter are 1 to the value of `LaunchConfiguration.InternetMaxBandwidthOut`, and the default value is the value of `LaunchConfiguration.InternetMaxBandwidthOut`.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.InternetMaxBandwidthOut|Integer|No|10|The maximum outbound public bandwidth. Unit: Mbit/s. Valid values: 0 to 100.

Default value: 0.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.InstanceName|String|No|k8s-node-\[1,4\]-alibabacloud|The name of the instance. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`. It can contain letters, digits, colons \(:\), underscores \(\_\), periods \(.\), and hyphens \(-\). The default value of this parameter is the `InstanceId` value.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.HostName|String|No|k8s-node-\[1,4\]-ecshost|The hostname of the instance.

-   The hostname cannot start or end with a period \(,\) or a hyphen \(-\). It cannot contain consecutive periods \(.\) or hyphens \(-\).
-   For a Windows instance, the hostname must be 2 to 15 characters in length and cannot contain periods \(.\) or contain only digits. It can contain letters, digits, and hyphens \(-\).
-   For instances that run other operating systems such as Linux, the hostname must be 2 to 64 characters in length. You can use periods \(.\) to separate the hostname into multiple segments. Each segment can contain letters, digits, and hyphens \(-\).

When you create multiple instances at a time, you can specify sequential hostnames. For more information, see [Specify sequential instance names or hostnames](~~196048~~).

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.InstanceDescription|String|No|Instance\_Description|The description of the instance. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.KeyPairName|String|No|KeyPair\_Name|The name of the key pair.

-   For Windows instances, this parameter is ignored This parameter is empty by default.
-   For Linux instances, the username and password authentication method is disabled by default.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.RamRoleName|String|No|RAM\_Name|The name of the RAM role. You can call the [ListRoles](~~28713~~) operation provided by RAM to query the RAM roles that you have created. When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.SecurityEnhancementStrategy|String|No|Active|Specifies whether to enable security hardening. Valid values:

-   Active: Security hardening is enabled. This value is applicable only to public images.
-   Deactive: Security hardening is disabled. This value is applicable to all image types.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.Tag.N.Key|String|No|TestKey|The key of tag N of the instance. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain `http://` or `https://`. When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.Tag.N.Value|String|No|TestValue|The value of tag N of the instance. Valid values of N: 1 to 20. The tag value can be an empty string. It can be up to 128 characters in length and cannot start with acs: or contain `http://` or `https://`. When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.UserData|String|No|ZWNobyBoZWxsbyBlY3Mh|The user data of the instance. User data must be encoded in Base64. The maximum size of raw data is 16 KB. When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.SystemDiskCategory|String|No|cloud\_ssd|The category of the system disk. Valid values:

-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: ESSD
-   cloud: basic disk

For non-I/O optimized instances of the phased-out instance types, the default value is cloud. For other instances, the default value is cloud\_efficiency.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.SystemDiskSize|Integer|No|40|The size of the system disk. Valid values: 20 to 500. Unit: GiB. The value of this parameter must be at least 20 and greater than or equal to the size of the image.

Default value: 40 or the size of the image, whichever is greater.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.SystemDiskName|String|No|cloud\_ssdSystem|The name of the system disk. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`. It can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).

This parameter is empty by default.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.SystemDiskDescription|String|No|SystemDisk\_Description|The description of the system disk. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.SystemDiskPerformanceLevel|String|No|PL0|The performance level of the ESSD used as the system disk. Default value: PL0. Valid values:

-   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

For more information about ESSD performance levels, see [ESSDs](~~122389~~).

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.PasswordInherit|Boolean|No|true|Specifies whether to use the password preset in the image. Valid values:

-   true: The preset password is used.
-   false: The preset password is not used.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which to assign the instance. When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|LaunchConfiguration.CreditSpecification|String|No|Standard|The performance mode of the burstable instance. Valid values:

-   Standard: the standard mode. For more information, see the "Standard mode" section of the [Burstable instances](~~59977~~) topic.
-   Unlimited: the unlimited mode. For more information, see the "Unlimited mode" section of the [Burstable instances](~~59977~~) topic.

This parameter is empty by default.

When both the LaunchTemplateId and LaunchConfiguration.\* parameters are specified, the LaunchTemplateId parameter is preferentially used. |
|SystemDiskConfig.N.DiskCategory|String|No|cloud\_ssd|Category N of the system disk. You can use this parameter to specify multiple disk categories and specify the priority order for each disk category. When a disk category is unavailable, the system changes the disk category. Valid values:

-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: ESSD
-   cloud: basic disk |
|DataDiskConfig.N.DiskCategory|String|No|cloud\_efficiency|Category N of the data disk. You can use this parameter to specify multiple disk categories and specify the priority order for each disk category. When a disk category is unavailable, the system changes the disk category. Valid values:

-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: ESSD
-   cloud: basic disk |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AutoProvisioningGroupId|String|apg-sn54avj8htgvtyh8\*\*\*\*|The ID of the auto provisioning group. |
|LaunchResults|Array of LaunchResult| |Details about instances in the auto provisioning group. This parameter value is returned only when the AutoProvisioningGroupType parameter is set to `instant`. |
|LaunchResult| | | |
|ErrorCode|String|InvalidParameter|The error code returned when the instance fails to be created. |
|ErrorMsg|String|Specific parameter is not valid.|The error message returned when the instance fails to be created. |
|InstanceIds|List|\["i-bp67acfmxazb4p\*\*\*\*"\]|The list of instances created. |
|InstanceType|String|ecs.g5.large|The instance type of the instance. |
|SpotStrategy|String|NoSpot|The preemption policy for the pay-as-you-go instance. Valid value:

-   NoSpot: The instance is created as a regular pay-as-you-go instance.
-   SpotWithPriceLimit: The instance is a preemptible instance that has a user-defined maximum hourly price.
-   SpotAsPriceGo: The instance is a preemptible instance whose price is based on the current market price. |
|ZoneId|String|cn-hangzhou-g|The zone ID of the instance. |
|RequestId|String|745CEC9F-0DD7-4451-9FE7-8B752F39\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateAutoProvisioningGroup
&LaunchTemplateId=lt-bp1fgzds4bdogu03****
&RegionId=cn-hangzhou
&TotalTargetCapacity=60
&SpotInstancePoolsToUseCount=2
&ExcessCapacityTerminationPolicy=termination
&TerminateInstancesWithExpiration=true
&TerminateInstances=false
&PayAsYouGoTargetCapacity=30
&SpotTargetCapacity=20
&DefaultTargetCapacityType=Spot
&LaunchTemplateConfig.1.InstanceType=ecs.g5.large
&LaunchTemplateConfig.1.MaxPrice=3
&LaunchTemplateConfig.1.VSwitchId=vsw-sn5bsitu4lfzgc5o7****
&LaunchTemplateConfig.1.WeightedCapacity=2
&LaunchTemplateConfig.1.Priority=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateAutoProvisioningGroupResponse>
    <CreateAutoProvisioningGroupId>apg-sn54avj8htgvtyh8****</CreateAutoProvisioningGroupId>
    <RequestId>745CEC9F-0DD7-4451-9FE7-8B752F39****</RequestId>
</CreateAutoProvisioningGroupResponse>
```

`JSON` format

```
{
    "CreateAutoProvisioningGroupId": "apg-sn54avj8htgvtyh8****",
    "RequestId": "745CEC9F-0DD7-4451-9FE7-8B752F39****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidFleetExcessCapacityTerminationPolicy.ValueNotSupported|The specified parameter "ExcessCapacityTerminationPolicy" is not supported.|The error message returned because the specified ExcessCapacityTerminationPolicy parameter is invalid.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|400|MissingParameter|%s|The error message returned because a required parameter is not specified.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

