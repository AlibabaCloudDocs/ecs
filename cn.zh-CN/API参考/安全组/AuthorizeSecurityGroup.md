# AuthorizeSecurityGroup

调用AuthorizeSecurityGroup增加一条入方向安全组规则。指定安全组入方向的访问权限，允许或者拒绝其他设备发送入方向流量到安全组里的实例。

## 接口说明

安全组的API文档中，流量的发起端为源端（Source），数据传输的接收端为目的端（Dest）。

调用该接口时，您需要了解：

-   出方向和入方向安全组规则总和不能超过200条。
-   安全组规则优先级（Priority）可选范围为1~100。数字越小，代表优先级越高。
-   优先级相同的安全组规则，以拒绝访问（drop）的规则优先。
-   源端设备可以是指定的IP地址范围（SourceCidrIp、Ipv6SourceCidrIp、SourcePrefixListId），也可以是其他安全组（SourceGroupId）中的ECS实例。
-   如果匹配的安全组规则已存在，此次AuthorizeSecurityGroup调用成功，但不会增加规则数。
-   以下任意一组参数可以确定一条安全组规则，只指定一个参数无法确定一条安全组规则。
    -   设置指定IP地址段的访问权限。此时，经典网络类型安全组的网卡类型（NicType）可设置公网（internet）和内网（intranet）。VPC类型安全组的网卡类型（NicType）只可设置内网（intranet）。如以下请求示例：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy和SourceCidrIp。

        ```
        
                https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
                &SecurityGroupId=sg-F876FF7**
                &SourceCidrIp=10.0.0.0/8
                &IpProtocol=tcp
                &PortRange=22/22
                &NicType=intranet
                &Policy=accept
                &<公共请求参数>
                
        ```

    -   设置其他安全组的访问权限。此时，网卡类型（NicType）只能为内网（intranet）。经典网络类型安全组之间互访时，可以设置同一地域中其他安全组对您的安全组的访问权限。这个安全组可以是您的也可以是其他阿里云账户（SourceGroupOwnerAccount）的。VPC类型安全组之间互访时，可以设置同一VPC内其他安全组访问该安全组的访问权限。如以下请求示例：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、SourceGroupOwnerAccount和SourceGroupId。

        ```
        
                https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
                &SecurityGroupId=sg-F876FF7**
                &SourceGroupId=sg-1651FBB**
                &SourceGroupOwnerAccount=test@aliyun.com
                &IpProtocol=tcp
                &PortRange=22/22
                &NicType=intranet
                &Policy=drop
                &<公共请求参数>
                
        ```

    -   在安全组规则中关联前缀列表。此时，前缀列表仅支持网络类型为VPC的安全组，网卡类型（NicType）只可设置为内网（intranet）。如以下请求示例：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy和SourcePrefixListId。

        ```
        
                https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
                &SecurityGroupId=sg-F876FF7**
                &SourcePrefixListId=pl-x1j1k5ykzqlixdcy****
                &SourceGroupOwnerAccount=test@aliyun.com
                &IpProtocol=tcp
                &PortRange=22/22
                &NicType=intranet
                &Policy=drop
                &<公共请求参数>
               
        ```

