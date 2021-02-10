# CreateNetworkInterface

调用CreateNetworkInterface创建一个弹性网卡（ENI）。

## 接口说明

-   新创建的弹性网卡处于可用（Available）状态。
-   弹性网卡只支持附加到同一可用区的VPC类型实例。
-   一个弹性网卡只能附加到一台实例。附加到新实例之前您需要将其与当前实例分离。
-   弹性网卡重新附加到另一台实例时，其属性不变，网络流量也会重定向到新的实例。
-   一个账号在一个阿里云地域内默认最多可创建100个弹性网卡。如果需要更多，请[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)申请。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateNetworkInterface&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateNetworkInterface|系统规定参数。取值：CreateNetworkInterface |
|RegionId|String|是|cn-hangzhou|实例所在地域的ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|VSwitchId|String|是|vsw-bp1s5fnvk4gn2tws03\*\*\*\*|指定VPC的交换机ID。弹性网卡的私网IP地址在交换机的IP地址段内的空闲地址中取值。 |
|Tag.N.Key|String|否|TestKey|弹性网卡的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|Tag.N.Value|String|否|TestValue|弹性网卡的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以acs:开头，不能包含http://或者https://。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4ph\*\*\*\*|资源组ID。 |
|PrimaryIpAddress|String|否|172.17.\*\*.\*\*|弹性网卡的主私有IP地址。

 指定IP必须是在所属交换机的地址段内的空闲地址，不指定则默认随机分配该交换机中的空闲地址。 |
|SecurityGroupId|String|否|sg-bp1fg655nh68xyz9i\*\*\*\*|加入一个安全组。安全组和弹性网卡必须在同一个专有网络VPC中。 |
|SecurityGroupIds.N|RepeatList|否|sg-bp1fg655nh68xyz9i\*\*\*\*|加入一个或多个安全组。安全组和弹性网卡必须在同一个专有网络VPC中。N的取值范围与弹性网卡能够加入安全组配额有关，更多详情，请参见[使用限制](~~25412~~)。

 **说明：** 不支持同时指定`SecurityGroupId`和`SecurityGroupIds.N`。 |
|NetworkInterfaceName|String|否|testNetworkInterfaceName|弹性网卡名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空 |
|Description|String|否|testDescription|弹性网卡的描述信息。长度为2~256个英文或中文字符，不能以http://和https://开头。

 默认值：空 |
|PrivateIpAddress.N|RepeatList|否|172.17.\*\*.\*\*|从弹性网卡所属交换机的CIDR地址段内的空闲地址中选择一个或多个辅助私有IP地址。N的取值范围：0~10

 **说明：** 分配辅助私有IP地址时，您不能同时指定参数`PrivateIpAddress.N`和参数`SecondaryPrivateIpAddressCount`。 |
|SecondaryPrivateIpAddressCount|Integer|否|1|指定私有IP地址数量，让ECS为您自动创建IP地址。 |
|QueueNumber|Integer|否|1|弹性网卡队列数。取值范围：1~2048

 绑定弹性网卡时，该值必须少于实例规格支持单块网卡的最大队列数。实例规格的单块网卡最大队列数可以通过[DescribeInstanceTypes](~~25620~~)接口查询`MaximumQueueNumberPerEni`字段。

 默认值：空。在绑定时会采用实例规格的弹性网卡默认队列数，实例规格的弹性网卡默认队列数可以通过[DescribeInstanceTypes](~~25620~~)接口查询`SecondaryEniQueueNumber`字段。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Description|String|testDescription|弹性网卡的描述信息。 |
