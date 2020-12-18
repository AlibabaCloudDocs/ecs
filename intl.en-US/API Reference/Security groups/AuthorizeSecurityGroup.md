# AuthorizeSecurityGroup

You can call this operation to create an inbound security group rule. The created rule allows or denies the inbound traffic from other devices to the ECS instances in the security group to which the rule belongs.

## Description

In the security group-related API documents, inbound traffic refers to the traffic sent by the source device and received at the destination device.

When you call this operation, take note of the following items:

-   The total number of outbound and inbound security group rules in each security group cannot exceed 200.
-   The priority \(`Priority`\) of a security group rule ranges from 1 to 100. A smaller value indicates a higher priority.
-   When multiple security group rules have the same priority, drop \(`drop`\) rules take precedence.
-   The source device can belong to a specified CIDR block \(SourceCidrIp\) or can be an ECS instance in another security group \(SourceGroupId\).
-   If the rule to be created matches an existing rule, the AuthorizeSecurityGroup operation succeeds but no rule is created.
-   You can determine a security group rule by specifying one of the following groups of parameters. You cannot determine a security group rule by specifying a single parameter.
    -   Parameters used to determine an inbound security group rule that controls access from a specified CIDR block: IpProtocol, PortRange, SourcePortRange \(optional\), NicType, Policy, and SourceCidrIp. For a security group of the classic network type, you can set the NicType parameter to internet or intranet. For a security group of the VPC type, you can set the NicType parameter only to intranet. Sample request:

        ```
        
                https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
                &SecurityGroupId=sg-F876FF7**
                &SourceCidrIp=10.0.0.0/8
                &IpProtocol=tcp
                &PortRange=22/22
                &NicType=intranet
                &Policy=accept
                &<Common request parameters>
                
        ```

    -   Parameters used to determine an inbound security group rule that controls access from another security group: IpProtocol, PortRange, SourcePortRange \(optional\), NicType, Policy, SourceGroupOwnerAccount, and SourceGroupId. To create an inbound security group rule to control access from another security group, you can set the NicType parameter only to intranet. For mutual access between security groups of the classic network type, you can allow or deny another security group in the same region access to your security group. The security group that is allowed access to your security group can belong to your own Alibaba Cloud account or another Alibaba Cloud account specified by the SourceGroupOwnerAccount parameter. For mutual access between security groups of the VPC type, you can allow or deny another security group in the same VPC access to your security group. Sample request:

        ```
        
                https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
                &SecurityGroupId=sg-F876FF7**
                &SourceGroupId=sg-1651FBB**
                &SourceGroupOwnerAccount=test@aliyun.com
                &IpProtocol=tcp
                &PortRange=22/22
                &NicType=intranet
                &Policy=drop
                &<Common request parameters>
               
        ```

