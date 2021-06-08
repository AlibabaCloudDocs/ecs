# CreateLaunchTemplateVersion

Creates a version for a specific launch template.

## Description

To modify the parameters of a launch template version, you can create another version for the launch template. You can create a maximum of 30 versions for each launch template.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateLaunchTemplateVersion&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateLaunchTemplateVersion|The operation that you want to perform. Set the value to CreateLaunchTemplateVersion. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the launch template. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|LaunchTemplateId|String|No|lt-m5eiaupmvm2op9d\*\*\*\*|The ID of the launch template. For more information, see [DescribeLaunchTemplates](~~73759~~). You must specify `LaunchTemplateId` or `LaunchTemplateName` to determine a launch template. |
|LaunchTemplateName|String|No|testLaunchTemplateName|The name of the launch template. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|VersionDescription|String|No|testVersionDescription|The description of the launch template version. The description must be 2 to 256 characters in length and cannot start with http:// or https://. |
|ImageId|String|No|win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20170915.vhd|The ID of the image. You can call the [DescribeImages](~~25534~~) operation to query the available images. |
|ImageOwnerAlias|String|No|system|The source of the image.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|InstanceType|String|No|ecs.g5.large|The instance type. For more information, see [Instance families](~~25378~~). Alternatively, you can call the [DescribeInstanceTypes](~~25620~~) operation to query the most recent instance type list. |
|SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg\*\*\*\*|The ID of the security group to which to assign the instance. Instances within the same security group can access each other.

 **Note:** You cannot specify both the `SecurityGroupId` and `SecurityGroupIds.N` parameters. |
|VpcId|String|No|vpc-bp12433upq1y5scen\*\*\*\*|The ID of the virtual private cloud \(VPC\). |
|VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws0\*\*\*\*|The ID of the vSwitch to which to connect the instance. This parameter is required if you specify the VpcId parameter. |
|InstanceName|String|No|testInstanceName|The name of the instance. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|Description|String|No|testDescription|The description of the instance. The description must be 2 to 256 characters in length and cannot start with http:// or https://. |
|InternetMaxBandwidthIn|Integer|No|50|The maximum inbound public bandwidth. Unit: Mbit/s. Valid values:

 -   If the purchased outbound public bandwidth is less than or equal to 10 Mbit/s, the valid values of this parameter are 1 to 10, and the default value is 10.
-   If the purchased outbound public bandwidth is greater than 10 Mbit/s, the valid values of this parameter are 1 to the `InternetMaxBandwidthOut` value, and the default value is the `InternetMaxBandwidthOut` value. |
|InternetMaxBandwidthOut|Integer|No|5|The maximum outbound public bandwidth. Unit: Mbit/s. Valid values: 0 to 100. |
|HostName|String|No|testHostName|The hostname of the instance.

 -   The hostname cannot start or end with a period \(.\) or a hyphen \(-\).It cannot contain consecutive periods \(.\) or hyphens \(-\).
-   For a Windows instance, the hostname must be 2 to 15 characters in length and can contain letters, digits, and hyphens \(-\). The hostname cannot contain periods \(.\) or only digits.
-   For an instance that runs an operating system of another type such as Linux, the hostname must be 2 to 64 characters in length. You can use periods \(.\) to separate the hostname into multiple segments. Each segment can contain letters, digits, and hyphens \(-\). |
|ZoneId|String|No|cn-hangzhou-g|The zone ID of the instance. |
|SystemDisk.Category|String|No|cloud\_ssd|The category of the system disk. Valid values:

 -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\) You can use the `SystemDisk.PerformanceLevel` parameter to set the performance level of the ESSD used as the system disk.

 For non-I/O optimized instances of retired instance types, the default value is cloud. For other instances, the default value is cloud\_efficiency. |
|SystemDisk.Size|Integer|No|40|The size of the system disk. Unit: GiB. Valid values: 20 to 500.

 The parameter value must be at least 20 and greater than or equal to the size of the image. |
|SystemDisk.DiskName|String|No|cloud\_ssdSystem|The name of the system disk. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|SystemDisk.Description|String|No|testSystemDiskDescription|The description of the system disk. The description must be 2 to 256 characters in length and cannot start with http:// or https://. |
|SystemDisk.PerformanceLevel|String|No|PL0|The performance level of the ESSD used as the system disk. Default value: PL0. Valid values:

 -   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

 For more information about ESSD performance levels, see [ESSDs](~~122389~~). |
