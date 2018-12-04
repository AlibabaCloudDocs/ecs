# ModifySecurityGroupRule {#ModifySecurityGroupRule .reference}

Modify the inbound rules of the security group. You can only modify the description information of the security group rules. If you have not added a security group rule, you can call  [AuthorizeSecurityGroup](reseller.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md#).

## Description {#section_vqh_lhn_ydb .section}

Any of the following sets of parameters can determine a Security Group Entry direction rule, specifying only one parameter cannot determine a security group rule.

-   Authorize assignment of IP Access to address segments: `IpProtocol`, `PortRange`, \(optional\) `SourcePortRange`, `NicType`, `Policy`, `DestCiderIp` and \(optional\) `SourceCidrIp`

-   Authorize access to other security groups: `IpProtocol`, `PortRange`, \(optional\) `SourcePortRange`, `NicType`, `Policy`, \(optional\)`DestCiderIp`, `DestGroupOwnerAccount` and `DestGroupId`


## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|Required parameter. Value: ModifySecurityGroupRule|
|RegionId|String|Yes.|Region ID of the destination security group.  See Regions and zones or [DescribeRegions](reseller.en-US/API Reference/Regions/DescribeRegions.md#) to query the RegionId list.|
|SecurityGroupId|String|Yes.|Source security group ID.|
|Description|String|Yes.|Either the SourceGroupId or SourceCidrIp must be specified. If both SourceGroupId and SourceCidrIp are set, SourceCidrIp is authenticated by default.|
|IpProtocol|String|Yes.| IP protocol. Not case sensitive. Optional values:-   icmp
-   gre
-   tcp
-   udp
-   all: Support four protocols at the same time

|
|PortRange|String|Yes.|Range of the port numbers of a specific IP protocol. value:-   TCP/UDP: 1/65535  . Use the slash \(/\) to separate the starting and ending ports. For example, `1/200` indicates that the range of the port numbers is \[1, 200\], and an error returns if you specify TCP/UDP to `200/1`.
-   ICMP: -1/-1
-   GRE: -1/-1
-   All: -1/-1

|
|SourcePortRange|String|No|Port ranges associated with the transport layer protocol that the source security group is open. Scope of value:-   TCP/UDP protocol: range of values \[1, 65535\] . Use the slash \(/\) to separate the starting and ending ports. Demonstration: `1/200`; error Demonstration: `200/1`.
-   ICMP protocol:-1/-1.
-   GRE Protocol:-1/-1.
-   All:-1/-1.

|
|Nictype|String|No|Network type.  value:-   internet
-   intranet

 In mutual security group authorization, when  `DestGroupId` is specified  and `DestCidrIp`is not specified,  you must set  `NicType` to intranet.  `intranet`. Default value: internet|
|Policy|String|No| Authorization policy.  Optional values:-   accept: access accepted
-   drop: access denied

Default value: accept|
|DestCidrIp|String|No|Destination IP address range. Supports IP address ranges in CIDR and IPv4 formats. Default: 0.0.0.0/0|
|SourceCidrIp|String|No|Source IP address range. The IP range must be specified in CIDR format. Default value: 0.0.0.0/0|
|SourceGroupId|String|No|Source security group ID. Either the `SourceGroupId`Settings or `SourceCidrIp` must be specified. If this parameter is specified but `SourceGroupId`  is not specified `SourceCidrIp`, you can only set `NicType` to `intranet`. If both `SourceGroupId`  and `SourceCidrIp` are set, `SourceCidrIp` is authenticated  by default.|
|SourceGroupOwnerAccount|String|No|Alibaba Cloud account ID of the source security group. This parameter is applicable in cross-user security group authorization.-   If neither this parameter nor `SourceGroupOwnerAccount` `SourceGroupOwnerID` are set, authorization is performed for security groups of the same account.
-   If `SourceCidrIp` is specified. `SourceGroupOwnerAccount`  is invalid.

|
|SourceGroupOwnerId|String|No|Alibaba Cloud account ID of the source security group. This parameter is applicable in cross-user security group revocation.-   If neither this parameter nor `SourceGroupOwnerAccount` `SourceGroupOwnerAccount`  are set, authorization is performed for security groups of the same account.
-   If `SourceCidrIp` is specified. `SourceGroupOwnerAccount` is invalid.

|
|Priority|String|No| Authorization policy priority. Value range: \[1, 100\]. |

## Response parameters {#section_f54_lk5_xdb .section}

All are common response parameters. For more information, see [Common Request Parameters](reseller.en-US/API Reference/Getting started/Common parameters.md#).

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=ModifySecurityGroupRule
&SecurityGroupId=sg-F876FF7BA
&SourceGroupId=sg-1651FBB64
&SourceGroupOwnerAccount=test@aliyun.com
&IpProtocol=tcp
&PortRange=80/80
&Policy=allow
&Description=This is a new security group rule.
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<ModifySecurityGroupRuleResponse>
    <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</ModifySecurityGroupRuleResponse>
```

 **JSON format** 

```
{
    "RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## Error codes {#ErrorCode .section}

|Error code|Error information|HTTP status code|Description|
|:---------|:----------------|:---------------|:----------|
|InvalidIpProtocol.Malformed|The specified parameter “IpProtocol” is not valid.|400|The specified `IpProtocol` is not valid.|
|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|400| The specified network type`NicType`does not match the security group rule.|
|InvalidNicType.ValueNotSupported|The specified NicType does notexist.|400|The specified `NicType` does not exist.|
|InvalidPolicy.Malformed|The specified parameter “Policy” is not valid.|400|The specified Parameter `Policy` is invalid.|
|InvalidPriority.Malformed|The specified parameter “Priority” is not valid.|400|The specified `Priority` is invalid.|
|InvalidPriority.ValueNotSupported|The specified Priority isinvalid.|400|The specified `Priority` is invalid.|
|InvalidSecurityGroupDiscription.Malformed|The specified security group rule description is not valid.|400|The description Description of  `Description` is invalid.|
|InvalidSourceCidrIp.Malformed|The specified parameter “SourceCidrIp” is not valid.|400|The specified `SourceCidrIp`  is invalid.|
|InvalidSourceGroup.NotFound|The specified SourceGroupId does not exist.|400|The specified `SourceGroupId` does not exist.|
|InvalidSourceGroupId.Mismatch|Specified security group and source group are not in the same VPC.|400|The specified security group and source security group do not belong to the same VPC.|
|OperationDenied|The specified IpProtocol does not exist or IpProtocol and PortRange do not match.|400|The specified `IpProtocol` does not exist. or the IP protocol does not match the port.|
|InvalidNetworkType.Mismatch|The specified SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|403|The network types of the two security groups must be the same..|
|InvalidParamter.Conflict|The specified SecurityGroupId should be different from the SourceGroupId.|403| `SecurityGroupId` `SourceGroupId` cannot have the same value.|
|InvalidSourceGroupId.Mismatch|NicType is required or NicType expects intranet.|403|`NicType` needs to be defined. `NicType` must be `intranet`.|
|MissingParameter|The input parameter “SourceGroupId” or “SourceCidrIp” cannot be both blank.|403| `SourceGroupId` or   `SourceCidrIp` must be specified.|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|The specified `RegionId`  does not exist.|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|The specified `SecurityGroupId` does not exist.|
|InvalidSourceGroupId.NotFound|The SourceGroupId provided does not exist in our records.|404|The specified  `SourceGroupId` does not exist.|

