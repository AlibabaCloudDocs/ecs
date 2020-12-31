# ModifyInstanceAttribute

调用ModifyInstanceAttribute修改一台ECS实例的部分信息，包括实例密码、名称、描述、主机名、所属安全组和自定义数据等。如果是突发性能实例，还可以切换这台实例的性能突发模式。

## 接口说明

查询ECS实例信息时，如果返回数据中包含`{"OperationLocks": {"LockReason" : "security"}}`，则禁止一切操作。

调用该接口完成以下操作时，您需要注意：

-   修改主机名（`HostName`）：重启实例后，修改生效，且必须是[在ECS控制台重启](~~25440~~)或者调用API [RebootInstance](~~25502~~)重启，新主机名才能生效。在操作系统内部重启不能生效。
-   重置密码（`Password`）：
    -   实例状态不能为**启动中**（`Starting`）。
    -   重启实例后，重置生效，且必须是[在ECS控制台重启](~~25440~~)或者调用API [RebootInstance](~~25502~~)重启，新密码才能生效。在操作系统内部重启不能生效。
-   修改自定义数据（`UserData`）：
    -   实例状态必须为**已停止**（`Stopped`）。
    -   实例必须满足自定义数据使用限制。详情请参见[生成实例自定义数据](~~49121~~)。
-   更换实例安全组（`SecurityGroupIds.N`）：
    -   支持切换安全组类型。

        当ECS实例跨类型切换安全组时，您需要充分了解两种安全组规则的配置区别，避免影响实例网络。

    -   不支持经典网络类型实例。

        其他注意事项请参见`SecurityGroupIds.N`的参数说明。

-   修改主网卡队列数（`NetworkInterfaceQueueNumber`）：
    -   实例必须为已停止（`Stopped`）状态。
    -   不能超过实例规格允许的单块网卡最大队列数。
    -   实例的所有网卡累加队列数不能超过实例规格允许的队列数总配额。实例规格的单块网卡最大队列数和总配额可以通过[DescribeInstanceTypes](~~25620~~)接口查询`MaximumQueueNumberPerEni`、`TotalEniQueueQuantity`字段。
    -   当取值为-1时，将重置主网卡队列数为对应实例规格的默认值。实例规格的弹性网卡默认队列数可以通过[DescribeInstanceTypes](~~25620~~)接口查询 `PrimaryEniQueueNumber`字段。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceAttribute&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyInstanceAttribute|系统规定参数。取值：ModifyInstanceAttribute |
|InstanceId|String|是|i-bp67acfmxazb4ph\*\*\*\*|实例ID。 |
|Password|String|否|Test123456|实例的密码。支持长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号中的三类字符。特殊符号可以是：

 ```

()`~!@#$%^&*-_+=|{}[]:;'<>,.?/

