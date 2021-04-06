# DescribeSnapshotGroups

调用DescribeSnapshotGroups查询一个或多个实例快照的信息。

## 接口说明

`InstanceId`、`SnapshotGroupId.N`和`Status.N`不是必需的请求参数，但是可以构建过滤器逻辑，参数之间为逻辑与（And）关系。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshotGroups&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSnapshotGroups|系统规定参数。取值：DescribeSnapshotGroups |
|RegionId|String|是|cn-hangzhou|所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|InstanceId|String|否|i-j6ca469urv8ei629\*\*\*\*|指定的实例ID。 |
|SnapshotGroupId.N|RepeatList|否|ssg-j6ciyh3k52qp7ovm\*\*\*\*|指定的实例快照ID。N的取值范围：1~10 |
|Status.N|RepeatList|否|accomplished|实例快照的状态。取值如下：

 -   progressing：创建中
-   accomplished：创建成功
-   failed：创建失败

 N的取值范围：1~3 |
|Name|String|否|testName|实例快照的名称。 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0a4883|查询凭证（Token），取值为上一次API调用返回的NextToken参数值。 |
|MaxResults|Integer|否|10|分页查询时每页行数。

 最大值：100

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|下一个查询起始标志。 |
|RequestId|String|3F9A4CC4-362F-469A-B9EF-B3204EF8AA3A|请求ID。 |
|SnapshotGroups|Array of SnapshotGroup| |实例快照的信息组成的数组。 |
|SnapshotGroup| | | |
|CreationTime|String|2021-03-23T10:58:48Z|创建时间。 |
|Description|String|This is description.|描述。 |
|InstanceId|String|i-j6ca469urv8ei629\*\*\*\*|实例快照所属的实例ID。 |
|Name|String|testName|实例快照的名称。 |
|ProgressStatus|String|null|**说明：** 该参数暂未开放使用 |
|SnapshotGroupId|String|ssg-j6ciyh3k52qp7ovm\*\*\*\*|实例快照ID。 |
|Snapshots|Array of Snapshot| |实例快照中包含的快照信息组成的数组。 |
|Snapshot| | | |
|InstantAccess|Boolean|true|是否开启了快照极速可用功能。可能值：

 -   true：开启。仅ESSD云盘支持开启该功能。
-   false：关闭。即快照为未开启快照极速可用功能的普通快照。 |
|InstantAccessRetentionDays|Integer|3|快照极速可用功能的保留时间，保留时间到期后快照将自动释放。 |
|Progress|String|100%|快照创建进度，单位为百分比。 |
|SnapshotId|String|s-j6cbzmrlbf09w72q\*\*\*\*|快照ID。 |
|SourceDiskId|String|d-j6c3ogynmvpi6wy7\*\*\*\*|源云盘ID。如果快照的源云盘已经被释放，该字段仍旧保留。 |
|SourceDiskType|String|system|源云盘类型。可能值：

 -   system：系统盘
-   data：数据盘 |
|Status|String|accomplished|实例快照的状态。取值如下：

 -   progressing：创建中
-   accomplished：创建成功
-   failed：创建失败 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeSnapshotGroups
&RegionId=cn-hangzhou
&SnapshotGroupId.1=ssg-j6ciyh3k52qp7ovm****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeSnapshotGroupsResponse>
      <RequestId>3F9A4CC4-362F-469A-B9EF-B3204EF8AA3A</RequestId>
      <NextToken></NextToken>
      <SnapshotGroups>
            <SnapshotGroup>
                  <Status>accomplished</Status>
                  <Description>This is description.</Description>
                  <InstanceId>i-j6ca469urv8ei629****</InstanceId>
                  <CreationTime>2021-03-23T10:58:48Z</CreationTime>
                  <SnapshotGroupId>ssg-j6ciyh3k52qp7ovm****</SnapshotGroupId>
                  <Snapshots>
                        <Snapshot>
                              <SnapshotId>s-j6cbzmrlbf09w72q****</SnapshotId>
                              <InstantAccess>true</InstantAccess>
                              <Progress>100%</Progress>
                              <SourceDiskType>system</SourceDiskType>
                              <InstantAccessRetentionDays>3</InstantAccessRetentionDays>
                              <SourceDiskId>d-j6c3ogynmvpi6wy7****</SourceDiskId>
                        </Snapshot>
                        <Snapshot>
                              <SnapshotId>s-j6cdofbycydvg7ey****</SnapshotId>
                              <InstantAccess>true</InstantAccess>
                              <Progress>100%</Progress>
                              <SourceDiskType>data</SourceDiskType>
                              <InstantAccessRetentionDays>3</InstantAccessRetentionDays>
                              <SourceDiskId>d-j6cf7l0ewidb78lq****</SourceDiskId>
                        </Snapshot>
                  </Snapshots>
                  <Name>testName</Name>
            </SnapshotGroup>
      </SnapshotGroups>
</DescribeSnapshotGroupsResponse>
```

`JSON`格式

```
{
	"RequestId": "3F9A4CC4-362F-469A-B9EF-B3204EF8AA3A",
	"NextToken": "",
	"SnapshotGroups": {
		"SnapshotGroup": [
			{
				"Status": "accomplished",
				"Description": "This is description.",
				"InstanceId": "i-j6ca469urv8ei629****",
				"CreationTime": "2021-03-23T10:58:48Z",
				"SnapshotGroupId": "ssg-j6ciyh3k52qp7ovm****",
				"Snapshots": {
					"Snapshot": [
						{
							"SnapshotId": "s-j6cbzmrlbf09w72q****",
							"InstantAccess": true,
							"Progress": "100%",
							"SourceDiskType": "system",
							"InstantAccessRetentionDays": 3,
							"SourceDiskId": "d-j6c3ogynmvpi6wy7****"
						},
						{
							"SnapshotId": "s-j6cdofbycydvg7ey****",
							"InstantAccess": true,
							"Progress": "100%",
							"SourceDiskType": "data",
							"InstantAccessRetentionDays": 3,
							"SourceDiskId": "d-j6cf7l0ewidb78lq****"
						}
					]
				},
				"Name": "testName"
			}
		]
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidStatus.ValueNotSupported|%s|该资源当前的状态不支持此操作。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

