# RevokeSecurityGroupEgress

调用RevokeSecurityGroupEgress删除一条出方向安全组规则，撤销安全组出方向的访问权限。

## 接口说明

安全组的API文档中，流量的发起端为源端（Source），数据传输的接收端为目的端（Dest）。

-   以下任意一组参数可以确定一条安全组规则，只指定一个参数无法确定一条安全组规则。
    -   撤销对指定IP地址段的访问权限，如以下请求示例：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、（可选）SourceCidrIp和DestCidrIp。

        ```
        
                https://ecs.aliyuncs.com/?Action=RevokeSecurityGroupEgress
                &SecurityGroupId=sg-bp67acfmxazb4ph***
                &IpProtocol=tcp
                &DestCidrIp=10.0.0.0/8
                &PortRange=-22/22
                &NicType=intranet
                &Policy=accept
                &<公共请求参数>
                
        ```

    -   撤销对其他安全组的访问权限，如以下请求示例：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、（可选）SourceCidrIp和DestGroupId。

        ```
        
                https://ecs.aliyuncs.com/?Action=RevokeSecurityGroupEgress
                &SecurityGroupId=sg-bp67acfmxazb4ph***
                &DestGroupId=sg-bp67acfmxa123b****
                &IpProtocol=tcp
                &PortRange=22/22
                &NicType=intranet
                &Policy=accept
                &<公共请求参数>
                
        ```

    -   撤销关联了前缀列表的安全组规则。如以下请求示例：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、（可选）SourceCidrIp和DestPrefixListId。

        ```
        
                https://ecs.aliyuncs.com/?Action=RevokeSecurityGroupEgress
                &SecurityGroupId=sg-bp67acfmxazb4ph***
                &IpProtocol=tcp
                &DestPrefixListId=pl-x1j1k5ykzqlixdcy****
                &PortRange=-22/22
                &NicType=intranet
                &Policy=accept
                &<公共请求参数>
                
        ```

-   如果匹配的安全组规则不存在，此次RevokeSecurityGroupEgress调用成功，但不会删除任何规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=RevokeSecurityGroupEgress&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RevokeSecurityGroupEgress|系统规定参数。取值：RevokeSecurityGroupEgress |
|IpProtocol|String|是|tcp|传输层协议。不区分大小写。取值范围：

 -   icmp
-   gre
-   tcp
-   udp
-   all：支持所有协议 |
|PortRange|String|是|22/22|目的端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP协议：取值范围为1~65535。使用斜线（/）隔开起始端口和终止端口。例如：1/200
-   ICMP协议：-1/-1
-   GRE协议：-1/-1
-   all：-1/-1 |
|RegionId|String|是|cn-hangzhou|源端安全组所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|SecurityGroupId|String|是|sg-bp67acfmxazb4p\*\*\*\*|源端安全组ID。 |
|DestGroupId|String|否|sg-bp67acfmxa123b\*\*\*\*|需要撤销访问权限的目的端安全组ID。至少设置一项`DestGroupId`或者`DestCidrIp`参数。

 -   如果指定了`DestGroupId`没有指定参数`DestCidrIp`，则参数`NicType`取值只能为intranet。
-   如果同时指定了`DestGroupId`和`DestCidrIp`，则默认以`DestCidrIp`为准。 |
|DestGroupOwnerId|Long|否|12345678910|跨账户删除安全组规则时，目的端安全组所属的阿里云账户ID。

 -   如果`DestGroupOwnerId`及`DestGroupOwnerAccount`均未设置，则认为是撤销您其他安全组的访问权限。
-   如果您已经设置参数`DestCidrIp`，则参数`DestGroupOwnerId`无效。 |
|DestGroupOwnerAccount|String|否|EcsforCloud@Alibaba.com|跨账户删除安全组规则时，目的端安全组所属的阿里云账户。

 -   如果`DestGroupOwnerAccount`及`DestGroupOwnerId`均未设置，则认为是撤销您其他安全组的访问权限。
