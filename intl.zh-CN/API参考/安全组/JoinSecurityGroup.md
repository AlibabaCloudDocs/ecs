# JoinSecurityGroup

调用JoinSecurityGroup将一台ECS实例或一个弹性网卡加入到指定的安全组。

## 接口说明

**说明：** 该API已不推荐使用。推荐您调用[ModifyInstanceAttribute](~~25503~~)接口将ECS实例加入或移除安全组；调用[ModifyNetworkInterfaceAttribute](~~58513~~)接口将弹性网卡（ENI）加入或移除安全组。

调用该接口时，您需要注意：

-   加入安全组之前，实例必须处于**已停止**（Stopped）或者**运行中**（Running）状态。
-   一台实例最多可以加入五个安全组。
-   您可以[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)申请将实例加入更多安全组，最多不能超过16个安全组。
-   每个普通安全组最多能管理2000台实例，企业安全组最多能管理65536台实例。
-   您的安全组和实例必须属于同一个阿里云地域。
-   您的安全组和实例的网络类型必须相同。如果网络类型为专有网络VPC，则安全组和实例必须属于同一个VPC。
-   不支持同时将实例和弹性网卡加入一个安全组，即参数`InstanceId`和`NetworkInterfaceId`不能同时传值。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=JoinSecurityGroup&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|JoinSecurityGroup|系统规定参数。取值：JoinSecurityGroup |
|SecurityGroupId|String|是|sg-bp67acfmxazb4p\*\*\*\*|安全组ID。您可以调用[DescribeSecurityGroups](~~25556~~)查看您可用的安全组。 |
|InstanceId|String|否|i-bp67acfmxazb4p\*\*\*\*|实例ID。

 **说明：** 当该参数传入值时，`NetworkInterfaceId`必须为空。 |
|NetworkInterfaceId|String|否|eni-bp13kd656hxambfe\*\*\*\*|弹性网卡ID。

 **说明：** 当该参数传入值时，`InstanceId`必须为空。 |
|RegionId|String|否|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 -   实例加入安全组的操作可以不指定地域ID。
-   弹性网卡加入安全组的操作必须指定弹性网卡所在的地域ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=JoinSecurityGroup
&InstanceId=i-bp67acfmxazb4p****
&SecurityGroupId=sg-bp67acfmxazb4p****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<JoinSecurityGroupResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</JoinSecurityGroupResponse>
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
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|指定的安全组在该用户账号下不存在，请您检查安全组ID是否正确。|
|400|InstanceSecurityGroupLimitExceeded|Exceeding the allowed amount of security groups that an instance can be in.|加入安全组失败，该实例加入的安全组数量已达到上限。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|SecurityGroupInstanceLimitExceeded|The maximum number of instances in a security group is exceeded.|该安全组内已有的实例数量已达到最大限制。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|InvalidInstanceId.Mismatch|Specified instance and security group are not in the same VPC.|指定的实例和安全组不属于同一个虚拟专有网络。（包含另外两种特殊情况：1.实例不属于VPC类型，安全组属于VPC类型；2.实例属于VPC类型，安全组不属于VPC类型。）|
|403|InvalidInstanceId.AlreadyExists|The specified instance already exists in the specified security group.|指定的实例已经在指定的安全组中。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|SecurityGroupInstanceLimitExceeded|%s|该安全组内已有的实例数量已达到最大限制。|
|403|AclLimitExceed|%s|AccessPoint已超出限额值。|
|403|InstanceSecurityGroupLimitExceeded|%s|实例绑定的安全组数量达到最大限制。|
|400|InvalidInstanceId.Malformed|The specified parameter "InstanceId" is not valid.|指定的参数InstanceId格式有误。|
|403|InvalidOperation.ResourceManagedByCloudProduct|%s|云产品托管的安全组不支持修改操作。|
|404|InvalidEniId.NotFound|%s|指定的弹性网卡ID不存在。|
|403|InvalidOperation.InvalidEniType|%s|当前弹性网卡的类型不支持此操作。|
|400|InvalidOperation.InvalidEniState|%s|弹性网卡当前的状态不支持此操作。|
|403|InvalidOperation.VpcMismatch|%s|您的操作无效，请确认该操作中的VPC与其它参数是否匹配。|
|400|NotBelongUser|%s|您没有权限操作此资源，请检查操作的资源是否正确。|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|RegionId是必选参数。|
|403|InvalidOperation.EniServiceManaged|%s|操作无效。|
|403|InvalidParam.EniIdAndInstanceId.Conflict|%s|InstanceId与NetworkInterfaceId两者冲突。两个参数不能同时被赋值。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

