# DetachInstanceRamRole {#DetachInstanceRamRole .reference}

收回一台或多台ECS实例的实例RAM角色。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DetachInstanceRamRole|
|RegionId|String|是|地域 ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceIds|Array|是|指定收回的实例ID的集合。最多支持一次查询100台实例，格式为 \["instanceId1", "instanceId2", "instanceId3"…\]。|
|RamRoleName|String|否|收回赋予了某一实例RAM角色的所有ECS实例。您可以使用*RAM* API [ListRoles](../../../../../cn.zh-CN/API参考/API 参考（RAM）/角色管理接口/ListRoles.md#) 查询实例RAM角色名称。参考相关API [CreateRole](../../../../../cn.zh-CN/API参考/API 参考（RAM）/角色管理接口/CreateRole.md#) 和[ListRoles](../../../../../cn.zh-CN/API参考/API 参考（RAM）/角色管理接口/ListRoles.md#) 。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|收回的实例RAM角色的总个数。|
|FailCount|Integer|收回失败的实例RAM角色的个数。|
|RamRoleName|String|收回实例RAM角色的名称。|
|DetachInstanceRamRoleResults|Array|由实例RAM角色类型（[DetachInstanceRamRoleResult](#)）组成的信息集。|

 **数据类型 DetachInstanceRamRoleResult** 

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|准备收回实例RAM角色的ECS实例。|
|Code|Integer|判断是否成功收回实例RAM角色。返回值为`200`表示成功收回，返回其他值表示收回失败，失败原因参阅[错误码](#)。|
|Message|String|判断是否成功收回实例RAM角色。返回值为`Success`表示成功收回，返回其他值表示收回失败，失败原因参阅[错误码](#)。|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DetachInstanceRamRole
&RegionId=cn-hangzhou
&RamRoleName=RamRoleTest
&InstanceIds=["i-instance1"]
&<公共请求参数>
```

**返回示例** 

**XML格式**

```
<DetachInstanceRamRoleResponse>
    <RequestId>E6352369-5C2B-41CD-AB50-471550C8F674</RequestId>
    <DetachInstanceRamRoleResults>
        <DetachInstanceRamRoleResult>
             <InstanceId>i-instance1</InstanceId>
             <Code>200</Code>
             <Message>success</Message>
        </DetachInstanceRamRoleResult>
    </DetachInstanceRamRoleResults>
    <TotalCount>1</TotalCount>
    <FailCount>0</FailCount>
    <RamRoleName>RamRoleTest</RamRoleName>
</DetachInstanceRamRoleResponse>

```

**JSON格式** 

```
{
    "RequestId": "E6352369-5C2B-41CD-AB50-471550C8F674",
    "DetachInstanceRamRoleResults": {
        "DetachInstanceRamRoleResult": [
            {
                "Message": "success",
                "InstanceId": "i-instance1",
                "Code": "200"
            }
        ]
    },
    "TotalCount": 1,
    "FailCount": 0,
    "RamRoleName": "RamRoleTest"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter.InstanceIds|The input parameter InstanceIds that is mandatory for processing this request is missing.|400|缺少必填参数InstanceIds。|
|MissingParameter.RegionId|The input parameter RegionId that is mandatory for processing this request is missing.|400|缺少必填参数RegionId。|
|InvalidInstanceIds.Malformed|The specified InstanceIds is not valid.|400|指定的InstanceIds不合法。|
|InvalidNetworkType.MismatchRamRole|Ram role cannot be attached to instances of Classic network type.|403|实例RAM角色功能不能被用于经典网络实例。|
|InvalidUser.PassRoleForbidden|The RAM user does not have the privilege to pass a RAM role.|403|您使用的RAM用户账号暂不具有`PassRole`的权限，请联系主账号拥有者[授权](../cn.zh-CN/快速入门/为 RAM 用户授权.md#)PassRole权限。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的实例 ID 不存在。|
|InvalidRamRole.NotFound|The specified RamRoleName does not exist.|404|指定的 RamRoleName 不存在。|

