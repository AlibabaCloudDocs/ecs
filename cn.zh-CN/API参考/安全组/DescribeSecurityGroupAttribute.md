# DescribeSecurityGroupAttribute

调用DescribeSecurityGroupAttribute查询一个安全组的安全组规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeSecurityGroupAttribute&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSecurityGroupAttribute|系统规定参数。取值：DescribeSecurityGroupAttribute |
|RegionId|String|是|cn-hangzhou|安全组所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|SecurityGroupId|String|是|sg-bp1gxw6bznjjvhu3\*\*\*\*|安全组ID。 |
|NicType|String|否|intranet|安全组规则的网卡类型。

 -   经典网络类型安全组的取值范围：
    -   internet（默认）：公网
    -   intranet：内网

**说明：** 单次调用只能查询一种网卡类型的安全组规则，查询全部类型请分两次调用。

-   专有网络类型安全组的取值只能为：intranet（默认），即内网。

**说明：** 如果传入internet或空值，则会默认转化为intranet。 |
|Direction|String|否|all|安全组规则授权方向。取值范围：

 -   egress：安全组出方向
-   ingress：安全组入方向
-   all：不区分方向

 默认值：all |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Description|String|This is description.|安全组描述信息。 |
|InnerAccessPolicy|String|Accept|安全组内网络连通策略。可能值：

 -   Accept：内网互通
-   Drop：内网隔离 |
|Permissions|Array of Permission| |安全组权限规则集合。 |
|Permission| | | |
|CreateTime|String|2018-12-12T07:28:38Z|创建时间，UTC时间。 |
|Description|String|Description Sample 01|安全组描述信息。 |
|DestCidrIp|String|0.0.0.0/0|目的端IP地址段，用于出方向授权。 |
|DestGroupId|String|sg-bp1czdx84jd88i7v\*\*\*\*|目的端安全组，用于出方向授权。 |
|DestGroupName|String|testDestGroupName|目的端安全组名称。 |
|DestGroupOwnerAccount|String|1234567890|目的端安全组所属阿里云账户ID。 |
|DestPrefixListId|String|pl-x1j1k5ykzqlixabc\*\*\*\*|目的端前缀列表ID，用于出方向授权。 |
|DestPrefixListName|String|DestPrefixListName Sample|目的端前缀列表的名称。 |
|Direction|String|ingress|授权方向。 |
|IpProtocol|String|TCP|IP协议。 |
|Ipv6DestCidrIp|String|2001:db8:1233:1a00::\*\*\*|目的端IPv6地址段。 |
|Ipv6SourceCidrIp|String|2001:db8:1234:1a00::\*\*\*|源端IPv6地址段。 |
|NicType|String|intranet|网络类型。 |
|Policy|String|Accept|授权策略。 |
|PortRange|String|80/80|端口范围。 |
|Priority|String|1|规则优先级。 |
|SourceCidrIp|String|0.0.0.0/0|源端IP地址段，用于入方向授权。 |
|SourceGroupId|String|sg-bp12kc4rqohaf2js\*\*\*\*|源端安全组，用于入方向授权。 |
|SourceGroupName|String|testSourceGroupName1|源端安全组名称。 |
|SourceGroupOwnerAccount|String|1234567890|源端安全组所属阿里云账户ID。 |
|SourcePortRange|String|80/80|源端端口范围。 |
|SourcePrefixListId|String|pl-x1j1k5ykzqlixdcy\*\*\*\*|源端前缀列表ID，用于入方向授权。 |
|SourcePrefixListName|String|SourcePrefixListName Sample|源端前缀列表的名称。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|SecurityGroupId|String|sg-bp1gxw6bznjjvhu3\*\*\*\*|目标安全组ID。 |
|SecurityGroupName|String|SecurityGroupName Sample|目标安全组名称。 |
|VpcId|String|vpc-bp1opxu1zkhn00gzv\*\*\*\*|VPC ID。如果返回VPC ID，表示该安全组网络类型为VPC。否则，表示是经典网络类型安全组。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?RegionId=cn-hangzhou
&SecurityGroupId=sg-bp1gxw6bznjjvhu3****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeSecurityGroupAttributeResponse>
      <SecurityGroupId>sg-bp1gxw6bznjjvhu3****</SecurityGroupId>
      <InnerAccessPolicy>Accept</InnerAccessPolicy>
      <SecurityGroupName>SecurityGroupName Sample</SecurityGroupName>
      <Description>This is description.</Description>
      <RegionId>cn-hangzhou</RegionId>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <Permissions>
            <Permission>
                  <SourceCidrIp>0.0.0.0/0</SourceCidrIp>
                  <Description>Description Sample 01</Description>
                  <DestCidrIp></DestCidrIp>
                  <NicType>intranet</NicType>
                  <DestGroupName></DestGroupName>
                  <PortRange>22/22</PortRange>
                  <DestGroupId></DestGroupId>
                  <Ipv6DestCidrIp></Ipv6DestCidrIp>
                  <DestPrefixListId></DestPrefixListId>
                  <DestPrefixListName></DestPrefixListName>
                  <Direction>ingress</Direction>
                  <Priority>1</Priority>
                  <IpProtocol>TCP</IpProtocol>
                  <SourcePortRange></SourcePortRange>
                  <SourceGroupOwnerAccount></SourceGroupOwnerAccount>
                  <Policy>Accept</Policy>
                  <CreateTime>2018-12-12T07:28:38Z</CreateTime>
                  <SourceGroupId></SourceGroupId>
                  <DestGroupOwnerAccount></DestGroupOwnerAccount>
                  <Ipv6SourceCidrIp></Ipv6SourceCidrIp>
                  <SourceGroupName></SourceGroupName>
                  <SourcePrefixListId></SourcePrefixListId>
                  <SourcePrefixListName></SourcePrefixListName>
            </Permission>
      </Permissions>
      <VpcId>vpc-bp1opxu1zkhn00gzv****</VpcId>
