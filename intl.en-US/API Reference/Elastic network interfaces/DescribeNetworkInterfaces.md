# DescribeNetworkInterfaces

Queries the details of one or more elastic network interfaces \(ENIs\).

## Description

You can use one of the following methods to check the responses returned by the `DescribeNetworkInterfaces` operation:

-   Method 1: Use `NextToken` to configure the query token. Set the value to the `NextToken` value returned in the last call to the `DescribeNetworkInterfaces` operation. Then, use `MaxResults` to specify the maximum number of entries to return on each page.
-   Method 2: Use `PageSize` to specify the number of entries to return on each page and then use `PageNumber` to specify the number of the page to return.

    You can use only one of the preceding methods. If a large number of entries are to be returned, we recommend that you use method 1. When `NextToken` is specified, `PageSize` and `PageNumber` do not take effect and `TotalCount` in the response is invalid.


## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeNetworkInterfaces&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeNetworkInterfaces|The operation that you want to perform. Set the value to DescribeNetworkInterfaces. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the ENI. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the ENI. Valid values of N: 1 to 20.

 If a single tag is specified to query resources, up to 1,000 resources that are bound with this tag can be displayed in the response. If multiple tags are specified to query resources, up to 1,000 resources that are bound with all these tags can be displayed in the response. To query more than 1,000 resources that are bound with specified tags, call the [ListTagResources](~~110425~~) operation. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the ENI. Valid values of N: 1 to 20. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the ENI belongs. If this parameter is specified to query resources, up to 1,000 resources that belong to the specified resource group can be displayed in the response. |
|VSwitchId|String|No|vsw-bp16usj2p27htro3\*\*\*\*|The ID of the vSwitch to which the ENI is connected. |
|VpcId|String|No|vsw-bp16usj2p27htro3\*\*\*\*|The ID of the virtual private cloud \(VPC\) to which the ENI belongs. |
|PrimaryIpAddress|String|No|192.168.\*\*.\*\*|The primary private IP address of the ENI. |
|PrivateIpAddress.N|RepeatList|No|192.168.\*\*.\*\*|Secondary private IP address N of the ENI. Valid values of N: 1 to 100. |
|SecurityGroupId|String|No|sg-bp144yr32sx6ndw\*\*\*\*|The ID of the security group to which the secondary ENI belongs.

 -   To query the details of secondary ENIs based on the ID of a security group, specify this parameter.
-   To query details of primary ENIs based on the ID of a security group, call the [DescribeInstances](~~25506~~) operation and specify the `SecurityGroupId` parameter. |
|NetworkInterfaceName|String|No|test-eni-name|The name of the ENI. |
|Type|String|No|Secondary|The type of the ENI. Valid values:

 -   Primary
-   Secondary

 This parameter is empty by default, which indicates that both primary and secondary ENIs are queried. |
|InstanceId|String|No|i-bp1e2l6djkndyuli\*\*\*\*|The ID of the instance to which the ENI is bound. |
|NetworkInterfaceId.N|RepeatList|No|eni-bp125p95hhdhn3ot\*\*\*\*|The ID of ENI N. Valid values of N: 1 to 100. |
|ServiceManaged|Boolean|No|true|Specifies whether the user is an Alibaba Cloud service or a distributor. |
|Status|String|No|Available|The status of the ENI. Valid values:

 -   Creating: The ENI is being created.
-   Available: The ENI is not bound.
-   Attaching: The ENI is being bound to an instance.
-   InUse: The ENI is bound to an instance.
-   Detaching: The ENI is being unbound from an instance.
-   Deleting: The ENI is being deleted.
-   CreateFailed: The ENI failed to be created.

 This parameter is empty by default, which indicates that ENIs in all states are queried. |
|PageNumber|Integer|No|1|The number of the page to return.

 Pages start from page 1.

 Default value: 1. |
|PageSize|Integer|No|100|The number of entries to return on each page.

 Maximum value: 100.

 Default value: 10.

 For more information about how to check the responses returned by this operation, see the preceding "Description" section. |
