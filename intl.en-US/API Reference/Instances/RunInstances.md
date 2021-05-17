# RunInstances

You can call this operation to create one or more pay-as-you-go or subscription Elastic Compute Service \(ECS\) instances.

## Description

-   **Preparations**:
    -   Cost estimation: Learn about the billing methods of ECS resources. For more information, see [Billing overview](~~25398~~).
    -   Selection of instance types: Call the [DescribeInstanceTypes](~~25620~~) operation to query the performance data of instance types. You can also see [Best practices for instance type selection](~~58291~~) to learn how to select instance types.
    -   Query of available resources: Call the [DescribeAvailableResource](~~66186~~) operation to query available resources in a specific region or zone.
    -   Network planning: Create security groups. For more information, see [CreateSecurityGroup](~~25553~~). Before you create a VPC-type instance, create a VPC in the region where you want to create the instance. For more information, see [Create a VPC](~~65430~~).
-   **Precautions**:
    -   You can create a maximum of 100 instances at a time.
    -   You can use the `AutoReleaseTime` parameter to set the time when the instances are automatically released.
    -   After instances are created, the system returns the IDs of the created instances. You can call the [DescribeInstances](~~25506~~) operation to check the status of the instances.
    -   By default, instances automatically start after they are created. Instances are ready for use when they are in the Running \(`Running`\) state.
    -   Starting from November 27, 2020, the maximum bandwidth value available for you to create ECS instances or change the configurations of ECS instances is subject to the throttling policy within your account. To increase the maximum bandwidth value, submit a ticket. The throttling policy includes the following requirements: Within a single region, the total maximum bandwidth value of all instances whose billing method for network usage is pay-by-traffic cannot not exceed 5 Gbit/s and that of all instances whose billing method for network usage is pay-by-bandwidth cannot exceed 50 Gbit/s.
    -   Different from the [CreateInstance](~~25499~~) operation, the `RunInstances` operation enables the system to assign public IP addresses to the new instances if you set the `InternetMaxBandwidthOut` parameter to a value greater than 0.
    -   After you call this operation, an error is returned if a parameter is invalid or if available resources are insufficient. For more information, see the "Error codes" section of this topic.

