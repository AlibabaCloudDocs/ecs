# DescribeNetworkInterfaces

调用DescribeNetworkInterfaces查询一个或多个弹性网卡（ENI）的详细信息。

## 接口说明

`DescribeNetworkInterfaces`支持两种查看返回数据的方式：

-   方式一：通过`NextToken`设置查询凭证（Token），其取值是上一次调用`DescribeNetworkInterfaces`返回的`NextToken`参数值，再通过`MaxResults`设置单页查询的最大条目数。
-   方式二：通过`PageSize`设置单页返回的条目数，再通过`PageNumber`设置页码。

    以上两种方式只能任选其中之一。当弹性网卡返回的条目数较多时，推荐使用方式一。如果设置了`NextToken`，则请求参数`PageSize`和`PageNumber`将失效，且返回数据中的`TotalCount`无效。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeNetworkInterfaces&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeNetworkInterfaces|系统规定参数。取值：DescribeNetworkInterfaces |
|RegionId|String|是|cn-hangzhou|所在地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Tag.N.Key|String|否|TestKey|弹性网卡的标签值。N的取值范围：1~20

 使用一个标签过滤资源，查询到该标签下的资源数量不能超过1000个；使用多个标签过滤资源，查询到同时绑定了多个标签的资源数量不能超过1000个。如果资源数量超过1000个，请使用[ListTagResources](~~110425~~)接口进行查询。 |
|Tag.N.Value|String|否|TestValue|弹性网卡的标签键。N的取值范围：1~20 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|资源组ID。使用该参数过滤资源时，资源数量不能超过1000个。 |
|VSwitchId|String|否|vsw-bp16usj2p27htro3\*\*\*\*|VPC的交换机ID。 |
|VpcId|String|否|vsw-bp16usj2p27htro3\*\*\*\*|网卡所属的专有网络VPC ID。 |
|PrimaryIpAddress|String|否|192.168.\*\*.\*\*|弹性网卡主私网IP地址。 |
|PrivateIpAddress.N|RepeatList|否|192.168.\*\*.\*\*|弹性网卡的辅助私网IP地址。N的取值范围：1~100 |
|SecurityGroupId|String|否|sg-bp144yr32sx6ndw\*\*\*\*|辅助网卡对应的安全组ID。

 -   如果您需要通过安全组ID查询辅助网卡的信息，请指定该参数。
-   如果您需要通过安全组ID查询主网卡信息，请调用[DescribeInstances](~~25506~~)指定`SecurityGroupId`参数进行查询。 |
|NetworkInterfaceName|String|否|test-eni-name|弹性网卡的名称。 |
|Type|String|否|Secondary|弹性网卡类型。取值范围：

 -   Primary：主网卡
-   Secondary：辅助网卡

 默认值：空，表示查询所有类型。 |
|InstanceId|String|否|i-bp1e2l6djkndyuli\*\*\*\*|弹性网卡当前关联的实例ID。 |
|NetworkInterfaceId.N|RepeatList|否|eni-bp125p95hhdhn3ot\*\*\*\*|弹性网卡ID。N的取值范围：1~100 |
|ServiceManaged|Boolean|否|true|该弹性网卡的使用者是否为云产品或虚商。 |
|Status|String|否|Available|网卡状态。取值范围：

 -   Creating：创建中
-   Available：可用
-   Attaching：绑定中
-   InUse：已绑定
-   Detaching：解绑中
-   Deleting：删除中
-   CreateFailed：创建失败，属于异常状态

 默认值：空，表示查询所有状态。 |
|PageNumber|Integer|否|1|查询结果的页码。

 起始值：1

 默认值：1 |
|PageSize|Integer|否|100|查询结果的分页大小。

 最大值：100

 默认值：10

 有关本接口查看返回数据的设置方式，请参见上文接口说明。 |
