# CopySnapshot

调用CopySnapshot将一份普通快照从一个地域复制到另一个地域。

## 接口说明

调用该接口时，您需要注意：

-   复制后的新快照不能回滚源快照对应的云盘。
-   不支持复制已加密的快照。
-   不支持复制本地快照。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CopySnapshot&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CopySnapshot|系统必选参数。取值：CopySnapshot |
|SnapshotId|String|是|s-bp67acfmxazb4p\*\*\*\*|源快照ID。 |
|RegionId|String|是|cn-chengdu|源快照所在的地域。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|DestinationRegionId|String|是|us-east-1|新快照的目标地域ID。 |
|DestinationSnapshotName|String|是|CopySnapshotDemo|新快照的名称。长度为2~128个英文或中文字符，必须以大小字母或中文开头，不能以http://和https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空 |
|DestinationSnapshotDescription|String|是|CopySnapshotDemo|新快照的描述信息。长度为2~256个英文或中文字符，不能以http://和https://开头。

 默认值：空 |
|RetentionDays|Integer|否|60|新快照的保留时长，单位为天，到期后快照会被自动释放。取值范围：1~65536。

 默认值：空，表示快照不会被自动释放。 |
|Tag.N.Key|String|否|TestKey|新快照的标签键。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|Tag.N.Value|String|否|TestValue|新快照的标签值。一旦传入该值，允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|C8B26B44-0189-443E-9816-D951F59623A9|请求ID。 |
|SnapshotId|String|s-bp17441ohwka0yui\*\*\*\*|新快照的ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CopySnapshot
&DestinationRegionId=us-east-1
&RegionId=cn-chengdu
&SnapshotId=s-bp67acfmxazb4p****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CopySnapshotResponse>
            <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
            <SnapshotId>s-bp17441ohwka0yuhi****</SnapshotId>
</CopySnapshotResponse>
```

`JSON`格式

```
{
        "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
        "SnapshotId": "s-bp17441ohwka0yui****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签中存在重复的键，请保持键的唯一性。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键参数有误。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值参数有误。|
|403|InvalidSnapshotId.NotFound|The specified snapshot is not exists.|指定的源快照不存在。|
|403|InvalidUser.NotInWhiteList|The user is not in the white list of copying snapshot.|您暂未授权执行该操作。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|快照服务未开通，操作无法执行。|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|指定的快照未完成。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