-   如果已经设置参数`DestCidrIp`，则参数`DestGroupOwnerAccount`无效。 |
|DestCidrIp|String|否|10.0.0.0/8|需要撤销访问权限的目的端IPv4 CIDR地址块。支持CIDR格式和IPv4格式的IP地址范围。

 默认值：无 |
|Ipv6DestCidrIp|String|否|2001:db8:1233:1a00::\*\*\*|需要撤销访问权限的目的端IPv6 CIDR地址块。支持CIDR格式和IPv6格式的IP地址范围。

 **说明：** 仅支持VPC类型的IP地址。

 默认值：无 |
|DestPrefixListId|String|否|pl-x1j1k5ykzqlixdcy\*\*\*\*|需要撤销访问权限的目的端前缀列表。您可以调用[DescribePrefixLists](~~205046~~)查询可以使用的前缀列表ID。

 注意事项：

 -   安全组的网络类型为经典网络时，不支持设置前缀列表。关于安全组以及前缀列表使用限制的更多信息，请参见[使用限制](~~25412~~)。
-   当您指定了`DestCidrIp`、`Ipv6DestCidrIp`、`DestGroupId`参数中的一个时，将忽略该参数。 |
|SourceCidrIp|String|否|10.0.0.0/8|源端IP地址范围。支持CIDR格式和IPv4格式的IP地址范围。

 默认值：无 |
|Ipv6SourceCidrIp|String|否|2001:db8:1234:1a00::\*\*\*|源端IPv6 CIDR地址段。支持CIDR格式和IPv6格式的IP地址范围。

 默认值：无

 **说明：** 仅支持VPC类型的IP地址。 |
|SourcePortRange|String|否|22/22|源端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP协议：取值范围为1~65535。使用斜线（/）隔开起始端口和终止端口。例如：1/200
-   ICMP协议：-1/-1
-   GRE协议：-1/-1
-   all：-1/-1 |
|Policy|String|否|accept|访问权限。取值范围：

 -   accept：接受访问。
-   drop：拒绝访问，不发回拒绝信息。

 默认值：accept |
|Priority|String|否|1|安全组规则优先级。取值范围：1~100

 默认值：1 |
|NicType|String|否|intranet|经典网络类型安全组规则的网卡类型。取值范围：

 -   internet：公网网卡
-   intranet：内网网卡

 默认值：internet

 在以下情况中，参数NicType取值只能为intranet：

 -   专有网络VPC类型安全组规则无需设置网卡类型，默认为intranet，只能为intranet。
-   设置安全组之间互相访问时，即仅指定了`DestGroupId`时，只能为intranet。 |
|ClientToken|String|否|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|Description|String|否|This is description.|安全组规则的描述。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=RevokeSecurityGroupEgress
&SecurityGroupId=sg-bp67acfmxazb4p****
&IpProtocol=tcp
&DestCidrIp=10.0.0.0/8
&PortRange=22/22
&NicType=intranet
&Policy=Allow
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<RevokeSecurityGroupEgressResponse>
       <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</RevokeSecurityGroupEgressResponse>
