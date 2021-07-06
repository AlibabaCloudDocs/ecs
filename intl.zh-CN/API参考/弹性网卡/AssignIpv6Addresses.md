# AssignIpv6Addresses

调用AssignIpv6Addresses为弹性网卡分配一个或多个IPv6地址。

## 接口说明

您可以指定弹性网卡所属交换机下CIDR的IPv6地址，也可以指定IPv6地址数量自动创建IPv6地址。

-   弹性网卡必须处于**可用**（`Available`）或**已挂载**（`InUse`）状态。
-   主网卡关联的ECS实例必须处于**运行中**（`Running`）或**已停止**（`Stopped`）状态。
-   单个网卡能够分配的IPv6地址数量和网卡附加的实例规格有关。
    -   如果弹性网卡处于**可用**（`Available`）状态，最多可以分配10个IPv6地址。
    -   如果弹性网卡挂载到实例上，能够分配的IPv6地址数将受到实例规格限制。更多信息，请参见[实例规格族](~~25378~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=AssignIpv6Addresses&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AssignIpv6Addresses|系统规定参数。取值：AssignIpv6Addresses |
|RegionId|String|是|cn-hangzhou|弹性网卡所在地域的ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|NetworkInterfaceId|String|是|eni-bp1iqejowblx6h8j\*\*\*\*|弹性网卡ID。 |
|Ipv6Address.N|RepeatList|否|2001:db8:1234:1a00::\*\*\*|为弹性网卡指定一个或多个IPv6地址。N的取值范围仅支持1。

 取值示例：Ipv6Address.1=2001:db8:1234:1a00::\*\*\*

 **说明：** 调用该接口时，您必须设置`Ipv6Addresses.N`参数或者`Ipv6AddressCount`参数的其中一个，但不能同时设置这两个参数。 |
|Ipv6AddressCount|Integer|否|1|为弹性网卡指定随机生成的IPv6地址数量。

 **说明：** 调用该接口时，您必须设置`Ipv6Addresses.N`参数或者`Ipv6AddressCount`参数的其中一个，但不能同时设置这两个参数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=AssignIpv6Addresses
&NetworkInterfaceId=eni-bp1iqejowblx6h8j****
&RegionId=cn-hangzhou
&Ipv6Address.1=2001:db8:1234:1a00::***
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<AssignIpv6AddressesResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AssignIpv6AddressesResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidUserType.NotSupported|%s|您当前的账号不支持此操作。|
|403|Abs.InvalidAccount.NotFound|%s|您的阿里云账号不存在，或者您的AccessKey已经过期。|
|403|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|403|Forbedden.NotSupportRAM|%s|暂不支持RAM用户执行该操作。|
|400|UnsupportedParameter|%s|不支持参数。|
|403|Forbbiden.SubUser|%s|您的账号没有操作此资源的权限，请向主账号申请相关的权限。|
|400|InvalidParameter|%s|无效的参数。|
|400|InvalidInstanceID.Malformed|%s|参数InstanceId格式错误。|
|400|InvalidParams.EniId|%s|指定的参数EniId无效。|
|400|InvalidOperation.InvalidEcsState|%s|实例当前的状态不支持此操作。|
|400|InvalidOperation.InvalidEniState|%s|弹性网卡当前的状态不支持此操作。|
|404|InvalidEniId.NotFound|%s|指定的弹性网卡ID不存在。|
|403|InvalidOperation.InvalidEniType|%s|当前弹性网卡的类型不支持此操作。|
|403|MaxEniIpv6IpsCountExceeded|%s|该弹性网卡挂载的IPv6个数达到上限。|
|403|InvalidIp.IpUnassigned|%s|指定的IP未被分配。|
|403|InvalidIp.IpRepeated|%s|指定的IP重复。|
|403|InvalidIp.IpAssigned|%s|指定的IP已被分配。|
|403|InvalidIp.Address|%s|指定的IPv6地址无效。|
|403|InvalidOperation.Ipv4CountExceeded|%s|IPv4数量达到上限，导致该操作无效。|
|403|InvalidOperation.Ipv6CountExceeded|%s|IPv6数量达到上限，导致该操作无效。|
|403|InvalidOperation.Ipv6NotSupport|%s|IPv6不支持当前操作。|
|403|InvalidVSwitch.Ipv6NotTurnOn|%s|您当前使用的交换机没有开启IPv6功能，请先开启此功能后重试。|
|403|InvalidVSwitchId.IpInvalid|%s|指定的私网IP无效。|
|403|Forbidden.RegionId|%s|当前地域暂时没有提供该服务。|
|403|InvalidOperation.EniServiceManaged|%s|操作无效。|
|400|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicated.|指定的私网IP已经被使用，请您更换IP再重试。|
|403|SecurityGroupInstanceLimitExceed|%s|该安全组内已有的实例数量已达到最大限制。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