</DescribeSecurityGroupAttributeResponse>
```

`JSON`格式

```
{
    "SecurityGroupId": "sg-bp1gxw6bznjjvhu3****",
    "InnerAccessPolicy": "Accept",
    "SecurityGroupName": "SecurityGroupName Sample",
    "Description": "This is description.",
    "RegionId": "cn-hangzhou",
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "Permissions": {
        "Permission": [
            {
                "SourceCidrIp": "0.0.0.0/0",
                "Description": "Description Sample 01",
                "DestCidrIp": "",
                "NicType": "intranet",
                "DestGroupName": "",
                "PortRange": "22/22",
                "DestGroupId": "",
                "Ipv6DestCidrIp": "",
				"DestPrefixListId": "",
				"DestPrefixListName":"",
                "Direction": "ingress",
                "Priority": 1,
                "IpProtocol": "TCP",
                "SourcePortRange": "",
                "SourceGroupOwnerAccount": "",
                "Policy": "Accept",
                "CreateTime": "2018-12-12T07:28:38Z",
                "SourceGroupId": "",
                "DestGroupOwnerAccount": "",
                "Ipv6SourceCidrIp": "",
                "SourceGroupName": "",
				"SourcePrefixListId": "",
				"SourcePrefixListName": ""
            }
        ]
    },
    "VpcId": "vpc-bp1opxu1zkhn00gzv****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的地域ID不存在。|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|指定的安全组在该用户账号下不存在，请您检查安全组ID是否正确。|
|400|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|指定的网络类型不存在，请您检查网络类型是否正确。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|InvalidParamter|Invalid Parameter|指定的参数不合法。|
|400|InvalidSecurityGroupId.Malformed|The specified parameter "SecurityGroupId" is not valid.|指定的参数SecurityGroupId无效。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

