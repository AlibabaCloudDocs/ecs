# CreateLaunchTemplateVersion

You can call this operation to create a version for a specific launch template.

## Description

To modify the parameters of a specific launch template version, you can create a new version for the launch template. You can create a maximum of 30 versions for each launch template.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateLaunchTemplateVersion&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateLaunchTemplateVersion|The operation that you want to perform. Set the value to CreateLaunchTemplateVersion. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|LaunchTemplateId|String|No|lt-m5eiaupmvm2op9d\*\*\*\*|The ID of the launch template. For more information, see [DescribeLaunchTemplates](~~73759~~). You must specify `LaunchTemplateId` or `LaunchTemplateName` to determine a launch template. |
|LaunchTemplateName|String|No|testLaunchTemplateName|The name of the launch template. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|VersionDescription|String|No|testVersionDescription|The description of the launch template version. The description must be 2 to 256 characters in length and cannot start with http:// or https://. |
|ImageId|String|No|win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20170915.vhd|The ID of the image. You can call the [DescribeImages](~~25534~~) operation to query the available images. |
|ImageOwnerAlias|String|No|system|The source of the image.

**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|InstanceType|String|No|ecs.g5.large|The instance type. For more information, see [Instance families](~~25378~~). Alternatively, you can call the [DescribeInstanceTypes](~~25620~~) operation to query the most recent instance type list. |
|SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg\*\*\*\*|The ID of the security group to which to assign the instance. Instances within the same security group can access each other. |
|VpcId|String|No|vpc-bp12433upq1y5scen\*\*\*\*|The ID of the VPC. |
|VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws0\*\*\*\*|The ID of the vSwitch. You must specify this parameter if you specify the VpcId parameter. |
|InstanceName|String|No|testInstanceName|The name of the instance. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|Description|String|No|testDescription|The description of the instance. The description must be 2 to 256 characters in length and cannot start with http:// or https://. |
|InternetMaxBandwidthIn|Integer|No|50|The maximum inbound public bandwidth. Unit: Mbit/s. Valid values:

-   If the purchased outbound public bandwidth is less than or equal to 10 Mbit/s, the valid values of this parameter are 1 to 10 and the default value is 10.
-   If the purchased outbound public bandwidth is greater than 10 Mbit/s, the valid values of this parameters are 1 to the value of `InternetMaxBandwidthOut` and the default value is the value of `InternetMaxBandwidthOut`. |
|InternetMaxBandwidthOut|Integer|No|5|The maximum outbound public bandwidth. Unit: Mbit/s. Valid values: 0 to 100. |
|HostName|String|No|testHostName|The hostname of the instance.

-   The hostname cannot start or end with a period \(.\) or a hyphen \(-\). It cannot contain consecutive periods \(.\) or hyphens \(-\).
-   For Windows instances, the hostname must be 2 to 15 characters in length and can contain letters, digits, and hyphens \(-\). The hostname cannot contain periods \(.\) or only digits.
-   For instances that run other operating systems such as Linux, the hostname must be 2 to 64 characters in length. You can use periods \(.\) to separate the hostname into multiple segments. Each segment can contain letters, digits, and hyphens \(-\). |
|ZoneId|String|No|cn-hangzhou-g|The ID of the zone. |
|SystemDisk.Category|String|No|cloud\_ssd|The category of the system disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\) |
|SystemDisk.Size|Integer|No|40|The size of the system disk. Unit: GiB. Valid values: 20 to 500.

The value of this parameter must be at least 20 and greater than or equal to the size of the image. |
|SystemDisk.DiskName|String|No|cloud\_ssdSystem|The name of the system disk. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|SystemDisk.Description|String|No|testSystemDiskDescription|The description of the system disk. The description must be 2 to 256 characters in length and cannot start with http:// or https://. |
|DataDisk.N.Size|Integer|No|2000|The size of data disk N. Valid values of N: 1 to 16. Unit: GiB. Valid values:

-   Valid values when DataDisk.N.Category is set to cloud: 5 to 2000
-   Valid values when DataDisk.N.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_ssd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_essd: 20 to 32768

The value of this parameter must be greater than or equal to the size of the snapshot specified by the `SnapshotId` parameter. |
|DataDisk.N.SnapshotId|String|No|s-bp17441ohwka0yuh\*\*\*\*|The ID of the snapshot used to create data disk N. Valid values of N: 1 to 16. When the `DataDisk.N.SnapshotId` parameter is specified, the `DataDisk.N.Size` parameter is ignored. The data disk is created based on the size of the specified snapshot.

Use snapshots created after July 15, 2013. Otherwise, an error is returned and your request is rejected. |
|DataDisk.N.Category|String|No|cloud\_ssd|The category of data disk N. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: ESSD |
|DataDisk.N.Encrypted|String|No|false|Specifies whether to encrypt data disk N. |
|DataDisk.N.DiskName|String|No|testDataDiskName|The name of data disk N. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|DataDisk.N.Description|String|No|testDataDiskDescription|The description of the instance. The description must be 2 to 256 characters in length and cannot start with http:// or https://. |
|DataDisk.N.DeleteWithInstance|Boolean|No|true|Specifies whether to release data disk N when its associated instance is released. |
|IoOptimized|String|No|optimized|Specifies whether the instance is I/O optimized. Valid values:

-   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized. |
|NetworkInterface.N.PrimaryIpAddress|String|No|192.168.\*\*. \*\*|The primary private IP address of elastic network interface \(ENI\) N.

**Note:** The value of N in `NetworkInterface.N` cannot be greater than 1. |
|NetworkInterface.N.VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws0\*\*\*\*|The ID of the vSwitch to which to connect ENI N. The instance and ENI N must be in the same zone of the same VPC, but they can be connected to different vSwitches.