-   For more information about examples on security group rule settings, see [Scenarios for security groups](~~25475~~) and [Security group quintuple rules](~~97439~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=AuthorizeSecurityGroup&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AuthorizeSecurityGroup|The operation that you want to perform. Set the value to AuthorizeSecurityGroup. |
|IpProtocol|String|Yes|all|The transport layer protocol. This value is case-sensitive. Valid values:

-   tcp
-   udp
-   icmp
-   gre
-   all

**Note:** IpProtocol can be set to icmp only for IPv4 addresses. |
|PortRange|String|Yes|22/22|The range of destination ports relevant to the transport layer protocol. Valid values:

-   When the IpProtocol parameter is set to tcp or udp, the port number range is 1 to 65535. Separate the start port and the end port with a forward slash \(/\). Example: 1/200.
-   When the IpProtocol parameter is set to icmp, the port number range is -1/-1, which indicates all ports.
-   When the IpProtocol parameter is set to gre, the port number range is -1/-1, which indicates all ports.
-   When the IpProtocol parameter is set to all, the port number range is -1/-1, which indicates all ports.

For more information, see [Typical applications of commonly used ports](~~40724~~). |
|RegionId|String|Yes|cn-hangzhou|The region ID of the security group. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|SecurityGroupId|String|Yes|sg-bp67acfmxazb4p\*\*\*\*|The ID of the destination security group. |
|SourceGroupId|String|No|sg-bp67acfmxazb4p\*\*\*\*|The ID of the source security group. At least one of SourceGroupId and SourceCidrIp must be specified.

-   If SourceGroupId is specified but SourceCidrIp is not, the NicType parameter can be set only to intranet.
-   If both SourceGroupId and SourceCidrIp are specified, SourceCidrIp takes precedence. |
|SourceGroupOwnerId|Long|No|1234567890|The ID of the Alibaba Cloud account that manages the source security group when you set a security group rule across accounts.

-   If both SourceGroupOwnerId and SourceGroupOwnerAccount are empty, access permissions are configured for another security group managed by your account.
-   If SourceCidrIp is specified, the SourceGroupOwnerId parameter is ignored. |
|SourceGroupOwnerAccount|String|No|test@aliyun.com|The Alibaba Cloud account that manages the source security group when you set a security group rule across accounts.

-   If both SourceGroupOwnerId and SourceGroupOwnerAccount are empty, access permissions are configured for another security group managed by your account.
-   If SourceCidrIp is specified, the SourceGroupOwnerAccount parameter is ignored. |
|SourceCidrIp|String|No|10.0.0.0/8|The range of source IPv4 addresses. CIDR blocks and IPv4 addresses are supported.

This parameter is empty by default. |
|Ipv6SourceCidrIp|String|No|2001:250:6000::\*\*\*|The range of source IPv6 addresses. CIDR blocks and IPv6 addresses are supported.

**Note:** Only IPv6 addresses of VPC-type instances are supported.

This parameter is empty by default. |
|SourcePortRange|String|No|22/22|The range of source ports relevant to the transport layer protocol. Valid values:

-   When the IpProtocol parameter is set to tcp or udp, the port number range is 1 to 65535. Separate the start port and the end port with a forward slash \(/\). Example: 1/200.
-   When the IpProtocol parameter is set to icmp, the port number range is -1/-1, which indicates all ports.
-   When the IpProtocol parameter is set to gre, the port number range is -1/-1, which indicates all ports.
-   When the IpProtocol parameter is set to all, the port number range is -1/-1, which indicates all ports. |
|DestCidrIp|String|No|10.0.0.0/8|The range of destination IPv4 addresses. CIDR blocks and IPv4 addresses are supported.

This parameter is empty by default. |
|Ipv6DestCidrIp|String|No|2001:250:6000::\*\*\*|The range of destination IPv6 addresses. CIDR blocks and IPv6 addresses are supported.

**Note:** Only IPv6 addresses of VPC-type instances are supported.

This parameter is empty by default. |
|Policy|String|No|accept|The access control policy. Default value: accept. Valid values:

-   accept: allows access.
-   drop: denies access without returning a rejection response. In this case, the request times out or the connection fails to be established. |
|Priority|String|No|1|The priority of the security group rule. A smaller value indicates a higher priority. Valid values: 1 to 100.

Default value: 1. |
|NicType|String|No|intranet|The NIC type of the security group rule when the security group is in the classic network. Valid values:

-   internet: public NIC
-   intranet: internal NIC
    -   If the security group is in a VPC, the parameter is set to intranet by default and cannot be modified.
    -   If DestGroupId is specified but DestCidrIp is not, this parameter must be set to intranet.

Default value: internet. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must ensure that it is unique among different requests. The **ClientToken** value can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [Ensure idempotence](~~25693~~). |
|Description|String|No|testDescription|The description of the security group rule. The description must be 1 to 512 characters in length. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
&SecurityGroupId=sg-bp67acfmxazb4p****
&SourceCidrIp=10.0.0.0/8
&IpProtocol=tcp
&PortRange=22/22
&NicType=intranet
&Policy=accept
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AuthorizeSecurityGroupResponse>
      <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</AuthorizeSecurityGroupResponse>
```

`JSON` format

```
{
    "RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|The error message returned because the specified security group does not exist under this account. Check whether the security group ID is correct.|
|404|InvalidSourceGroupId.NotFound|The SourceGroupId provided does not exist in our records.|The error message returned because the specified SourceGroupId parameter does not exist.|
|400|OperationDenied|The specified IpProtocol does not exist or IpProtocol and PortRange do not match.|The error message returned because the specified IpProtocol parameter does not exist or does not match the specified port range.|
|400|InvalidIpProtocol.Malformed|The specified parameter "PortRange" is not valid.|The error message returned because the specified IpProtocol or PortRange parameter is invalid.|
|403|InvalidSourceGroupId.Mismatch|NicType is required or NicType expects intranet.|The error message returned because the NicType parameter is not specified or is not set to intranet.|
|400|InvalidSourceCidrIp.Malformed|The specified parameter "SourceCidrIp" is not valid.|The error message returned because the specified SourceCidrIp parameter is invalid.|
|403|MissingParameter|The input parameter "SourceGroupId" or "SourceCidrIp" cannot be both blank.|The error message returned because both the SourceGroupId and SourceCidrIp parameters are empty.|
|400|InvalidPolicy.Malformed|The specified parameter "Policy" is not valid.|The error message returned because the specified Policy parameter is invalid.|
|400|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|The error message returned because the specified NicType parameter does not exist.|
|400|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|The error message returned because the specified NIC type conflicts with the authorization record.|
|403|AuthorizationLimitExceed|The limit of authorization records in the security group reaches.|The error message returned because the maximum number of rules in the security group has been reached.|
|403|InvalidParamter.Conflict|The specified SecurityGroupId should be different from the SourceGroupId.|The error message returned because the destination security group is the same as the source security group.|
|400|InvalidSourceGroupId.Mismatch|Specified security group and source group are not in the same VPC.|The error message returned because the destination security group and the source security group do not belong to the same VPC.|
|400|InvalidSourceGroup.NotFound|Specified source security group does not exist.|The error message returned because the specified inbound security group rule does not exist or relevant parameters are not specified.|
|400|VPCDisabled|Can't use the SecurityGroup in VPC.|The error message returned because the current VPC does not support security groups.|
|400|InvalidPriority.Malformed|The parameter Priority is invalid.|The error message returned because the specified Priority parameter is invalid.|
|400|InvalidPriority.ValueNotSupported|The parameter Priority is invalid.|The error message returned because the specified Priority parameter is invalid.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|InvalidNetworkType.Mismatch|The specified SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|The error message returned because the network type of the destination security group is different from that of the source security group.|
|403|InvalidNetworkType.Conflict|The specified SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|The error message returned because the network type of the destination security group is different from that of the source security group.|
|400|InvalidNicType.ValueNotSupported|The specified NicType is not valid.|The error message returned because the specified NicType parameter does not exist.|
|400|InvalidSecurityGroupDiscription.Malformed|The specified security group rule description is not valid.|The error message returned because the specified Description parameter is invalid.|
|400|InvalidSecurityGroup.InvalidNetworkType|The specified security group network type is not support this operation, please check the security group network types. For VPC security groups, ClassicLink must be enabled.|The error message returned because the operation is not supported while the security group is of the current network type. If the network type is VPC, ClassicLink must be enabled.|
|400|MissingParameter.Source|Either SourceCidrIp or SourceGroupId must be specified.|The error message returned because both the SourceCidrIp and SourceGroupId parameters are empty.|
|400|InvalidIpProtocol.ValueNotSupported|The parameter IpProtocol must be specified with case insensitive TCP, UDP, ICMP, GRE or All.|The error message returned because the IpProtocol parameter is not set to tcp, udp, icmp, gre, or all.|
|400|InvalidSecurityGroupId.Malformed|The specified parameter "SecurityGroupId" is not valid.|The error message returned because the specified SecurityGroupId parameter is invalid.|
|400|InvalidParamter.Conflict|The specified SourceCidrIp should be different from the DestCidrIp.|The error message returned because the value of SourceCidrIp is the same as that of DestCidrIp.|
|500|InvalidGressFlow.Malformed|The specified parameter GressFlow is not valid,it cause by internal,try calling again.|The error message returned because the specified GressFlow parameter is invalid.|
|400|InvalidSourcePortRange.Malformed|The specified parameter "SourcePortRange" is not valid.|The error message returned because the specified SourcePortRange parameter is invalid.|
|400|InvalidParam.SourceIp|%s|The error message returned because the specified SourceCidrIp parameter is invalid.|
|400|InvalidParam.DestIp|%s|The error message returned because the specified DestCidrIp parameter is invalid.|
|400|InvalidParam.Ipv6DestCidrIp|%s|The error message returned because the specified Ipv6DestCidrIp parameter is invalid.|
|400|InvalidParam.Ipv6SourceCidrIp|%s|The error message returned because the specified Ipv6SourceCidrIp parameter is invalid.|
|400|InvalidParam.Ipv4ProtocolConflictWithIpv6Address|%s|The error message returned because the specified parameter is invalid. Check whether you have entered an IPv6 address under an IPv4 protocol by mistake.|
|400|InvalidParam.Ipv6ProtocolConflictWithIpv4Address|%s|The error message returned because the specified parameter is invalid. Check whether you have entered an IPv4 address under an IPv6 protocol by mistake.|
|400|ILLEGAL\_IPV6\_CIDR|%s|The error message returned because the specified IPv6 address is invalid.|
|400|InvalidDestCidrIp.Malformed|The specified parameter DestCidrIp is not valid.|The error message returned because the specified DestCidrIp parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