**Note:** If the `QuotaExceed.ElasticQuota` error is returned when you create ECS instances, the maximum number of instances of the specified instance type that can be created in the current region or the maximum number of vCPUs for all instance types has been reached. You can go to the [ECS console](https://ecs.console.aliyun.com/?spm=a2c8b.12215451.favorites.decs.5e3a336aMGTtzy#/privileges/quota) or [Quota Center](https://quotas.console.aliyun.com/products/ecs/quotas) to request a quota increase.

-   **Best practices**:
    -   We recommend that you use auto provisioning groups in the following scenarios: resources are insufficient to create more than 100 instances at a time, you want to create instances in a quick manner and have no specific requirements on resource configurations such as instance types or zones, and you focus on the number of vCPUs and have no specific requirements on the instance quantity. You can call the [CreateAutoProvisioningGroup](~~122738~~) operation to create an auto provisioning group to deploy an instance cluster across different billing methods, instance families, and zones. For more information, see [Use auto provisioning group-related API operations to create multiple ECS instances at the same time](~~200772~~).
    -   The `RunInstances` operation allows you to create multiple instances at a time. To better manage and search for these instances, we recommend that you specify tags for the instances by using the `Tag.N.Key` and `Tag.N.Value` parameters. You can also append incremental suffixes specified by the `UniqueSuffix` parameter to the hostnames specified by the `HostName` parameter and instance names specified by the `InstanceName` parameter.
    -   A launch template contains parameters required to create an instance so that you do not have to specify these parameters every time you create an instance. You can call the [CreateLaunchTemplate](~~74686~~) operation to create a launch template. Then, in your request to call the `RunInstances` operation, specify the `LaunchTemplateId` and `LaunchTemplateVersion` parameters to use the launch template.
    -   When you create an instance in the [ECS console](https://ecs.console.aliyun.com/), you can view the best practices for calling the `RunInstances` operation. In the Preview step, click View Open API in the Configurations Selected section. In the dialog box that appears, the left-side **API Workflow** section shows the operations and request parameters that are related to the `RunInstances` operation. The right-side section shows the SDK examples in the **Java** and **Python** programming languages.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=RunInstances&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RunInstances|The operation that you want to perform. Set the value to RunInstances. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region in which to create the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ImageId|String|No|aliyun\_2\_1903\_x64\_20G\_alibase\_20200324.vhd|The ID of the image used to create the instance. You can call the [DescribeImages](~~25534~~) operation to query the available images. If you do not use the `LaunchTemplateId` or `LaunchTemplateName` parameter to specify an instance launch template, or if you do not set the `ImageFamily` parameter to obtain the latest available custom image within the specified image family, you must specify the `ImageId` parameter. |
|ImageFamily|String|No|hangzhou-daily-update|The name of the image family. You can set this parameter to obtain the latest available custom image within the specified image family to create instances.

 -   If you set the `ImageId` parameter, you cannot set the ImageFamily parameter.
-   If you do not set the `ImageId` parameter, but you set the `ImageId` parameter in the launch template specified by the `LaunchTemplateId` or `LaunchTemplateName` parameter, you cannot set the ImageFamily parameter.
-   If you do not set the `ImageId` parameter, and do not set the `ImageId` parameter in the launch template specified by the `LaunchTemplateId` or `LaunchTemplateName` parameter, you can set the ImageFamily parameter.
-   If you do not set the `ImageId` parameter, or do not set the `LaunchTemplateId` or `LaunchTemplateName` parameter, you can set the ImageFamily parameter. |
|InstanceType|String|No|ecs.g6.large|The instance type. If you do not set `LaunchTemplateId` or `LaunchTemplateName` to specify a launch template, you must set the `InstanceType` parameter.

 -   Selection of instance types: See [Instance families](~~25378~~) or call the [DescribeInstanceTypes](~~25620~~) operation to query the performance data of instance types, or see [Best practices for instance type selection](~~58291~~) to learn how to select instance types.
-   Query of available resources: Call the [DescribeAvailableResource](~~66186~~) operation to query available resources in a specific region or zone. |
|SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg7\*\*\*\*|The ID of the security group to which to assign the instance. Instances in the same security group can communicate with each other. The number of instances that a security group can contain depends on the type of the security group. For more information, see the "Security group limits" section of the [Limits](~~25412~~) topic.

 **Note:** The SecurityGroupId parameter determines the network type of instances in the security group. For example, a security group of the VPC type can contain only VPC-type instances, and you must also specify the VSwitchId parameter for the instances.

 If you do not use the `LaunchTemplateId` or `LaunchTemplateName` parameter to specify a launch template, you must set the `SecurityGroupId` parameter. |
|SecurityGroupIds.N|RepeatList|No|sg-bp15ed6xe1yxeycg7\*\*\*\*|The ID of security group N to which to assign the instance. Valid values of N are based on the maximum number of security groups to which an instance can belong. For more information, see the "Security group limits" section of the [Limits](~~101348~~) topic.

 **Note:** You cannot specify both SecurityGroupId and SecurityGroupIds.N. |
|VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws0\*\*\*\*|The ID of the vSwitch to which to connect the instance. You must specify this parameter when you create a VPC-type instance. The vSwitch and security group must belong to the same VPC. You can call the [DescribeVSwitches](~~35748~~) operation to query the created vSwitches.

 **Note:** If you specify the `VSwitchId` parameter, the zone specified by the `ZoneId` parameter must be the same as the zone of the vSwitch. You can also leave the `ZoneId` parameter empty. Then, the system selects the zone where the vSwitch is located. |
|InstanceName|String|No|k8s-node-\[1,4\]-alibabacloud|The name of the instance. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`. It can contain letters, digits, colons \(:\), underscores \(\_\), periods \(.\),and hyphens \(-\). The default value of this parameter is the `InstanceId` value.

 When you create multiple instances at a time, you can specify sequential names for the instances. For more information, see [Batch configure sequential names or hostnames for multiple instances](~~196048~~). |
|Description|String|No|Instance\_Description|The description of the instance. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. |
|InternetMaxBandwidthIn|Integer|No|10|The maximum inbound public bandwidth. Unit: Mbit/s. Valid values:

 -   If the purchased outbound public bandwidth is less than or equal to 10 Mbit/s, the valid values of this parameter are 1 to 10 and the default value of this parameter is 10.
-   If the purchased outbound public bandwidth is greater than 10 Mbit/s, the valid values of this parameter are 1 to the value of `InternetMaxBandwidthOut` and the default value is the value of `InternetMaxBandwidthOut`. |
|InternetMaxBandwidthOut|Integer|No|10|The maximum outbound public bandwidth. Unit: Mbit/s. Valid values: 0 to 100.

 Default value: 0. |
|HostName|String|No|k8s-node-\[1,4\]-ecshost|The hostname of the instance.

 -   The hostname cannot start or end with a period \(.\) or hyphen \(-\).It cannot contain consecutive periods \(.\) or hyphens \(-\).
-   For Windows instances, the hostname must be 2 to 15 characters in length and cannot contain periods \(.\) or contain only digits. It can contain letters, digits, and hyphens \(-\).
-   For instances that run other operating systems such as Linux,
    -   the hostname must be 2 to 64 characters in length. You can use periods \(.\) to separate a hostname into multiple segments. Each segment can contain letters, digits, and hyphens \(-\).
    -   You can use the `${instance_id}` placeholder to pass instance IDs into the hostnames specified by `HostName`. For example, if you set `HostName` to k8s-$\{instance\_id\} and the instance is assigned an ID of `i-123abc****` when the instance is created, the hostname of the instance is `k8s-i-123abc****`.

 When you create multiple instances, you can perform the following operations:

 -   Batch configure sequential hostnames for the instances. For more information, see [Batch configure sequential names or hostnames for multiple instances](~~196048~~).
-   Use the `HostNames.N` parameter to configure hostnames for the instances. You cannot specify both the `HostName`and `HostNames.N` parameters. |
|HostNames.N|RepeatList|No|ecs-host-01|The hostname of instance N. You can use this parameter to specify different hostnames for multiple instances.

 -   The maximum value of N must be the same as the `Amount` value.
-   You cannot specify both the `HostName` and `HostNames.N` parameters.
-   The hostname cannot start or end with a period \(.\) or hyphen \(-\).It cannot contain consecutive periods \(.\) or hyphens \(-\).
-   For Windows instances, the hostname must be 2 to 15 characters in length and cannot contain periods \(.\) or contain only digits. It can contain letters, digits, and hyphens \(-\).
-   For instances that run other operating systems such as Linux, the hostname must be 2 to 64 characters in length. You can use periods \(.\) to separate a hostname into multiple segments. Each segment can contain letters, digits, and hyphens \(-\). |
|UniqueSuffix|Boolean|No|true|Specifies whether to automatically append incremental suffixes to the hostnames specified by the `HostName` parameter and instance names specified by the `InstanceName` parameter when you create multiple instances at a time. The incremental suffixes range from 001 to 999. Valid values:

 -   true
-   false

 Default value: false.

 When the `HostName` or `InstanceName` value is set based on the specified sorting format and `name_suffix` is not specified, the hostnames or instance names are in the `name_prefix[begin_number,bits]` format, and the `UniqueSuffix` parameter does not take effect. The names are sorted in the specified sequence.

 For more information, see [Batch configure sequential names or hostnames for multiple instances](~~196048~~). |
|Password|String|No|EcsV587!|The password of the instance. The password must be 8 to 30 characters in length and include at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include:

 ```

( ) ` ~ ! @ # $ % ^ & * - _ + = | { } [ ] : ; ' < > , . ? /

```

 For Windows instances, the password cannot start with a forward slash \(/\).

 **Note:** For security reasons, we recommend that you use Hypertext Transfer Protocol Secure \(HTTPS\) to send requests if the `Password` parameter is specified. |
|PasswordInherit|Boolean|No|false|Specifies whether to use the password preset in the image. Valid values:

 -   true
-   false

 **Note:** If PasswordInherit is specified, leave Password empty and make sure that the selected image has a password preset. |
|ZoneId|String|No|cn-hangzhou-g|The ID of the zone in which to create the instance. You can call the [DescribeZones](~~25610~~) operation to query the zone list.

 **Note:** If you specify the `VSwitchId` parameter, the zone specified by the `ZoneId` parameter must be the same as the zone of the vSwitch. You can also leave the `ZoneId` parameter empty. Then, the system selects the zone where the vSwitch is located.

 This parameter is empty by default. |
|InternetChargeType|String|No|PayByTraffic|The billing method for network usage. Default value: PayByTraffic. Valid values:

 -   PayByBandwidth: pay-by-bandwidth
-   PayByTraffic: pay-by-traffic

 **Note:** When the **pay-by-traffic** billing method is used, the maximum inbound and outbound bandwidths are both the upper limits of bandwidths and for reference only. When resources are insufficient, these maximum bandwidths cannot be guaranteed. If you want guaranteed bandwidths for your instances, use the **pay-by-bandwidth** billing method. |
|SystemDisk.Size|String|No|40|The size of the system disk. Unit: GiB. Valid values: 20 to 500.

 The value of this parameter must be at least 20 and greater than or equal to the image size.

 The default value is 40 or the size of the image, depending on whichever is greater. |
|SystemDisk.Category|String|No|cloud\_ssd|The category of the system disk. Valid values:

 -   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\)
-   cloud: basic disk

 For non-I/O optimized instances of the retired instance types, the default value is cloud. For other instances, the default value is cloud\_efficiency. |
|SystemDisk.DiskName|String|No|cloud\_ssdSystem|The name of the system disk. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`. It can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).

 This parameter is empty by default. |
|SystemDisk.Description|String|No|SystemDisk\_Description|The description of the system disk. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. |
|SystemDisk.PerformanceLevel|String|No|PL0|The performance level of the ESSD used as the system disk. Default value: PL1. Valid values:

 -   PL0: A single ESSD can deliver up to 10,000 random read/write input/output operations per second \(IOPS\).
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD delivers up to 100,000 random read/write IOPS.
-   PL3: A single ESSD delivers up to 1,000,000 random read/write IOPS.

 For more information about ESSD performance levels, see [ESSDs](~~122389~~). |
|SystemDisk.AutoSnapshotPolicyId|String|No|sp-bp67acfmxazb4p\*\*\*\*|The ID of the automatic snapshot policy to be applied to the system disk. |
|DataDisk.N.Size|Integer|No|2000|The size of data disk N. Valid values of N: 1 to 16. Unit: GiB. Valid values:

 -   Valid values when DataDisk.N.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when DiskCategory is set to cloud\_ssd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_essd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud: 5 to 2000

 The value of this parameter must be greater than or equal to the size of the snapshot specified by the `SnapshotId` parameter. |
|DataDisk.N.SnapshotId|String|No|s-bp17441ohwka0yuh\*\*\*\*|The ID of the snapshot used to create data disk N. Valid values of N: 1 to 16.

 When the `DataDisk.N.SnapshotId` parameter is specified, the `DataDisk.N.Size` parameter is ignored. The data disk is created based on the size of the specified snapshot. Use snapshots created after July 15, 2013. Otherwise, an error message is returned and your request is rejected. |
|DataDisk.N.Category|String|No|cloud\_ssd|The category of data disk N. Valid values:

 -   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: ESSD
-   cloud: basic disk

 For I/O optimized instances, the default value is cloud\_efficiency. For non-I/O optimized instances, the default value is cloud. |
|DataDisk.N.Encrypted|String|No|false|Specifies whether to encrypt data disk N. Valid values:

 -   true: encrypts data disk N.
-   false: does not encrypt data disk N.

 Default value: false. |
|DataDisk.N.KMSKeyId|String|No|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|The ID of the Key Management Service \(KMS\) key to be used by data disk N. |
|DataDisk.N.DiskName|String|No|cloud\_ssdData|The name of data disk N. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`. It can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).

 This parameter is empty by default. |
|DataDisk.N.Description|String|No|DataDisk\_Description|The description of data disk N. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. |
|DataDisk.N.Device|String|No|null|The mount point of data disk N.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|DataDisk.N.DeleteWithInstance|Boolean|No|true|Specifies whether to release data disk N together with the instance. Valid values:

 -   true: releases data disk N together with the instance.
-   false: does not release data disk N together with the instance.

 Default value: true. |
|DataDisk.N.PerformanceLevel|String|No|PL1|The performance level of the ESSD used as data disk N. The N value must be the same as that in DataDisk.N.Category when `DataDisk.N.Category` is set to cloud\_essd. Valid values:

 -   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD delivers up to 100,000 random read/write IOPS.
-   PL3: A single ESSD delivers up to 1,000,000 random read/write IOPS.

 For more information about ESSD performance levels, see [ESSDs](~~122389~~). |
|DataDisk.N.AutoSnapshotPolicyId|String|No|sp-bp67acfmxazb4p\*\*\*\*|The ID of the automatic snapshot policy to be applied to data disk N. |
|IoOptimized|String|No|optimized|Specifies whether the instance is I/O optimized. For instances of retired instance types, the default value is none. For other instances, the default value is optimized. For more information, see [Retired instance types](~~55263~~). Valid values:

 -   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized. |
|NetworkInterface.N.PrimaryIpAddress|String|No|172.16.\*\*.\*\*|The primary IP address of secondary elastic network interface \(ENI\) N. Set the value of N to 1.

 **Note:** You can bind only one secondary ENI when you create an ECS instance. After the instance is created, you can call the [CreateNetworkInterface](~~58504~~) and [AttachNetworkInterface](~~58515~~) operations to bind more secondary ENIs.

 The default value is an IP address that is randomly selected from within the CIDR block of the vSwitch to which to connect the secondary ENI. |