```

`JSON`格式

```
{
    "RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|指定的安全组在该用户账号下不存在，请您检查安全组ID是否正确。|
|400|InvalidIpProtocol.ValueNotSupported|The specified IpProtocol does not exist.|IP协议参数指定的值不支持。|
|400|InvalidIpPortRange.Malformed|The specified parameter "PortRange" is not valid.|IP协议相关的端口号范围格式不正确。|
|404|InvalidDestGroupId.NotFound|The DestGroupId provided does not exist in our records.|指定的出方向安全组不存在。|
|403|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|指定的NIC类型与规则信息冲突。|
|403|InvalidGroupAuthItem.NotFound|Specified group authorized item does not exist in our records.|指定的组授权条目不存在。|
|400|InvalidDestCidrIp.sMalformed|The specified parameter "DestCidrIp" is not valid.|指定的参数DestCidrIp不合法。|
|400|MissingParameter|The input parameter "DestGroupId" or "DestCidrIp" cannot be both blank.|参数DestGroupId和DestCidrIp不得为空。|
|400|InvalidPolicy.Malformed|The specified parameter "Policy" is not valid.|指定的参数无效，请您检查该参数是否正确。|
|400|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|指定的网络类型不存在，请您检查网络类型是否正确。|
|400|InvalidDestGroupId.Mismatch|Specified security group and destination group are not in the same VPC.|指定的安全组和目标组不在同一个VPC下。|
|400|VPCDisabled|Can't use the SecurityGroup in VPC.|VPC 不支持安全组。|
|403|InvalidSecurityGroup.IsSame|The authorized SecurityGroupId should be different from the DestGroupId.|已授权的SecurityGroupId不能与DestGroupId相同。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|InvalidDestCidrIp.Malformed|The specified parameter "DestCidrIp" is not valid.|指定的DestCidrIp无效，请您检查该参数是否正确。|
|400|MissingParameter.Dest|One of the parameters DestCidrIp, DestGroupId or DestPrefixListId must be specified.|至少需要指定参数DestCidrIp、DestGroupId或DestPrefixListId中的一个。|
|400|InvalidIpProtocol.ValueNotSupported|The parameter IpProtocol must be specified with case insensitive TCP, UDP, ICMP, GRE or All.|协议类型只能是TCP、UDP、ICMP、GRE或者All。|
|400|InvalidPriority.Malformed|The parameter Priority is invalid.|指定的参数Priority无效。|
|400|InvalidPriority.ValueNotSupported|The parameter Priority is invalid.|指定的参数Priority无效。|
|403|InvalidParamter.Conflict|The specified SecurityGroupId should be different from the SourceGroupId.|授权与被授权安全组必须不同。|
|400|InvalidDestCidrIp.Malformed|The specified parameter DestCidrIp is not valid.|指定的DestCidrIp无效，请您检查该参数是否正确。|
|400|InvalidParam.SourceIp|%s|指定的参数SourceIp无效。|
|400|InvalidParam.DestIp|%s|指定的参数DestIp无效。|
|400|InvalidParam.Ipv6DestCidrIp|%s|您输入的参数无效。|
|400|InvalidParam.Ipv6SourceCidrIp|%s|您输入的参数无效。|
|400|InvalidParam.Ipv4ProtocolConflictWithIpv6Address|%s|您输入的参数无效，请检查IPv4协议下是否填写了IPv6地址。|
|400|InvalidParam.Ipv6ProtocolConflictWithIpv4Address|%s|您输入的参数无效，请检查IPv6协议下是否填写了IPv4地址。|
|400|ILLEGAL\_IPV6\_CIDR|%s|指定的IPv6地址无效。|
|400|InvalidSecurityGroupId.Malformed|The specified parameter "SecurityGroupId" is not valid.|指定的参数SecurityGroupId无效。|
|400|InvalidSourcePortRange.Malformed|The specified parameter "SourcePortRange" is not valid.|指定的参数SourcePortRange无效。|
|400|InvalidSecurityGroupDiscription.Malformed|The specified security group rule description is not valid.|指定的安全组规则描述不合法。|
|403|InvalidOperation.ResourceManagedByCloudProduct|%s|云产品托管的安全组不支持修改操作。|
|404|InvalidPrefixListId.NotFound|The specified prefix list was not found.|前缀列表不存在。|
|404|NotSupported.GrayFunction|The prefix list is a gray-scale function, not currently supported.|前缀列表功能正在邀测中，暂不支持本次操作。|
|400|NotSupported.ClassicNetworkPrefixList|The prefix list is not supported when the network type of security group is classic.|安全组的网络类型为经典网络，不支持前缀列表。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

