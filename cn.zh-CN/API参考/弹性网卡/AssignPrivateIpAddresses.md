# AssignPrivateIpAddresses

调用AssignPrivateIpAddresses为一块弹性网卡分配一个或多个辅助私有IP地址。可以为网卡指定在所属交换机（VSwitch）的空闲私有IP地址，或者通过指定私有网络地址数量自动分配私有IP地址。

## 接口说明

-   只支持可用（Available）或者已绑定（InUse）状态下的弹性网卡。
-   操作主网卡时，网卡附加的实例必须处于运行中（Running）或者已停止（Stopped）状态。
-   网卡处于可用（Available）状态时，最多可以分配10个辅助私有IP地址。一旦挂载到实例上，网卡能分配的辅助私有IP地址数将受到实例规格限制。更多详情，请参见[实例规格族](~~25378~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=AssignPrivateIpAddresses&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AssignPrivateIpAddresses|系统规定参数。取值：AssignPrivateIpAddresses |
|NetworkInterfaceId|String|是|eni-bp67acfmxazb4p\*\*\*\*|弹性网卡ID。 |
|RegionId|String|是|cn-hangzhou|弹性网卡所属的地域。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|PrivateIpAddress.N|RepeatList|否|10.1.\*\*.\*\*|从弹性网卡所属交换机的空闲IP地址中选择一个或多个辅助私有IP地址。N的取值范围：

 -   弹性网卡处于可用（`Available`）状态：1~10。
-   弹性网卡处于已绑定（`InUse`）状态：受到实例规格限制，更多详情，请参见[实例规格族](~~25378~~)。

 分配辅助私有IP地址时，您不能同时指定参数`PrivateIpAddress.N`和参数`SecondaryPrivateIpAddressCount`。 |
|SecondaryPrivateIpAddressCount|Integer|否|1|指定私有IP地址数量，自动从交换机的空闲IP地址中分配IP地址。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AssignedPrivateIpAddressesSet|Struct| |已分配辅助私有IP地址的弹性网卡集合。 |
|NetworkInterfaceId|String|eni-bp125p95hhdhn3ot\*\*\*\*|弹性网卡ID。 |
|PrivateIpSet|List|\[ "192.168.\*\*.\*\*" \]|私网IP地址集合。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=AssignPrivateIpAddresses
&NetworkInterfaceId=eni-bp67acfmxazb4p****
&RegionId=cn-hangzhou
&PrivateIpAddress.1=10.1.**.**
&PrivateIpAddress.2=10.1.**.**
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<AssignPrivateIpAddressesResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <AssignedPrivateIpAddressesSet>
            <PrivateIpSet>
                  <PrivateIpAddress>192.168.**.**</PrivateIpAddress>
            </PrivateIpSet>
            <NetworkInterfaceId>eni-bp125p95hhdhn3ot****</NetworkInterfaceId>
      </AssignedPrivateIpAddressesSet>
</AssignPrivateIpAddressesResponse>
```

`JSON`格式

```
{
	"RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"AssignedPrivateIpAddressesSet": {
		"PrivateIpSet": {
			"PrivateIpAddress": [
				"192.168.**.**"
			]
		},
		"NetworkInterfaceId": "eni-bp125p95hhdhn3ot****"
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Throttling|Request was denied due to request throttling.|当前的操作太过频繁，请稍后重试。|
|400|UnsupportedParameter|%s|不支持参数。|
|400|InvalidParameter|%s|无效的参数。|
|400|InvalidInstanceID.Malformed|%s|参数InstanceId格式错误。|
|400|InvalidOperation.InvalidEcsState|%s|实例当前的状态不支持此操作。|
|400|InvalidOperation.InvalidEniState|%s|弹性网卡当前的状态不支持此操作。|
|400|InvalidOperation.DetachPrimaryEniNotAllowed|%s|不允许解绑实例的主网卡。|
|400|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|400|Forbidden.RegionId|%s|当前地域暂时没有提供该服务。|
|400|InvalidAction|%s|操作无效。|
|400|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicated.|指定的私网IP已经被使用，请您更换IP再重试。|
|403|InvalidUserType.NotSupported|%s|您当前的账号不支持此操作。|
|403|Abs.InvalidAccount.NotFound|%s|您的阿里云账号不存在，或者您的AccessKey已经过期。|
|403|Forbidden.NotSupportRAM|%s|暂不支持RAM用户执行该操作。|
|403|Forbidden.SubUser|%s|您的账号没有操作此资源的权限，请向主账号申请相关的权限。|
|403|MaxEniCountExceeded|%s|已超过可以操作的最大弹性网卡数。|
|403|EniPerInstanceLimitExceeded|%s|实例绑定的弹性网卡数量已经达到了最大限度，不能在为实例绑定弹性网卡。|
|403|InvalidOperation.AvailabilityZoneMismatch|%s|该操作无效。|
|403|InvalidOperation.VpcMismatch|%s|您的操作无效，请确认该操作中的VPC与其它参数是否匹配。|
|403|SecurityGroupInstanceLimitExceed|%s|该安全组内已有的实例数量已达到最大限制。|
|403|InvalidSecurityGroupId.NotVpc|%s|参数SecurityGroupId无效，该安全组的网络类型不是专有网络。|
|403|InvalidOperation.InvalidEniType|%s|当前弹性网卡的类型不支持此操作。|
|403|InvalidVSwitchId.IpNotEnough|%s|指定的交换机内IP数量不足。|
|403|InvalidVSwitchId.IpInvalid|%s|指定的私网IP无效。|
|403|InvalidIp.IpAssigned|%s|指定的IP已被分配。|
|403|MaxEniPrivateIpsCountExceeded|%s|指定的ENI分配的辅助私网IP数量超过限制，具体信息请参见错误信息%s占位符的实际返回结果。|
|403|Operation.Conflict|%s|您当前的操作与其它正在执行的操作有冲突，请稍后重试。|
|403|InvalidOperation.Ipv4CountExceeded|%s|IPv4数量达到上限，导致该操作无效。|
|403|InvalidOperation.EniServiceManaged|%s|操作无效。|
|403|InvalidIp.IpRepeated|%s|指定的IP重复。|
|404|InvalidEcsId.NotFound|%s|指定的实例ID不存在。|
|404|InvalidEniId.NotFound|%s|指定的弹性网卡ID不存在。|
|404|InvalidVSwitchId.NotFound|%s|指定的交换机不存在。|
|404|InvalidSecurityGroupId.NotFound|%s|指定的安全组ID不存在。|
|404|InvalidInstanceId.NotFound|%s|指定的实例不存在，请确认参数InstanceId是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