|NextToken|String|No|AAAAAdDWBF2\*\*\*\*|The query token. Set the value to the `NextToken` value returned in the last call to the DescribeNetworkInterfaces operation.

 For more information about how to check the responses returned by this operation, see the preceding "Description" section. |
|MaxResults|Integer|No|50|The maximum number of entries to return on each page. Valid values: 1 to 500.

 Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NetworkInterfaceSets|Array of NetworkInterfaceSet| |Details about the ENIs. |
|NetworkInterfaceSet| | | |
|AssociatedPublicIp|Struct| |The elastic IP address \(EIP\) associated with the secondary private IP address of the ENI. |
|AllocationId|String|eip-2ze88m67qx5z\*\*\*\*|The ID of the EIP. |
|PublicIpAddress|String|116.62.\*\*.\*\*|The public IP address. |
|Attachment|Struct| |**Note:** This parameter is in invitational preview and unavailable. |
|DeviceIndex|Integer|0|**Note:** This parameter is in invitational preview and unavailable. |
|InstanceId|String|null|**Note:** This parameter is in invitational preview and unavailable. |
|TrunkNetworkInterfaceId|String|null|**Note:** This parameter is in invitational preview and unavailable. |
|CreationTime|String|2017-11-24T06:14:22Z|The time when the ENI was created. |
|Description|String|DescriptionTest|The description of the ENI. |
|InstanceId|String|i-bp1e2l6djkndyuli\*\*\*\*|The ID of the instance to which the ENI is bound.

 **Note:** For the ENIs that are managed and controlled by other Alibaba Cloud services, no instance IDs are returned. |
|Ipv6Sets|Array of Ipv6Set| |The IPv6 addresses assigned to the ENI. |
|Ipv6Set| | | |
|Ipv6Address|String|2408:4321:180:1701:94c7:bc38:3bfa:\*\*\*|The IPv6 address assigned to the ENI. |
|MacAddress|String|00:16:3e:12:e7:\*\*|The MAC address of the ENI. |
|NetworkInterfaceId|String|eni-bp125p95hhdhn3ot\*\*\*\*|The ID of the ENI. |
|NetworkInterfaceName|String|my-eni-name|The name of the ENI. |
|NetworkInterfaceTrafficMode|String|null|**Note:** This parameter is in invitational preview and unavailable. |
|OwnerId|String|123456\*\*\*\*|The ID of the account to which the ENI belongs. |
|PrivateIpAddress|String|172.17.\*\*.\*\*|The private IP address of the ENI. |
|PrivateIpSets|Array of PrivateIpSet| |Details about the private IP addresses of the ENI. |
|PrivateIpSet| | | |
|AssociatedPublicIp|Struct| |The EIP associated with the ENI. |
|AllocationId|String|eip-2ze88m67qx5z\*\*\*\*|The ID of the EIP. |
|PublicIpAddress|String|116.62.\*\*.\*\*|The public IP address of the instance. |
|Primary|Boolean|true|Indicates whether the IP address is the primary private IP address. Valid values:

 -   true
-   false |
|PrivateIpAddress|String|172.17.\*\*.\*\*|The private IP address of the instance. |
|QueueNumber|Integer|8|The number of queues supported by the ENI.

 -   If the ENI is a secondary ENI in the InUse \(InUse\) state and the number of queues supported by this ENI has never been modified, the default number of queues per secondary ENI that the instance type supports is returned.