|NetworkInterface.N.VSwitchId|String|No|vsw-bp67acfmxazb4p\*\*\*\*|The ID of the vSwitch to which to connect secondary ENI N. Set the value of N to 1.

 Default value: the ID of the vSwitch to which to connect the instance. |
|NetworkInterface.N.SecurityGroupId|String|No|sg-bp67acfmxazb4p\*\*\*\*|The ID of the security group to which to assign secondary ENI N. Set the value of N to 1.

 Default value: the ID of the security group to which to assign the instance. |
|NetworkInterface.N.SecurityGroupIds.N|RepeatList|No|sg-bp15ed6xe1yxeycg7\*\*\*\*|The ID of security group N to which to assign secondary ENI N. The valid values of N in `SecurityGroupIds.N` are based on the maximum number of security groups to which an ENI can belong. For more information, see [Limits](~~25412~~).

 **Note:** You cannot specify both the `NetworkInterface.N.SecurityGroupId` and `NetworkInterface.N.SecurityGroupIds.N` parameters. |
|NetworkInterface.N.NetworkInterfaceName|String|No|Network\_Name|The name of secondary ENI N. Set the value of N to 1. |
|NetworkInterface.N.Description|String|No|Network\_Description|The description of secondary ENI N. Set the value of N to 1. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. |
|NetworkInterface.N.QueueNumber|Integer|No|8|The number of queues supported by secondary ENI N. Set the value of N to 1.

 -   The value of this parameter cannot exceed the maximum number of queues per ENI allowed for the instance type.
-   The total number of queues for all ENIs bound to the instance cannot exceed the queue quota allowed for the instance type. To learn the maximum number of queues per ENI and the queue quota allowed for an instance type, you can call the [DescribeInstanceTypes](~~25620~~) operation to query the `MaximumQueueNumberPerEni` and `TotalEniQueueQuantity` parameters. |
|UserData|String|No|ZWNobyBoZWxsbyBlY3Mh|The user data of the instance. User data must be encoded in Base64. The maximum size of raw data is 16 KB. |
|KeyPairName|String|No|KeyPair\_Name|The name of the key pair.

 -   For Windows instances, this parameter is ignored and is empty by default. The `Password` parameter takes effect even if the KeyPairName parameter is specified.
-   For Linux instances, the username and password logon method is disabled by default. |
|RamRoleName|String|No|RAM\_Name|The name of the instance Resource Access Management \(RAM\) role. You can call the [ListRoles](~~28713~~) operation provided by RAM to query the instance RAM roles that you have created. |
|Amount|Integer|No|3|The number of instances that you want to create. Valid values: 1 to 100.

 Default value : 1. |
|MinAmount|Integer|No|2|The minimum number of instances that can be created. Valid values: 1 to 100.

 -   If the number of ECS instances that available resources are sufficient to create is less than the MinAmount value, instances cannot be created.
-   If the number of ECS instances that available resources are sufficient to create is greater than or equal to the MinAmount value, instances are created based on the number of available resources. |
|AutoReleaseTime|String|No|2018-01-01T12:05:00Z|The automatic release time of the pay-as-you-go instance. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

 -   If the value of the second \(`ss`\) is not `00`, the time is automatically rounded down to the nearest minute based on the value of the minute \(`mm`\).
-   The release time must be at least 30 minutes later than the current time.
-   The release time must be at most three years from the current time. |
|SpotStrategy|String|No|NoSpot|The preemption policy for the pay-as-you-go instance. This parameter takes effect only when the `InstanceChargeType` parameter is set to `PostPaid`. Default value: NoSpot. Valid values:

 -   NoSpot: The instance is created as a regular pay-as-you-go instance.
-   SpotWithPriceLimit: The instance is created as a preemptible instance with a user-defined maximum hourly price.
-   SpotAsPriceGo: The instance is created as a preemptible instance whose price is based on the market price at the time of purchase. |
|SpotDuration|Integer|No|1|The protection period of the preemptible instance. Unit: hours. Valid values: 0, 1, 2, 3, 4, 5, and 6.

 -   Protection periods of 2, 3, 4, 5, and 6 hours are in invitational preview. If you want to set this parameter to one of these values, submit a ticket.
-   If this parameter is set to 0, no protection period is configured for the preemptible instance.

 Default value: 1. |
|SpotPriceLimit|Float|No|0.97|The maximum hourly price of the instance. This parameter takes effect only when the `SpotStrategy` parameter is set to `SpotWithPriceLimit`. A maximum of three decimal places are allowed. |
|SpotInterruptionBehavior|String|No|Terminate|The interruption mode of the preemptible instance. Default value: Terminate. Set the value to Terminate, which indicates that the instance is released. |
|SecurityEnhancementStrategy|String|No|Active|Specifies whether to enable security hardening. Valid values:

 -   Active: enables security hardening. This value is applicable only to public images.
-   Deactive: does not enable security hardening. This value is applicable to all image types. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|Tag.N.Key|String|No|TestKey|The key of tag N to be bound to the instance, disks, and primary ENI. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. |
|Tag.N.Value|String|No|TestValue|The value of tag N to be bound to the instance, disks, and primary ENI. Valid values of N: 1 to 20. The tag value can be an empty string. It can be up to 128 characters in length and cannot start with acs:. It cannot contain http:// or https://. |
|HpcClusterId|String|No|hpc-bp67acfmxazb4p\*\*\*\*|The ID of the Elastic High Performance Computing \(E-HPC\) cluster to which to assign the instance. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Default value: false. Valid values:

 -   true: The validity of the request is checked but the request is not made. Check items include the request format, service limits, available ECS resources, and whether required parameters are specified. If the check fails, the corresponding error code is returned. If the check succeeds, the `DryRunOperation` error code is returned.
-   false: The validity of the request is checked. If the check succeeds, the request is made. |
|DedicatedHostId|String|No|dh-bp67acfmxazb4p\*\*\*\*|The ID of the dedicated host on which to create the instance. If the `DedicatedHostId` parameter is specified, the `SpotStrategy` and `SpotPriceLimit` parameters are ignored. This is because preemptible instances cannot be created on dedicated hosts.

 You can call the [DescribeDedicatedHosts](~~134242~~) operation to query the dedicated host list. |
|LaunchTemplateId|String|No|lt-bp1apo0bbbkuy0rj\*\*\*\*|The ID of the launch template. For more information, see [DescribeLaunchTemplates](~~73759~~).

 To use a launch template to create an instance, you must specify the launch template by using the `LaunchTemplateId` or `LaunchTemplateName` parameter. |
|LaunchTemplateName|String|No|LaunchTemplate\_Name|The name of the launch template.

 To use a launch template to create an instance, you must specify the launch template by using the `LaunchTemplateId` or `LaunchTemplateName` parameter. |
|LaunchTemplateVersion|Long|No|3|The version of the launch template. If you specify `LaunchTemplateId` or `LaunchTemplateName` but do not specify the version number of the launch template, the default template version is used. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which to assign the instance. |
|Period|Integer|No|1|The subscription period of the instance. The unit is specified by the `PeriodUnit` parameter. This parameter is valid and required only when `InstanceChargeType` is set to `PrePaid`. If the `DedicatedHostId` parameter is specified, the subscription period of the instance cannot be longer than that of the dedicated host. Valid values:

 -   Valid values when PeriodUnit is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60. |
|PeriodUnit|String|No|Month|The unit of the subscription period. Default value: Month. Valid values:

 -   Month |
|AutoRenew|Boolean|No|true|Specifies whether to enable auto-renewal for the instance. This parameter takes effect only when the `InstanceChargeType` parameter is set to `PrePaid`. Default value: false. Valid values:

 -   true: enables auto-renewal for the instance.
-   false: does not enable auto-renewal for the instance |
|AutoRenewPeriod|Integer|No|1|The auto-renewal period of the instance. Valid values:

 -   Valid values when PeriodUnit is set to Month: 1, 2, 3, 6, 12, 24, 36, 48, and 60.

 Default value: 1. |
|InstanceChargeType|String|No|PrePaid|The billing method of the instance. Default value: PostPaid. Valid values:

 -   PrePaid: subscription
-   PostPaid: pay-as-you-go

 If you set this parameter to PrePaid, make sure that you have sufficient credit in your account. Otherwise, the `InvalidPayMethod` error is returned. |
|DeploymentSetId|String|No|ds-bp1brhwhoqinyjd6\*\*\*\*|The ID of the deployment set to which to deploy the instance. |
|PrivateIpAddress|String|No|10.1.\*\*.\*\*|The private IP address of the instance.

 To assign a private IP address to a VPC-type ECS instance, make sure that the IP address is an idle IP address within the CIDR block of the vSwitch specified by the `VSwitchId` parameter.

 **Note:** When you specify the `PrivateIpAddress` parameter, the `Amount` parameter must be set to 1. |
|CreditSpecification|String|No|Standard|The performance mode of the burstable instance. Valid values:

 -   Standard: the standard mode. For more information, see the "Standard mode" section of the [Burstable instances](~~59977~~) topic.
