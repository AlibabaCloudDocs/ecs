# CreateInstance

You can call this operation to create a subscription or pay-as-you-go ECS instance.

## Description

**Note:** You can call the [DescribeAvailableResource](~~66186~~) operation to query available instance resources in a specific region or zone. If you want to create multiple instances at a time that automatically enter the Running state after they are created, we recommend that you call the [RunInstances](~~63440~~) operation.

When you create an ECS instance, take note of the following items:

-   **Billing**:
    -   You must fully understand the ECS billing methods before you create an instance, because you may be charged for resources used by the instance. For more information, see [Billing overview](~~25398~~).
    -   If you create a subscription instance \(`PrePaid`\), available coupons in your account are used by default.
-   **Instance type**:
    -   You can use the `IoOptimized` parameter to specify whether to create an I/O optimized instance.
    -   Select an appropriate instance type: For the performance data about instance types, see [Instance families](~~25378~~) or call the [DescribeInstanceTypes](~~25620~~) operation. You can also see [Best practices for instance type selection](~~58291~~) to learn how to select instance types.
    -   Query available resources: You can call the [DescribeAvailableResource](~~66186~~) operation to query available resources in a specific region or zone.

**Note:** If the `QuotaExceed.ElasticQuota` error is returned when you create an instance, the maximum number of instances of the specified instance type in the current region has been reached, or the maximum number of vCPUs for all instance types has been reached. You can go to the [ECS console](https://ecs.console.aliyun.com/?spm=a2c8b.12215451.favorites.decs.5e3a336aMGTtzy#/privileges/quota) or [Quota Center](https://quotas.console.aliyun.com/products/ecs/quotas) to request a quota increase.

-   **Image**:
    -   The image determines the system disk configurations of the instance. The system disk of the new instance is a clone of the specified image.
    -   If the instance memory size is 512 MiB, you cannot use Windows Server images except for Windows Server Semi-Annual Channel images.
    -   If the instance memory size is 4 GiB or larger, you cannot use 32-bit OS images.
-   **Network type**:
    -   Each VPC-type instance must be connected to only one vSwitch.
    -   If `VSwitchId` is specified, the security group specified by `SecurityGroupId` and the vSwitch specified by `VSwitchId` must belong to the same VPC.
    -   The value of `PrivateIpAddress` depends on the value of `VSwitchId` and cannot be specified separately.`` If you specify both `VSwitchId` and `PrivateIpAddress`, the IP address specified by `PrivateIpAddress` must be available in the CIDR block of the specified vSwitch.
-   **Public bandwidth**:
    -   As of November 27, 2020, the maximum bandwidth available for you to create ECS instances or change the configurations of ECS instances is subject to the throttling policy in your account. To increase the maximum bandwidth value, submit a ticket. According to the throttling policy, the total maximum bandwidth of all instances whose billing method for network usage is pay-by-traffic cannot exceed 5 Gbit/s and that of all instances whose billing method for network usage is pay-by-bandwidth cannot exceed 50 Gbit/s in a single region.
    -   If you call the `CreateInstance` operation to create an instance, no public IP address is assigned to the instance. You can call the [AllocatePublicIpAddress](~~25544~~) operation to allocate public IP addresses manually.
    -   Bandwidth fees are determined based on the settings of `InternetChargeType` and `InternetMaxBandwidthOut`.
    -   The `InternetMaxBandwidthIn` value is irrelevant to billing because inbound data traffic is free of charge.
    -   If `InternetChargeType` is set to PayByBandwidth, `InternetMaxBandwidthOut` specifies the bandwidth value.
    -   If `InternetChargeType` is set to PayByTraffic, `InternetMaxBandwidthOut` specifies the maximum bandwidth value. Actual costs are calculated based on the network traffic.
-   **Security group**:
    -   If no security group is available in the region where you want to create an instance, you must call the [CreateSecurityGroup](~~25553~~) operation to create a security group in that region first.
    -   The maximum number of instances that a security group can contain depends on the security group type. For more information, see the "Security group limits" section of the [Limits](~~25412~~) topic.
    -   Instances in the same security group can communicate with each other over the internal network. By default, instances in different security groups cannot communicate with each other. However, you can allow communication between instances by authorizing mutual access between their security groups. For more information, see [AuthorizeSecurityGroup](~~25554~~) and [AuthorizeSecurityGroupEgress](~~25560~~).
-   **Storage**:
    -   The instance is assigned a system disk whose capacity is based on the image you specified. The capacity of the system disk must be at least `20 GiB and greater than or equal to the size of the image`. For more information about system disk categories, see the description of the `SystemDisk.Category` parameter.
    -   The system disk of an I/O optimized instance can only be an enhanced SSD \(ESSD\) \(`cloud_essd`\), a standard SSD \(`cloud_ssd`\), or an ultra disk \(`cloud_efficiency`\).
    -   The maximum capacity of data disks varies based on their categories. For more information, see the description of the `DataDisk.N.Size` parameter.
    -   A maximum of 16 data disks can be attached to each instance. The mount points of data disks are allocated by the system in alphabetical order from /dev/xvdb to /dev/xvdz.
-   **User data**: If the instance type supports user data, you can use the UserData parameter to pass in user data. For more information, see [Prepare user data](~~49121~~). User data is encoded in Base64. We recommend that you do not pass in confidential information such as passwords or private keys in plaintext. This is because the system does not encrypt `UserData` values when API requests are transferred. If you must pass in confidential information, we recommend that you encrypt and encode the user data in Base64, and then decode and decrypt it in the same way within the instance.
-   **Others**: When you call API operations by using Alibaba Cloud Command Line Interface \(CLI\) and SDKs, you must delete periods \(.\) from request parameters before you use them. For example, use `SystemDiskCategory` instead of `SystemDisk.Category` as a request parameter.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateInstance&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateInstance|The operation that you want to perform. Set the value to CreateInstance. |
|InstanceType|String|Yes|ecs.g6.large|The instance type of the instance.

-   Select an appropriate instance type. For information about the performance data of instance types, see [Instance families](~~25378~~) or call the [DescribeInstanceTypes](~~25620~~) operation. You can also see [Best practices for instance type selection](~~58291~~) to learn how to select instance types.
-   Query available resources. You can call the [DescribeAvailableResource](~~66186~~) operation to query available resources in a specific region or zone. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ImageId|String|No|ubuntu\_18\_04\_64\_20G\_alibase\_20190624.vhd|The ID of the image used to create the instance. If you want to use Alibaba Cloud Marketplace images, you can view `image IDs` on the product pages of Alibaba Cloud Marketplace images. If you do not select the latest available custom image from the image family specified by `ImageFamily`, you must specify ImageId. |
|ImageFamily|String|No|hangzhou-daily-update|The name of the image family. You can set this parameter to select the latest available custom image from the specified image family to create the instance.

-   ImageFamily must be empty if `ImageId` is specified.
-   ImageFamily can be specified if `ImageId` is not specified. |
|SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg\*\*\*\*|The ID of the security group to which to assign the instance. Instances in the same security group can communicate with each other. |
|InstanceName|String|No|2018-12-06T103200Z|The name of the instance. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), periods \(.\). and hyphens \(-\). If you do not specify this parameter, the instance ID is used. |
|InternetChargeType|String|No|PayByTraffic|The billing method for network usage. Default value: PayByTraffic. Valid values:

-   PayByBandwidth
-   PayByTraffic

**Note:** When the **pay-by-traffic** billing method is used, the maximum inbound and outbound bandwidths are both the upper limits of bandwidths and used only for reference. In the event of resource contention, these maximum bandwidths cannot be guaranteed. If you want guaranteed bandwidths for your instances, use the **pay-by-bandwidth** billing method. |
|AutoRenew|Boolean|No|true|Specifies whether to enable auto-renewal for the instance. This parameter takes effect only when the `InstanceChargeType` parameter is set to `PrePaid`. Default value: false. Valid values:

-   true: Auto-renewal is enabled for the instance.
-   false: Auto-renewal is disabled for the instance. |
|AutoRenewPeriod|Integer|No|2|The auto-renewal period of the instance. This parameter is required when AutoRenew is set to true.

Valid values when PeriodUnit is set to Month: 1, 2, 3, 6, and 12. |
|InternetMaxBandwidthIn|Integer|No|50|The maximum inbound public bandwidth. Unit: Mbit/s. Valid values:

-   When the purchased outbound public bandwidth is less than or equal to 10 Mbit/s, valid values are 1 to 10 and the default value is 10.
-   When the purchased outbound public bandwidth is greater than 10, valid values are 1 to the value of `InternetMaxBandwidthOut` and the default value is the value of `InternetMaxBandwidthOut`. |
|InternetMaxBandwidthOut|Integer|No|5|The maximum outbound bandwidth for the public network. Unit: Mbit/s. Valid values: 0 to 100

Default value: 0. |
|HostName|String|No|LocalHostName|The hostname of the instance.

-   The hostname cannot start or end with a period \(,\) or a hyphen \(-\). It cannot contain consecutive periods \(,\) or hyphens \(-\).
-   For a Windows instance, the hostname must be 2 to 15 characters in length and can contain letters, digits, and hyphens \(-\). It cannot contain periods \(.\) or contain only digits.
-   For an instance that runs one of other operating systems such as Linux, the hostname must be 2 to 64 characters in length. You can use periods \(.\) to separate the hostname into multiple segments. Each segment can contain letters, digits, and hyphens \(-\). |
|Password|String|No|TestEcs123!|The password of the instance. The password must be 8 to 30 characters in length. It must include at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include

```

( ) ` ~ ! @ # $ % ^ & * - _ + = | { } [ ] : ; ' < > , . ? /
                                