-   If the number of queues supported by the secondary ENI has been modified, the new number of queues is returned.
-   If the ENI is a secondary ENI in the Available \(Available\) state and the number of queues supported by this ENI has never been modified, an empty value is returned.
-   If the ENI is a primary ENI, the default number of queues per primary ENI that the instance type supports is returned. |
|QueuePairNumber|Integer|0|**Note:** This parameter is in invitational preview and unavailable. |
|ResourceGroupId|String|rg-2ze88m67qx5z\*\*\*\*|The ID of the resource group to which the ENI belongs. |
|SecurityGroupIds|List|sg-bp18kz60mefsicfg\*\*\*\*|The IDs of the security groups to which the ENI belongs. |
|ServiceID|Long|12345678910|The ID of the distributor to which the ENI belongs. |
|ServiceManaged|Boolean|true|Indicates whether the user is an Alibaba Cloud service or a distributor. |
|Status|String|Available|The status of the ENI. |
|Tags|Array of Tag| |The tags of the ENI. |
|Tag| | | |
|TagKey|String|TestKey|The tag key of the ENI. |
|TagValue|String|TestValue|The tag value of the ENI. |
|Type|String|Secondary|The type of the ENI. |
|VSwitchId|String|vsw-bp16usj2p27htro3\*\*\*\*|The ID of the vSwitch to which the ENI is connected. |
|VpcId|String|vpc-bp1j7w3gc1cexjqd\*\*\*\*|The ID of the VPC to which the ENI belongs. |
|ZoneId|String|cn-hangzhou-e|The zone ID of the ENI. |
|NextToken|String|AAAAAdDWBF2\*\*\*\*|The query token returned in this call. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|1|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|70|The total number of ENIs. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeNetworkInterfaces
&RegionId=cn-hangzhou
&PrivateIpAddress.1=192.168.**.**
&PrivateIpAddress.2=192.168.**.**
&NextToken=AAAAAdDWBF2****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeNetworkInterfacesResponse>
      <TotalCount>1</TotalCount>
      <RequestId>5C0E2B68-EDB0-421D-B146-E58A04808242</RequestId>
      <PageSize>10</PageSize>
      <NextToken>AAAAAdDWBF2w6Olxc+cMPjUtUMpaCa3hjTbxWpikFyOaihc****/JSvFWO/sGLK3bh****</NextToken>
      <PageNumber>1</PageNumber>
      <NetworkInterfaceSets>
            <NetworkInterfaceSet>
                  <Status>InUse</Status>
                  <PrivateIpAddress>192.168.**.**</PrivateIpAddress>
                  <ZoneId>cn-shenzhen-c</ZoneId>
                  <ResourceGroupId>rg-aek2boynwys****</ResourceGroupId>
                  <InstanceId>i-wz91t9p4j9xsw2pn****</InstanceId>
                  <VSwitchId>vsw-wz9vqfgwgkj94ubb1****</VSwitchId>
                  <NetworkInterfaceId>eni-wz9iib303as7e5c3****</NetworkInterfaceId>
                  <MacAddress>00:16:3e:**:**:c2</MacAddress>
                  <SecurityGroupIds>
                        <SecurityGroupId>sg-wz9iib303as7e5c7****</SecurityGroupId>
                  </SecurityGroupIds>
                  <Type>Primary</Type>
                  <Ipv6Sets>
                        <Ipv6Set>
                              <Ipv6Address>2408:4321:180:1701:94c7:bc38:3bfa:***</Ipv6Address>
                        </Ipv6Set>
                  </Ipv6Sets>
                  <VpcId>vpc-wz9wh0fywtu5szszb****</VpcId>
                  <OwnerId>140692647406****</OwnerId>
                  <AssociatedPublicIp></AssociatedPublicIp>
                  <CreationTime>2019-12-25T12:31:31Z</CreationTime>
                  <Tags>
                        <Tag>
                              <TagKey>owner</TagKey>
                              <TagValue>lisi</TagValue>
                        </Tag>
                  </Tags>
                  <PrivateIpSets>
                        <PrivateIpSet>
                              <PrivateIpAddress>192.168.**.**</PrivateIpAddress>
                              <AssociatedPublicIp></AssociatedPublicIp>
                              <Primary>true</Primary>
                        </PrivateIpSet>
                  </PrivateIpSets>
            </NetworkInterfaceSet>
      </NetworkInterfaceSets>