-   更多关于安全组规则的设置示例，请参见[应用案例](~~25475~~)和[安全组五元组规则介绍](~~97439~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=AuthorizeSecurityGroup&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AuthorizeSecurityGroup|系统规定参数。取值：AuthorizeSecurityGroup |
|IpProtocol|String|是|all|传输层协议。取值大小写敏感。取值范围：

 -   tcp
-   udp
-   icmp
-   gre
-   all：支持所有协议

 **说明：** 此处icmp协议仅支持IPv4地址。 |
|PortRange|String|是|22/22|目的端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP协议：取值范围为1~65535。使用斜线（/）隔开起始端口和终止端口。例如：1/200
-   ICMP协议：-1/-1
-   GRE协议：-1/-1
-   IpProtocol取值为all：-1/-1

 了解端口的应用场景，请参见[典型应用的常用端口](~~40724~~)。 |
|RegionId|String|是|cn-hangzhou|安全组所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|SecurityGroupId|String|是|sg-bp67acfmxazb4p\*\*\*\*|目的端安全组ID。 |
|SourceGroupId|String|否|sg-bp67acfmxazb4p\*\*\*\*|需要设置访问权限的源端安全组ID。至少设置一项`SourceGroupId`或者`SourceCidrIp`参数。

 -   如果指定了`SourceGroupId`没有指定参数`SourceCidrIp`，则参数`NicType`取值只能为`intranet`。
-   如果同时指定了`SourceGroupId`和`SourceCidrIp`，则默认以`SourceCidrIp`为准。 |
|SourceGroupOwnerId|Long|否|1234567890|跨账户设置安全组规则时，源端安全组所属的阿里云账户ID。

 -   如果`SourceGroupOwnerId`及`SourceGroupOwnerAccount`均未设置，则认为是设置您其他安全组的访问权限。
-   如果您已经设置参数`SourceCidrIp`，则参数`SourceGroupOwnerId`无效。 |
|SourceGroupOwnerAccount|String|否|test@aliyun.com|跨账户设置安全组规则时，源端安全组所属的阿里云账户。

 -   如果`SourceGroupOwnerAccount`及`SourceGroupOwnerId`均未设置，则认为是设置您其他安全组的访问权限。
-   如果已经设置参数`SourceCidrIp`，则参数`SourceGroupOwnerAccount`无效。 |
|SourceCidrIp|String|否|10.0.0.0/8|需要设置访问权限的源端IPv4 CIDR地址块。支持CIDR格式和IPv4格式的IP地址范围。

 默认值：无 |
|Ipv6SourceCidrIp|String|否|2001:250:6000::\*\*\*|需要设置访问权限的源端IPv6 CIDR地址块。支持CIDR格式和IPv6格式的IP地址范围。

 **说明：** 仅支持VPC类型ECS实例的IPv6地址。

 默认值：无 |
|SourcePrefixListId|String|否|pl-x1j1k5ykzqlixdcy\*\*\*\*|需要设置访问权限的源端前缀列表ID。您可以调用[DescribePrefixLists](~~205046~~)查询可以使用的前缀列表ID。

 注意事项：

 -   安全组的网络类型为经典网络时，不支持设置前缀列表。关于安全组以及前缀列表使用限制的更多信息，请参见[使用限制](~~25412~~)。
-   当您指定了`SourceCidrIp`、`Ipv6SourceCidrIp`或`SourceGroupId`参数中的一个时，将忽略该参数。 |
|SourcePortRange|String|否|22/22|源端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP协议：取值范围为1~65535。使用斜线（/）隔开起始端口和终止端口。例如：1/200
-   ICMP协议：-1/-1
-   GRE协议：-1/-1
-   IpProtocol取值为all：-1/-1 |
|DestCidrIp|String|否|10.0.0.0/8|目的端IPv4 CIDR地址段。支持CIDR格式和IPv4格式的IP地址范围。

 默认值：无 |
|Ipv6DestCidrIp|String|否|2001:250:6000::\*\*\*|目的端IPv6 CIDR地址段。支持CIDR格式和IPv6格式的IP地址范围。

 **说明：** 仅支持VPC类型ECS实例的IPv6地址。

 默认值：无 |
|Policy|String|否|accept|设置访问权限。取值范围：

 -   accept（默认）：接受访问。
-   drop：拒绝访问，不返回拒绝信息，表现为发起端请求超时或者无法建立连接的类似信息。 |
|Priority|String|否|1|安全组规则优先级，数字越小，代表优先级越高。取值范围：1~100

 默认值：1 |
|NicType|String|否|intranet|经典网络类型安全组规则的网卡类型。取值范围：

 -   internet：公网网卡。
-   intranet：内网网卡。
    -   专有网络VPC类型安全组规则无需设置网卡类型，默认为intranet，只能为intranet。
    -   设置安全组之间互相访问时，即仅指定了`SourceGroupId`参数时，只能为intranet。

 默认值：internet |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|Description|String|否|This is description.|安全组规则的描述信息。长度为1~512个字符。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
&SecurityGroupId=sg-bp67acfmxazb4p****
&SourceCidrIp=10.0.0.0/8
&IpProtocol=tcp
&PortRange=22/22
&NicType=intranet
&Policy=accept
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<AuthorizeSecurityGroupResponse>
      <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</AuthorizeSecurityGroupResponse>
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
|404|InvalidSourceGroupId.NotFound|The SourceGroupId provided does not exist in our records.|指定的入方向安全组不存在。|
|400|OperationDenied|The specified IpProtocol does not exist or IpProtocol and PortRange do not match.|指定的IP协议不存在，或与端口范围不匹配。|
|400|InvalidIpProtocol.Malformed|The specified parameter "PortRange" is not valid.|IP协议参数格式不正确，PortRange参数不正确。|
|403|InvalidSourceGroupId.Mismatch|NicType is required or NicType expects intranet.|需要提供NicType，NicType仅在内网中使用。|
|400|InvalidSourceCidrIp.Malformed|The specified parameter "SourceCidrIp" is not valid.|源IP地址范围参数格式不正确。|
|403|MissingParameter|The input parameter "SourceGroupId" or "SourceCidrIp" cannot be both blank.|参数SourceGroupId和SourceCidrIp不能同时为空。|
|400|InvalidPolicy.Malformed|The specified parameter "Policy" is not valid.|指定的参数无效，请您检查该参数是否正确。|
|400|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|指定的网络类型不存在，请您检查网络类型是否正确。|
|400|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|指定的NIC类型与规则信息冲突。|
|403|AuthorizationLimitExceed|The limit of authorization records in the security group reaches.|安全组授权规则数达到上限，请您检查授权规则是否合理。|
|403|InvalidParamter.Conflict|The specified SecurityGroupId should be different from the SourceGroupId.|授权与被授权安全组必须不同。|
|400|InvalidSourceGroupId.Mismatch|Specified security group and source group are not in the same VPC.|指定的安全组和源安全组不在一个VPC内。|
|400|InvalidSourceGroup.NotFound|Specified source security group does not exist.|指定的安全组入方向规则不存在，或相关参数缺失。|
|400|VPCDisabled|Can't use the SecurityGroup in VPC.|VPC 不支持安全组。|
|400|InvalidPriority.Malformed|The parameter Priority is invalid.|指定的参数Priority无效。|
|400|InvalidPriority.ValueNotSupported|The parameter Priority is invalid.|指定的参数Priority无效。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InvalidNetworkType.Mismatch|The specified SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|指定的SecurityGroup的网络类型必须与SouceGroup的网络类型一致。|
|403|InvalidNetworkType.Conflict|The specified SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|指定的SecurityGroup的网络类型必须与SouceGroup的网络类型一致。|
|400|InvalidNicType.ValueNotSupported|The specified NicType is not valid.|指定的网络类型不存在，请您检查网络类型是否正确。|
|400|InvalidSecurityGroupDiscription.Malformed|The specified security group rule description is not valid.|指定的安全组规则描述不合法。|
|400|InvalidSecurityGroup.InvalidNetworkType|The specified security group network type is not support this operation, please check the security group network types. For VPC security groups, ClassicLink must be enabled.|指定的安全组网络类型不支持此操作，请检查安全组网络类型。对于VPC安全组，必须启用ClassicLink。|
|400|MissingParameter.Source|One of the parameters SourceCidrIp, SourceGroupId or SourcePrefixListId must be specified.|至少需要指定参数SourceCidrIp、SourceGroupId或SourcePrefixListId中的一个。|
|400|InvalidIpProtocol.ValueNotSupported|The parameter IpProtocol must be specified with case insensitive TCP, UDP, ICMP, GRE or All.|协议类型只能是TCP、UDP、ICMP、GRE或者All。|
|400|InvalidSecurityGroupId.Malformed|The specified parameter "SecurityGroupId" is not valid.|指定的参数SecurityGroupId无效。|
|400|InvalidParamter.Conflict|The specified SourceCidrIp should be different from the DestCidrIp.|参数SourceCidrIp和DestCidrIp不能相同。|
|500|InvalidGressFlow.Malformed|The specified parameter GressFlow is not valid,it cause by internal,try calling again.|指定的参数GressFlow无效，请稍后重试。|
|400|InvalidSourcePortRange.Malformed|The specified parameter "SourcePortRange" is not valid.|指定的参数SourcePortRange无效。|
|400|InvalidParam.SourceIp|%s|指定的参数SourceIp无效。|
|400|InvalidParam.DestIp|%s|指定的参数DestIp无效。|
|400|InvalidParam.Ipv6DestCidrIp|%s|您输入的参数无效。|
|400|InvalidParam.Ipv6SourceCidrIp|%s|您输入的参数无效。|
|400|InvalidParam.Ipv4ProtocolConflictWithIpv6Address|%s|您输入的参数无效，请检查IPv4协议下是否填写了IPv6地址。|
|400|InvalidParam.Ipv6ProtocolConflictWithIpv4Address|%s|您输入的参数无效，请检查IPv6协议下是否填写了IPv4地址。|
|400|ILLEGAL\_IPV6\_CIDR|%s|指定的IPv6地址无效。|
|400|InvalidDestCidrIp.Malformed|The specified parameter DestCidrIp is not valid.|指定的DestCidrIp无效，请您检查该参数是否正确。|
|403|InvalidOperation.ResourceManagedByCloudProduct|%s|云产品托管的安全组不支持修改操作。|
|404|InvalidPrefixListId.NotFound|The specified prefix list was not found.|前缀列表不存在。|
|404|NotSupported.GrayFunction|The prefix list is a gray-scale function, not currently supported.|前缀列表功能正在邀测中，暂不支持本次操作。|
|403|LimitExceed.PrefixListAssociationResource|The number of resources associated with the prefix list exceeds the limit.|与前缀列表关联的资源数量超出限制。|
|400|InvalidParam.PrefixListAddressFamilyMismatch|The address family of the specified prefix list does not match the specified CidrIp.|指定前缀列表的地址族，与指定的CidrIP的地址族不匹配。|
|400|NotSupported.ClassicNetworkPrefixList|The prefix list is not supported when the network type of security group is classic.|安全组的网络类型为经典网络，不支持前缀列表。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