```

For a Windows instance, the password cannot start with a forward slash \(/\).

**Note:** If the `Password` parameter is specified, we recommend that you send requests over HTTPS to avoid password leaks. |
|PasswordInherit|Boolean|No|false|Specifies whether to use the password preset in the image. If PasswordInherit is set to true, leave Password empty and make sure that the selected image has a password preset. |
|DeploymentSetId|String|No|ds-bp1brhwhoqinyjd6\*\*\*\*|The ID of the deployment set. |
|ZoneId|String|No|cn-hangzhou-g|The zone ID of the instance. You can call the [DescribeZones](~~25610~~) operation to query the zone list.

This parameter is empty by default. If you do not specify a zone, the system randomly selects one. |
|ClusterId|String|No|c-bp67acfmxazb4p\*\*\*\*|The ID of the cluster.

**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|VlanId|String|No|10|The ID of the virtual local area network \(VLAN\). |
|InnerIpAddress|String|No|192.168.\*\*. \*\*|The private IP address of the instance. |
|SystemDisk.Size|Integer|No|40|The size of the system disk. Unit: GiB. Valid values: 20 to 500.

The parameter must be at least 20 and equal to or more than the size of the image.

The default value is 40 or the size of the image, depending on whichever is greater. |
|SystemDisk.Category|String|No|cloud\_ssd|The category of the system disk. Valid values:

-   cloud\_essd: ESSD. When the parameter is set to this value, you can use the `SystemDisk.PerformanceLevel` parameter to specify the performance level of the disk.
-   cloud\_efficiency: ultra disk.
-   cloud\_ssd: standard SSD.
-   cloud: basic disk.

For non-I/O optimized instances of retired instance types, the default value is cloud. For other instances, the default value is cloud\_efficiency. |
|SystemDisk.DiskName|String|No|SystemDiskName|The name of the system disk. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

This parameter is empty by default. |
|SystemDisk.Description|String|No|TestDescription|The description of the system disk. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

This parameter is empty by default. |
|SystemDisk.PerformanceLevel|String|No|PL1|The performance level of the ESSD used as the system disk. Default value: PL0. Valid values:

-   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

For more information about ESSD performance levels, see [ESSDs](~~122389~~). |
|DataDisk.N.Size|Integer|No|2000|The size of data disk N. Valid values of N: 1 to 16. Unit: GiB. Valid values:

-   Valid values when DataDisk.N.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_ssd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_essd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud: 5 to 2000

The value of this parameter must be greater than or equal to the size of the snapshot specified by the `SnapshotId` parameter. |
|DataDisk.N.SnapshotId|String|No|s-bp17441ohwka0yuh\*\*\*\*|The ID of the snapshot used to create data disk N. Valid values of N: 1 to 16.

-   When the `DataDisk.N.SnapshotId` parameter is specified, the `DataDisk.N.Size` parameter is ignored. The data disk is created based on the size of the specified snapshot.
-   Use snapshots created after July 15, 2013. Otherwise, an error is returned and your request is rejected. |
|DataDisk.N.Category|String|No|cloud\_ssd|The category of data disk N. Valid values:

-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: ESSD
-   cloud: basic disk

For I/O optimized instances, the default value is cloud\_efficiency. For non-I/O optimized instances, the default value is cloud. |
|DataDisk.N.DiskName|String|No|DataDiskName|The name of data disk N. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

This parameter is empty by default. |
|DataDisk.N.Description|String|No|TestDescription|The description of data disk N. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

This parameter is empty by default. |
|DataDisk.N.Device|String|No|null|The mount point of data disk N.

**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|DataDisk.N.DeleteWithInstance|Boolean|No|true|Specifies whether to release data disk N when the instance is released.

Default value: true |
|DataDisk.N.Encrypted|Boolean|No|false|Specifies whether to encrypt data disk N.

Default value: false. |
|DataDisk.N.KMSKeyId|String|No|0e478b7a-4262-4802-b8cb-00d\*\*\*\*|The ID of the KMS key to be used by data disk N. |
|DataDisk.N.PerformanceLevel|String|No|PL2|The performance level of the ESSD used as data disk N. The N value must be the same as that in DataDisk.N.Category when `DataDisk.N.Category` is set to cloud\_essd. Default value: PL1. Valid values:

-   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

For more information about ESSD performance levels, see [ESSDs](~~122389~~). |
|Description|String|No|InstanceTest|The description of the instance. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

This parameter is empty by default. |
|VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws0\*\*\*\*|The ID of the vSwitch. This parameter is required when you create a VPC-type instance. |
|PrivateIpAddress|String|No|172.16.236.\*|The private IP address to be assigned to the instance. The private IP address must be an available IP address in the CIDR block of the vSwitch. |
|IoOptimized|String|No|optimized|Specifies whether the instance is I/O optimized. Valid values:

-   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized.

For retired instance types, the default value is none. For more information, see [Retired instance types](~~55263~~).

For other instance types, the default value is optimized. |
|UseAdditionalService|Boolean|No|true|Specifies whether to use the virtual machine system configuration provided by Alibaba Cloud \(Windows: NTP and KMS. Linux: NTP and YUM\). |
|InstanceChargeType|String|No|PrePaid|The billing method of the instance. Default value: PostPaid. Valid values:

-   PrePaid: subscription. If you set this parameter to PrePaid, make sure that you have sufficient balance or credit in your payment account. Otherwise, an `InvalidPayMethod` error is returned.
-   PostPaid: pay-as-you-go. |
|Period|Integer|No|1|The subscription period of the instance. The unit is specified by the `PeriodUnit` parameter. This parameter is valid and required only when `InstanceChargeType` is set to `PrePaid`. If the `DedicatedHostId` parameter is specified, the subscription period of the instance cannot be longer than that of the dedicated host. Valid values:

-   Valid values when PeriodUnit is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60. |
|PeriodUnit|String|No|Month|The unit of the subscription period. Default value: Month.

Set the value to Month. |
|Tag.N.value|String|No|null|The value of the tag N.

**Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Value parameter to ensure compatibility. |
|Tag.N.key|String|No|null|The key of the tag N.

**Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Key parameter to ensure compatibility. |
|Tag.N.Key|String|No|TestKey|The key of tag N to be bound to the instance, disks, and primary ENI. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. |
|Tag.N.Value|String|No|TestValue|The value of tag N to be bound to the instance, disks, and primary ENI. Valid values of N: 1 to 20. The tag value can be an empty string. The tag value can be up to 128 characters in length and cannot contain http:// or https://. It cannot start with acs:. |
|UserData|String|No|ZWNobyBoZWxsbyBlY3Mh|The user data of the instance. User data must be encoded in Base64. The maximum size of raw data is 16 KB. |
|SpotStrategy|String|No|NoSpot|The preemption policy for a pay-as-you-go instance. This parameter takes effect only when the `InstanceChargeType` parameter is set to `PostPaid`. Default value: NoSpot. Valid values:

-   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances that have maximum hourly prices.
-   SpotAsPriceGo: applies to pay-as-you-go instances that are of the market price at the time of purchase. |
|KeyPairName|String|No|KeyPairTestName|The name of the key pair to be bound to the instance.

-   For Windows instances, this parameter is ignored and is empty by default. The `Password` parameter takes effect even if the KeyPairName parameter is specified.
-   For Linux instances, the username and password authentication method is disabled by default. To make the instances more secure, we recommend that you use key pairs for logons. |
|SpotPriceLimit|Float|No|0.98|The maximum hourly price of the instance. This parameter takes effect only when `SpotStrategy` is set to `SpotWithPriceLimit`. A maximum of three decimal places are allowed. |
|SpotDuration|Integer|No|1|The retention period of the preemptible instance. Unit: hours. Valid values: 0, 1, 2, 3, 4, 5, and 6.

-   Protection periods of two to six hours are in invitational preview. If you want to set this parameter to one of these values, submit a ticket.
-   If this parameter is set to 0, no protection period is configured for the preemptible instance.

Default value : 1. |
|SpotInterruptionBehavior|String|No|Terminate|The interruption mode of the preemptible instance. Only the Terminate mode is supported, in which the instance is released. Default value: Terminate. |
|RamRoleName|String|No|RAMTestName|The instance RAM role. You can call the [ListRoles](~~28713~~) operation provided by RAM to query the instance RAM roles that you have created. |
|SecurityEnhancementStrategy|String|No|Active|Specifies whether to enable security hardening. Valid values:

-   Active: Security hardening is enabled. This value is applicable to only public images.
-   Deactive: Security hardening is disabled. This value is applicable to all images. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which to assign the instance. |
|HpcClusterId|String|No|hpc-bp67acfmxazb4p\*\*\*\*|The ID of the HPC cluster to which to assign the instance. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Default value: false. Valid values:

-   true: The validity of the request is checked but the request is not made. Check items include the required parameters, request format, service limits, and available ECS resources. If the check fails, the corresponding error code is returned. If the check succeeds, the `DryRunOperation` error code is returned.
-   false: The request is checked, and the instance is created if the check succeeds. |
|DedicatedHostId|String|No|dh-bp67acfmxazb4p\*\*\*\*|The ID of the dedicated host on which to create the instance.

You can call the [DescribeDedicatedHosts](~~134242~~) operation to query the dedicated host list.

When the `DedicatedHostId` parameter is specified, the `SpotStrategy` and `SpotPriceLimit` parameters are ignored. This is because preemptible instances cannot be created on dedicated hosts. |
|CreditSpecification|String|No|Standard|The performance mode of the burstable instance. Valid values:

-   Standard: the standard mode. For more information, see the "Standard mode" section of the [Burstable instances](~~59977~~) topic.
-   Unlimited: the unlimited mode. For more information, see the "Unlimited mode" section of the [Burstable instances](~~59977~~) topic.

This parameter is empty by default. |
|DeletionProtection|Boolean|No|false|The release protection property of the instance. It specifies whether you can use the ECS console or call the [DeleteInstance](~~25507~~) operation to manually release the instance. Default value: false. Valid values:

-   true: Release protection is enabled.
-   false: Release protection is disabled.

**Note:** This parameter takes effect only on pay-as-you-go instances. It can protect instances only against manual releases, not against automatic releases. |
|Affinity|String|No|default|Specifies whether an instance on a dedicated host is associated with the dedicated host. Valid values:

-   default: The instance is not associated with the dedicated host. When the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled and the instance is restarted, the instance is automatically deployed to another dedicated host in the automatic deployment resource pool if resources of the original dedicated host are insufficient.
-   host: The instance is associated with the dedicated host. When the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled and the instance is restarted, the instance still resides on the original dedicated host. If the available resources of the original dedicated host are insufficient, the instance fails to restart.

Default value: default. |
|Tenancy|String|No|default|Specifies whether to create the instance on a dedicated host. Valid values:

-   default: The instance is created on a non-dedicated host.
-   host: The instance is created on a dedicated host. If you do not specify the `DedicatedHostId` parameter, Alibaba Cloud automatically selects a dedicated host for the instance.

Default value: default. |
|StorageSetId|String|No|ss-bp1j4i2jdf3owlhe\*\*\*\*|The ID of the storage set. |
|StorageSetPartitionNumber|Integer|No|2|The maximum number of partitions in the storage set. Valid values: greater than or equal to 2. |
|HttpEndpoint|String|No|enabled|Specifies whether to enable the access channel for the instance metadata. Valid values:

-   enabled
-   disabled

Default value: enabled.

**Note:** For more information about instance metadata, see [Overview](~~49122~~). |
|HttpTokens|String|No|optional|Specifies whether to forcibly use the security-enhanced mode \(IMDSv2\) to access instance metadata. Valid values:

-   optional: The security-enhanced mode \(IMDSv2\) is not forcibly used.
-   required: The security-enhanced mode \(IMDSv2\) is forcibly used. After you set this parameter to required, you cannot access the instance metadata in normal mode.

Default value: optional.

**Note:** For more information about the modes of accessing instance metadata, see [Access mode of instance metadata](~~150575~~). |
|PrivatePoolOptions.MatchCriteria|String|No|Open|The type of the private pool. After an elasticity assurance or capacity reservation takes effect, a private pool is generated. You can select a private pool when you create an instance. Valid values:

-   Open: The system automatically matches a private pool of the Open type for the instance to start up. If no matching private pools exist, the instance takes up capacity of public pool resources. If the parameter is set to Open, the `PrivatePoolOptions.Id` parameter must be empty.
-   Target: The instance takes up capacity of a specific private pool to start up. If the specified private pool is unavailable, the instance fails to start up. If the parameter is set to Target, the `PrivatePoolOptions.Id` parameter must be specified.
-   None: The instance does not take up capacity of a private pool to start up.

This parameter is empty by default.

In the following scenarios, the PrivatePoolOptions.MatchCriteria parameter can only be set to `None` or left empty:

-   The instance is a preemptible instance.
-   The instance is in the classic network.
-   The instance is created on a dedicated host.

**Note:** This parameter is in invitational preview. For more information, submit a ticket. |
|PrivatePoolOptions.Id|String|No|eap-bp67acfmxazb4\*\*\*\*|The ID of the private pool. The value of this parameter indicates the ID of the elasticity assurance or capacity reservation that generates the private pool.

**Note:** This parameter is in invitational preview. For more information, submit a ticket. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|OrderId|String|1234567890|The ID of the order. This parameter is returned only when `InstanceChargeType` is set to PrePaid. |
|TradePrice|Float|0.165|The transaction price. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateInstance
&RegionId=cn-hangzhou
&ImageId=ubuntu_18_04_64_20G_alibase_20190624.vhd
&SecurityGroupId=sg-bp15ed6xe1yxeycg****
&HostName=LocalHostName
&InstanceType=ecs.g6.large
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateInstanceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <InstanceId>i-bp67acfmxazb4p****</InstanceId>
      <OrderId>1234567890</OrderId>
      <TradePrice>0.165</TradePrice>
</CreateInstanceResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "InstanceId": "i-bp67acfmxazb4p****",
    "OrderId": "1234567890",
    "TradePrice": "0.165"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|The error message returned because you are not authorized to use the specified instance type.|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|The error message returned because the specified InternetChargeType parameter is invalid.|
|400|InvalidParameter|The specified parameter "InternetMaxBandwidthOut" is not valid.|The error message returned because the specified InternetMaxBandwidthOut parameter is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter " SystemDisk.Category " is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|404|IoOptimized.NotSupported|The specified instancetype is not support IoOptimized instance|The error message returned because the specified instance type does not support I/O optimization.|
|400|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned because the specified DataDisk.N.Size parameter is invalid or the snapshot size exceeds the maximum capacity that is allowed for the specified disk category.|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not support the specified instance type.|The error message returned because the specified disk category does not support the instance type.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned because the specified instance type does not exist or you are not authorized to manage the instance type.|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|The error message returned because the specified security group does not exist in this account. Check whether the security group ID is correct.|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|The error message returned because the specified Description parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|The error message returned because the specified HostName parameter is invalid.|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|The error message returned because the specified Password parameter is invalid.|
|400|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|The error message returned because the Password parameter is specified when PasswdInherit is set to true.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|400|InvalidDiskName.Malformed|The specified parameter "SystemDisk.DiskName or DataDisk.n.DiskName" is not valid.|The error message returned because the specified SystemDisk.DiskName or DataDisk.N.DiskName parameter is invalid.|
|400|InvalidDiskDescription.Malformed|The specified parameter "SystemDisk.DiskDescription" or "DataDisk.n.Description" is not valid.|The error message returned because the specified SystemDisk.Description or DataDisk.N.Description parameter is invalid.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.n.Category" is not valid.|The error message returned because the specified DataDisk.N.Category parameter is invalid.|
|404|InvalidDataDiskSnapshotId.NotFound|The specified parameter "DataDisk.n.SnapshotId" is not valid.|The error message returned because the specified DataDisk.N.SnapshotId parameter is invalid.|
|400|InvalidDataDevice.Malformed|The specified parameter "DataDisk.n.Device" is not valid.|The error message returned because the specified DataDisk.N.Device parameter is invalid.|
|400|InvalidNodeControllerId.Malformed|The specified parameter "NodeControllerId" is not valid.|The error message returned because the specified NodeControllerId parameter is invalid.|
|400|InvalidInnerIpAddress.Malformed|The specified parameter "InnerIpAddress" is not valid.|The error message returned because the specified InnerIpAddress parameter is invalid.|
|400|InvalidInnerIpAddress.Unusable|The specified InnerIpAddress is already used or not found in usable ip range.|The error message returned because the specified internal IP address is unavailable.|
|400|OperationDenied|The specified parameter "VlanId" is not valid or vlan has not enough IP address.|The error message returned because the specified VlanId parameter is invalid or no more IP addresses are available in the specified VLAN.|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|The error message returned because the specified image does not support the specified instance type.|
|400|ImageNotSupportCloudInit|The specified image does not support cloud-init.|The error message returned because the specified image does not support cloud-init.|
|400|InvalidSnapshotId.BasedSnapshotTooOld|The specified snapshot is created before 2013-07-15.|The error message returned because the specified snapshot was created before July 15, 2013.|
|400|QuotaExceed.AfterpayInstance|The maximum number of Pay-As-You-Go instances is exceeded: %s|The error message returned because the pay-as-you-go instances of the specified instance type are insufficient. Reduce the number of instances to be created.|
|403|ImageNotSubscribed|The specified image has not be subscribed.|The error message returned because you have not subscribed to the specified Alibaba Cloud Marketplace image.|
|400|InvalidMarketImageChargeType.NotSupport|The specified chargeType of marketImage is unsupported.|The error message returned because the billing method of the Alibaba Cloud Marketplace image is not supported.|
|403|OperationDenied|The specified Image is disabled or is deleted.|The error message returned because the specified image has been disabled or deleted.|
|403|InvalidSystemDiskCategory.ValueUnauthorized|The disk category is not authorized.|The error message returned because you are not authorized to use the specified disk category.|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|The error message returned because the specified snapshot is being created.|
|403|OperationDenied|The specified snapshot is not allowed to create disk.|The error message returned because the specified snapshot cannot be used to create disks.|
|403|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|The error message returned because the total size of the specified disks exceeds the maximum capacity that is allowed for the disk category.|
|403|InvalidDevice.InUse|The specified device has been occupied.|The error message returned because the specified device already has a disk attached.|
|403|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|The error message returned because the specified Alibaba Cloud Marketplace image is unavailable, or the specified custom image contains the product code of the Alibaba Cloud Marketplace image from which the custom image is derived and the Alibaba Cloud Marketplace image has been removed from Alibaba Cloud Marketplace.|
|404|InvalidClusterId.NotFound|The ClusterId provided does not exist in our records.|The error message returned because the specified ClusterId parameter does not exist.|
|403|OperationDenied|The creation of Instance to the specified Zone is not allowed.|The error message returned because instances cannot be created in the specified zone.|
|403|CategoryNotSupported|The specified zone does not offer the specified disk category.|The error message returned because the specified disk category is unavailable in the specified zone.|
|403|OperationDenied|The specified Zone or cluster does not offer the specified disk category or the speicified zone and cluster do not match.|The error message returned because the specified disk category is unavailable in the specified zone or cluster, or because the specified zone and cluster do not correspond to each other.|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|The error message returned because resources are insufficient in the specified zone.|
|400|InvalidInstanceName.Malformed|The specified parameter "InstanceName" is not valid.|The error message returned because the specified InstanceName parameter is invalid. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.|
|400|InvalidDiskDescription.Malformed|The specified parameter "SystemDisk.DiskDescription or DataDisk.n.Description" is not valid.|The error message returned because the specified SystemDisk.Description or DataDisk.N.Description parameter is invalid.|
|403|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|The error message returned because the maximum number of removable disks has been reached.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|OperationDenied|Sales of this resource are temporarily suspended in the specified region; please try again later.|The error message returned because the requested resource is unavailable in the specified region. Try again later.|
|400|InvalidParameter.Conflict|The specified region and cluster do not match.|The error message returned because the specified region and cluster do not correspond to each other.|
|403|SecurityGroupInstanceLimitExceed|The maximum number of instances in a security group is exceeded.|The error message returned because the maximum number of instances in the specified security group has been reached.|
|403|NodeControllerUnavailable|The Node Controller is temporarily unavailable.|The error message returned because the node controller is currently unavailable.|
|403|RegionUnauthorized|There is no authority to create instance in the specified region.|The error message returned because you are not authorized to create instances in the specified region.|
|403|CategoryNotSupported|The specified Zone or cluster does not offer the specified disk category.|The error message returned because the specified disk category is unavailable in the specified zone or cluster.|
|403|InvalidSnapshotId.NotDataDiskSnapshot|The specified snapshot is system disk snapshot.|The error message returned because the specified snapshot is a system disk snapshot.|
|403|CategoryNotSupported|The specified cluster does not offer the specified disk category.|The error message returned because the specified disk category is unavailable in the specified cluster.|
|404|InvalidVSwitchId.NotFound|Specified virtual switch does not exist.|The error message returned because the specified VSwitchId parameter does not exist.|
|400|InvalidParameter.Mismatch|Specified security group and virtual switch are not in the same VPC.|The error message returned because the specified security group and vSwitch do not belong to the same VPC.|
|400|InvalidNetworkType.Mismatch|Specified parameter "InternetChargeType" conflict with instance network type.|The error message returned because the network type of the instance does not support the specified billing method for network usage.|
|400|InvalidPrivateIpAddress|Specified private IP address is not in the CIDR block of virtual switch.|The error message returned because the specified private IP address is not within the CIDR block of the vSwitch.|
|400|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicated.|The error message returned because the specified private IP address has been used. Change the IP address and try again.|
|400|QuotaExceeded.PrivateIpAddress|Don't have enough private IPs in this switch|The error message returned because all the private IP addresses on the vSwitch are already in use. Try another vSwitch.|
|400|QuotaExceeded|Living instances quota exceeded in this VPC.|The error message returned because the maximum number of active instances has been reached.|
|400|IncorrectVSwitchStatus|The current status of virtual switch does not support this operation.|The error message returned because the specified vSwitch is in the Pending state and cannot be deleted.|
|400|InvalidParameter.Mismatch|Specified virtual switch is not in the specified zone.|The error message returned because the specified vSwitch does not exist in the specified zone.|
|400|ResourceNotAvailable|Resource you requested is not available in this region or zone.|The error message returned because VPC is not supported by the specified region or zone.|
|400|MissingParameter|The input parameter "VSwitchId" that is mandatory for processing this request is not supplied.|The error message returned because the VSwitchId parameter is not specified.|
|400|InvalidDiskCategory.Mismatch|The specified disk categories' combination is not supported.|The error message returned because the combination of the specified disk categories is not supported.|
|403|DeleteWithInstance.Conflict|The specified disk is not a portable disk and cannot be set to DeleteWithInstance attribute.|The error message returned because the specified disk is not removable and cannot be released along with the instance.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned because the specified image does not exist in this account. Check whether the image ID is correct.|
|403|InstanceDiskNumLimitExceed|The number of specified disk in an instance exceeds.|The error message returned because the maximum number of disks that can be attached to the instance has been reached.|
|403|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|The error message returned because the specified image does not support I/O optimized instances.|
|403|ImageNotSupportInstanceType|The specified image don't support the InstanceType instance.|The error message returned because the specified image does not support this instance type.|
|400|InvalidIoOptimizedValue.ValueNotSupported|IoOptimized value not supported.|The error message returned because the specified IoOptimized parameter is invalid.|
|404|OperationDenied|Another Instance has been creating|The error message returned because no new instances can be created.|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot|The error message returned because the capacity of the specified disk is smaller than that of the snapshot.|
|403|OperationDenied|The type of the disk does not support the operation|The error message returned because the operation is not supported by the specified disk category.|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|The error message returned because the specified InstanceChargeType parameter does not exist.|
|400|MissingParamter|The specified parameter "Period" is not null.|The error message returned because the Period parameter is not specified.|
|400|InvalidPeriod|The specified period is not valid.|The error message returned because the specified Period parameter is invalid.|
|403|InvalidDiskCategory.Mismatch|The specified disk categories combination is not supported.|The error message returned because the combination of the specified disk categories is not supported.|
|403|IoOptimized.NotSupported|Vpc is not support IoOptimized instance.|The error message returned because I/O optimized instances are not supported in the VPC.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter " DataDisk.n.Category " is not valid.|The error message returned because the specified DataDisk.N.Category parameter is invalid.|
|400|InstanceDiskCategoryLimitExceed|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned because the specified DataDisk.N.Size parameter is invalid or the snapshot size exceeds the maximum capacity that is allowed for the specified disk category.|
|403|OperationDenied|The resource is out of usage.|The error message returned because the instance is not in the Running state. Start the instance or check whether the operation is valid.|
|403|QuotaExceed.BuyImage|The specified image is from the image market, You have not bought it or your quota has been exceeded.|The error message returned because you have not purchased the specified Alibaba Cloud Marketplace image or your image quota has been used up.|
|404|DependencyViolation.IoOptimized|The specified instancetype must be IoOptimized instance.|The error message returned because the specified instance type is not I/O optimized.|
|404|PaymentMethodNotFound|No payment method has been registered on the account.|The error message returned because you have not configured the payment method for your account.|
|404|HOSTNAME\_ILLEGAL|hostname is not valid.|The error message returned because the specified HostName parameter is invalid.|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|The error message returned because the specified system disk size is smaller than the size of the image.|
|404|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the min size.|The error message returned because the specified system disk size is smaller than the minimum size.|
|404|InvalidSystemDiskSize.MoreThanMaxSize|The specified SystemDisk.Size parameter exceeds the maximum size.|The error message returned because the specified system disk size exceeds the allowed maximum size.|
|404|InvalidDataDiskSnapshotId.NotFound|The specified parameter DataDisk.n.SnapshotId is not valid.|The error message returned because the specified DataDisk.N.SnapshotId parameter is invalid.|
|403|InvalidVSwitchId.NotFound|The VSwitchId provided does not exist in our records.|The error message returned because the specified VSwitchId parameter does not exist.|
|400|InvalidParameter|The specified vm bandwidth is not valid.|The error message returned because the specified bandwidth is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter SystemDisk.Category is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|403|InvalidParameter.ResourceOwnerAccount|ResourceOwnerAccount is Invalid.|The error message returned because the specified ResourceOwnerAccount parameter is invalid.|
|404|InvalidSystemDiskSize|The specified parameter SystemDisk.Size is invalid.|The error message returned because the specified SystemDisk.Size parameter is invalid.|
|400|InvalidParameter.Bandwidth|The specified parameter Bandwidth is not valid.|The error message returned because the specified bandwidth is invalid.|
|400|InvalidIPAddress.AlreadyUsed|The specified IPAddress is already used by other resource.|The error message returned because the specified IP address is being used. Try another one.|
|403|InvalidUserData.Forbidden|User not authorized to input the parameter "UserData", please apply for permission "UserData"|The error message returned because you are not authorized to manage user data. Apply for the permission first.|
|400|InvalidUserData.SizeExceeded|The specified parameter "UserData" exceeds the size.|The error message returned because the maximum size of user data specified by the UserData parameter has been reached.|
|400|InvalidUserData.NotSupported|The specified parameter "UserData" only support the vpc and IoOptimized Instance.|The error message returned because the specified UserData parameter is not supported. UserData is supported only on VPC-type instances and I/O optimized instances.|
|403|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|The error message returned because you are not authorized to purchase resources in the specified zone.|
|403|Zone.NotOnSale|The specified zone is not available for purchase.|The error message returned because the requested resources are unavailable in the specified zone. Change the resource type or select a different zone.|
|403|InvalidClusterId.NotFound|The specified clusterId does not exist.|The error message returned because the specified ClusterId parameter does not exist.|
|403|InvalidInstanceType.ZoneNotSupported|The specified zone does not support this instancetype.|The error message returned because the specified instance type is not supported in the specified zone.|
|400|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|The error message returned because the maximum number of disks that can be attached to the instance has been reached.|
|400|Account.Arrearage|Your account has an outstanding payment.|The error message returned because you have overdue payments in your account.|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|400|InvalidAutoRenewPeriod.ValueNotSupported|The specified autoRenewPeriod is not valid.|The error message returned because the specified AutoRenewPeriod parameter is invalid.|
|400|QuotaExceed.AfterpayInstance|The maximum number of Pay-As-You-Go instances is exceeded.|The error message returned because the pay-as-you-go instances of the specified instance type are insufficient. Reduce the number of instances to be created.|
|400|InvalidSpotStrategy|The specified SpotStrategy is not valid.|The error message returned because the specified SpotStrategy parameter is invalid.|
|400|InvalidSpotParam.EmptyZoneID|The specified ZoneId is empty when SpotStrategy is set.|The error message returned because the ZoneId parameter is not specified while the SpotStrategy parameter is specified.|
|400|InvalidSpotPriceLimit|The specified SpotPriceLimitis not valid.|The error message returned because the specified SpotPriceLimit parameter is invalid.|
|400|InvalidSpotDuration|The specified SpotDuration is not valid.|The error message returned because the specified SpotDuration parameter is invalid.|
|400|InvalidSpotAuthorized|The specified Spot param is unauthorized.|The error message returned because you are not authorized to set SpotDuration to a value in the range of 2 to 6.|
|400|InvalidSpotPrepaid|The specified Spot type is not support PrePay Instance.|The error message returned because preemptible instances do not support the subscription billing method.|
|400|InvalidSpotAliUid|The specified UID is not authorized to use SPOT instance.|The error message returned because you are not authorized to create preemptible instances.|
|403|InvalidPayMethod|The specified pay method is not valid.|The error message returned because the specified payment method is invalid.|
|403|OperationDenied.ImageNotValid|The specified Image is disabled or is deleted.|The error message returned because the specified ImageId parameter does not exist.|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|The error message returned because the specified Tag.N.Key parameter is invalid.|
|400|InvalidParameter.Bandwidth|%s|The error message returned because the specified bandwidth is invalid.|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|The error message returned because the specified DataDisk.N.Category parameter is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|The error message returned because the operation is not supported by the specified system disk category.|
|400|InvalidParameter.Conflict|%s|The error message returned because a specified parameter is invalid. Check whether the parameter conflicts with another parameter.|
|400|InvalidInternetChargeType.ValueNotSupported|%s|The error message returned because the specified InternetChargeType parameter is not supported. Check whether the parameter is correct.|
|400|InvalidInstanceType.ValueNotSupported|%s|The error message returned because this operation cannot be performed on instances of the specified instance type.|
|403|InstanceType.Offline|%s|The error message returned because the operation is not supported when the instance type is retired or resources of the instance type are insufficient.|
|400|RegionUnauthorized|%s|The error message returned because you are not authorized to perform the operation in the specified region.|
|500|InternalError|%s|The error message returned because an internal error has occurred.|
|400|Zone.NotOnSale|%s|The error message returned because the requested resources are unavailable in the specified zone.|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|The error message returned because the specified system disk size is invalid.|
|400|InvalidDataDiskSize.ValueNotSupported|%s|The error message returned because the specified DataDisk.N.Size parameter is invalid.|
|403|DependencyViolation.WindowsInstance|The instance creating is window, cannot use ssh key pair to login.|The error message returned because the specified instance is a Windows instance and does not support logons based on SSH key pairs.|
|400|InvalidInstanceType.ValueNotSupported|The specified parameter "KeyPairName" only support IoOptimized Instance.|The error message returned because non-I/O optimized instances do not support SSH key pairs.|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|The error message returned because you have not completed real-name verification. Complete real-name verification and try again.|
|403|InvalidNetworkType.MismatchRamRole|Ram role cannot be applied to instances of Classic network type.|The error message returned because an instance RAM role can be used only for instances in VPCs, not for instances in the classic network.|
|403|InvalidUser.PassRoleForbidden|The RAM user does not have the privilege to pass a RAM role.|The error message returned because the RAM user is not authorized to pass the RAM role.|
|404|InvalidRamRole.NotFound|The specified RAMRoleName does not exist.|The error message returned because the specified RamRoleName parameter does not exist.|
|400|OperationDenied|The specified InstanceType or Zone is not available or not authorized.|The error message returned because the specified instance type or zone is unavailable or unauthorized.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because you have insufficient balance in your account. Add funds to your account and try again.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|The error message returned because the specified ResourceGroupId parameter does not exist.|
|403|IncorrectVpcStatus|Current VPC status does not support this operation.|The error message returned because the operation is not supported while the VPC is in the current state.|
|400|InvalidParameter.EncryptedIllegal|%s|The error message returned because the specified parameter is invalid. Check whether the encryption is valid.|
|400|InvalidParameter.EncryptedNotSupported|%s|The error message returned because the specified parameter is invalid and your encryption operation is not supported.|
|400|EncryptedOption.Conflict|%s|The error message returned because the specified DataDisk.N.Encrypted parameter is not supported.|
|400|InvalidSpotPriceLimit.LowerThanPublicPrice|The specified parameter "soptPriceLimit" can't be lower than current public price.|The error message returned because the specified value of the SpotPriceLimit parameter is lower than the current market price.|
|400|InvalidHpcClusterId.Unnecessary|The specified HpcClusterId is unnecessary.|The error message returned because the HpcClusterId parameter is specified.|
|400|InvalidVSwitchId.Necessary|The VSwitchId is necessary.|The error message returned because the VSwitchId parameter is not specified.|
|400|InvalidHpcClusterId.Necessary|The HpcClusterId is necessary.|The error message returned because the HpcClusterId parameter is not specified.|
|400|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found.|The error message returned because the specified HpcClusterId parameter does not exist.|
|400|InvalidHpcClusterId.Creating|The specified HpcClusterId is creating.|The error message returned because the specified HPC cluster is being created.|
|400|QuotaExceeded.PrivateIpAddress|Don't have enough private IPs in this switch.|The error message returned because no private IP address is available in the CIDR block of the vSwitch. Try another vSwitch.|
|400|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|The error message returned because the specified PeriodUnit parameter is invalid.|
|400|IncorrectImageStatus|Encrypted snapshots do not support this operation.|The error message returned because the operation is not supported by encrypted snapshots.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The error message returned because the specified Tag.N.Value parameter is invalid.|
|400|InvalidSecurityGroup.NotInDefaultVpc|%s|The error message returned because the specified security group is not in the default VPC. Check whether the specified value of the SecurityGroupId parameter is correct.|
|400|VpcNotFound|Vpc is not found according to the specified VSwitch or the vpc does not belong to you.|The error message returned because the specified vSwitch does not belong to any VPC, or the corresponding VPC does not belong to you.|
|403|InvalidParameter.NotMatch|%s|The error message returned because a specified parameter is invalid. Check whether the parameter conflicts with another parameter.|
|403|OperationDenied.InvalidNetworkType|%s|The error message returned because the operation is not supported by the specified network type.|
|400|InvalidSpotInterruptionBehavior|%s|The error message returned because the specified SpotInterruptionBehavior parameter is invalid.|
|403|InvalidSpotInterruptionBehavior.ClassicNetworkNotSupport|The specified SpotInterruptionBehavior does not support Classic network Instance.|The error message returned because the operation is not applicable to instances in the classic network.|
|403|InvalidSpotInterruptionBehavior.LocalDiskNotSupport|The specified SpotInterruptionBehavior does not support local disk instance.|The error message returned because the operation is not supported by instances that have local disks attached.|
|400|OperationDenied.IllegalPaymentPolicy|The current payment policy is illegal, please connect your service provider to authenticate relative agreement.|The error message returned because the current payment policy is invalid. Contact your service provider for authentication.|
|400|InvalidDeploymentOnHost|%s|The error message returned because the instance cannot be deployed in the specified deployment set.|
|400|InvalidInstanceChargeType.NotSupport|The Dedicated host not support the specified Instance charge type.|The error message returned because the dedicated host does not support instances that use the specified billing method.|
|400|InvalidNetworkType.NotSupported|The classic networkType not support create ECS on dedicatedHost|The error message returned because the dedicated host does not support instances in the classic network.|
|400|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|The error message returned because the specified DedicatedHostId parameter does not exist.|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|The error message returned because the operation is not supported while the dedicated host is in the current state.|
|400|IncorrectDedicatedHostStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed|The error message returned because subscription instances cannot be deployed on pay-as-you-go dedicated hosts.|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|The error message returned because the expiration date of the instance is later than that of the dedicated host.|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorize.|The error message returned because you are not authorized to use the specified instance type.|
|400|DedicatedHostType.Unmatched|The specified DedicatedHostType doesn? t match the instance type.|The error message returned because the specified dedicated host type does not correspond to the specified instance type.|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed.|The error message returned because subscription instances cannot be deployed on pay-as-you-go dedicated hosts.|
|400|InvalidParam.Tenancy|The specified Tenancy is invalid.|The error message returned because the specified Tenancy parameter is invalid.|
|403|OperationDenied.ImageNotValid|%s|The error message returned because the current image does not support the operation.|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|The error message returned because the maximum number of pay-as-you-go disks has been exceeded.|
|403|QuotaExceed.DeploymentSetInstanceQuotaFull|instance quota in one deployment set exceeded.|The error message returned because the maximum number of instances in the current deployment set has been reached.|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|The error message returned because the specified disk category does not support the current operation.|
|400|InvalidParameter.CreditSpecification|The specified CreditSpecification is not supported in this region.|The error message returned because the specified credit policy is not supported in the region.|
|403|OperationDenied.ImageNotValid|the specified image is not published in the region.|The error message returned because the specified image is not available in the current region.|
|403|OperationDenied.ImageNotValid|the specified image is not found in marketplace.|The error message returned because the specified image does not exist in Alibaba Cloud Marketplace.|
|404|InvalidMarketImage.NotFound|The specified marketplace image does not exist, please change the imageId and try again.|The error message returned because the specified Alibaba Cloud Marketplace image does not exist. Modify the parameter value and try again later.|
|400|InvalidInstanceType.NotSupported|The specified instanceType is not supported by the deployment set.|The error message returned because the specified instance type is not supported by the current deployment set. Try another instance type.|
|400|InvalidVpcZone.NotSupported|Zone of the specified VSwitch is not available for creating, please try in other zones.|The error message returned because the default vSwitch cannot be created in the specified zone. Try another zone.|
|400|IncorrectDefaultVpcStatus|The status of the default VPC is invalid.|The error message returned because the status of the default VPC is invalid.|
|404|DeploymentSet.NotFound|The specified deployment set does not exist.|The error message returned because the specified DeploymentSetId parameter does not exist.|
|403|OperationDenied.LocalDiskUnsupported|The configuration change is not allowed when the specified instance has local disks mounted.|The error message returned because the instance types of instances that have local disks attached cannot be changed.|
|403|OperationDenied.InconsistentNetwork|The specified security group and vswitch are not in the same vpc.|The error message returned because the specified security group and vSwitch do not belong to the same VPC.|
|403|OperationDenied|If the network segment of the vswitch is the same as that of its VPC. Therefore, the VPC cannot create other vswitchs across the region.|The error message returned because the VPC and vSwitch have the same CIDR block and no additional vSwitches can be created for other zones of this VPC.|
|403|DefaultVswitch.Existed|The default vswitch for VPC already exists.|The error message returned because a default vSwitch already exists in the current VPC.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|CategoryViolation|The specified instance does not support this operation because of its disk category.|The error message returned because the configurations of instances that have local disks attached cannot be upgraded or downgraded.|
|403|ResourcesNotInSameZone|The specified instance and dedicated host are not in the same zone.|The error message returned because the specified instance and the dedicated host are not in the same region.|
|403|InvalidRegion.NotSupport|The specified region does not support byok.|The error message returned because the bring your own key \(BYOK\) feature is not supported in this region.|
|403|UserNotInTheWhiteList|The user is not in byok white list.|The error message returned because you are not in the BYOK whitelist. Try again when you are in the whitelist.|
|400|InvalidParameter.EncryptedIllegal|The specified parameter Encrypted must be true when kmsKeyId is not empty.|The error message returned because the encryption feature is not enabled after a KMS key ID is specified.|
|400|IoOptimized.NotSupported|The specified instance must be IoOptimized instance when kmsKeyId is not empty.|The error message returned because I/O optimized instances are not used after a KMS key ID is specified.|
|404|InvalidParameter.KMSKeyId.NotFound|The specified KMSKeyId does not exist.|The error message returned because the specified DataDisk.N.KMSKeyId parameter does not exist.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because ECS is not authorized to access your KMS resources.|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|The error message returned because your default credit card or debit card is exposed to security risks. Click the link in the email for verification.|
|403|InvalidDisk.SystemDiskSize|The specified SystemDiskSize beyond the permitted range.|The error message returned because the maximum size of the specified system disk has been reached.|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|The error message returned because the specified ClientToken parameter is invalid.|
|400|OperationDenied|The current user does not support this operation.|The error message returned because your account does not support this operation.|
|403|InsufficientBalance|Your account does not have enough balance.|The error message returned because you have insufficient balance in your account. Add funds to your account and try again.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The error message returned because the specified tag key already exists. Tag keys must be unique.|
|404|InvalidSecurityGroupId.NotFound|%s|The error message returned because the specified SecurityGroupId parameter does not exist.|
|403|InvalidVSwitchId.IpInvalid|%s|The error message returned because the specified InnerIpAddress parameter is invalid.|
|404|InvalidDiskIds.NotPortable|The specified DiskId is not portable.|The error message returned because the specified disk is not removable.|
|403|QuotaExceed.Tags|%s|The error message returned because the maximum number of tags has been reached.|
|401|InvalidRamRole.NotEcsRole|The specified ram role is not authorized for ecs, please check your role policy.|The error message returned because the specified RAM role is not authorized to use ECS. Check your role policy.|
|403|QuotaExceed.ElasticQuota|No additional quota is available for the specified ECS instance type.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of vCPUs for all instance types has been reached. You can go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type, or the number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of instances of the specified instance type that can be created in the current region has been reached, or because the maximum number of vCPUs for all instance types has been reached. Go to the ECS console or Quota Center to request a quota increase.|
|400|InvalidHttpEndpoint.NotSupported|The specified HttpEndpoint not supported, you can use enabled\(default\) or disabled.|The error message returned because the specified HttpEndpoint parameter is invalid. Set this parameter to enabled \(default value\) or disabled.|
|400|InvalidHttpTokens.NotSupported|The specified HttpTokens not supported, you can use optional\(default\) or required.|The error message returned because the specified HttpTokens parameter is invalid. Set this parameter to optional \(default value\) or required.|
|400|InvalidHttpPutResponseHopLimit.NotSupported|The specified HttpPutResponseHopLimit not supported, more than 1 and less than 64 is reasonable.|The error message returned because the specified HttpPutResponseHopLimit parameter is invalid. The value must be in the range of 1 to 64.|
|400|InvalidPrivateIpAddress.Malformed|Specified private IP address is malformed.|The error message returned because the specified PrivateIpAddress parameter is invalid.|
|400|InvalidOperation.VpcHasEnabledAdvancedNetworkFeature|The specified vpc has enabled advanced network feature.|The error message returned because the specified VPC has advanced features enabled. You cannot create instances that have low specifications in the VPC.|
|400|MissingParameter.PrivatePoolOptionsId|The specified PrivatePoolOptions.Id should not be null.|The error message returned because the PrivatePoolOptions.Id parameter is not specified.|
|400|Invalid.PrivatePoolOptionsId|The specified PrivatePoolOptions.Id is invalid.|The error message returned because the specified PrivatePoolOptions.Id parameter is invalid.|
|400|Invalid.PrivatePoolOptionsId|The parameter PrivatePoolOptions.Id should be null when PrivatePoolOptions.MatchCriteria is not Target.|The error message returned because the PrivatePoolOptions.Id parameter is specified when the PrivatePoolOptions.MatchCriteria parameter is set to Open or None.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

