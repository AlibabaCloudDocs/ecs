# ModifyNetworkInterfaceAttribute

调用ModifyNetworkInterfaceAttribute修改一个弹性网卡（ENI）的名称、描述以及所属安全组等。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyNetworkInterfaceAttribute&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyNetworkInterfaceAttribute|系统规定参数。取值：ModifyNetworkInterfaceAttribute |
|NetworkInterfaceId|String|是|eni-bp67acfmxazb4p\*\*\*\*|弹性网卡ID。 |
|RegionId|String|是|cn-hangzhou|弹性网卡所在地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|SecurityGroupId.N|RepeatList|否|sg-bp67acfmxazb4p\*\*\*\*|SecurityGroupId列表，弹性网卡最终加入的安全组，并会移出已有的安全组。N的取值范围为1-5。

 **说明：** 修改安全组后很快会生效，但可能有较小的延迟。 |
|NetworkInterfaceName|String|否|eniTestName|弹性网卡的名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以`http://`和`https://`开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空 |
|QueueNumber|Integer|否|8|网卡队列数。取值范围：1~2048

 -   只允许修改辅助网卡队列数。
-   允许修改处于可用状态（`Available`）的辅助网卡队列数，或者已绑定（`InUse`）至实例但实例为已停止（`Stopped`）状态的辅助网卡队列数。
-   辅助网卡队列数不能超过实例规格允许的单块网卡最大队列数，同时实例的所有网卡累加队列数不能超过实例规格允许的队列数总配额。实例规格的单块网卡最大队列数和总配额可以通过[DescribeInstanceTypes](~~25620~~)接口查询`MaximumQueueNumberPerEni`、`TotalEniQueueQuantity`字段。 |
|Description|String|否|testDescription|弹性网卡的描述信息。 长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。

 默认值：空 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyNetworkInterfaceAttribute
&NetworkInterfaceId=eni-bp67acfmxazb4p****
&RegionId=cn-hangzhou
&SecurityGroupId.1=sg-bp67acfmxazb4p****
&NetworkInterfaceName=eniTestName
&Description=testDescription
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DetachNetworkInterfaceResponse>
        <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</DetachNetworkInterfaceResponse>
```

`JSON`格式

```
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx"
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
|400|InvalidParams.EniId|%s|指定的参数EniId无效。|
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
|403|InvalidOperation.EniServiceManaged|%s|操作无效。|
|403|InvalidOperation.ResourceManagedByCloudProduct|%s|云产品托管的安全组不支持修改操作。|
|403|InvalidParameter.InvalidEniQueueNumber|%s|弹性网卡队列数有误，具体信息请参见错误信息%s占位符的实际返回结果。|
|403|InvalidOperation.MaxEniQueueNumberExceeded|%s|弹性网卡队列数超过上限，具体信息请参见错误信息%s占位符的实际返回结果。|
|403|InvalidOperation.ExceedInstanceTypeQueueNumber|%s|弹性网卡队列总数超过上限，具体信息请参见错误信息%s占位符的实际返回结果。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

