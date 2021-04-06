# DeleteSnapshotGroup

调用DeleteSnapshotGroup删除指定的实例快照。

## 接口说明

如果实例快照中的云盘快照已经用于创建自定义镜像，则实例快照删除时相关的云盘快照不会被删除。您如果需要删除相关的云盘快照，请先删除已创建的自定义镜像（[DeleteImage](~~25537~~)），再删除相关的云盘快照（[DeleteSnapshot](~~25525~~)）。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DeleteSnapshotGroup&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DeleteSnapshotGroup|系统规定参数。取值：DeleteSnapshotGroup |
|RegionId|String|是|cn-hangzhou|实例快照所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|SnapshotGroupId|String|是|ssg-j6c9lpuyxo2uxxny\*\*\*\*|实例快照ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|OperationProgressSet|Array of OperationProgress| |删除实例快照时操作状态信息合集。 |
|OperationProgress| | | |
|ErrorCode|String|400|错误码。删除成功时返回空值。

 错误码和错误信息，请参见[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。 |
|ErrorMsg|String|testErrorMsg|错误信息。删除成功时返回空值。

 错误码和错误信息，请参见[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。 |
|OperationStatus|String|Success|操作是否成功。成功返回Success，失败返回ErrorCode和ErrorMsg信息。 |
|RelatedItemSet|Array of RelatedItem| |资源信息。 |
|RelatedItem| | | |
|Name|String|SnapshotId|资源名称。 |
|Value|String|s-j6c9lpuyxo2uxxnx\*\*\*\*|资源ID。 |
|RequestId|String|6EDE885A-FDC1-4FAE-BC44-6EACAEA6CC6E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DeleteSnapshotGroup
&RegionId=cn-hangzhou
&SnapshotGroupId=ssg-j6c9lpuyxo2uxxny****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteSnapshotGroupResponse>
      <RequestId>6EDE885A-FDC1-4FAE-BC44-6EACAEA6CC6E</RequestId>
      <OperationProgressSet>
            <OperationProgress>
                  <OperationStatus>Success</OperationStatus>
                  <ErrorMsg></ErrorMsg>
                  <RelatedItemSet>
                        <RelatedItem>
                              <Value>s-j6c9lpuyxo2uxxnx****</Value>
                              <Name>SnapshotId</Name>
                        </RelatedItem>
                  </RelatedItemSet>
                  <ErrorCode></ErrorCode>
            </OperationProgress>
            <OperationProgress>
                  <OperationStatus>Success</OperationStatus>
                  <ErrorMsg></ErrorMsg>
                  <RelatedItemSet>
                        <RelatedItem>
                              <Value>s-j6c9lpuyxo2uxxnx****</Value>
                              <Name>SnapshotId</Name>
                        </RelatedItem>
                  </RelatedItemSet>
                  <ErrorCode></ErrorCode>
            </OperationProgress>
      </OperationProgressSet>
</DeleteSnapshotGroupResponse>
```

`JSON`格式

```
{
	"RequestId": "6EDE885A-FDC1-4FAE-BC44-6EACAEA6CC6E",
	"OperationProgressSet": {
		"OperationProgress": [
			{
				"OperationStatus": "Success",
				"ErrorMsg": "",
				"RelatedItemSet": {
					"RelatedItem": [
						{
							"Value": "s-j6c9lpuyxo2uxxnx****",
							"Name": "SnapshotId"
						}
					]
				},
				"ErrorCode": ""
			},
			{
				"OperationStatus": "Success",
				"ErrorMsg": "",
				"RelatedItemSet": {
					"RelatedItem": [
						{
							"Value": "s-j6c9lpuyxo2uxxnx****",
							"Name": "SnapshotId"
						}
					]
				},
				"ErrorCode": ""
			}
		]
	}
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