|SystemDisk.DeleteWithInstance|Boolean|No|true|Specifies whether to release the system disk when the instance is released. Valid values:

 -   true: releases the system disk when the instance is released.
-   false: does not release the system disk when the instance is released.

 Default value: true. |
|DataDisk.N.Size|Integer|No|2000|The size of data disk N. Valid values of N: 1 to 16. Unit: GiB. Valid values:

 -   Valid values when DataDisk.N.Category is set to cloud: 5 to 2000
-   Valid values when DataDisk.N.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_ssd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_essd: 20 to 32768

 The value of this parameter must be greater than or equal to the size of the snapshot specified by the `SnapshotId` parameter. |
|DataDisk.N.SnapshotId|String|No|s-bp17441ohwka0yuh\*\*\*\*|The ID of the snapshot used to create data disk N. Valid values of N: 1 to 16. When the `DataDisk.N.SnapshotId` parameter is specified, the `DataDisk.N.Size` parameter is ignored and the data disk is created based on the size of the specified snapshot.

 Use snapshots created after July 15, 2013. Otherwise, an error is returned and your request is rejected. |
|DataDisk.N.Category|String|No|cloud\_ssd|The category of data disk N. Valid values:

 -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: ESSD

 For I/O optimized instances, the default value is cloud\_efficiency. For non-I/O optimized instances, the default value is cloud. |
|DataDisk.N.Encrypted|String|No|false|Specifies whether to encrypt data disk N. |
|DataDisk.N.DiskName|String|No|testDataDiskName|The name of data disk N. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|DataDisk.N.Description|String|No|testDataDiskDescription|The description of data disk N. The description must be 2 to 256 characters in length and cannot start with http:// or https://. |
|DataDisk.N.DeleteWithInstance|Boolean|No|true|Specifies whether to release data disk N when the instance is released. Valid values:

 -   true: releases data disk N when the instance is released.
-   false: does not release data disk N when the instance is released.

 Default value: true. |
|DataDisk.N.PerformanceLevel|String|No|PL1|The performance level of the ESSD used as data disk N. The value of N must be the same as that in DataDisk.N.Category when `DataDisk.N.Category` is set to cloud\_essd. Default value: PL1. Valid values:

 -   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

 For more information about ESSD performance levels, see [ESSDs](~~122389~~). |
|IoOptimized|String|No|optimized|Specifies whether the instance is I/O optimized. Valid values:

 -   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized. |
|NetworkInterface.N.PrimaryIpAddress|String|No|192.168.\*\*.\*\*|The primary private IP address of secondary elastic network interface \(ENI\) N. The value of N in `NetworkInterface.N` cannot be greater than 1. |
|NetworkInterface.N.VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws0\*\*\*\*|The ID of the vSwitch to which to connect secondary ENI N. The instance and the ENI must be located within the same zone of the same VPC, but they can be connected to different vSwitches. The value of N in `NetworkInterface.N` cannot be greater than 1. |
|NetworkInterface.N.SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg\*\*\*\*|The ID of the security group to which to assign secondary ENI N. The security groups of secondary ENI N and of the instance must belong to the same VPC. The value of N in `NetworkInterface.N` cannot be greater than 1.

 **Note:** You cannot specify both the `NetworkInterface.N.SecurityGroupId` and `NetworkInterface.N.SecurityGroupIds.N` parameters. |
|NetworkInterface.N.NetworkInterfaceName|String|No|testNetworkInterfaceName|The name of secondary ENI N. The value of N in `NetworkInterface.N` cannot be greater than 1. |
|NetworkInterface.N.Description|String|No|testNetworkInterfaceDescription|The description of secondary ENI N. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. The value of N in `NetworkInterface.N` cannot be greater than 1. |
|NetworkInterface.N.SecurityGroupIds.N|RepeatList|No|sg-bp67acfmxazb4p\*\*\*\*|The ID of security group N to which to assign secondary ENI N. The security group and secondary ENI N must belong to the same VPC. The valid values of N in `SecurityGroupIds.N` depend on the maximum number of security groups to which an ENI can belong. For more information, see the "Security group limits" section in [Limits](~~25412~~). The value of N in `NetworkInterface.N` cannot be greater than 1.

 **Note:** You cannot specify both the `NetworkInterface.N.SecurityGroupId` and `NetworkInterface.N.SecurityGroupIds.N` parameters. |
