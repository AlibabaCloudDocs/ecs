# DescribeLaunchTemplateVersions

Queries the versions of a launch template.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeLaunchTemplateVersions&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeLaunchTemplateVersions|The operation that you want to perform. Set the value to DescribeLaunchTemplateVersions. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the launch template.

 You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|LaunchTemplateId|String|No|lt-bp168lnahrdwl39p\*\*\*\*|The ID of the launch template.

 You must specify LaunchTemplateId or LaunchTemplateName to determine a launch template. |
|LaunchTemplateName|String|No|testLaunchTemplateName|The name of the launch template. |
|LaunchTemplateVersion.N|RepeatList|No|1|Version N of the launch template. |
|MinVersion|Long|No|1|The minimum version number in the version range to query. |
|MaxVersion|Long|No|10|The maximum version number in the version range to query. |
|DefaultVersion|Boolean|No|true|Specifies whether to query the default version. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

 Default value: 1. |
|PageSize|Integer|No|10|The number of entries to return on each page.

 Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|LaunchTemplateVersionSets|Array of LaunchTemplateVersionSet| |Details about the launch template versions. |
|LaunchTemplateVersionSet| | | |
|CreateTime|String|2018-05-14T14:18:00Z|The time when the launch template was created. |
|CreatedBy|String|1234567890|The creator of the launch template. |
|DefaultVersion|Boolean|true|The default version of the launch template. |
|LaunchTemplateData|Struct| |The configurations of the launch template. |
|AutoReleaseTime|String|2018-05-14T14:18:00Z|The time when to automatically release the launch template. |
|DataDisks|Array of DataDisk| |Details about the data disks. |
|DataDisk| | | |
|Category|String|cloud\_ssd|The category of the data disk. |
|DeleteWithInstance|Boolean|true|Indicates whether to release the data disk when the instance is released. |
|Description|String|testDiskDescription|The description of the data disk. |
|Device|String|/dev/xvda|The device name of the data disk.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|DiskName|String|testDiskName|The name of the data disk. |
|Encrypted|String|false|Indicates whether to encrypt the data disk. |
|PerformanceLevel|String|PL1|The performance level of the enhanced SSD \(ESSD\) used as the data disk. This parameter has a value only when the value of `Category` is cloud\_essd. Valid values:

 -   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS. |
|Size|Integer|2000|The size of the data disk. |
|SnapshotId|String|s-bp67acfmxazb4p\*\*\*\*|The ID of the snapshot used to create the data disk. |
|DeploymentSetId|String|ds-bp1brhwhoqinyjd6\*\*\*\*|The ID of the deployment set. |
|Description|String|testInstanceDescription|The description of the instance. |
|EnableVmOsConfig|Boolean|false|Indicates whether to enable the operating system configuration of the instance. |
|HostName|String|testHostName|The hostname of the instance. |
|ImageId|String|m-bp67acfmxazb4p\*\*\*\*|The ID of the image. |
|ImageOwnerAlias|String|system|The source of the image. |
|InstanceChargeType|String|Postpaid|The billing method of the instance. |
|InstanceName|String|testInstanceName|The name of the instance. |
|InstanceType|String|ecs.g5.large|The instance type. |
|InternetChargeType|String|PayByTraffic|The billing method for network usage. |
|InternetMaxBandwidthIn|Integer|5|The maximum inbound public bandwidth. |
|InternetMaxBandwidthOut|Integer|100|The maximum outbound public bandwidth. |
|IoOptimized|String|none|Indicates whether the instance is I/O optimized. |
|KeyPairName|String|testKeyPairName|The name of the key pair. |
|NetworkInterfaces|Array of NetworkInterface| |Details about the secondary elastic network interfaces \(ENIs\). |
|NetworkInterface| | | |
|Description|String|testNetworkInterfacesDescription|The description of the secondary ENI. |
|NetworkInterfaceName|String|testNetworkInterfaceName|The name of the secondary ENI. |
|PrimaryIpAddress|String|203.0.\*.\*|The primary private IP address of the secondary ENI. |
|SecurityGroupId|String|sg-bp67acfmxazb4p\*\*\*\*|The ID of the security group to which to assign the secondary ENI. The security group and the ENI must belong to the same virtual private cloud \(VPC\).

 **Note:** The SecurityGroupId and SecurityGroupIds parameters are mutually exclusive in the response. |
|SecurityGroupIds|List|\["sg-bp15ed6xe1yxeycg7\*\*\*\*"\]|The IDs of the security groups to which to assign the secondary ENI.

 **Note:** The SecurityGroupId and SecurityGroupIds parameters are mutually exclusive in the response. |