|NextToken|String|否|AAAAAdDWBF2\*\*\*\*|查询凭证（Token），取值为上一次API调用返回的`NextToken`参数值。

 有关本接口查看返回数据的设置方式，请参见上文接口说明。 |
|MaxResults|Integer|否|50|返回的最大数。取值范围：1~500

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NetworkInterfaceSets|Array of NetworkInterfaceSet| |弹性网卡信息组成的集合。 |
|NetworkInterfaceSet| | | |
|AssociatedPublicIp|Struct| |弹性网卡辅助私有IP地址关联的弹性公网IP。 |
|AllocationId|String|eip-2ze88m67qx5z\*\*\*\*|EIP的ID。 |
|PublicIpAddress|String|116.62.\*\*.\*\*|公网IP地址。 |
|Attachment|Struct| |**说明：** 该参数正在邀测中，暂未开放使用。 |
|DeviceIndex|Integer|0|**说明：** 该参数正在邀测中，暂未开放使用。 |
|InstanceId|String|null|**说明：** 该参数正在邀测中，暂未开放使用。 |
|TrunkNetworkInterfaceId|String|null|**说明：** 该参数正在邀测中，暂未开放使用。 |
|CreationTime|String|2017-11-24T06:14:22Z|创建时间。 |
|Description|String|DescriptionTest|描述。 |
|InstanceId|String|i-bp1e2l6djkndyuli\*\*\*\*|弹性网卡绑定的实例ID。

 **说明：** 由其他阿里云服务管理和控制的弹性网卡不会返回实例ID。 |
|Ipv6Sets|Array of Ipv6Set| |为弹性网卡分配的IPv6地址集合。 |
|Ipv6Set| | | |
|Ipv6Address|String|2408:4321:180:1701:94c7:bc38:3bfa:\*\*\*|为弹性网卡指定的IPv6地址。 |
|MacAddress|String|00:16:3e:12:e7:\*\*|弹性网卡的MAC地址。 |
|NetworkInterfaceId|String|eni-bp125p95hhdhn3ot\*\*\*\*|弹性网卡ID。 |
|NetworkInterfaceName|String|my-eni-name|弹性网卡的名称。 |
|NetworkInterfaceTrafficMode|String|null|**说明：** 该参数正在邀测中，暂未开放使用。 |
|OwnerId|String|123456\*\*\*\*|弹性网卡的所属账号ID。 |
|PrivateIpAddress|String|172.17.\*\*.\*\*|弹性网卡的私网IP地址。 |
|PrivateIpSets|Array of PrivateIpSet| |PrivateIpSet组成的集合。 |
|PrivateIpSet| | | |
|AssociatedPublicIp|Struct| |弹性网卡关联的弹性公网IP。 |
|AllocationId|String|eip-2ze88m67qx5z\*\*\*\*|EIP的ID。 |
|PublicIpAddress|String|116.62.\*\*.\*\*|实例的公网IP。 |
|Primary|Boolean|true|是否是主私网IP地址。可能值：

 -   true：主私网IP
-   false：辅助私网IP |
|PrivateIpAddress|String|172.17.\*\*.\*\*|实例的私网IP地址。 |
|QueueNumber|Integer|8|网卡的队列数。

 -   如果辅助网卡是已挂载（InUse）状态且没有修改过队列数，则返回实例规格默认的辅助网卡队列数。
