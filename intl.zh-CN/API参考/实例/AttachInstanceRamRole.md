# AttachInstanceRamRole

调用AttachInstanceRamRole为一台或多台ECS实例授予实例RAM角色。如果实例已有RAM角色，则报错提示您不能附加新的角色。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=AttachInstanceRamRole&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AttachInstanceRamRole|系统规定参数。取值：AttachInstanceRamRole |
|InstanceIds|String|是|\[“i-bp14ss25xca5ex1u\*\*\*\*”, “i-bp154z5o1qjalfse\*\*\*\*”, “i-bp10ws62o04ubhvi\*\*\*\*”…\]|实例ID。取值可以由多个实例ID组成一个JSON数组，最多支持100个ID，ID之间用半角逗号（,）隔开。 |
|RamRoleName|String|是|testRamRoleName|实例RAM角色名称。您可以使用RAM API [ListRoles](~~28713~~)查询您已创建的实例RAM角色。 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Policy|String|否|\{"Statement": \[\{"Action": \["\*"\],"Effect": "Allow","Resource": \["\*"\]\}\],"Version":"1"\}|权限策略。长度为1~1024个字符。为一台或多台ECS实例授予实例RAM角色时，可以指定一个额外的权限策略，以进一步限制RAM角色的权限。更多信息，请参见[权限策略概览](~~93732~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AttachInstanceRamRoleResults|Array of AttachInstanceRamRoleResult| |由实例RAM角色类型（AttachInstanceRamRoleResult）组成的信息集。 |
|AttachInstanceRamRoleResult| | | |
|Code|String|200|判断是否成功授予实例RAM角色。返回值为200表示成功授予，返回其他值表示授予失败，失败原因参见错误码。 |
|InstanceId|String|i-bp10ws62o04ubhvi\*\*\*\*|实例ID。 |
|Message|String|success|判断是否成功授予实例RAM角色。返回值为Success表示成功授予，返回其他值表示授予失败，失败原因参见错误码。 |
|Success|Boolean|true|是否成功授予实例RAM角色。 |
|FailCount|Integer|0|授予实例RAM角色的失败个数。 |
|RamRoleName|String|testRamRoleName|实例RAM角色的名称。 |
|RequestId|String|D9553E4C-6C3A-4D66-AE79-9835AF705639|请求ID。 |
|TotalCount|Integer|1|授予的实例RAM角色总个数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=AttachInstanceRamRole
&InstanceIds=["i-bp10ws62o04ubhvi****"]
&RamRoleName=testRamRoleName
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<AttachInstanceRamRoleResponse>
      <RequestId>E6352369-5C2B-41CD-AB50-471550C8F674</RequestId>
      <AttachInstanceRamRoleResults>
            <AttachInstanceRamRoleResult>
                   <InstanceId>i-bp10ws62o04ubhvi****</InstanceId>
                   <Code>200</Code>
                   <Message>success</Message>
            </AttachInstanceRamRoleResult>
      </AttachInstanceRamRoleResults>
      <TotalCount>1</TotalCount>
      <FailCount>0</FailCount>
      <RamRoleName>testRamRoleName</RamRoleName>
</AttachInstanceRamRoleResponse>
```

`JSON` 格式

```
{
    "RequestId": "D9553E4C-6C3A-4D66-AE79-9835AF705639",
    "AttachInstanceRamRoleResults": {
        "AttachInstanceRamRoleResult": [
            {
                "Message": "success",
                "InstanceId": "i-bp10ws62o04ubhvi****",
                "Code": "200"
            }
        ]
    },
    "TotalCount": 1,
    "FailCount": 0,
    "RamRoleName": "testRamRoleName"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInstanceIds.Malformed|The specified instanceIds are not valid.|指定的多个InstanceId不合法。|
|404|InvalidInstanceId.NotFound|The specified instanceId does not exist|指定的实例不存在，请您检查实例ID是否正确。|
|403|InvalidNetworkType.MismatchRamRole|Ram role cannot be applied to instances of Classic network type.|实例RAM角色不能被用于经典网络类型的实例，RAM角色只能使用在VPC类型的实例上。|
|403|InvalidUser.PassRoleForbidden|The RAM user does not have the privilege to pass a RAM role.|该RAM用户无权传递RAM角色。|
|404|InvalidRamRole.NotFound|The specified RAMRoleName does not exist.|指定的RamRoleName不存在。|
|404|InvalidRamRole.NotEcsRole|The specified ram role is not authorized for ecs, please check your role policy.|指定的RAM角色无权使用ECS，请检查您的角色策略。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