|MacAddress|String|00:16:3e:12:\*\*:\*\*|弹性网卡的MAC地址。 |
|NetworkInterfaceId|String|eni-bp14v2sdd3v8htlnm\*\*\*|弹性网卡ID。 |
|NetworkInterfaceName|String|my-eni-name|弹性网卡的名称。 |
|OwnerId|String|123456\*\*\*\*|弹性网卡的所属账号ID。 |
|PrivateIpAddress|String|172.17.\*\*.\*\*|弹性网卡的私网IP地址。 |
|PrivateIpSets|Array of PrivateIpSet| |PrivateIpSet组成的集合。 |
|PrivateIpSet| | | |
|Primary|Boolean|true|是否是主私网IP地址。 |
|PrivateIpAddress|String|172.17.\*\*.\*\*|实例的私网IP地址。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
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

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateNetworkInterface
&RegionId=cn-hangzhou
&SecurityGroupIds.1=sg-bp1fg655nh68xyz9i****
&SecurityGroupIds.2=sg-bp67acfmxazb4ph****
&VSwitchId=vsw-bp1s5fnvk4gn2tws03****
&Tag.1.Key=TestKey
&Tag.1.Value=TestValue
&ResourceGroupId=rg-bp67acfmxazb4ph****
&PrimaryIpAddress=172.17.**.**
&NetworkInterfaceName=testNetworkInterfaceName
&Description=testDescription
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateNetworkInterfaceResponse>
      <Description>testDescription</Description>
      <MacAddress>00:16:3e:12:**:**</MacAddress>
      <NetworkInterfaceName>my-eni-name</NetworkInterfaceName>
      <PrivateIpAddress>172.17.**.**</PrivateIpAddress>
      <RequestId>0910A187-1002-4488-9FE5-EF770D142B73</RequestId>
      <ResourceGroupId>rg-2ze88m67qx5z****</ResourceGroupId>
      <VSwitchId>vsw-bp16usj2p27htro3****</VSwitchId>
      <VpcId>vpc-bp1j7w3gc1cexjqd****</VpcId>
      <ZoneId>cn-hangzhou-e</ZoneId>
      <NetworkInterfaceId>eni-bp1bighqoqowq73yw91r</NetworkInterfaceId>
      <Status>InUse</Status>
      <SecurityGroupIds>
            <SecurityGroupId>sg-bp18kz60mefsicfg****</SecurityGroupId>
      </SecurityGroupIds>
      <Type>Primary</Type>
      <OwnerId>123456****</OwnerId>
      <PrivateIpSets>
            <PrivateIpSet>
                  <PrivateIpAddress>192.168.0.49</PrivateIpAddress>
                  <Primary>true</Primary>
            </PrivateIpSet>
      </PrivateIpSets>
</CreateNetworkInterfaceResponse>
```

`JSON`格式

```
{
	"Description": "testDescription",
	"MacAddress": "00:16:3e:12:**:**",
	"NetworkInterfaceName":"my-eni-name",
	"PrivateIpAddress": "172.17.**.**",
	"RequestId": "0910A187-1002-4488-9FE5-EF770D142B73",
	"ResourceGroupId": "rg-2ze88m67qx5z****",
	"VSwitchId": "vsw-bp16usj2p27htro3****",
	"VpcId": "vpc-bp1j7w3gc1cexjqd****",
	"ZoneId": "cn-hangzhou-e",
	"NetworkInterfaceId": "eni-bp1bighqoqowq73yw91r",
	"Status": "InUse",
	"SecurityGroupIds": {
		"SecurityGroupId": [
			"sg-bp18kz60mefsicfg****"
		]
	},
	"Type": "Primary",
	"OwnerId": "123456****",
	"PrivateIpSets": {
		"PrivateIpSet": [
			{
				"PrivateIpAddress": "192.168.0.49",
				"Primary": true
			}
		]
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
|403|InvalidVSwitchId.IpNotEnough|%s|指定的交换机内IP数量不足。|
|403|InvalidVSwitchId.IpInvalid|%s|指定的私网IP无效。|
|400|Forbidden.RegionId|%s|当前地域暂时没有提供该服务。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签中存在重复的键，请保持键的唯一性。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键参数有误。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值参数有误。|
|403|QuotaExceed.Tags|%s|标签数超过可以配置的最大数量。|
|400|JoinedGroupLimitExceed|%s|指定资源所能加入的安全组数量达到上限。具体信息请参见错误信息%s占位符的实际返回结果。|
|403|InvalidIp.Address|%s|指定的IPv6地址无效。|
|403|InvalidIp.IpRepeated|%s|指定的IP重复。|
|403|MaxEniPrivateIpsCountExceeded|%s|指定的ENI分配的辅助私网IP数量超过限制，具体信息请参见错误信息%s占位符的实际返回结果。|
|400|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicated.|指定的私网IP已经被使用，请您更换IP再重试。|
|400|InvalidParameter.Conflict|%s|您输入的参数无效，请检查参数之间是否冲突。|
|403|InvalidOperation.ResourceManagedByCloudProduct|%s|云产品托管的安全组不支持修改操作。|
|403|InvalidParameter.InvalidEniQueueNumber|%s|弹性网卡队列数有误，具体信息请参见错误信息%s占位符的实际返回结果。|
|403|InvalidOperation.MaxEniQueueNumberExceeded|%s|弹性网卡队列数超过上限，具体信息请参见错误信息%s占位符的实际返回结果。|
|403|InvalidOperation.ExceedInstanceTypeQueueNumber|%s|弹性网卡队列总数超过上限，具体信息请参见错误信息%s占位符的实际返回结果。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