-   如果辅助网卡修改过队列数，则返回修改后的队列数。
-   如果辅助网卡是未挂载（Available）状态且未修改过队列数，则返回值为空。
-   主网卡返回实例规格默认的主网卡队列数。 |
|QueuePairNumber|Integer|0|**说明：** 该参数正在邀测中，暂未开放使用。 |
|ResourceGroupId|String|rg-2ze88m67qx5z\*\*\*\*|资源组ID。 |
|SecurityGroupIds|List|sg-bp18kz60mefsicfg\*\*\*\*|所属的安全组集合。 |
|ServiceID|Long|12345678910|弹性网卡对应的虚商ID。 |
|ServiceManaged|Boolean|true|该弹性网卡的使用者是否为云产品或虚商。 |
|Status|String|Available|弹性网卡的状态。 |
|Tags|Array of Tag| |标签。 |
|Tag| | | |
|TagKey|String|TestKey|标签键。 |
|TagValue|String|TestValue|标签值。 |
|Type|String|Secondary|弹性网卡的类型。 |
|VSwitchId|String|vsw-bp16usj2p27htro3\*\*\*\*|VPC的交换机ID。 |
|VpcId|String|vpc-bp1j7w3gc1cexjqd\*\*\*\*|网卡所属的专有网络VPC ID。 |
|ZoneId|String|cn-hangzhou-e|可用区ID。 |
|NextToken|String|AAAAAdDWBF2\*\*\*\*|本次调用返回的查询凭证值。 |
|PageNumber|Integer|1|返回数据列表页码。 |
|PageSize|Integer|1|查询时设置的每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|70|返回的弹性网卡总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeNetworkInterfaces
&RegionId=cn-hangzhou
&PrivateIpAddress.1=192.168.**.**
&PrivateIpAddress.2=192.168.**.**
&NextToken=AAAAAdDWBF2****
&<公共请求参数>
```

正常返回示例

`XML`格式

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

`JSON`格式

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

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidUserType.NotSupported|%s|您当前的账号不支持此操作。|
|403|Abs.InvalidAccount.NotFound|%s|您的阿里云账号不存在，或者您的AccessKey已经过期。|
|400|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|403|Forbidden.NotSupportRAM|%s|暂不支持RAM用户执行该操作。|
|400|UnsupportedParameter|%s|不支持参数。|
|403|Forbidden.SubUser|%s|您的账号没有操作此资源的权限，请向主账号申请相关的权限。|
|400|InvalidParameter|%s|无效的参数。|
|400|InvalidInstanceID.Malformed|%s|参数InstanceId格式错误。|
|400|InvalidOperation.InvalidEcsState|%s|实例当前的状态不支持此操作。|
|400|InvalidOperation.InvalidEniState|%s|弹性网卡当前的状态不支持此操作。|
|400|InvalidOperation.DetachPrimaryEniNotAllowed|%s|不允许解绑实例的主网卡。|
|404|InvalidEcsId.NotFound|%s|指定的实例ID不存在。|
|404|InvalidEniId.NotFound|%s|指定的弹性网卡ID不存在。|
|404|InvalidVSwitchId.NotFound|%s|指定的交换机不存在。|
|404|InvalidSecurityGroupId.NotFound|%s|指定的安全组ID不存在。|
|403|MaxEniCountExceeded|%s|已超过可以操作的最大弹性网卡数。|
|403|EniPerInstanceLimitExceeded|%s|实例绑定的弹性网卡数量已经达到了最大限度，不能在为实例绑定弹性网卡。|
|403|InvalidOperation.AvailabilityZoneMismatch|%s|该操作无效。|
|403|InvalidOperation.VpcMismatch|%s|您的操作无效，请确认该操作中的VPC与其它参数是否匹配。|
|403|SecurityGroupInstanceLimitExceed|%s|该安全组内已有的实例数量已达到最大限制。|
|403|InvalidSecurityGroupId.NotVpc|%s|参数SecurityGroupId无效，该安全组的网络类型不是专有网络。|
|403|InvalidOperation.InvalidEniType|%s|当前弹性网卡的类型不支持此操作。|
|400|Forbidden.RegionId|%s|当前地域暂时没有提供该服务。|
|403|InvalidVpc.Empty|%s|指定的VPC下没有创建交换机，具体信息请参见错误信息%s占位符的实际返回结果。|
|400|InvalidRegionId.MalFormed|The specified parameter RegionId is not valid.|指定的RegionId不合法。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

