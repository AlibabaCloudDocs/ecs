# ResetDisks

调用ResetDisks通过实例快照回滚一个或多个云盘。

## 接口说明

调用该接口回滚云盘前，请您务必了解回滚功能的注意事项。更多信息，请参见[通过实例快照回滚云盘](~~209160~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ResetDisks&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|ResetDisks|系统规定参数。取值：ResetDisks |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Disk.N.SnapshotId|String|否|s-j6cdofbycydvg7ey\*\*\*\*|实例快照中，指定云盘对应的快照ID。N的取值范围：1~10 |
|Disk.N.DiskId|String|否|d-j6cf7l0ewidb78lq\*\*\*\*|指定待回滚的云盘ID。N的取值范围：1~10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|OperationProgressSet|Array of OperationProgress| |回滚一个或多个云盘时的操作状态信息合集。 |
|OperationProgress| | | |
|ErrorCode|String|400|错误码。回滚成功时返回空值。

 错误码和错误信息，请参见[错误中心](https://error-center.aliyun.com/status/product/Ecs)。 |
|ErrorMsg|String|testErrorMsg|错误信息。回滚成功时返回空值。

 错误码和错误信息，请参见[错误中心](https://error-center.aliyun.com/status/product/Ecs)。 |
|OperationStatus|String|Success|操作是否成功。

 成功返回Success，失败返回ErrorCode和ErrorMsg信息。 |
|RelatedItemSet|Array of RelatedItem| |资源信息。 |
|RelatedItem| | | |
|Name|String|SnapshotId|资源名称。 |
|Value|String|s-j6cdofbycydvg7ey\*\*\*\*|资源ID。 |
|RequestId|String|3D66C85C-AA97-4A00-B0ED-2D9A80FE782C|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ResetDisks
&RegionId=cn-hangzhou
&Disk.1.DiskId=d-j6cf7l0ewidb78lq****
&Disk.1.SnapshotId=s-j6cdofbycydvg7ey****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ResetDisksResponse>
      <RequestId>5C4160C1-C77D-4FD0-9C47-DB9FFA3D1220</RequestId>
      <OperationProgressSet>
            <OperationProgress>
                  <OperationStatus>Success</OperationStatus>
                  <ErrorMsg></ErrorMsg>
                  <RelatedItemSet>
                        <RelatedItem>
                              <Value>s-j6cdofbycydvg7ey****</Value>
                              <Name>SnapshotId</Name>
                        </RelatedItem>
                        <RelatedItem>
                              <Value>d-j6cf7l0ewidb78lq****</Value>
                              <Name>DiskId</Name>
                        </RelatedItem>
                  </RelatedItemSet>
                  <ErrorCode></ErrorCode>
            </OperationProgress>
      </OperationProgressSet>
</ResetDisksResponse>
```

`JSON`格式

```
{
	"RequestId": "5C4160C1-C77D-4FD0-9C47-DB9FFA3D1220",
	"OperationProgressSet": {
		"OperationProgress": [
			{
				"OperationStatus": "Success",
				"ErrorMsg": "",
				"RelatedItemSet": {
					"RelatedItem": [
						{
							"Value": "s-j6cdofbycydvg7ey****",
							"Name": "SnapshotId"
						},
						{
							"Value": "d-j6cf7l0ewidb78lq****",
							"Name": "DiskId"
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

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|由于磁盘种类限制，指定的磁盘不支持该操作。|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|指定的RegionId不合法。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|InvalidParameter.Mismatch|The specified snapshot is not created from the specified disk.|未加密的磁盘无法通过加密的快照重置。|
|403|InvalidSnapshot.TooOld|The snapshotId is created before 2013-07-15, it cannot be restored since the first time the disk detached.|创建于2013年7月15日之前的快照不支持此操作。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|OperationDenied|The specified snapshot dees not support ResetDisk.|指定的快照不支持重置磁盘。|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|指定的快照未完成。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|快照服务未开通，操作无法执行。|
|403|Operation.Conflict|The operation may conflicts with others.|该操作与其他操作冲突。|
|403|UserNotInTheWhiteList|The user is not in disk white list.|您不在磁盘白名单中，请加入白名单后重试。|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|加密云盘设置了KMSKeyId后，CMK必须处于启用状态。您可以调用密钥管理服务的DescribeKey接口查询指定CMK的相关信息。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|403|InvalidOperation.MultiAttachDisk|Multi attach disk does not support this operation.|开启多重挂载特性的云盘不支持该操作。|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|404|Disk.NotFound|The specified disk does not exist.|指定的磁盘不存在，请您检查磁盘是否正确。|
|404|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|指定的快照不存在，请您检查快照是否正确。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

