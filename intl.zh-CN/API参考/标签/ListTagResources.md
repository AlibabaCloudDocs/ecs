# ListTagResources

调用ListTagResources查询一个或多个ECS资源已经绑定的标签列表。

## 接口说明

请求中至少指定以下任一参数，以确定查询对象。

-   `ResourceId.N`
-   `Tag.N`（`Tag.N.Key`与`Tag.N.Value`）
-   `TagFilter.N`

同时指定下列参数时，返回结果中仅包含同时满足这两个条件的ECS资源。

-   `Tag.N`和`ResourceId.N`
-   `TagFilter.N`和`ResourceId.N`

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ListTagResources&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListTagResources|系统规定参数。取值：ListTagResources |
|RegionId|String|是|cn-hangzhou|资源所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
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
|TagFilter.N.TagKey|String|是|env|模糊查找ECS资源时使用的标签键。标签键长度的取值范围：1~128。N的取值范围：1~5

 `TagFilter.N`用于模糊查找绑定了指定标签的ECS资源，由一个键和一个或多个值组成。模糊查询可能会有2秒延时，仅支持模糊过滤后资源数小于等于5000的情况。

 -   通过标签键（`TagFilter.N.TagKey`）模糊查找ECS资源时，标签值（`TagFilter.N.TagValues.N`）必须为空。例如，模糊搜索标签键为`environment`的ECS资源时，`TagFilter.1.TagKey`可以设置为`env*`（前缀匹配的模糊搜索方式）、`*env*`（两边匹配的模糊搜索方式）或者`env`（精确搜索方式），而`TagFilter.1.TagValues`必须为空。
-   通过标签值（`TagFilter.N.TagValues.N`）模糊查找ECS资源时，标签键（`TagFilter.N.TagKey`）必须设置为精确值。例如，模糊搜索标签键为`env`，标签值为`product`的ECS资源时，`TagFilter.1.TagKey`必须精确设置为`env`，`TagFilter.1.TagValues.1`可以设置为`proc*`（前缀匹配的模糊搜索方式）、`*proc*`（两边匹配的模糊搜索方式）或者`proc`（精确搜索方式）。同一个`TagKey`下只能用同一种搜索方式，如果设置了多个不同的搜索方式，则以第一个方式为准。
-   标签键之间为交集关系，即仅同时满足您指定的所有标签键的ECS资源才会被查找到。
-   同一标签键下的标签值之间为并集关系，即满足您为该标签键指定的任一标签值的ECS资源均会被查找到。

 **说明：** `TagFilter.N`与`Tag.N`参数不能同时使用，否则会返回错误信息。 |
|ResourceId.N|RepeatList|否|i-bp1j6qtvdm8w0z1o\*\*\*\*|ECS资源ID。N的取值范围：1~50 |
|Tag.N.Key|String|否|TestKey|精确查找ECS资源时使用的标签键。标签键长度的取值范围：1~128。N的取值范围：1~20

 `Tag.N`用于精确查找绑定了指定标签的ECS资源，由一个键值对组成。

 -   仅指定`Tag.N.Key`时，则返回关联该标签键的所有资源。
-   仅指定`Tag.N.Value`，则报错`InvalidParameter.TagValue`。
-   同时指定多个标签键值对时，仅同时满足所有标签键值对的ECS资源会被查找到。 |
|Tag.N.Value|String|否|TestValue|精确查找ECS资源时使用的标签值。标签值长度的取值范围：1~128。N的取值范围：1~20 |
|TagFilter.N.TagValues.N|RepeatList|否|TestTagFilter|模糊查找ECS资源时使用的标签值。标签值长度的取值范围：1~128。N的取值范围：1~5。具体的参数说明请参见`TagFilter.N.TagKey`参数描述。 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0a4883|下一个查询开始Token。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|下一个查询开始Token。 |
|RequestId|String|484256DA-D816-44D2-9D86-B6EE4D5BA78C|请求ID。 |
|TagResources|Array of TagResource| |由资源及其标签组成的集合，包含了资源ID、资源类型和标签键值等信息。 |
|TagResource| | | |
|ResourceId|String|i-bp1j6qtvdm8w0z1o\*\*\*\*|资源ID。 |
|ResourceType|String|instance|资源类型。可能值：

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
|TagKey|String|TestKey|标签键。 |
|TagValue|String|TestValue|标签值。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ListTagResources
&RegionId=cn-hangzhou
&ResourceType=instance
&ResourceId.1=i-bp1j6qtvdm8w0z1o****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ListTagResourcesResponse>
	  <TagResources>
		    <TagResource>
			      <ResourceType>instance</ResourceType>
			      <TagValue>TestValue</TagValue>
			      <ResourceId>i-bp1j6qtvdm8w0z1o****</ResourceId>
			      <TagKey>TestKey</TagKey>
		    </TagResource>
	  </TagResources>
	  <RequestId>DE65F6B7-7566-4802-9007-96F2494AC5XX</RequestId>
</ListTagResourcesResponse>
```

`JSON`格式

```
{
    "TagResources": {
        "TagResource": [
            {
                "ResourceType": "instance",
                "TagValue": "TestValue",
                "ResourceId": "i-bp1j6qtvdm8w0z1o****",
                "TagKey": "TestKey"
            }
        ]
    },
    "RequestId": "DE65F6B7-7566-4802-9007-96F2494AC512"
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

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