-   Unlimited: the unlimited mode. For more information, see the "Unlimited mode" section of the [Burstable instances](~~59977~~) topic.

 This parameter is empty by default. |
|Ipv6Address.N|RepeatList|No|Ipv6Address.1=2001:db8:1234:1a00::\*\*\*|IPv6 address N to be assigned to the primary ENI. Set the value of N to 1. Example: `Ipv6Address.1=2001:db8:1234:1a00::***`.

 **Note:** If the `Ipv6Address.N` parameter is specified, the `Amount` parameter must be set to 1 and the `Ipv6AddressCount` parameter must be empty. |
|Ipv6AddressCount|Integer|No|1|The number of IPv6 addresses to be randomly generated for the primary ENI.

 **Note:** You cannot specify both the `Ipv6Addresses.N` and `Ipv6AddressCount` parameters. |
|NetworkInterfaceQueueNumber|Integer|No|8|The number of queues supported by the primary ENI.

 -   The value of this parameter cannot exceed the maximum number of queues per ENI allowed for the instance type.
-   The total number of queues for all ENIs bound to the instance cannot exceed the queue quota allowed for the instance type. To learn the maximum number of queues per ENI and the queue quota allowed for an instance type, you can call the [DescribeInstanceTypes](~~25620~~) operation to query the `MaximumQueueNumberPerEni` and `TotalEniQueueQuantity` parameters. |
|DeletionProtection|Boolean|No|false|The release protection property of the instance. It specifies whether you can use the ECS console or call the [DeleteInstance](~~25507~~) operation to manually release the instance. Default value: false. Valid values:

 -   true: Release protection is enabled.
-   false: Release protection is disabled.

 **Note:** This parameter is applicable only to pay-as-you-go instances. It can protect instances only against manual releases, not against automatic releases. |
|Affinity|String|No|default|Specifies whether to associate the instance on a dedicated host with the dedicated host. Valid values:

 -   default: does not associate the instance with the dedicated host. When you restart an instance in the No Fees for Stopped Instances \(VPC-Connected\) state, the instance is automatically deployed to another dedicated host in the automatic deployment resource pool if the available resources of the original dedicated host are insufficient.
-   host: associates the instance with the dedicated host. When you restart an instance in the No Fees for Stopped Instances \(VPC-Connected\) state, the instance still resides on the original dedicated host. If the available resources of the original dedicated host are insufficient, the instance fails to restart.

 Default value: default. |
|Tenancy|String|No|default|Specifies whether to create the instance on a dedicated host. Valid values:

 -   default: creates the instance on a non-dedicated host.
-   host: creates the instance on a dedicated host. If you do not specify the `DedicatedHostId` parameter, Alibaba Cloud automatically selects a dedicated host for the instance.

 Default value: default. |
|StorageSetId|String|No|ss-bp67acfmxazb4p\*\*\*\*|The ID of the storage set. |
|StorageSetPartitionNumber|Integer|No|2|The maximum number of partitions in the storage set. Valid values: greater than or equal to 2. |
|CpuOptions.Core|Integer|No|2|The number of CPU cores. This parameter cannot be specified but only uses its default value. |
|CpuOptions.ThreadsPerCore|Integer|No|2|The number of threads per core. The following formula is used to calculate the number of vCPUs of the instance: `CpuOptions.Core` value × `CpuOptions.ThreadPerCore` value.

 -   If the `CpuOptions.ThreadPerCore` parameter is set to 1, CPU Hyper-Threading is disabled.
-   This parameter is applicable only to specific instance types. |
|CpuOptions.Numa|String|No|1|The number of CPU Numa nodes. |
|SecurityOptions.TrustedSystemMode|String|No|vTPM|The trusted system mode. Set the value to vTPM.

 The trusted system mode supports the g7, c7, and r7 instance families as well as the following seventh-generation security-enhanced instance families: g7t, c7t, and r7t.

 To create instances of the preceding instance families, you must specify this parameter.

 -   To use the Alibaba Cloud trusted system, set this parameter to vTPM. Then, the Alibaba Cloud trusted system performs trust verifications when instances start.
-   If you do not want to use the Alibaba Cloud trusted system, leave this parameter empty.

 For more information about the trusted system, see [Overview](~~201394~~). |
|HttpEndpoint|String|No|enabled|Specifies whether to enable the access channel for the instance metadata. Valid values:

 -   enabled: enables the access channel for instance metadata.
-   disabled: disables the access channel for instance metadata.

 Default value: enabled.

 **Note:** For more information about instance metadata, see [Overview](~~49122~~). |
|HttpTokens|String|No|optional|Specifies whether to forcibly use the security-enhanced mode \(IMDSv2\) to access instance metadata. Valid values:

 -   optional: does not forcibly use the security-enhanced mode \(IMDSv2\).
-   required: forcibly uses the security-enhanced mode \(IMDSv2\). After you set this parameter to required, you cannot access the instance metadata in normal mode.

 Default value: optional.

 **Note:** For more information about the modes of accessing instance metadata, see [Access mode of instance metadata](~~150575~~). |
|PrivatePoolOptions.MatchCriteria|String|No|Open|The type of the private pool. After an elasticity assurance or capacity reservation takes effect, a private pool is generated. You can select a private pool when you create an instance. Valid values:

 -   Open: open private pool. The system selects a matching open private pool to create the instance. If no matching open private pools exist, resources in the public pool are used to create the instance. When this parameter is set to Open, the `PrivatePoolOptions.Id` parameter must be empty.
-   Target: targeted private pool. The capacity in a specific private pool is used to create the instance. If the specified private pool is unavailable, the instance cannot be created. If the parameter is set to Target, the `PrivatePoolOptions.Id` parameter must be specified.
-   None: no private pool. The capacity in private pools is not used to create the instance.

 Default value: None.

 In the following scenarios, the PrivatePoolOptions.MatchCriteria parameter can be set only to `None` or left empty:

 -   The instance is a preemptible instance.
-   The instance is in the classic network.
-   The instance is created on a dedicated host. |
|PrivatePoolOptions.Id|String|No|eap-bp67acfmxazb4\*\*\*\*|The ID of the private pool. The ID of a private pool is the same as that of the elasticity assurance or capacity reservation for which the private pool is generated. |
|SchedulerOptions.DedicatedHostClusterId|String|No|dc-bp12wlf6am0vz9v2\*\*\*\*|The ID of the dedicated cluster in which to create the instance. The system selects one dedicated host from the cluster to create the instance.

 **Note:** This parameter takes effect only when the `Tenancy` parameter is set to `host`.

 When you specify both `DedicatedHostId` and `SchedulerOptions.DedicatedHostClusterId`, take note of the following items:

 -   If the specified dedicated host belongs to the specified dedicated host cluster, the instance is preferentially deployed on the specified dedicated host.
-   If the specified dedicated host does not belong to the specified dedicated host cluster, the instance cannot be created.

 You can call the [DescribeDedicatedHostClusters](~~184145~~) operation to query the dedicated host cluster list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|InstanceIdSets|List|\["i-bp67acfmxazb4pd2\*\*\*\*", "i-bp1i43l28m7u48p1\*\*\*\*", "i-bp12yqg7jdyxl11f\*\*\*\*"\]|The IDs of the instances \(`InstanceIdSet`\). |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TradePrice|Float|0.165|The transaction price. |
|OrderId|String|1234567890|The ID of the order. This parameter is returned only when `InstanceChargeType` is set to PrePaid. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=RunInstances
&RegionId=cn-hangzhou
&ImageId=aliyun_2_1903_x64_20G_alibase_20200324.vhd
&InstanceType=ecs.g6.large
&SecurityGroupId=sg-bp67acfmxazb4p****
&VSwitchId=vsw-bp1s5fnvk4gn2tws0****
&SystemDisk.AutoSnapshotPolicyId=sp-bp67acfmxazb4p****
&Amount=3
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RunInstancesResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <InstanceIdSets>
            <InstanceIdSet>i-bp67acfmxazb4pd2****</InstanceIdSet>
            <InstanceIdSet>i-bp1i43l28m7u48p1****</InstanceIdSet>
            <InstanceIdSet>i-bp12yqg7jdyxl11f****</InstanceIdSet>
      </InstanceIdSets>
      <OrderId>1234567890</OrderId>
      <TradePrice>0.165</TradePrice>
</RunInstancesResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E", 
    "InstanceIdSets": {
        "InstanceIdSet": [
            "i-bp67acfmxazb4pd2****",
            "i-bp1i43l28m7u48p1****",
            "i-bp12yqg7jdyxl11f****"
        ]
    },
    "OrderId": "1234567890", 
    "TradePrice": "0.165"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|The error message returned because you are not authorized to use the specified instance type.|
