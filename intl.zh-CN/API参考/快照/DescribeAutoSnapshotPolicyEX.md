# DescribeAutoSnapshotPolicyEX

调用DescribeAutoSnapshotPolicyEX查询您已创建的自动快照策略。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeAutoSnapshotPolicyEx&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAutoSnapshotPolicyEx|系统规定参数。取值：DescribeAutoSnapshotPolicyEx |
|RegionId|String|是|cn-hangzhou|要查询的自动快照策略所在的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|AutoSnapshotPolicyId|String|否|sp-bp67acfmxazb4ph\*\*\*\*|自动快照策略ID。 |
|PageNumber|Integer|否|1|自动快照策略返回结果分多页展示。

 起始值：1

 默认值：1 |
|PageSize|Integer|否|1|分页展示返回的自动快照策略时的每页行数。

 最大值：100

 默认值：10 |
|Tag.N.Key|String|否|TestKey|快照的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|Tag.N.Value|String|否|TestValue|快照的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以acs:开头，不能包含http://或者https://。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoSnapshotPolicies|Array of AutoSnapshotPolicy| |自动快照策略详情AutoSnapshotPolicy组成的集合。 |
|AutoSnapshotPolicy| | | |
|AutoSnapshotPolicyId|String|sp-bp67acfmxazb4ph\*\*\*\*|自动快照策略ID。 |
|AutoSnapshotPolicyName|String|testAutoSnapshotPolicyName|自动快照策略的名称。 |
|CopiedSnapshotsRetentionDays|Integer|0|**说明：** 该参数即将上线。 |
|CreationTime|String|2014-04-21T12:08:52Z|创建时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|DiskNums|Integer|1|启用该策略的云盘数量。 |
|EnableCrossRegionCopy|Boolean|false|**说明：** 该参数即将上线。 |
|RegionId|String|cn-hangzhou|自动快照策略所属的地域ID。 |
|RepeatWeekdays|String|\["6"\]|指定自动快照的重复日期。选定周一到周日中需要创建快照的日期，参数为1~7的数字，如1表示周一。允许选择多个日期。 |
|RetentionDays|Integer|30|指定自动快照的保留时间，单位为天。可能值：

 -   -1：永久保存
-   1~65536：指定保存天数 |
|Status|String|Normal|自动快照策略状态。可能值：

 -   Normal：正常。
-   Expire：由于账号欠费无法使用该策略。 |
|Tags|Array of Tag| |快照的标签键值集合。 |
|Tag| | | |
|TagKey|String|TestKey|快照标签键。 |
|TagValue|String|TestValue|快照标签值。 |
|TargetCopyRegions|String|test|**说明：** 该参数即将上线。 |
|TimePoints|String|\["4", "19"\]|指定自动快照的创建时间点。

 使用UTC +8时间，单位为小时。从00:00~23:00共24个时间点可选，参数为0~23的数字，如：1代表在01:00时间点。可以选定多个时间点。

 传递参数为一个带有格式的Json Array：`"0", "1", ... "23"`，最多24个时间点，用半角逗号字符（,）隔开。 |
|VolumeNums|Integer|2|启用该策略的拓展卷数量。 |
|PageNumber|Integer|1|自动快照策略列表的页码。 |
|PageSize|Integer|1|分页展示返回的自动快照策略时的每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|2|自动快照策略的总个数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeAutoSnapshotPolicyEx
&RegionId=cn-hangzhou
&AutoSnapshotPolicyId=sp-bp67acfmxazb4ph****
&PageNumber=1
&PageSize=1
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeAutoSnapshotPolicyExResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>2</TotalCount>
      <AutoSnapshotPolicies>
            <AutoSnapshotPolicy>
                  <CreationTime>2019-01-22 11:38:08</CreationTime>
                  <Status>Normal</Status>
                  <DiskNums>1</DiskNums>
                  <AutoSnapshotPolicyName>testAutoSnapshotPolicyName</AutoSnapshotPolicyName>
                  <RegionId>cn-hangzhou</RegionId>
                  <VolumeNums>2</VolumeNums>
                  <RetentionDays>30</RetentionDays>
                  <TimePoints>["0"]</TimePoints>
                  <AutoSnapshotPolicyId>sp-bp67acfmxazb4ph****</AutoSnapshotPolicyId>
                  <RepeatWeekdays>["7"]</RepeatWeekdays>
                  <Tags>
                        <Tag>
                              <TagKey>TestKey</TagKey>
                              <TagValue>TestValue</TagValue>
                        </Tag>
                  </Tags>
            </AutoSnapshotPolicy>
      </AutoSnapshotPolicies>
      <PageSize>1</PageSize>
      <RequestId>CC323EDF-BBB7-420F-BCD1-D9B9D2E9D424</RequestId>
</DescribeAutoSnapshotPolicyExResponse>
```

`JSON`格式

```
{
	"PageNumber": 1,
	"TotalCount": 2,
	"AutoSnapshotPolicies": {
		"AutoSnapshotPolicy": [
			{
				"CreationTime": "2019-01-22 11:38:08",
				"Status": "Normal",
				"DiskNums": 1,
				"AutoSnapshotPolicyName": "testAutoSnapshotPolicyName",
				"RegionId": "cn-hangzhou",
				"VolumeNums": 2,
				"RetentionDays": 30,
				"TimePoints": "[\"0\"]",
				"AutoSnapshotPolicyId": "sp-bp67acfmxazb4ph****",
				"RepeatWeekdays": "[\"7\"]",
                "Tags": {
					"Tag": [
						{
							"TagKey": "TestKey",
							"TagValue": "TestValue"
						}
					]
				}
			}
		]
	},
	"PageSize": 1,
	"RequestId": "CC323EDF-BBB7-420F-BCD1-D9B9D2E9D424"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的地域ID不存在。|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|指定的Tag.N.Key和Tag.N.Value不匹配。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

