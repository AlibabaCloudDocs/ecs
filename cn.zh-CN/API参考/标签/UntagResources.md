# UntagResources

调用UntagResources为指定的ECS资源列表统一解绑标签。解绑后，如果该标签没有绑定其他任何资源，会被自动删除。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=UntagResources&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UntagResources|系统规定参数。取值：UntagResources |
|RegionId|String|是|cn-hangzhou|资源所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ResourceId.N|RepeatList|是|i-bp67acfmxazb4ph\*\*\*\*|资源ID。N的取值范围：1~50 |
|ResourceType|String|是|instance|资源类型定义。取值范围：

 -   instance：ECS实例
-   disk：磁盘
-   snapshot：快照
-   image：镜像
-   securitygroup：安全组
-   volume：存储卷
-   eni：弹性网卡
-   ddh：专有宿主机
-   ddhcluster：专有宿主机集群
-   keypair：SSH密钥对
-   launchtemplate：启动模板
-   reservedinstance：预留实例券
-   snapshotpolicy：自动快照策略
-   elasticityassurance：弹性保障
-   capacityreservation：容量预定 |
|TagKey.N|RepeatList|否|TestKey|资源的标签键。N的取值范围：1~20 |
|All|Boolean|否|false|是否解绑资源上全部的标签。当请求中未设置TagKey.N时，该参数才有效。取值范围：

 -   true
-   false

 默认值：false |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|C46FF5A8-C5F0-4024-8262-B16B639225A0|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=UntagResources
&RegionId=cn-hangzhou
&ResourceType=instance
&ResourceId.1=i-bp1j6qtvdm8w0z1o0****
&TagKey.1=TestKey
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<UntagResourcesResponse>
    <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</UntagResourcesResponse>
```

`JSON`格式

```
{
	"RequestId":"C46FF5A8-C5F0-4024-8262-B16B639225A0"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidRegionId.NotFound|%s|提供的地域ID不存在。|
|404|MissingParameter.TagOwnerUid|The parameter - TagOwnerUid should not be null|参数TagOwnerUid不能为空。|
|404|MissingParameter.TagOwnerBid|The parameter - TagOwnerBid should not be null|参数TagOwnerBid不能为空。|
|404|MissingParameter.ResourceType|The parameter - ResourceType should not be null|参数ResourceType不能为空。|
|404|MissingParameter.Tags|The parameter - Tags should not be null|参数Tags不能为空。|
|404|MissingParameter.RegionId|The parameter - RegionId should not be null|参数RegionId不能为空。|
|403|PermissionDenied.TagOwnerUid|The specified operator not have permission to set TagOwnerUid value.|无权设置标签归属者。|
|403|PermissionDenied.Scope|The specified operator not have permission to set Scope value.|指定的操作员无权设置范围值。|
|400|NumberExceed.ResourceIds|The ResourceIds parameter's number is exceed , Valid : 50|参数“ResourceIds”中包含的“ResourceId”不能超过 50 个。|
|400|NumberExceed.Tags|The Tags parameter's number is exceed , Valid : 20|标签个数超过最大限制，本操作最多可以操作 20 个标签。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签中存在重复的键，请保持键的唯一性。|
|404|InvalidResourceId.NotFound|The specified ResourceIds are not found in our records.|指定的资源不存在，请检查参数ResourceId是否正确。|
|404|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|指定的资源类型不存在。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键参数有误。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值参数有误。|
|400|OperationDenied.QuotaExceed|The quota of tags on resource is beyond permitted range.|资源标签已达上限。|
|403|InvalidResourceId.NotSupported|The specified ResourceId does not support tagging.|指定的资源ID不支持标记。|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|指定的Tag.N.Key和Tag.N.Value不匹配。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的地域ID不存在。|
|400|Invalid.Scope|The specified scope is invalid.|可见范围参数无效。|
|403|NoPermission.Tag|The operator is not permission for the tag.|您没有操作该资源标签的权限。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