|InstanceChargeType|String|No|PrePaid|The billing method of the instance. Valid values:

 -   PrePaid: subscription. If you set this parameter to PrePaid, make sure that your account supports credit payment. Otherwise, an `InvalidPayMethod` error is returned.
-   PostPaid: pay-as-you-go. |
|Period|Integer|No|1|The subscription period of the instance. Unit: months. This parameter is valid and required only when `InstanceChargeType` is set to `PrePaid`. If the DedicatedHostId parameter is specified, the value of Period must not exceed the subscription period of the specified dedicated host. Valid values:

 -   When the `PeriodUnit` parameter is set to Week, the valid values of the Period parameter are 1, 2, 3, and 4.
-   When the `PeriodUnit` parameter is set to Month, the valid values of the Period parameter are 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60. |
|InternetChargeType|String|No|PayByTraffic|The billing method for network usage. Valid values:

 -   PayByBandwidth: pay-by-bandwidth
-   PayByTraffic: pay-by-traffic

 **Note:** When the **pay-by-traffic** billing method is used, the peak inbound and outbound bandwidths are used as upper limits of bandwidths instead of guaranteed performance. When demands exceed resource supplies, these maximum bandwidths may be limited. If you want guaranteed bandwidths for your instances, use the **pay-by-bandwidth** billing method. |
|EnableVmOsConfig|Boolean|No|false|Specifies whether to enable the operating system configuration of the instance. |
|NetworkType|String|No|vpc|The network type of the instance. Valid values:

 -   classic
-   vpc |
|UserData|String|No|ZWNobyBoZWxsbyBl\*\*\*\*|The user data of the instance. User data must be encoded in Base64. The maximum size of raw data is 16 KB. |
|KeyPairName|String|No|testKeyPairName|The name of the key pair.

 -   For Windows instances, this parameter is ignored, and the `Password` parameter is valid even if the KeyPairName parameter is specified.
-   For Linux instances, the password-based logon method is disabled by default. |
|RamRoleName|String|No|testRamRoleName|The name of the instance Resource Access Management \(RAM\) role. You can call the [ListRoles](~~28713~~) operation provided by RAM to query the instance RAM roles that you created. |
|AutoReleaseTime|String|No|2018-01-01T12:05:00Z|The time scheduled for the instance to be automatically released. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

 -   If the value of seconds \(`ss`\) is not `00`, the time is automatically rounded down to the nearest minute based on the value of minutes \(`mm`\).
-   The release time must be at least 30 minutes later than the current time.
-   The release time must be at most three years from the current time. |
|SpotStrategy|String|No|NoSpot|The bidding policy for the pay-as-you-go instance. This parameter is valid only when the `InstanceChargeType` parameter is set to `PostPaid`. Valid values:

 -   NoSpot: The instance is a regular pay-as-you-go instance.
-   SpotWithPriceLimit: The instance is a preemptible instance with a user-defined maximum hourly price.
-   SpotAsPriceGo: The instance is a preemptible instance for which the market price at the time of purchase is automatically used as the bid price. |
|SpotPriceLimit|Float|No|0.97|The maximum hourly price of the instance. A maximum of three decimal places are allowed. |
|SpotDuration|Integer|No|1|The protection period of the preemptible instance. Unit: hours. Valid values: 0, 1, 2, 3, 4, 5, and 6.

 -   Protection periods of 2, 3, 4, 5, and 6 hours are in invitational preview. If you want to set this parameter to one of these values, submit a ticket.
-   If this parameter is set to 0, no protection period is configured for the preemptible instance.

 Default value: 1. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group. |
|SecurityEnhancementStrategy|String|No|Active|Specifies whether to enable security hardening for the operating system. Valid values:

 -   Active: enables security hardening. This value is applicable only to public images.