|VSwitchId|String|vsw-bp67acfmxazb4p\*\*\*\*|The ID of the vSwitch to which to connect the ENI. |
|NetworkType|String|vpc|The network type. |
|PasswordInherit|Boolean|true|Indicates whether the username and password pair preset in the image is used. |
|Period|Integer|1|The subscription period. |
|PrivateIpAddress|String|10.1.\*\*.\*\*|The private IP address of the instance. |
|RamRoleName|String|testRamRoleName|The name of the instance Resource Access Management \(RAM\) role. |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the launch template belongs. |
|SecurityEnhancementStrategy|String|active|Indicates whether to enable security hardening. |
|SecurityGroupId|String|sg-bp67acfmxazb4p\*\*\*\*|The ID of the security group to which to assign the instance.

 **Note:** The `SecurityGroupId` and `SecurityGroupIds` parameters are mutually exclusive in the response. |
|SecurityGroupIds|List|\["sg-bp15ed6xe1yxeycg7\*\*\*\*"\]|The IDs of the security groups to which to assign the instance.

 **Note:** The `SecurityGroupId` and `SecurityGroupIds` parameters are mutually exclusive in the response. |
|SpotDuration|Integer|1|The protection period of the preemptible instance. Unit: hours. Valid values: 0 to 6.

 -   Protection periods of 2, 3, 4, 5, and 6 hours are in invitational preview. If you want to set this parameter to one of these values, submit a ticket.
-   A value of 0 indicates that no protection period is configured for the preemptible instance. |
|SpotPriceLimit|Float|0.98|The maximum hourly price of the preemptible instance. |
|SpotStrategy|String|NoSpot|The bidding policy of the preemptible instance. |
|SystemDisk.Category|String|cloud\_ssd|The category of the system disk. |
|SystemDisk.DeleteWithInstance|Boolean|true|Indicates whether to release the system disk when the instance is released. |
|SystemDisk.Description|String|testSystemDiskDescription|The description of the system disk. |
|SystemDisk.DiskName|String|testSystemDiskName|The name of the system disk. |
|SystemDisk.Iops|Integer|30000|The number of I/O operations per second \(IOPS\) on the system disk.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|SystemDisk.PerformanceLevel|String|PL0|The performance level of the ESSD used as the system disk. This parameter has a value only when the value of `SystemDisk.Category` is cloud\_essd. Valid values:

 -   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS. |