**Note:** The value of N in `NetworkInterface.N` cannot be greater than 1. |
|NetworkInterface.N.SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg\*\*\*\*|The ID of the security group to which to assign ENI N. The security group of ENI N must belong to the same VPC as that of the instance.

**Note:** The value of N in `NetworkInterface.N` cannot be greater than 1. |
|NetworkInterface.N.NetworkInterfaceName|String|No|testNetworkInterfaceName|The name of ENI N.

**Note:** The value of N in `NetworkInterface.N` cannot be greater than 1. |
|NetworkInterface.N.Description|String|No|testNetworkInterfaceDescription|The description of ENI N. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

**Note:** The value of N in `NetworkInterface.N` cannot be greater than 1. |
|InstanceChargeType|String|No|PrePaid|The billing method of the instance. Valid values:

-   PrePaid: subscription. If you set this parameter to PrePaid, make sure that your account supports credit payment. Otherwise, an `InvalidPayMethod` error is returned.
-   PostPaid: pay-as-you-go. |
|Period|Integer|No|1|The subscription period of the instance. Unit: months. This parameter takes effect and is required only when `InstanceChargeType` is set to `PrePaid`. If the DedicatedHostId parameter is specified, values of the Period parameter must be within the subscription period of the dedicated host. Valid values:

-   When the `PeriodUnit` parameter is set to Week, the valid values of the Period parameter are 1, 2, 3, and 4.
-   When the `PeriodUnit` parameter is set to Month, the valid values of the Period parameter are 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60. |
|InternetChargeType|String|No|PayByTraffic|The billing method for network usage. Valid values:

-   PayByBandwidth: pay-by bandwidth
-   PayByTraffic: pay-by-traffic

**Note:** When the **pay-by-traffic** billing method is used, the peak inbound and outbound bandwidths are used as bandwidth limits instead of guaranteed performance metrics. In scenarios where demands exceed resource supplies, the peak bandwidths may be limited. If you want guaranteed bandwidths for your instance, use the **pay-by-bandwidth** billing method. |
|EnableVmOsConfig|Boolean|No|false|Specifies whether to enable the operating system configuration of the instance. |
|NetworkType|String|No|vpc|The network type of the instance. Valid values:

-   classic: classic network
-   vpc: VPC |
|UserData|String|No|ZWNobyBoZWxsbyBl\*\*\*\*|The user data of the instance. User data must be encoded in Base64. The maximum size of raw data is 16 KB. |
|KeyPairName|String|No|testKeyPairName|The name of the SSH key pair.

-   For Windows instances, this parameter is ignored. The `Password` parameter takes effect even if the KeyPairName parameter is specified.
-   For Linux instances, the username and password logon method is disabled by default. |
|RamRoleName|String|No|testRamRoleName|The name of the instance RAM role. You can call the [ListRoles](~~28713~~) operation provided by RAM to query the instance RAM roles that you have created. |
|AutoReleaseTime|String|No|2018-01-01T12:05:00Z|The time scheduled for the instance to be automatically released. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

-   If the value of seconds \(`ss`\) is not `00`, the time is automatically rounded down to the nearest whole minute \(`mm`\).
-   The release time must be at least 30 minutes later than the current time.
-   The release time must be at most three years from the current time. |
|SpotStrategy|String|No|NoSpot|The preemption policy for a pay-as-you-go instance. This parameter takes effect only when the `InstanceChargeType` parameter is set to `PostPaid`. Valid values:

-   NoSpot: The instance is a regular pay-as-you-go instance.
-   SpotWithPriceLimit: The instance is a preemptible instance that has a user-defined maximum hourly price.
-   SpotAsPriceGo: The instance is a preemptible instance whose price is based on the current market price. |
|SpotPriceLimit|Float|No|0.97|The maximum hourly price of the instance. A maximum of three decimal places are allowed. |
|SpotDuration|Integer|No|1|The protection period of the preemptible instance. Unit: hours. Valid values: 0, 1, 2, 3, 4, 5, and 6.

-   The values 2, 3, 4, 5, and 6 of this parameter are in invitational preview. Submit a ticket to use these values.
-   If this parameter is set to 0, the preemptible instance has no protection period.

Default value : 1 |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group. |
|SecurityEnhancementStrategy|String|No|Active|Specifies whether to enable security hardening for the operating system. Valid values:

-   Active: enables security hardening. This value is applicable only to public images.
-   Deactive: disables security hardening. This value is applicable to all image types. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the instance, Elastic Block Storage \(EBS\) device, or primary NIC. Valid values of N: 1 to 5. The tag key cannot be an empty string. It can be up to 64 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the instance, EBS device, or primary NIC. Valid values of N: 1 to 5. The tag value can be an empty string. It can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. |

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
&NetworkInterface.1.PrimaryIpAddress=192.168. **. **
&NetworkInterface.1.VSwitchId=vsw-bp1s5fnvk4gn2tws0****
&NetworkInterface.1.SecurityGroupId=sg-bp15ed6xe1yxeycg****
&NetworkInterface.1.NetworkInterfaceName=testNetworkInterfaceName
&NetworkInterface.1.Description=testNetworkInterfaceDescription
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
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|The error message returned because the specified Description parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|403|InnerServiceFailed|%s|The error message returned because an internal service failed to be called.|
|400|InvalidUserData.SizeExceeded|%s|The error message returned because the size of the specified user data exceeds the upper limit.|
|400|InvalidUserData.Base64FormatInvalid|%s|The error message returned because the specified UserData parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

