# DeleteSecurityGroup

调用DeleteSecurityGroup删除一个安全组。

## 接口说明

删除安全组之前，请确保安全组内不存在实例，并且没有其他安全组与该安全组有授权行为（[DescribeSecurityGroupReferences](~~57320~~)），否则DeleteSecurityGroup请求失败。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DeleteSecurityGroup&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteSecurityGroup|系统规定参数。取值：DeleteSecurityGroup |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|SecurityGroupId|String|是|sg-bp1fg655nh68xyz9\*\*\*\*|安全组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DeleteSecurityGroup
&RegionId=cn-hangzhou
&SecurityGroupId=sg-bp1fg655nh68xyz9****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteSecurityGroupResponse>
       <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteSecurityGroupResponse>
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
|403|DependencyViolation|There is still instance\(s\) in the specified security group.|安全组中还有未释放的实例，请您先释放实例再进行该操作。|
|403|DependencyViolation|The specified security group has been authorized in another one.|指定的安全组已在另一个组中授权，不允许重复授权。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InvalidOperation.ResourceManagedByCloudProduct|%s|云产品托管的安全组不支持修改操作。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

