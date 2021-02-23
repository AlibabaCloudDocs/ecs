# DeleteAutoProvisioningGroup

调用DeleteAutoProvisioningGroup删除一个弹性供应组。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DeleteAutoProvisioningGroup&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteAutoProvisioningGroup|系统规定参数。取值：DeleteAutoProvisioningGroup |
|AutoProvisioningGroupId|String|是|apg-bpuf6jel2bbl62wh13\*\*\*\*|弹性供应组的ID。 |
|RegionId|String|是|cn-hangzhou|弹性供应组所在地域的ID。 |
|TerminateInstances|Boolean|是|true|删除弹性供应组时是否释放组内实例。取值范围：

 -   true：释放组内实例
-   false：组内实例继续运行 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://ecs.aliyuncs.com/?Action=DeleteAutoProvisioningGroup
&AutoProvisioningGroupId=apg-bpuf6jel2bbl62wh13****
&RegionId=cn-hangzhou
&TerminateInstances=true
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteAutoProvisioningGroupResponse>
    <RequestId>928E2273-5715-46B9-A730-238DC996****</RequestId>
</DeleteAutoProvisioningGroupResponse>
```

`JSON`格式

```
{
    "RequestId": "B48A12CD-1295-4A38-A8F0-0E92C937****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|您没有操作此资源的权限，或者此 API 不支持 RAM 角色。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