</DescribeNetworkInterfacesResponse>
```

`JSON` format

```
{
	"TotalCount": 1,
	"RequestId": "5C0E2B68-EDB0-421D-B146-E58A04808242",
	"PageSize": 10,
	"NextToken": "AAAAAdDWBF2w6Olxc+cMPjUtUMpaCa3hjTbxWpikFyOaihc****/JSvFWO/sGLK3bh****",
	"PageNumber": 1,
	"NetworkInterfaceSets": {
		"NetworkInterfaceSet": [{
			"Status": "InUse",
			"PrivateIpAddress": "192.168.**.**",
			"ZoneId": "cn-shenzhen-c",
			"ResourceGroupId": "rg-aek2boynwys****",
			"InstanceId": "i-wz91t9p4j9xsw2pn****",
			"VSwitchId": "vsw-wz9vqfgwgkj94ubb1****",
			"NetworkInterfaceId": "eni-wz9iib303as7e5c3****",
			"MacAddress": "00:16:3e:**:**:c2",
			"SecurityGroupIds": {
				"SecurityGroupId": [
					"sg-wz9iib303as7e5c7****"
				]
			},
			"Type": "Primary",
			"Ipv6Sets": {
				"Ipv6Set": [{
					"Ipv6Address": "2408:4321:180:1701:94c7:bc38:3bfa:***"
				}]
			},
			"VpcId": "vpc-wz9wh0fywtu5szszb****",
			"OwnerId": "140692647406****",
			"AssociatedPublicIp": {},
			"CreationTime": "2019-12-25T12:31:31Z",
			"Tags": {
				"Tag": [{
					"TagKey": "owner",
					"TagValue": "lisi"
				}]
			},
			"PrivateIpSets": {
				"PrivateIpSet": [{
					"PrivateIpAddress": "192.168.**.**",
					"AssociatedPublicIp": {},
					"Primary": true
				}]
			}
		}]
	}
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidUserType.NotSupported|%s|The error message returned because your account does not support this operation.|
|403|Abs.InvalidAccount.NotFound|%s|The error message returned because your Alibaba Cloud account does not exist or because your AccessKey pair has expired.|
|400|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|403|Forbidden.NotSupportRAM|%s|The error message returned because RAM users are not authorized to perform this operation.|
|400|UnsupportedParameter|%s|The error message returned because a specific parameter is not supported.|
|403|Forbidden.SubUser|%s|The error message returned because you are not authorized to manage this resource. Contact the owner of the Alibaba Cloud account for authorization.|
|400|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|400|InvalidInstanceID.Malformed|%s|The error message returned because the specified InstanceId parameter is invalid.|
|400|InvalidOperation.InvalidEcsState|%s|The error message returned because the operation is not supported while the instance is in the current state.|
|400|InvalidOperation.InvalidEniState|%s|The error message returned because the operation is not supported while the ENI is in the current state.|
|400|InvalidOperation.DetachPrimaryEniNotAllowed|%s|The error message returned because the primary ENI cannot be unbound from the instance.|
|404|InvalidEcsId.NotFound|%s|The error message returned because the specified InstanceId parameter does not exist.|
|404|InvalidEniId.NotFound|%s|The error message returned because the specified ENI ID does not exist.|
|404|InvalidVSwitchId.NotFound|%s|The error message returned because the specified VSwitchId parameter does not exist.|
|404|InvalidSecurityGroupId.NotFound|%s|The error message returned because the specified SecurityGroupId parameter does not exist.|
|403|MaxEniCountExceeded|%s|The error message returned because the maximum number of ENIs that can be managed has been reached.|
|403|EniPerInstanceLimitExceeded|%s|The error message returned because the maximum number of ENIs that can be bound to the specified instance has been reached.|
|403|InvalidOperation.AvailabilityZoneMismatch|%s|The error message returned because the operation is invalid.|
|403|InvalidOperation.VpcMismatch|%s|The error message returned because this operation is invalid. Check whether the VPC in the operation corresponds to other parameters.|
|403|SecurityGroupInstanceLimitExceed|%s|The error message returned because the maximum number of instances in the specified security group has been reached.|
|403|InvalidSecurityGroupId.NotVpc|%s|The error message returned because the specified SecurityGroupId parameter is invalid and the network type of the security group is not VPC.|
|403|InvalidOperation.InvalidEniType|%s|The error message returned because the operation is not supported while the ENI is of the current type.|
|400|Forbidden.RegionId|%s|The error message returned because the service is unavailable in the current region.|
|403|InvalidVpc.Empty|%s|The error message returned because no vSwitches exist in the specified VPC. For more information, see the return value of the %s placeholder in the error message.|
|400|InvalidRegionId.MalFormed|The specified parameter RegionId is not valid.|The error message returned because the specified RegionId parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