```

 其中，Windows实例不能以斜线号（/）为密码首字符。

 **说明：** 如果传入`Password`参数，建议您使用HTTPS协议发送请求，避免密码泄露。 |
|HostName|String|否|testHostName|操作系统的主机名。修改主机名后，请调用RebootInstance使修改生效。

 -   Windows Server系统：长度为2-15个字符，允许使用大小写字母、数字或连字符（-）。不能以连字符（-）开头或结尾，不能连续使用连字符（-），也不能仅使用数字。
-   其他类型实例（Linux等）：长度为2-64个字符，允许使用点号（.）分隔字符成多段，每段允许使用大小写字母、数字或连字符（-），但不能连续使用点号（.）或连字符（-）。不能以点号（.）或连字符（-）开头或结尾。 |
|InstanceName|String|否|testInstanceName|实例名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|Description|String|否|testInstanceDescription|实例描述。长度为2~256个英文或中文字符，不能以http://和https://开头。

 默认值：无 |
|UserData|String|否|ZWNobyBoZWxsbyBlY3Mh|实例自定义数据，需要以Base64编码。

 编码前，原始数据不能超过16KB。建议不要明文传入敏感信息，例如密码和私钥等。如果必须传入敏感信息，建议您加密后再以Base64编码传入，在实例内部以同样的方式解密。 |
|CreditSpecification|String|否|Standard|修改突发性能实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的性能约束模式章节。
-   Unlimited：无性能约束模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的无性能约束模式章节。

 默认值：无 |
|DeletionProtection|Boolean|否|false|实例释放保护属性，指定是否支持通过控制台或API（[DeleteInstance](~~25507~~)）释放实例。

 默认值：无

 **说明：** 该属性仅适用于按量付费实例，且只能限制手动释放操作，对系统释放操作不生效。 |
|SecurityGroupIds.N|RepeatList|否|sg-bp15ed6xe1yxeycg7o\*\*\*\*|实例重新加入的安全组列表。

 -   安全组ID不能重复。
-   实例会离开当前的安全组，如需保留设置，您需要在列表中添加当前的安全组ID。
-   支持切换安全组类型，但设置的安全组列表中不能同时包含普通安全组和企业安全组。
-   安全组必须和实例属于同一个VPC。
-   N的取值范围与实例能够加入安全组配额有关，更多详情，请参见[使用限制](~~25412#SecurityGroupQuota1~~)安全组章节。
-   修改安全组后很快会生效于对应的实例，但可能有较小的延迟。 |
|NetworkInterfaceQueueNumber|Integer|否|8|主网卡队列数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceAttribute
&InstanceId=i-bp67acfmxazb4ph****
&Action=ModifyInstanceAttribute
&CreditSpecification=Standard
&DeletionProtection=false
&Description=testInstanceDescription
&HostName=testHostName
&InstanceName=testInstanceName
&Password=Test123456
&SecurityGroupIds.1=sg-bp15ed6xe1yxeycg7o****
&SecurityGroupIds.2=sg-bp15ed6xe1yxeycg7p****
&SecurityGroupIds.3=sg-bp15ed6xe1yxeycg7q****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyInstanceAttributeResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceAttributeResponse>
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
|400|InvalidInstanceName.Malformed|The specified parameter "InstanceName" is not valid.|指定的实例名称格式不合法。长度为2-128个字符，以英文字母或中文开头，可包含数字，点号（.），下划线（\_）或连字符（-）。不能以http://和https://开头。|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|400|InvalidHostPassword.Malformed|The specified parameter "Password" is not valid.|指定的实例密码格式不合法。|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|指定的HostName格式不合法。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|指定的安全组在该用户账号下不存在，请您检查安全组ID是否正确。|
|403|OperationDenied|The instance amount in the specified SecurityGroup reach its limit.|指定安全组的实例数已达最大值。|
|403|OperationDenied|The current status of the resource does not support this operation.|该资源状态不支持此类操作。|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|指定的Password参数不合法。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InvalidUserData.Forbidden|User not authorized to input the parameter "UserData"please apply for permission "UserData"|该用户无权输入UserData。请先申请权限。|
|400|InvalidUserData.SizeExceeded|The specified parameter "UserData" exceeds the size.|指定的UserData超过大小限制。|
|400|InvalidUserData.NotSupported|The specified parameter "UserData" only support the vpc and IoOptimized Instance.|指定的UserData仅支持VPC和I/O优化型实例。|
|400|ImageNotSupportCloudInit|The specified image does not support cloud-init.|指定的镜像不支持cloud-init。|
|400|ChargeTypeViolation|Pay-As-You-Go instances do not support this operation.|按量付费实例不支持该操作，检查实例的付费类型是否与该操作冲突。|
|400|InvalidParameter.RecycleBin|You do not have permission to set recyclable properties.|您未被授权执行该操作。|
|400|InvalidParameter.CreditSpecification|The specified CreditSpecification is not supported in this region.|该地区不支持指定的信贷规范。|
|400|InvalidInstanceStatus.CreditSpecRestricted|The current status of the resource does not support this operation.|当前资源的状态不支持此操作。|
|400|InvalidInstanceStatus.NotRunning|The current status of the resource is invalid, you can only do this operation when instance is running.|当前实例的状态不支持此操作，当实例状态为Running时再进行此操作。|
|404|Credit.NotFound|The specified credit information does not exist.|指定的信用信息不存在。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InvalidUser.Unauthorized|The user is not authorized|您当前使用的账号无权限。|
|403|SecurityGroupInstanceLimitExceed|%s|该安全组内已有的实例数量已达到最大限制。|
|403|InstanceNotInSecurityGroup|The instance not in the group.|指定的实例不在安全组内。|
|403|InvalidOperation.InvalidRegion|%s|指定的参数RegionId无效。|
|400|InvalidParameter|The specified parameter is not valid.|无效的参数，请检查该参数是否正确。|
|403|OperationDenied|The specified Image is disabled or is deleted.|指定的镜像被禁用或被删除。|
|400|InvalidOperation.InvalidEcsState|%s|实例当前的状态不支持此操作。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