|SystemDisk.Size|Integer|80|The size of the system disk. Unit: GiB. |
|Tags|Array of InstanceTag| |The tags of the instance. |
|InstanceTag| | | |
|Key|String|TestKey|The tag key of the instance. |
|Value|String|TestValue|The tag value of the instance. |
|UserData|String|SGVsbG9FQ1M=|The user data of the instance, which is Base64-encoded. |
|VSwitchId|String|vsw-bp67acfmxazb4p\*\*\*\*|The ID of the vSwitch to which to connect the instance. |
|VpcId|String|v-bp67acfmxazb4p\*\*\*\*|The ID of the VPC. |
|ZoneId|String|cn-hangzhou-g|The ID of the zone. |
|LaunchTemplateId|String|lt-bp67acfmxazb4p\*\*\*\*|The ID of the launch template. |
|LaunchTemplateName|String|testLaunchTemplateName|The name of the launch template. |
|ModifiedTime|String|2018-05-14T14:18:00Z|The time when the launch template was modified. |
|VersionDescription|String|testVersionDescription|The description of the launch template version. |
|VersionNumber|Long|1|The number of the launch template version. |
|RequestId|String|3989ED0C-20A1-4351-A127-2067FF8390AX|The ID of the request. |
|PageSize|Integer|10|The number of entries returned per page. |
|PageNumber|Integer|1|The page number of the returned page. |
|TotalCount|Integer|1|The total number of launch templates. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeLaunchTemplateVersions
&RegionId=cn-hangzhou
&LaunchTemplateName=lt-bp168lnahrdwl39p****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeLaunchTemplateVersionsResponse> 
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <RequestId>3989ED0C-20A1-4351-A127-2067FF8390AX</RequestId>
      <PageNumber>1</PageNumber>
      <LaunchTemplateVersionSets>
            <LaunchTemplateVersionSet>
                  <LaunchTemplateName>testLaunchTemplateName</LaunchTemplateName>
                  <CreatedBy>1234567890</CreatedBy>
                  <VersionDescription>testVersionDescription</VersionDescription>
                  <ModifiedTime>2018-05-14T14:18:00Z</ModifiedTime>
                  <DefaultVersion>true</DefaultVersion>
                  <CreateTime>2018-05-14T14:18:00Z</CreateTime>
                  <LaunchTemplateId>lt-bp67acfmxazb4p****</LaunchTemplateId>
                  <VersionNumber>1</VersionNumber>
            </LaunchTemplateVersionSet>
            <LaunchTemplateVersionSet>
                  <LaunchTemplateData>
                        <ImageOwnerAlias>system</ImageOwnerAlias>
                        <PrivateIpAddress>10.1.**.**</PrivateIpAddress>
                        <DeploymentSetId>ds-bp1brhwhoqinyjd6****</DeploymentSetId>
                        <Description>testInstanceDescription</Description>
                        <ResourceGroupId>rg-bp67acfmxazb4p****</ResourceGroupId>
                        <DataDisks>
                              <DataDisk>
                                    <SnapshotId>s-bp67acfmxazb4p****</SnapshotId>
                                    <Description>testDiskDescription</Description>
                                    <Category>cloud_ssd</Category>
                                    <PerformanceLevel>PL1</PerformanceLevel>
                                    <Device>/dev/xvda</Device>
                                    <Encrypted>false</Encrypted>
                                    <Size>2000</Size>
                                    <DeleteWithInstance>true</DeleteWithInstance>
                                    <DiskName>testDiskName</DiskName>
                              </DataDisk>
                        </DataDisks>
                        <UserData>SGVsbG9FQ1M=</UserData>
                        <InstanceChargeType>Postpaid</InstanceChargeType>
                        <SpotDuration>1</SpotDuration>
                        <SystemDisk.DiskName>testSystemDiskName</SystemDisk.DiskName>
                        <SystemDisk.Size>80</SystemDisk.Size>
                        <SystemDisk.PerformanceLevel>PL0</SystemDisk.PerformanceLevel>
                        <RamRoleName>testRamRoleName</RamRoleName>
                        <NetworkType>vpc</NetworkType>
                        <NetworkInterfaces>
                              <NetworkInterface>
                                    <NetworkInterfaceName>testNetworkInterfaceName</NetworkInterfaceName>
                                    <PrimaryIpAddress>203.0.*.*</PrimaryIpAddress>
                                    <Description>testNetworkInterfacesDescription</Description>
                                    <SecurityGroupId>sg-bp67acfmxazb4p****</SecurityGroupId>
                                    <VSwitchId>vsw-bp67acfmxazb4p****</VSwitchId>
                              </NetworkInterface>
                        </NetworkInterfaces>
                        <SystemDisk.DeleteWithInstance>true</SystemDisk.DeleteWithInstance>
                        <ImageId>m-bp67acfmxazb4p****</ImageId>
                        <SpotPriceLimit>0.98</SpotPriceLimit>
                        <SystemDisk.Category>cloud_ssd</SystemDisk.Category>
                        <InstanceType>ecs.g5.large</InstanceType>
                        <SpotStrategy>NoSpot</SpotStrategy>
                        <HostName>testHostName</HostName>
                        <Tags>
                              <InstanceTag>
                                    <Value>TestValue</Value>
                                    <Key>TestKey</Key>
                              </InstanceTag>
                        </Tags>
                        <PasswordInherit>true</PasswordInherit>
                        <KeyPairName>testKeyPairName</KeyPairName>
                        <SystemDisk.Iops>30000</SystemDisk.Iops>
                        <IoOptimized>none</IoOptimized>
                        <SystemDisk.Description>testSystemDiskDescription</SystemDisk.Description>
                        <ZoneId>cn-hangzhou-g</ZoneId>
                        <VSwitchId>vsw-bp67acfmxazb4p****</VSwitchId>
                        <SecurityGroupId>sg-bp67acfmxazb4p****</SecurityGroupId>
                        <Period>1</Period>
                        <InternetChargeType>PayByTraffic</InternetChargeType>
                        <InstanceName>testInstanceName</InstanceName>
                        <EnableVmOsConfig>false</EnableVmOsConfig>
                        <InternetMaxBandwidthOut>100</InternetMaxBandwidthOut>
                        <InternetMaxBandwidthIn>5</InternetMaxBandwidthIn>
                        <VpcId>v-bp67acfmxazb4p****</VpcId>
                        <SecurityEnhancementStrategy>active</SecurityEnhancementStrategy>
                        <AutoReleaseTime>2018-05-14T14:18:00Z</AutoReleaseTime>
                  </LaunchTemplateData>
            </LaunchTemplateVersionSet>
      </LaunchTemplateVersionSets>
