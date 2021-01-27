# DescribeLaunchTemplateVersions

调用DescribeLaunchTemplateVersions查询ECS实例启动模板版本。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeLaunchTemplateVersions&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeLaunchTemplateVersions|系统规定参数。取值：DescribeLaunchTemplateVersions |
|RegionId|String|是|cn-hangzhou|实例启动模板所属的地域ID。

 您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|LaunchTemplateId|String|否|lt-bp168lnahrdwl39p\*\*\*\*|实例启动模板ID。

 您必须指定LaunchTemplateId或LaunchTemplateName以确定模板。 |
|LaunchTemplateName|String|否|testLaunchTemplateName|实例启动模板名称。 |
|LaunchTemplateVersion.N|RepeatList|否|1|一个或多个实例启动模板版本。 |
|MinVersion|Long|否|1|通过范围指定版本时的最小版本号。 |
|MaxVersion|Long|否|10|通过范围指定版本时的最大版本号。 |
|DefaultVersion|Boolean|否|true|是否查询默认版本。 |
|PageNumber|Integer|否|1|实例启动模板列表的页码。起始值：1

 默认值：1 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|LaunchTemplateVersionSets|Array of LaunchTemplateVersionSet| |关于模板版本的信息。 |
|LaunchTemplateVersionSet| | | |
|CreateTime|String|2018-05-14T14:18:00Z|模板创建时间。 |
|CreatedBy|String|1234567890|模板的创建者。 |
|DefaultVersion|Boolean|true|模板默认版本。 |
|LaunchTemplateData|Struct| |模板具体配置。 |
|AutoReleaseTime|String|2018-05-14T14:18:00Z|自动释放时间。 |
|DataDisks|Array of DataDisk| |数据盘集合。 |
|DataDisk| | | |
|Category|String|cloud\_ssd|数据盘的云盘种类。 |
|DeleteWithInstance|Boolean|true|数据盘是否随实例释放而释放。 |
|Description|String|testDiskDescription|数据盘描述。 |
|Device|String|/dev/xvda|数据盘的设备名。

 **说明：** 该参数即将停止使用，为提高代码兼容性，建议您尽量不要使用该参数。 |
|DiskName|String|testDiskName|数据盘名称。 |
|Encrypted|String|false|数据盘是否加密。 |
|PerformanceLevel|String|PL1|创建ESSD云盘作为数据盘使用时，设置云盘的性能等级。当`Category=cloud_essd`时该参数有返回值。可能值：

 -   PL0：单盘最高随机读写IOPS 1万。
-   PL1：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。 |
|Size|Integer|2000|数据盘大小。 |
|SnapshotId|String|s-bp67acfmxazb4p\*\*\*\*|数据盘使用的快照ID。 |
|DeploymentSetId|String|ds-bp1brhwhoqinyjd6\*\*\*\*|部署集ID。 |
|Description|String|testInstanceDescription|实例描述。 |
|EnableVmOsConfig|Boolean|false|是否启用实例操作系统配置。 |
|HostName|String|testHostName|实例主机名。 |
|ImageId|String|m-bp67acfmxazb4p\*\*\*\*|实例使用的镜像ID。 |
|ImageOwnerAlias|String|system|镜像来源。 |
|InstanceChargeType|String|Postpaid|实例计费类型。 |
|InstanceName|String|testInstanceName|实例名称。 |
|InstanceType|String|ecs.g5.large|实例规格。 |
|InternetChargeType|String|PayByTraffic|公网带宽计费方式。 |
|InternetMaxBandwidthIn|Integer|5|公网入带宽最大值。 |
|InternetMaxBandwidthOut|Integer|100|公网出带宽最大值。 |
|IoOptimized|String|none|是否为I/O优化实例。 |
|KeyPairName|String|testKeyPairName|密钥对名称。 |
|NetworkInterfaces|Array of NetworkInterface| |辅助弹性网卡的属性集合。 |
|NetworkInterface| | | |
|Description|String|testNetworkInterfacesDescription|辅助弹性网卡描述信息。 |
|NetworkInterfaceName|String|testNetworkInterfaceName|辅助弹性网卡名称。 |
|PrimaryIpAddress|String|203.0.\*.\*|辅助弹性网卡的主私有IP地址。 |
|SecurityGroupId|String|sg-bp67acfmxazb4p\*\*\*\*|辅助弹性网卡所属的安全组ID。必须是同一个VPC下的安全组。

 **说明：** SecurityGroupId和SecurityGroupIds不会同时返回值。 |
