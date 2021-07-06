# UnassignIpv6Addresses

若弹性网卡已被分配了IPv6地址，调用UnassignIpv6Addresses可以回收一个或多个IPv6地址。

## 接口说明

调用该接口时，您需要注意：

-   弹性网卡必须处于**可用**（Available）或**已挂载**（InUse）状态。
-   主网卡关联的ECS实例必须处于**运行中**（Running）或**已停止**（Stopped）状态。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=UnassignIpv6Addresses&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UnassignIpv6Addresses|系统规定参数。取值：UnassignIpv6Addresses |
|Ipv6Address.N|RepeatList|是|2001:db8:1234:1a00::\*\*\*|为弹性网卡指定一个或多个IPv6地址。N的取值范围仅支持1。 |
|NetworkInterfaceId|String|是|eni-bp14v2sdd3v8ht\*\*\*\*|弹性网卡ID。 |
|RegionId|String|是|cn-hangzhou|弹性网卡所在地域的ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=UnassignIpv6Addresses
&Ipv6Address.1=2001:db8:1234:1a00::***
&NetworkInterfaceId=eni-bp14v2sdd3v8ht****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<UnassignIpv6AddressesResponse>
      <RequestId>48285314-3192-47FE-B4C8-9D51E7Fxxxxx</RequestId>
</UnassignIpv6AddressesResponse>
```

`JSON` 格式

```
{
    "RequestId": "48285314-3192-47FE-B4C8-9D51E7Fxxxxx"
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
|400|InvalidOperation.InvalidEcsState|%s|实例当前的状态不支持此操作。|
|400|InvalidOperation.InvalidEniState|%s|弹性网卡当前的状态不支持此操作。|
|404|InvalidEniId.NotFound|%s|指定的弹性网卡ID不存在。|
|403|InvalidOperation.InvalidEniType|%s|当前弹性网卡的类型不支持此操作。|
|403|InvalidIp.IpUnassigned|%s|指定的IP未被分配。|
|403|InvalidIp.IpRepeated|%s|指定的IP重复。|
|403|InvalidIp.Address|%s|指定的IPv6地址无效。|
|403|Forbidden.RegionId|%s|当前地域暂时没有提供该服务。|
|403|InvalidOperation.EniServiceManaged|%s|操作无效。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