-   Deactive: does not enable security hardening. This value is applicable to all image types. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the instance, Elastic Block Storage \(EBS\) devices, or primary ENI. Valid values of N: 1 to 5. The tag key cannot be an empty string. It can be up to 64 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the instance, EBS devices, or primary ENI. Valid values of N: 1 to 5. The tag value can be an empty string. It can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. |
|SecurityGroupIds.N|RepeatList|No|sg-bp15ed6xe1yxeycg7\*\*\*\*|The ID of security group N to which to assign the instance. The valid values of N depend on the maximum number of security groups to which an instance can belong. For more information, see the "Security group limits" section in [Limits](~~25412~~).

 **Note:** You cannot specify both the `SecurityGroupId` and `SecurityGroupIds.N` parameters. |
|PrivateIpAddress|String|No|10.1.\*\*.\*\*|The private IP address of the instance.

 To assign a private IP address to a VPC-type ECS instance, make sure that the IP address is an idle IP address within the CIDR block of the vSwitch specified by the `VSwitchId` parameter. |
|DeploymentSetId|String|No|ds-bp1brhwhoqinyjd6\*\*\*\*|The ID of the deployment set. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|LaunchTemplateVersionNumber|Long|2|The version number of the launch template. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateLaunchTemplateVersion
&RegionId=cn-hangzhou
&LaunchTemplateId=lt-m5eiaupmvm2op9d****
&LaunchTemplateName=testLaunchTemplateName
&VersionDescription=testVersionDescription
&ImageId=win2008r2_64_ent_sp1_en-us_40G_alibase_20170915.vhd
&InstanceType=ecs.g5.large
&SecurityGroupId=sg-bp15ed6xe1yxeycg****
&VpcId=vpc-bp12433upq1y5scen****
&VSwitchId=vsw-bp1s5fnvk4gn2tws0****
&InstanceName=testInstanceName
&Description=testDescription
&InternetMaxBandwidthIn=50
&InternetMaxBandwidthOut=5
&HostName=testHostName
&ZoneId=cn-hangzhou-g
&SystemDisk.Category=cloud_ssd
&SystemDisk.Size=40
&SystemDisk.DiskName=testSystemDiskName
&SystemDisk.Description=testSystemDiskDescription
&DataDisk.1.Size=2000
&DataDisk.1.SnapshotId=s-bp17441ohwka0yuh****
&DataDisk.1.Category=cloud_ssd
&DataDisk.1.Encrypted=false
&DataDisk.1.DiskName=cloud_ssdData
&DataDisk.1.Description=testDataDiskDescription
&DataDisk.1.DeleteWithInstance=true
&IoOptimized=optimized
&NetworkInterface.1.PrimaryIpAddress=192.168.**.**
&NetworkInterface.1.VSwitchId=vsw-bp1s5fnvk4gn2tws0****
&NetworkInterface.1.SecurityGroupId=sg-bp15ed6xe1yxeycg****
&NetworkInterface.1.NetworkInterfaceName=testNetworkInterfaceName
&NetworkInterface.1.Description=testNetworkInterfaceDescription
&PrivateIpAddress=10.1.**.**
&InstanceChargeType=PrePaid
&Period=1
&InternetChargeType=PayByTraffic
&NetworkType=vpc
&UserData=ZWNobyBoZWxsbyBl****
&RamRoleName=testRamRoleName
&AutoReleaseTime=2020-02-02T12:05:00Z
&SpotStrategy=NoSpot
&SpotPriceLimit=0.97
&SecurityEnhancementStrategy=Active
&Tag.1.Key=TestKey
&Tag.1.Value=TestValue
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateLaunchTemplateVersionResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
      <LaunchTemplateVersionNumber>2</LaunchTemplateVersionNumber>
</CreateLaunchTemplateVersionResponse>
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FExxxxx",
    "LaunchTemplateVersionNumber": 2
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRegion.NotExist|%s|The error message returned because the specified RegionId parameter does not exist.|
|403|LaunchTemplateVersionLimitExceed|%s|The error message returned because the maximum number of launch template versions has been reached.|
|404|InvalidLaunchTemplate.NotFound|%s|The error message returned because the specified launch template does not exist. Check whether the specified LaunchTemplateId or LaunchTemplateName parameter is correct.|
|400|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|400|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|The error message returned because the specified description is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|InvalidUserData.SizeExceeded|%s|The error message returned because the size of the specified user data exceeds the upper limit.|
|400|InvalidUserData.Base64FormatInvalid|%s|The error message returned because the specified UserData parameter is invalid.|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|The error message returned because the specified ResourceGroupId parameter does not exist.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|The error message returned because the specified HostName parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

