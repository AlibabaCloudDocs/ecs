# CreateAutoSnapshotPolicy

调用CreateAutoSnapshotPolicy创建一条自动快照策略。

## 接口说明

创建的自动快照策略可以应用到任一云盘（[ApplyAutoSnapshotPolicy](~~25531~~)），成功创建的自动快照策略可以后续修改策略内容（[ModifyAutoSnapshotPolicyEx](~~25529~~)）。

调用该接口时，您需要注意：

-   一个阿里云账户在一个地域最多能创建100条自动快照策略。
-   如果云盘数据较多，单次创建自动快照的时长超过两个时间点间隔，则自动跳过下一时间点。示例：您设置了09:00、10:00、11:00和12:00为自动快照时间点。由于云盘数据较多，09:00开始创建快照，10:20完成创建快照，实际耗时80分钟。系统会跳过时间点10:00，等到11:00继续为您创建自动快照。
-   跨地域复制快照的注意事项请参见[复制快照](~~159441~~)的背景信息章节。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateAutoSnapshotPolicy&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateAutoSnapshotPolicy|系统规定参数。取值：CreateAutoSnapshotPolicy |
|regionId|String|是|cn-hangzhou|自动快照策略所属的地域。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|repeatWeekdays|String|是|\["1","2"\]|自动快照的重复日期，单位为天，周期为星期。取值范围：1~7，如1表示周一。

 当一星期内需要创建多次自动快照时，可以传入多个时间点：

 -   最多传入7个时间点。
-   多个时间点用一个格式类似`["1","2"..."7"]`的JSON数组表示，时间点之间用半角逗号（,）隔开。 |
|retentionDays|Integer|是|30|自动快照的保留时间，单位为天。取值范围：

 -   -1：永久保存
-   1~65535：指定保存天数

 默认值：-1 |
|timePoints|String|是|\["0", "1", … "23"\]|自动快照的创建时间点。使用UTC +8时间，单位为小时。取值范围：0~23，代表00:00至23:00共24个时间点，如1表示01:00。

 当一天内需要创建多次自动快照时，可以传入多个时间点，最多传入24个时间点。 |
|autoSnapshotPolicyName|String|否|TestName|自动快照策略的名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空 |
|EnableCrossRegionCopy|Boolean|否|false|是否允许自动跨地域复制。

 -   true：允许
-   false：不允许 |
|TargetCopyRegions|String|否|\["cn-hangzhou"\]|跨地域复制快照的目标地域。目前支持设置一个目标地域。 |
|CopiedSnapshotsRetentionDays|Integer|否|30|跨地域复制快照的保留时间，单位为天。取值范围：

 -   -1：永久保存
-   1~65535：指定保存天数

 默认值：-1 |
|Tag.N.Key|String|否|TestKey|快照的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|Tag.N.Value|String|否|TestValue|快照的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以acs:开头，不能包含http://或者https://。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoSnapshotPolicyId|String|sp-bp12m37ccmxvbmi5\*\*\*\*|自动快照策略ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateAutoSnapshotPolicy
&regionId=cn-hangzhou
&repeatWeekdays=["1"]
&retentionDays=30
&timePoints=["0", "19"]
&autoSnapshotPolicyName=TestName
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateAutoSnapshotPolicyResponse>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
      <AutoSnapshotPolicyId>sp-bp12m37ccmxvbmi5****</AutoSnapshotPolicyId>
</CreateAutoSnapshotPolicyResponse>
```

`JSON`格式

```
{
    "RequestId": "F3CD6886-D8D0-4FEE-B93E-1B73239673DE",
    "AutoSnapshotPolicyId": "sp-bp12m37ccmxvbmi5****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|ParameterInvalid|The specified RegionId parameter is invalid.|指定的地域ID无效，请您检查该地域是否正确。|
|403|ParameterInvalid|The specified RepeatWeekDays parameter is invalid.|指定的日期无效，请您检查该日期是否正确。|
|403|ParameterInvalid|The specified TimePoints parameter is invalid.|指定的时间点不合法，请您查看该时间点是否填写正确。|
|403|ParameterInvalid|The specified RetentionDays parameter is invalid.|指定的保持天数不合法。|
|403|AutoSnapshotPolicy.QuotaExceed|The maximum number of automatic snapshot policy has been reached.|自动快照策略数超出最大值。|
|400|DiskCategory.OperationNotSupported|The type of the specified disk does not support creating a snapshot.|当前磁盘类型不支持此操作。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|快照服务未开通，操作无法执行。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签中存在重复的键，请保持键的唯一性。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键参数有误。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值参数有误。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

