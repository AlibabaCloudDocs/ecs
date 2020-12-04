# DetachNetworkInterface

调用DetachNetworkInterface从一台ECS实例上分离一个弹性网卡（ENI）。

## 接口描述

调用该接口时，您需要注意：

-   不允许分离实例主网卡。
-   弹性网卡必须处于解绑中（Detaching）或者已绑定（InUse）状态。
-   实例必须处于运行中（Running）或者已停止（Stopped）状态。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DetachNetworkInterface&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DetachNetworkInterface|系统规定参数。取值：DetachNetworkInterface |
|InstanceId|String|是|i-bp67acfmxazb4p\*\*\*\*|实例ID。 |
|NetworkInterfaceId|String|是|eni-bp67acfmxazb4p\*\*\*\*|弹性网卡ID。 |
|RegionId|String|是|cn-hangzhou|资源所属地域。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DetachNetworkInterface
&InstanceId=i-bp67acfmxazb4p****
&NetworkInterfaceId=eni-bp67acfmxazb4p****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DetachNetworkInterfaceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachNetworkInterfaceResponse>
```

`JSON` 格式

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
|400|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|403|Forbidden.NotSupportRAM|%s|暂不支持RAM用户执行该操作。|
|400|UnsupportedParameter|%s|不支持参数。|
|403|Forbidden.SubUser|%s|您的账号没有操作此资源的权限，请向主账号申请相关的权限。|
|400|InvalidParameter|%s|无效的参数。|
|400|InvalidInstanceID.Malformed|%s|参数InstanceId格式错误。|
|400|InvalidOperation.InvalidRegion|%s|指定的参数RegionId无效。|
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
|400|InvalidParams.EniId|%s|指定的参数EniId无效。|
|403|InvalidOperation.EniServiceManaged|%s|操作无效。|
|403|InvalidOperation.EniLinked|%s|实例的当前弹性网卡关联了其他弹性网卡，导致操作无效。需要解除关联后才能从实例解绑。|
|403|InvalidInstanceId.NotFound|%s|指定的实例不存在，请确认参数InstanceId是否正确。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