</DescribeLaunchTemplateVersionsResponse>
```

`JSON` format

```
{
    "TotalCount": "1", 
    "PageSize": "10", 
    "RequestId": "3989ED0C-20A1-4351-A127-2067FF8390AX", 
    "PageNumber": "1", 
    "LaunchTemplateVersionSets": {
        "LaunchTemplateVersionSet": [
            {
                "LaunchTemplateName": "testLaunchTemplateName", 
                "CreatedBy": "1234567890", 
                "VersionDescription": "testVersionDescription", 
                "ModifiedTime": "2018-05-14T14:18:00Z", 
                "DefaultVersion": "true", 
                "CreateTime": "2018-05-14T14:18:00Z", 
                "LaunchTemplateId": "lt-bp67acfmxazb4p****", 
                "VersionNumber": "1"
            }, 
            {
                "LaunchTemplateData": {
                    "ImageOwnerAlias": "system", 
                    "PrivateIpAddress": "10.1.**.**", 
                    "DeploymentSetId": "ds-bp1brhwhoqinyjd6****",
                    "Description": "testInstanceDescription", 
                    "ResourceGroupId": "rg-bp67acfmxazb4p****", 
                    "DataDisks": {
                        "DataDisk": [
                            {
                                "SnapshotId": "s-bp67acfmxazb4p****", 
                                "Description": "testDiskDescription", 
                                "Category": "cloud_ssd", 
                                "PerformanceLevel": "PL1", 
                                "Device": "/dev/xvda", 
                                "Encrypted": "false", 
                                "Size": "2000", 
                                "DeleteWithInstance": "true", 
                                "DiskName": "testDiskName"
                            }
                        ]
                    }, 
                    "UserData": "SGVsbG9FQ1M=", 
                    "InstanceChargeType": "Postpaid", 
                    "SpotDuration": "1", 
                    "SystemDisk.DiskName": "testSystemDiskName", 
                    "SystemDisk.Size": "80", 
                    "SystemDisk.PerformanceLevel": "PL0", 
                    "RamRoleName": "testRamRoleName", 
                    "NetworkType": "vpc", 
                    "NetworkInterfaces": {
                        "NetworkInterface": [
                            {
                                "NetworkInterfaceName": "testNetworkInterfaceName", 
                                "PrimaryIpAddress": "203.0.*.*", 
                                "Description": "testNetworkInterfacesDescription", 
                                "SecurityGroupId": "sg-bp67acfmxazb4p****", 
                                "VSwitchId": "vsw-bp67acfmxazb4p****"
                            }
                        ]
                    }, 
                    "SystemDisk.DeleteWithInstance": "true", 
                    "ImageId": "m-bp67acfmxazb4p****", 
                    "SpotPriceLimit": "0.98", 
                    "SystemDisk.Category": "cloud_ssd", 
                    "InstanceType": "ecs.g5.large", 
                    "SpotStrategy": "NoSpot", 
                    "HostName": "testHostName", 
                    "Tags": {
                        "InstanceTag": [
                            {
                                "Value": "TestValue", 
                                "Key": "TestKey"
                            }
                        ]
                    }, 
                    "PasswordInherit": "true", 
                    "KeyPairName": "testKeyPairName", 
                    "SystemDisk.Iops": "30000", 
                    "IoOptimized": "none", 
                    "SystemDisk.Description": "testSystemDiskDescription", 
                    "ZoneId": "cn-hangzhou-g", 
                    "VSwitchId": "vsw-bp67acfmxazb4p****", 
                    "SecurityGroupId": "sg-bp67acfmxazb4p****", 
                    "Period": "1", 
                    "InternetChargeType": "PayByTraffic", 
                    "InstanceName": "testInstanceName", 
                    "EnableVmOsConfig": "false", 
                    "InternetMaxBandwidthOut": "100", 
                    "InternetMaxBandwidthIn": "5", 
                    "VpcId": "v-bp67acfmxazb4p****", 
                    "SecurityEnhancementStrategy": "active", 
                    "AutoReleaseTime": "2018-05-14T14:18:00Z"
                }
            }
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRegion.NotExist|%s|The error message returned because the specified RegionId parameter does not exist.|
|400|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|400|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|404|InvalidLaunchTemplate.NotFound|The specified LaunchTemplate is not found.|The error message returned because the specified launch template does not exist.|
|403|InnerServiceFailed|%s|The error message returned because an internal service failed to be called.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