|404|InvalidSecurityGroupId|The specified SecurityGroupId is invalid or does not exist.|The error message returned because the specified SecurityGroupId parameter is invalid or does not exist.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType beyond the permitted range.|The error message returned because the specified InstanceType parameter is invalid.|
|404|InvalidSecurityGroupId.NotFound|The SecurityGroupId provided does not exist in our records.|The error message returned because the specified security group does not exist within this account. Check whether the security group ID is correct.|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|The error message returned because the specified Description parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|The error message returned because the specified InternetChargeType parameter is invalid.|
|400|InvalidParameter|The specified parameter "InternetMaxBandwidthOut" is not valid.|The error message returned because the specified InternetMaxBandwidthOut parameter is invalid.|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|The error message returned because the specified HostName parameter is invalid.|
|403|InvalidParams.InstanceNameExceed|The uniqueSuffix takes three naming places, please shorten your InstanceName.|The error message returned because the instance name must be shortened to make space for the sequential suffix specified by UniqueSuffix. The sequential suffix is three characters in length.|
|403|InvalidParams.HostnameExceed|The uniqueSuffix takes three naming places, please shorten your Hostname.|The error message returned because the instance hostname must be shortened to make space for the sequential suffix specified by UniqueSuffix. The sequential suffix is three characters in length.|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|The error message returned because the specified Password parameter is invalid.|
|400|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|The error message returned because the Password parameter is specified when PasswdInherit is specified.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|400|InvalidDiskName.Malformed|The specified parameter "SyatemDisk.DiskName or DataDisk.n.DiskName" is not valid.|The error message returned because the specified SystemDisk.DiskName or DataDisk.N.DiskName parameter is invalid. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.|
|400|InvalidDiskDescription.Malformed|The specified parameter "SyatemDisk.DiskDescription" or "DataDisk.n.Description" is not valid.|The error message returned because the specified SystemDisk.Description or DataDisk.N.Description parameter is invalid.|
|400|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned because the specified DataDisk.N.Size parameter is invalid or the snapshot size exceeds the maximum capacity allowed for the specified disk category.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.n.Category" is not valid.|The error message returned because the specified DataDisk.N.Category parameter is invalid.|
|404|InvalidDataDiskSnapshotId.NotFound|The specified parameter "DataDisk.n.SnapshotId" is not valid.|The error message returned because the specified DataDisk.N.SnapshotId parameter is invalid.|
|400|InvalidDataDevice.Malformed|The specified parameter "DataDisk.n.Device" is not valid.|The error message returned because the specified DataDisk.N.Device parameter is invalid.|
|400|InvalidNodeControllerId.Malformed|The specified parameter "NodeControllerId" is not valid.|The error message returned because the specified NodeControllerId parameter is invalid.|
|400|InvalidInnerIpAddress.Malformed|The specified parameter "InnerIpAddress" is not valid.|The error message returned because the specified InnerIpAddress parameter is invalid.|
|400|InvalidInnerIpAddress.Unusable|The specified InnerIpAddress is already used or not found in usable ip range.|The error message returned because the specified internal IP address is unavailable.|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|The error message returned because the specified image does not support the specified instance type.|
|400|ImageNotSupportCloudInit|The specified image does not support cloud-init.|The error message returned because the specified image does not support cloud-init.|
|400|InvalidSnapshotId.BasedSnapshotTooOld|The specified snapshot is created before 2013-07-15.|The error message returned because the specified snapshot was created before July 15, 2013.|
|400|QuotaExceed.AfterpayInstance|Living afterpay instances quota exceeded.|The error message returned because the maximum number of active pay-as-you-go instances has been reached.|
|403|ImageNotSubscribed|The specified image has not be subscribed.|The error message returned because you have not subscribed to the specified Alibaba Cloud Marketplace image.|
|403|InvalidSystemDiskCategory.ValueUnauthorized|The disk category is not authorized.|The error message returned because you are not authorized to use the specified disk category.|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|The error message returned because the specified snapshot is being created.|
|403|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|The error message returned because the total capacity of disks of the specified category exceeds the maximum capacity allowed for an instance.|
|403|InvalidDevice.InUse|The specified device has been occupied.|The error message returned because the specified device already has a disk attached.|
|403|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|The error message returned because the specified Alibaba Cloud Marketplace image is unavailable, or because the specified custom image contains the product code of the Alibaba Cloud Marketplace image from which the custom image is derived and the Alibaba Cloud Marketplace image has been removed from Alibaba Cloud Marketplace.|
|404|InvalidClusterId.NotFound|The ClusterId provided does not exist in our records.|The error message returned because the specified cluster ID does not exist.|
|403|CategoryNotSupported|The specified zone does not offer the specified disk category.|The error message returned because the specified disk category is unavailable in the specified zone.|
|400|InvalidInstanceName.Malformed|The specified parameter "InstanceName" is not valid.|The error message returned because the specified InstanceName parameter is invalid. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.|
|400|InvalidDiskDescription.Malformed|The specified parameter "SyatemDisk.DiskDescription or DataDisk.n.Description" is not valid.|The error message returned because the specified SystemDisk.Description or DataDisk.N.Description parameter is invalid.|
|403|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|The error message returned because the maximum number of removable disks has been reached.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|400|InvalidParameter.Conflict|The speicified region and cluster do not match.|The error message returned because the specified region and the specified cluster do not correspond to each other.|
|403|SecurityGroupInstanceLimitExceed|Exceeding the allowed amount of instances of a security group.|The error message returned because the maximum number of instances in the security group has been reached.|
|403|NodeControllerUnavailable|The Node Controller is temporarily unavailable.|The error message returned because the node controller is unavailable.|
|403|RegionUnauthorized|There is no authority to create instance in the specified region.|The error message returned because you are not authorized to create instances in the specified region.|
|403|CategoryNotSupported|The specified Zone or cluster does not offer the specified disk category.|The error message returned because the specified disk category is unavailable in the specified zone or cluster.|
|403|InvalidSnapshotId.NotDataDiskSnapshot|The specified snapshot is system disk snapshot.|The error message returned because the specified snapshot is a system disk snapshot.|
|403|CategoryNotSupported|The specified cluster does not offer the specified disk category.|The error message returned because the specified disk category is unavailable in the specified cluster.|
|404|InvalidVSwitchId.NotFound|Specified virtual switch does not exist.|The error message returned because the specified VSwitchId parameter does not exist.|
|404|InvalidVSwitchId.NotFound|%s|The error message returned because the specified VSwitchId parameter does not exist.|
|400|InvalidParameter.Mismatch|Specified security group and virtual switch are not in the same VPC.|The error message returned because the specified security group and vSwitch do not belong to the same VPC.|
|400|InvalidNetworkType.Mismatch|Specified parameter "InternetMaxBandwidthIn" or "InternetMaxBandwidthOut" conflict with instance network type.|The error message returned because the specified InternetMaxBandwidthIn or InternetMaxBandwidthOut parameter conflicts with the instance network type.|
|400|InvalidNetworkType.Mismatch|Specified parameter "InternetChargeType" conflict with instance network type.|The error message returned because the network type of the instance does not support the specified billing method for network usage.|
|400|InvalidPrivateIpAddress|Specified private IP address is not in the CIDR block of virtual switch.|The error message returned because the specified private IP address is not within the CIDR block of the vSwitch.|
|400|InvalidPrivateIpAddress.Malformed|Specified private IP address is malformed.|The error message returned because the specified PrivateIpAddress parameter is invalid.|
|400|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicated.|The error message returned because the specified private IP address is already in use. Try another IP address.|
|400|QuotaExceeded.PrivateIpAddress|Don't have enough private IPs in this switch|The error message returned because all the private IP addresses within the CIDR block of the specified vSwitch are already in use. Try another vSwitch.|
|400|QuotaExceeded|Living instances quota exceeded in this VPC.|The error message returned because the maximum number of active instances has been reached.|
|400|IncorrectVSwitchStatus|The current status of virtual switch does not support this operation.|The error message returned because the specified vSwitch is in the Pending state and cannot be deleted.|
|400|InvalidParameter.Mismatch|Specified virtual switch is not in the specified zone.|The error message returned because the specified vSwitch does not exist in the specified zone.|
|400|ResourceNotAvailable|Resource you requested is not available in this region or zone.|The error message returned because VPC is not supported by the specified region or zone.|
|400|MissingParameter|The input parameter "VSwitchId" that is mandatory for processing this request is not supplied.|The error message returned because the VSwitchId parameter is not specified.|
|400|InvalidDiskCategory.Mismatch|The specified disk categories' combination is not supported.|The error message returned because the combination of the specified disk categories is not supported.|
|403|Forbbiden|User not authorized to operate on the specified resource.|The error message returned because you are not authorized to perform operations on the specified resource.|
|403|DeleteWithInstance.Conflict|The specified disk is not a portable disk and cannot be set to DeleteWithInstance attribute.|The error message returned because the specified disk is not removable and cannot be released together with the instance.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned because the specified image does not exist within this account. Check whether the image ID is correct.|
|403|InstanceDiskNumLimitExceed|The number of specified disk in an instance exceeds.|The error message returned because the number of specified disks exceeds the upper limit for an instance.|
|403|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|The error message returned because the specified image does not support I/O optimized instances.|
|404|IoOptimized.NotSupported|The specified instancetype is not support IoOptimized instance|The error message returned because the specified instance type does not support I/O optimization.|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot|The error message returned because the specified disk size is smaller than the snapshot size.|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|The error message returned because the specified InstanceChargeType parameter does not exist.|
|400|MissingParamter|The specified parameter "Period" is not null.|The error message returned because the Period parameter is not specified.|
|400|InvalidPeriod|The specified period is not valid.|The error message returned because the specified Period parameter is invalid.|
|403|InvalidDiskCategory.Mismatch|The specified disk categories combination is not supported.|The error message returned because the combination of the specified disk categories is not supported.|
|403|IoOptimized.NotSupported|Vpc is not support IoOptimized instance.|The error message returned because I/O optimized instances are not supported in the VPC.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter " DataDisk.n.Category " is not valid.|The error message returned because the specified DataDisk.N.Category parameter is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter " SystemDisk.Category " is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not support the specified instance type.|The error message returned because the specified disk category does not support the instance type.|
|400|InstanceDiskCategoryLimitExceed|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned because the specified DataDisk.N.Size parameter is invalid or the snapshot size exceeds the maximum capacity allowed for the specified disk category.|
|403|QuotaExceed.BuyImage|The specified image is from the image market?You have not bought it or your quota has been exceeded.|The error message returned because the specified Alibaba Cloud Marketplace image has not been purchased or the maximum number of images has been reached.|
|404|DependencyViolation.IoOptimized|The specified instancetype must be IoOptimized instance.|The error message returned because the specified instance type is not I/O optimized.|
|404|PaymentMethodNotFound|No payment method has been registered on the account.|The error message returned because you have not configured a payment method for your account.|
|400|InvalidInstanceType.ValueNotSupported|InternetMaxBandwidthOut should be set.|The error message returned because the InternetMaxBandwidthOut parameter is not specified.|
|400|InvalidInstanceType.ValueNotSupported|instancetype is not valid.|The error message returned because the specified InstanceType parameter is invalid.|
|400|InvalidClientToken.ValueNotSupported|clienttoken is not valid.|The error message returned because the specified ClientToken parameter is invalid.|
|400|InvalidIoOptimize.ValueNotSupported|The specified IoOptimize is not valid.|The error message returned because the specified IoOptimized parameter is invalid.|
|400|InvalidHostName.Malformed|The specified parameter HostName is not valid.|The error message returned because the specified HostName parameter is invalid.|
|404|HOSTNAME\_ILLEGAL|hostname is not valid.|The error message returned because the specified HostName parameter is invalid.|
|400|InvalidInternetMaxBandwidthOut.Malformed|The specified parameter internetMaxBandwidthOut is not valid.|The error message returned because the specified InternetMaxBandwidthOut parameter is invalid.|
|400|InvalidInternetMaxBandwidthIn.Malformed|The specified parameter internetMaxBandwidthIn is not valid.|The error message returned because the specified InternetMaxBandwidthIn parameter is invalid.|
|400|InvalidSnapshotId.NotFound|The specified parameter SnapshotId is not exist.|The error message returned because the specified snapshot does not exist.|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|The error message returned because the specified Tag.N.Key parameter is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The error message returned because the specified Tag.N.Value parameter is invalid.|
|403|InvalidResourceId.NotSupported|The specified ResourceId does not support tagging.|The error message returned because the specified resource does not support tagging.|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|The error message returned because the specified Tag.N.Key and Tag.N.Value parameters do not match.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned because the number of specified tags has reached the upper limit.|
|400|InvalidMinAmount.Malformed|The specified parameter MinAmount is not valid.|The error message returned because the specified MinAmount parameter is invalid.|
|400|InvalidMaxAmount.Malformed|The specified parameter MaxAmount is not valid.|The error message returned because the specified MaxAmount parameter is invalid.|
|400|InvalidAutoReleaseTime.Malformed|The specified parameter AutoReleaseTime is not valid.|The error message returned because the specified AutoReleaseTime parameter is invalid. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.|
|400|InvalidPrivateIpAddress.Malformed|The specified parameter PrivateIpAddress is not valid.|The error message returned because the specified PrivateIpAddress parameter is invalid.|
|400|InvalidInnerIpAddress.Malformed|The specified parameter InnerIpAddress is not valid.|The error message returned because the specified InnerIpAddress parameter is invalid.|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|The error message returned because the specified system disk size is smaller than the size of the image.|
|404|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the min size.|The error message returned because the specified system disk size is smaller than the minimum allowable size.|
|403|OperationDenied|The specified RegionId does not support the creation of the network type ECS instance.|The error message returned because instances of the specified network type cannot be created in the specified region. Check whether instance resources of this network type are available in the region.|
|400|OperationDenied.NoVlan|The specified parameter "VlanId" is not valid or vlan has not enough IP address.|The error message returned because the specified virtual LAN \(VLAN\) ID is invalid or because available IP addresses in the specified VLAN are insufficient.|
|403|OperationDenied.ImageNotValid|The specified Image is disabled or is deleted.|The error message returned because the specified ImageId parameter does not exist.|
|403|OperationDenied.SnapshotNotValid|The specified snapshot is not allowed to create disk.|The error message returned because the specified snapshot cannot be used to create disks.|
|403|OperationDenied.SnapshotNotAllowed|The specified snapshot is not allowed to create disk.|The error message returned because the specified snapshot cannot be used to create disks.|
|403|OperationDenied.ZoneNotAllowed|The creation of Instance to the specified Zone is not allowed.|The error message returned because instances cannot be created in the specified zone.|
|403|OperationDenied.ZoneSystemCategoryNotMatch|The specified Zone or cluster does not offer the specified disk category or the speicified zone and cluster do not match.|The error message returned because the specified disk category is unavailable in the specified zone or cluster, or because the specified zone and cluster do not correspond to each other.|
|403|OperationDenied.ResourceControl|The specified region is in resource control, please try later.|The error message returned because the specified region is under resource control. Try again later.|
|403|OperationDenied.NoStock|The resource is out of usage.|The error message returned because the instance is not in the Running state. Start the instance or check whether the specified operation is valid.|
|403|OperationDenied.SnapshotParamsNotValid|The capacity of snapshot exceeds the size limit of the specified disk category or the specified category is not authorizied.|The error message returned because the maximum snapshot size has been reached or because you are not authorized to use the specified disk category.|
|404|OperationDenied.CreatingConflict|Another Instance has been creating|The error message returned because no other instances can be created while an instance is being created.|
|403|OperationDenied.DiskTypeNotSupport|The type of the disk does not support the operation|The error message returned because the specified operation is invalid.|
|400|OperationDenied.QuotaExceed|The quota of tags on resource is beyond permitted range.|The error message returned because the maximum number of tags that can be bound to the resource has been reached.|
|400|Account.Arrearage|Your account has been in arrears.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|403|InvalidUserData.Forbidden|User not authorized to input the parameter "UserData", please apply for permission "UserData"|The error message returned because you are not authorized to manage user data. Apply for the permission first.|
|400|InvalidUserData.SizeExceeded|The specified parameter "UserData" exceeds the size.|The error message returned because the maximum size of user data specified by the UserData parameter has been reached.|
|400|InvalidUserData.NotSupported|The specified parameter "UserData" only support the vpc and IoOptimized Instance.|The error message returned because the specified UserData parameter is not supported. UserData is supported only by VPC-type I/O optimized instances.|
|404|InvalidZoneId.NotFound|The specified zoneId does not exist.|The error message returned because the specified ZoneId parameter does not exist.|
|403|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|The error message returned because you are not authorized to purchase resources in the specified zone.|
|403|Zone.NotOnSale|The resource in the specified zone is no longer available for sale. Please try other regions and zones.|The error message returned because the specified resource is unavailable in the specified zone. Try other resource types or select other regions or zones.|
|403|InvalidClusterId.NotFound|The specified clusterId does not exist.|The error message returned because the specified cluster ID does not exist.|
|403|OperationDenied.NoStock|The resource is out of stock in the specified zone. Please try other types, or choose other regions and zones.|The error message returned because the specified resource is unavailable in the specified zone. Try other resource types or select other regions or zones.|
|403|InvalidInstanceType.ZoneNotSupported|The specified zone does not support this instancetype.|The error message returned because the specified instance type is not supported in the specified zone.|
|400|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|The error message returned because the number of specified disks exceeds the upper limit for an instance.|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|400|InvalidSpotStrategy|The specified SpotStrategy is not valid.|The error message returned because the specified SpotStrategy parameter is invalid.|
|400|InvalidSpotPriceLimit|The specified SpotPriceLimitis not valid.|The error message returned because the specified SpotPriceLimit parameter is invalid.|
|400|InvalidSpotDuration|The specified SpotDuration is not valid.|The error message returned because the specified SpotDuration parameter is invalid.|
|400|InvalidSpotAuthorized|The specified Spot param is unauthorized.|The error message returned because you are not authorized to set the SpotDuration parameter.|
|400|InvalidSpotPrepaid|The specified Spot type is not support PrePay Instance.|The error message returned because preemptible instances do not support the subscription billing method.|
|400|InvalidSpotAliUid|The specified UID is not authorized to use SPOT instance.|The error message returned because you are not authorized to create preemptible instances.|
|400|InvalidParameter.Bandwidth|%s|The error message returned because the specified bandwidth is invalid.|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|The error message returned because the specified data disk category is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|The error message returned because the operation is not supported by the specified system disk category.|
|400|InvalidParameter.Conflict|%s|The error message returned because a specified parameter is invalid. Check whether parameter conflicts exist.|
|400|InvalidInternetChargeType.ValueNotSupported|%s|The error message returned because the specified billing method for network usage is not supported.|
|400|InvalidInstanceType.ValueNotSupported|%s|The error message returned because the operation is not supported by the specified instance type.|
|403|InstanceType.Offline|%s|The error message returned because the operation is not supported while the instance type is retired or resources of the instance type are insufficient.|
|400|RegionUnauthorized|%s|The error message returned because you are not authorized to create disks in the specified region.|
|400|Zone.NotOnSale|%s|The error message returned because the requested resources are unavailable in the specified zone.|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|The error message returned because the specified system disk size is invalid.|
|400|InvalidDataDiskSize.ValueNotSupported|%s|The error message returned because the specified data disk size is invalid.|
|403|DependencyViolation.WindowsInstance|The instance creating is window, cannot use ssh key pair to login.|The error message returned because the specified instance is a Windows instance and does not support logons based on SSH key pairs.|
|400|InvalidInstanceType.ValueNotSupported|The specified parameter "KeyPairName" only support IoOptimized Instance.|The error message returned because non-I/O optimized instances do not support SSH key pairs.|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|The error message returned because the specified ResourceGroupId parameter does not exist.|
|403|InvalidUser.PassRoleForbidden|The RAM user does not have the privilege to pass a RAM role.|The error message returned because the RAM user is not authorized to pass the RAM role.|
|404|InvalidRamRole.NotFound|The specified parameter "RAMRoleName" does not exist.|The error message returned because the specified RAMRoleName parameter does not exist.|
|404|InvalidLaunchTemplate.NotFound|%s|The error message returned because the specified launch template does not exist. Check whether the parameter is correct.|
|404|InvalidLaunchTemplateVersion.NotFound|%s|The error message returned because the specified launch template of the specified version does not exist. Check whether the parameter is correct.|
|400|InvalidInstanceType.ElasticNetworkInterfaceNotSupported|The specified instance type does not support Elastic Network Interface, you can not attach Elastic Network Interface to generation I instances.|The error message returned because ENIs are not supported by the specified instance type.|
|400|InvalidParameter.EncryptedIllegal|%s|The error message returned because the specified parameter is invalid. Check whether your encryption operation is valid.|
|400|InvalidParameter.EncryptedNotSupported|%s|The error message returned because the specified parameter is invalid and your encryption operation is not supported.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|403|Forbidden.RiskControl|This operation is forbidden by Aliyun RiskControl system.|The error message returned because the operation is forbidden by the risk control system.|
|403|InvalidInstance.UnPaidOrder|The specified Instance has unpaid order.|The error message returned because you have unpaid orders for the specified instance. Pay for the orders and try again.|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|The error message returned because you have not completed real-name verification. Complete real-name verification and try again.|
|403|InvalidInstanceType.NotSupported|The specified InstanceType is not Supported.|The error message returned because the specified InstanceType parameter is not supported.|
|403|InvalidPayMethod|The specified pay method is not valid.|The error message returned because the specified payment method is invalid.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|400|InvalidSpotPriceLimit.LowerThanPublicPrice|The specified parameter "spotPriceLimit" can't be lower than current public price.|The error message returned because the specified value of SpotPriceLimit is less than the current market price.|
|400|InvalidRelationResource.NotFound|The relation resource has been deleted.|The error message returned because the associated resource is deleted.|
|400|IncorrectRecycleBinStatus|The operation is not permitted due to resource status.|The error message returned because the operation is not supported while the resource is in the current state.|
|400|InvalidHpcClusterId.Unnecessary|The specified HpcClusterId is unnecessary|The error message returned because the HpcClusterId parameter is specified.|
|400|InvalidVSwitchId.Necessary|The VSwitchId is necessary|The error message returned because the VSwitchId parameter is not specified.|
|400|InvalidHpcClusterId.Necessary|The HpcClusterId is necessary|The error message returned because the HpcClusterId parameter is not specified.|
|400|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found|The error message returned because the specified HpcClusterId parameter does not exist.|
|404|InvalidVSwitchId.NotExist|%s|The error message returned because the specified VSwitchId parameter does not exist.|
|403|ImageNotSupportInstanceType|The specified image does not support the specified InstanceType.|The error message returned because the specified image does not support the specified instance type.|
|400|InvalidSecurityGroup.NotInDefaultVpc|%s|The error message returned because the specified security group is not in the default VPC. Check whether the specified SecurityGroupId parameter is correct.|
|400|VpcNotFound|Vpc is not found according to the specified VSwitch or the vpc does not belong to you.|The error message returned because no VPC is found based on the specified vSwitch or because the corresponding VPC does not belong to you.|
|400|InvalidSystemDiskSize.ImageNotSupportResize|The specified image does not support resize.|The error message returned because the specified image does not support resizing.|
|403|OperationDenied.InvalidNetworkType|%s|The error message returned because the operation is not supported by the specified network type.|
|400|InvalidSpotInterruptionBehavior|%s|The error message returned because the specified SpotInterruptionBehavior parameter is invalid.|
|403|InvalidSpotInterruptionBehavior.ClassicNetworkNotSupport|The specified SpotInterruptionBehavior does not support Classic network Instance.|The error message returned because the operation is not supported by instances in the classic network.|
|403|InvalidSpotInterruptionBehavior.LocalDiskNotSupport|The specified SpotInterruptionBehavior does not support local disk instance.|The error message returned because the operation is not supported by instances that have local disks attached.|
|400|InvalidDeploymentOnHost|%s|The error message returned because the instance cannot be deployed in the specified deployment set.|
|400|InvalidInstanceChargeType.NotSupport|The Dedicated host not support the specified Instance charge type.|The error message returned because the dedicated host does not support instances that use the specified billing method.|
|400|InvalidNetworkType.NotSupported|The classic networkType not support create ECS on dedicatedHost|The error message returned because the dedicated host does not support instances in the classic network.|
|400|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|The error message returned because the specified DedicatedHostId parameter does not exist.|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|The error message returned because the operation is not supported while the dedicated host is in the current state.|
|400|IncorrectDedicatedHostStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed|The error message returned because subscription instances cannot be deployed on pay-as-you-go dedicated hosts.|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|The error message returned because the expiration date of the instance is later than that of the dedicated host.|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorize.|The error message returned because you are not authorized to use the specified instance type.|
|400|DedicatedHostType.Unmatched|The specified DedicatedHostType doesn?t match the instance type.|The error message returned because the specified dedicated host type does not correspond to the specified instance type.|
|400|MissingParameter|The input parameter ImageId that is mandatory for processing this request is not supplied.|The error message returned because the ImageId parameter is not specified.|
|400|MissingParameter|The input parameter InstanceType that is mandatory for processing this request is not supplied.|The error message returned because the InstanceType parameter is not specified.|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed.|The error message returned because subscription instances cannot be deployed on pay-as-you-go dedicated hosts.|
|400|InvalidParam.NetworkInterface|%s|The error message returned because a specified parameter is invalid. Check whether the parameter corresponds to the operation.|
|403|OperationDenied.ImageNotValid|%s|The error message returned because the image does not support the operation.|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|The error message returned because the maximum number of pay-as-you-go disks has been reached.|
|401|InvalidRamRole.NotEcsRole|The specified ram role is not authorized for ecs, please check your role policy.|The error message returned because the specified RAM role is not authorized to use ECS. Check your role policy.|
|403|InvalidParameter.NotMatch|%s|The error message returned because a specified parameter is invalid. Check whether parameter conflicts exist.|
|400|InvalidParameter.CreditSpecification|The specified CreditSpecification is not supported in this region.|The error message returned because the specified credit policy is not supported in the region.|
|404|InvalidMarketImage.NotFound|The specified marketplace image does not exist, please change the imageId and try again.|The error message returned because the specified Alibaba Cloud Marketplace image does not exist. Modify the parameter and try again later.|
|400|IncorrectVpcStatus|Current VPC status does not support this operation.|The error message returned because the operation is not supported while the VPC is in the current state.|
|400|InvalidInstanceType.NotSupported|The specified instanceType is not supported by the deployment set.|The error message returned because the specified instance type is not supported by the deployment set. Try another instance type.|
|400|InvalidVpcZone.NotSupported|The specified operation is not allowed in the zone to which your VPC belongs, please try in other zones.|The error message returned because the region to which the VPC belongs does not support the specified operation. Try another region.|
|400|IncorrectDefaultVpcStatus|The status of the default VPC is invalid.|The error message returned because the status of the default VPC is invalid.|
|404|DeploymentSet.NotFound|The specified deployment set does not exist.|The error message returned because the specified DeploymentSetId parameter does not exist.|
|400|InvalidAutoRenewPeriod.ValueNotSupported|The specified autoRenewPeriod is invalid.|The error message returned because the specified AutoRenewPeriod parameter is invalid.|
|403|OperationDenied.LocalDiskUnsupported|The configuration change is not allowed when the specified instance has local disks mounted.|The error message returned because the instance types of instances that have local disks attached cannot be changed.|
|403|OperationDenied.InconsistentNetwork|The specified security group and vswitch are not in the same vpc.|The error message returned because the specified security group and vSwitch do not belong to the same VPC.|
|403|OperationDenied|If the network segment of the vswitch is the same as that of its VPC. Therefore, the VPC cannot create other vswitchs across the region.|The error message returned because the VPC and vSwitch have the same CIDR block and no additional vSwitches can be created for zones in this VPC.|
|403|DefaultVswitch.Existed|The default vswitch for VPC already exists.|The error message returned because a default vSwitch already exists in the current VPC.|
|400|InvalidMarketImageChargeType.NotSupport|The specified chargeType of marketImage is unsupported.|The error message returned because the billing method of the Alibaba Cloud Marketplace image is not supported.|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|The error message returned because resources are insufficient in the specified zone. Try other types of resources, or select other regions and zones.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|CategoryViolation|The specified instance does not support this operation because of its disk category.|The error message returned because the configurations of instances that have local disks attached cannot be upgraded or downgraded.|
|400|InvalidPeriodType.ValueNotSupported|The specified parameter PeriodType is invalid.|The error message returned because the specified PeriodType parameter is invalid.|
|403|ResourcesNotInSameZone|The specified instance and dedicated host are not in the same zone.|The error message returned because the specified instance and dedicated host are not located within the same region.|
|403|InvalidDisk.SystemDiskSize|The specified SystemDiskSize beyond the permitted range.|The error message returned because the maximum size of the specified system disk has been reached.|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|The error message returned because the specified ClientToken parameter is invalid.|
|400|OperationDenied|The current user does not support this operation.|The error message returned because your account does not support the operation.|
|403|InsufficientBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned because the specified InstanceType parameter does not exist or because you are not authorized to manage instances of this instance type.|
|400|InvalidParam.Tenancy|The specified Tenancy is invalid.|The error message returned because the specified Tenancy parameter is invalid.|
|403|MaxEniIpv6IpsCountExceeded|%s|The error message returned because the maximum number of IPv6 addresses that can be assigned to the ENI has been reached.|
|403|InvalidIp.IpRepeated|%s|The error message returned because the specified IP address already exists.|
|403|InvalidIp.IpAssigned|%s|The error message returned because the specified IP address is already assigned.|
|403|InvalidIp.Address|%s|The error message returned because the specified IPv6 address is invalid.|
|403|InvalidOperation.Ipv4CountExceeded|%s|The error message returned because the maximum number of IPv4 addresses has been reached.|
|403|InvalidOperation.Ipv6CountExceeded|%s|The error message returned because the maximum number of IPv6 addresses has been reached.|
|403|InvalidOperation.Ipv6NotSupport|%s|The error message returned because IPv6 does not support the operation.|
|403|InvalidVSwitch.Ipv6NotTurnOn|%s|The error message returned because the IPv6 feature is not enabled on your current vSwitch. Enable the feature and try again.|
|403|InvalidParam.Amount|%s|The error message returned because the specified Amount parameter is invalid.|
|403|InvalidVSwitchId.IpInvalid|%s|The error message returned because the specified private IP address is invalid.|
|403|Forbidden.RegionId|%s|The error message returned because the service is unavailable in the current region.|
|400|IncorrectVpcStatus|The current status of vpc does not support this operation.|The error message returned because the operation is not supported while the VPC is in the current state.|
|403|QuotaExceed.DeploymentSetInstanceQuotaFull|instance quota in one deployment set exceeded.|The error message returned because the maximum number of instances in the deployment set has been reached.|
|403|InvalidRegion.NotSupport|The specified region does not support byok.|The error message returned because the bring your own key \(BYOK\) feature is not supported in the region.|
|403|UserNotInTheWhiteList|The user is not in byok white list.|The error message returned because you are not in the BYOK whitelist. Try again when you are in the whitelist.|
|400|InvalidParameter.EncryptedIllegal|The specified parameter Encrypted must be true when kmsKeyId is not empty.|The error message returned because the encryption feature is not enabled after a KMS key ID is specified.|
|400|IoOptimized.NotSupported|The specified instance must be IoOptimized instance when kmsKeyId is not empty.|The error message returned because I/O optimized instances must be used after the KMSKeyId parameter is specified.|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|The error message returned because the customer master key \(CMK\) is not enabled when a KMS key ID is specified for a disk. You can call the DescribeKey operation of KMS to query information about the specified CMK.|
|404|InvalidParameter.KMSKeyId.NotFound|The specified KMSKeyId does not exist.|The error message returned because the specified DataDisk.N.KMSKeyId parameter does not exist.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because ECS is not authorized to access your KMS resources.|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|The error message returned because risks are detected in your default credit card or debit card. Click the link in the email for verification.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The error message returned because the specified tag key already exists. Tag keys must be unique.|
|400|JoinedGroupLimitExceed|%s|The error message returned because the maximum number of security groups to which the specified resource can belong has been reached. For more information, see the return value of the %s placeholder in the error message.|
|404|InvalidSecurityGroupId.NotFound|%s|The error message returned because the specified SecurityGroupId parameter does not exist.|
|404|InvalidDiskIds.NotPortable|The specified DiskId is not portable.|The error message returned because the specified disk is not removable.|
|403|QuotaExceed.Tags|%s|The error message returned because the maximum number of tags has been reached.|
|403|QuotaExceed.ElasticQuota|No additional quota is available for the specified ECS instance type.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of vCPUs for all instance types has been reached. You can go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type, or the number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of instances of the specified instance type that can be created in the current region has been reached, or because the maximum number of vCPUs for all instance types has been reached. Go to the ECS console or Quota Center to request a quota increase.|
|400|InvalidHttpEndpoint.NotSupported|The specified HttpEndpoint not supported, you can use enabled\(default\) or disabled.|The error message returned because the specified HttpEndpoint parameter is invalid. Valid values of this parameter are enabled and disabled. The default value is enabled.|
|400|InvalidHttpTokens.NotSupported|The specified HttpTokens not supported, you can use optional\(default\) or required.|The error message returned because the specified HttpTokens parameter is invalid. Valid values of this parameter are optional and required. The default value is optional.|
|400|InvalidHttpPutResponseHopLimit.NotSupported|The specified HttpPutResponseHopLimit not supported, more than 1 and less than 64 is reasonable.|The error message returned because the specified HttpPutResponseHopLimit parameter is invalid. Valid values of this parameter are 1 to 64.|
|400|InvalidOperation.VpcHasEnabledAdvancedNetworkFeature|The specified vpc has enabled advanced network feature.|The error message returned because the specified VPC has advanced features enabled. You cannot create instances that have low specifications in the VPC.|
|403|InvalidOperation.ResourceManagedByCloudProduct|%s|The error message returned because the security groups managed by cloud services cannot be modified.|
|403|InvalidParameter.InvalidEniQueueNumber|%s|The error message returned because the NetworkInterface.N.QueueNumber parameter is invalid. For more information, see the return value of the %s placeholder in the error message.|
|403|InvalidOperation.MaxEniQueueNumberExceeded|%s|The error message returned because the maximum number of queues per ENI has been reached. For more information, see the return value of the %s placeholder in the error message.|
|403|InvalidOperation.ExceedInstanceTypeQueueNumber|%s|The error message returned because the maximum number of queues for all ENIs bound to an instance has been reached. For more information, see the return value of the %s placeholder in the error message.|
|400|MissingParameter.PrivatePoolOptionsId|The specified PrivatePoolOptions.Id should not be null.|The error message returned because the PrivatePoolOptions.Id parameter is not specified.|
|400|Invalid.PrivatePoolOptionsId|The specified PrivatePoolOptions.Id is invalid.|The error message returned because the specified PrivatePoolOptions.Id parameter is invalid.|
|400|Invalid.PrivatePoolOptionsId|The parameter PrivatePoolOptions.Id should be null when PrivatePoolOptions.MatchCriteria is not Target.|The error message returned because the PrivatePoolOptions.Id parameter is specified when the PrivatePoolOptions.MatchCriteria parameter is set to Open or None.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