|SecurityGroupIds|List|\["sg-bp15ed6xe1yxeycg7\*\*\*\*"\]|辅助弹性网卡加入的一个或多个安全组。

 **说明：** SecurityGroupId和SecurityGroupIds不会同时返回值。 |
|VSwitchId|String|vsw-bp67acfmxazb4p\*\*\*\*|弹性网卡所属的虚拟交换机ID。 |
|NetworkType|String|vpc|网络类型。 |
|PasswordInherit|Boolean|true|是否继承原镜像里设置的用户名密码。 |
|Period|Integer|1|购买资源的时长。 |
|PrivateIpAddress|String|10.1.\*\*.\*\*|实例私网IP地址。 |
|RamRoleName|String|testRamRoleName|实例RAM角色名称。 |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|启动模板所在的企业资源组ID。 |
|SecurityEnhancementStrategy|String|active|是否开启安全加固。 |
|SecurityGroupId|String|sg-bp67acfmxazb4p\*\*\*\*|实例的安全组ID。

 **说明：** `SecurityGroupId`和`SecurityGroupIds`不会同时返回值。 |
|SecurityGroupIds|List|\["sg-bp15ed6xe1yxeycg7\*\*\*\*"\]|实例加入的一个或多个安全组。

 **说明：** `SecurityGroupId`和`SecurityGroupIds`不会同时返回值。 |
|SpotDuration|Integer|1|抢占式实例的保留时长，单位为小时。可能值：0~6

 -   保留时长2~6正在邀测中，如需开通请提交工单。
-   取值为0，则为无保护期模式。 |
|SpotPriceLimit|Float|0.98|设置实例的每小时最高价格。 |
|SpotStrategy|String|NoSpot|按量付费实例的竞价策略。 |
|SystemDisk.Category|String|cloud\_ssd|系统盘种类。 |
|SystemDisk.DeleteWithInstance|Boolean|true|系统盘是否随实例释放。 |
|SystemDisk.Description|String|testSystemDiskDescription|系统盘描述。 |
|SystemDisk.DiskName|String|testSystemDiskName|系统盘名称。 |
|SystemDisk.Iops|Integer|30000|系统盘每秒I/O次数。

 **说明：** 该参数即将停止使用，为提高代码兼容性，请尽量使用其他参数。 |
|SystemDisk.PerformanceLevel|String|PL0|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。当`SystemDisk.Category=cloud_essd`时该参数有返回值。可能值：

 -   PL0：单盘最高随机读写IOPS 1万。
-   PL1：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。 |
|SystemDisk.Size|Integer|80|系统盘大小，单位为GiB。 |
|Tags|Array of InstanceTag| |实例的标签。 |
|InstanceTag| | | |
|Key|String|TestKey|实例的标签键。 |
|Value|String|TestValue|实例的标签值。 |
|UserData|String|SGVsbG9FQ1M=|实例自定义数据，以Base64方式编码。 |
|VSwitchId|String|vsw-bp67acfmxazb4p\*\*\*\*|实例所属的虚拟交换机ID。 |
|VpcId|String|v-bp67acfmxazb4p\*\*\*\*|专有网络VPC ID。 |
|ZoneId|String|cn-hangzhou-g|可用区ID。 |
|LaunchTemplateId|String|lt-bp67acfmxazb4p\*\*\*\*|模板ID。 |
|LaunchTemplateName|String|testLaunchTemplateName|模板名称。 |
|ModifiedTime|String|2018-05-14T14:18:00Z|模板修改时间。 |
|VersionDescription|String|testVersionDescription|模板版本描述。 |
|VersionNumber|Long|1|模板版本号。 |
|RequestId|String|3989ED0C-20A1-4351-A127-2067FF8390AX|请求ID。 |
|PageSize|Integer|10|分页查询时设置的每页行数。 |
|PageNumber|Integer|1|当前页码。 |
|TotalCount|Integer|1|实例启动模板总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeLaunchTemplateVersions
&RegionId=cn-hangzhou
&LaunchTemplateName=lt-bp168lnahrdwl39p****
&<公共请求参数>
```

正常返回示例

`XML`格式

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

`JSON`格式

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

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegion.NotExist|%s|指定的地域不存在，请确认参数是否正确。|
|400|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|400|InvalidParameter|%s|无效的参数。|
|404|InvalidLaunchTemplate.NotFound|The specified LaunchTemplate is not found.|指定的模板未找到。|
|403|InnerServiceFailed|%s|内部服务调用失败。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

