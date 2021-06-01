# DescribeImages

调用DescribeImages查询您可以使用的镜像资源。

## 接口说明

-   您可以查询的镜像资源包括您的自定义镜像、阿里云提供的公共镜像、云市场镜像以及其他阿里云用户主动共享给您的共享镜像。
-   支持分页查询，查询结果包括可使用的镜像资源的总数和当前页的镜像资源。每页的数量默认为10条。
-   通过阿里云CLI调用API时，不同数据类型的请求参数取值必须遵循格式要求，详情请参见[CLI参数格式说明](~~110340~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeImages&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeImages|系统规定参数。取值：DescribeImages |
|RegionId|String|是|cn-hangzhou|镜像所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Status|String|否|Available|查询某种状态下的镜像。取值范围：

 -   Creating：镜像正在创建中。
-   Waiting：多任务排队中。
-   Available（默认）：您可以使用的镜像。
-   UnAvailable：您不能使用的镜像。
-   CreateFailed：创建失败的镜像。
-   Deprecated：已弃用的镜像。

 支持同时取多个值，值之间以半角逗号（,）隔开。 |
|ImageId|String|否|m-bp1g7004ksh0oeuc\*\*\*\*|镜像ID。 |
|ShowExpired|Boolean|否|false|订阅型镜像是否已经超过使用期限。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。 |
|SnapshotId|String|否|s-bp17ot2q7x72ggtw\*\*\*\*|根据某一快照ID创建的自定义镜像。 |
|ImageName|String|否|testImageName|镜像名称。 |
|ImageFamily|String|否|hangzhou-daily-update|镜像族系名称，查询镜像时可通过设置该参数来过滤当前族系对应的镜像。

 默认值：空 |
|ImageOwnerAlias|String|否|self|镜像来源。取值范围：

 -   system：阿里云提供的公共镜像。
-   self：您创建的自定义镜像。
-   others：其他阿里云用户共享给您的镜像。
-   marketplace：镜像市场提供的镜像。您查询到的云市场镜像可以直接使用，无需提前订阅。您需要自行留意云市场镜像的收费详情。

 默认值：空，空表示返回取值为system、self以及others的结果。 |
|InstanceType|String|否|ecs.g5.large|指定实例类型可以使用的镜像。 |
|IsSupportIoOptimized|Boolean|否|true|镜像是否可以运行在I/O优化实例上。 |
|IsSupportCloudinit|Boolean|否|true|镜像是否支持cloud-init。 |
|OSType|String|否|linux|镜像的操作系统类型。取值范围：

 -   windows
-   linux |
|Architecture|String|否|i386|镜像的体系架构。取值范围：

 -   i386
-   x86\_64
-   arm64 |
|PageNumber|Integer|否|1|镜像资源列表的页码。起始值：1

 默认值：1 |
|PageSize|Integer|否|1|分页查询时设置的每页行数。最大值：100

 默认值：10 |
|Usage|String|否|instance|镜像是否已经运行在ECS实例中。取值范围：

 -   instance：镜像处于运行状态，有ECS实例使用。
-   none：镜像处于闲置状态，暂无ECS实例使用。 |
|Tag.N.value|String|否|null|镜像的标签值。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用Tag.N.Value参数。 |
|Tag.N.key|String|否|null|镜像的标签键。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用Tag.N.Key参数。 |
|Tag.N.Key|String|否|TestKey|镜像的标签键。N的取值范围：1~20

 使用一个标签过滤资源，查询到该标签下的资源数量不能超过1000个；使用多个标签过滤资源，查询到同时绑定了多个标签的资源数量不能超过1000个。如果资源数量超过1000个，请使用[ListTagResources](~~110425~~)接口进行查询。 |
|Tag.N.Value|String|否|TestValue|镜像的标签值。N的取值范围：1~20 |
|DryRun|Boolean|否|false|是否只预检此次请求。

 -   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码DryRunOperation。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

 默认值：false |
|ActionType|String|否|CreateEcs|镜像需要被使用到的场景。取值范围：

 -   CreateEcs（默认）：创建实例。
-   ChangeOS：更换系统盘/更换操作系统。 |
|Filter.N.Key|String|否|CreationStartTime|查询资源时的筛选键。取值范围：

 -   当该参数取值为`CreationStartTime`时，可以查询在指定时间点（`Filter.N.Value`）后创建的资源信息。
-   当该参数取值为`CreationEndTime`时，可以查询在指定时间点（`Filter.N.Value`）前创建的资源信息。 |
|Filter.N.Value|String|否|2017-12-05T22:40Z|查询资源时的筛选值。指定该参数时必须同时指定`Filter.N.Key`参数，格式为：`yyyy-MM-ddTHH:mmZ`，采用UTC +0时区。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|自定义镜像所在的企业资源组ID。使用该参数过滤资源时，资源数量不能超过1000个。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Images|Array of Image| |镜像信息Images组成的集合。 |
|Image| | | |
|Architecture|String|x86\_64|镜像系统架构类型。可能值：

 -   i386
-   x86\_64
-   arm64 |
|CreationTime|String|2019-11-15T06:07:05Z|镜像的创建时间。 |
|Description|String|Archive log for Oracle|描述信息。 |
|DiskDeviceMappings|Array of DiskDeviceMapping| |镜像下包含云盘和快照的映射关系。 |
|DiskDeviceMapping| | | |
|Device|String|/dev/xvda|云盘的设备信息，例如/dev/xvdb。

 **说明：** 该参数即将停止使用，为提高代码的兼容性，建议您尽量不要使用该参数。 |
|Format|String|qcow2|镜像格式。 |
|ImportOSSBucket|String|testEcsImport|导入镜像所属OSS的bucket。 |
|ImportOSSObject|String|imageImport|导入镜像所属OSS的object。 |
|Progress|String|32%|对于复制中的镜像，返回复制任务的进度。 |
|RemainTime|Integer|233|对于复制中的镜像，返回复制任务的剩余时间，单位为秒。 |
|Size|String|60|云盘的大小。 |
|SnapshotId|String|s-bp17ot2q7x72ggtw\*\*\*\*|快照ID。 |
|Type|String|system|镜像的类型。 |
|ImageFamily|String|hangzhou-daily-update|镜像族系名称。 |
|ImageId|String|m-bp1g7004ksh0oeuc\*\*\*\*|镜像ID。 |
|ImageName|String|testImageName|镜像的名称。 |
|ImageOwnerAlias|String|self|镜像来源。可能值：

 -   system：阿里云提供的公共镜像。
-   self：您创建的自定义镜像。
-   others：其他阿里云用户共享给您的镜像。
-   marketplace：镜像市场提供的镜像。 |
|ImageVersion|String|2|镜像版本。 |
|IsCopied|Boolean|false|是否是拷贝的镜像。 |
|IsSelfShared|String|true|是否共享过该自定义镜像给其他用户。 |
|IsSubscribed|Boolean|false|是否订阅了该镜像的商品码对应的镜像商品的服务条款。 |
|IsSupportCloudinit|Boolean|true|是否支持Cloud Init。 |
|IsSupportIoOptimized|Boolean|true|是否可以在I/O优化实例上运行。 |
|OSName|String|Windows Server 2016 数据中心版 64位中文版|操作系统的中文显示名称。 |
|OSNameEn|String|Windows Server 2016 Data Center Edition 64bit Chinese Edition|操作系统的英文显示名称。 |
|OSType|String|windows|操作系统类型。可能值：

 -   windows
-   linux |
|Platform|String|Windows Server 2016|操作系统平台。 |
|ProductCode|String|test000\*\*\*\*|镜像市场的镜像商品标示。 |
|Progress|String|100%|镜像完成的进度，单位为百分比。 |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|镜像所在的企业资源组ID。 |
|Size|Integer|60|镜像大小，单位GiB。 |
|Status|String|Available|镜像的状态。可能值：

 -   UnAvailable：不可用
-   Available：可用
-   Creating：创建中
-   CreateFailed：创建失败 |
|Tags|Array of Tag| |镜像的标签对信息。 |
|Tag| | | |
|TagKey|String|DTS|镜像的标签键。 |
|TagValue|String|Oracle|镜像的标签值。 |
|Usage|String|none|有引用关系的资源类型。可能值：

 -   instance：创建了一台或多台ECS实例。
-   none：未创建过ECS实例。 |
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|1|当前分页包含多少条目。 |
|RegionId|String|cn-hangzhou|镜像所属地域ID。 |
|RequestId|String|66189103-EDB2-43E2-BB60-BFF2B62F4EB8|请求ID。 |
|TotalCount|Integer|1|镜像总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeImages
&RegionId=cn-hangzhou
&PageSize=1
&PageNumber=1
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeImagesResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>1</TotalCount>
      <PageSize>1</PageSize>
      <RegionId>cn-hangzhou</RegionId>
      <RequestId>66189103-EDB2-43E2-BB60-BFF2B62F4EB8</RequestId>
      <Images>
            <Image>
                  <ImageId>m-bp1g7004ksh0oeuc****</ImageId>
                  <ImageFamily>hangzhou-daily-update</ImageFamily>
                  <Description>Archive log for Oracle</Description>
                  <OSNameEn>Windows Server  2016 Data Center Edition 64bit Chinese Edition</OSNameEn>
                  <ProductCode></ProductCode>
                  <ResourceGroupId></ResourceGroupId>
                  <OSType>windows</OSType>
                  <Architecture>x86_64</Architecture>
                  <OSName>Windows Server  2016 数据中心版 64位中文版</OSName>
                  <DiskDeviceMappings>
                        <DiskDeviceMapping>
                              <ImportOSSObject></ImportOSSObject>
                              <Format></Format>
                              <Device>/dev/xvda</Device>
                              <Type>system</Type>
                              <SnapshotId>s-bp17ot2q7x72ggtw****</SnapshotId>
                              <ImportOSSBucket></ImportOSSBucket>
                              <Progress></Progress>
                              <Size>60</Size>
                        </DiskDeviceMapping>
                  </DiskDeviceMappings>
                  <ImageOwnerAlias>self</ImageOwnerAlias>
                  <Progress>100%</Progress>
                  <IsSupportCloudinit>true</IsSupportCloudinit>
                  <Usage>none</Usage>
                  <CreationTime>2019-11-15T06:07:05Z</CreationTime>
                  <ImageVersion></ImageVersion>
                  <Tags>
                        <Tag>
                              <TagValue>Oracle</TagValue>
                              <TagKey>DTS</TagKey>
                        </Tag>
                  </Tags>
                  <Status>Available</Status>
                  <ImageName>testImageName</ImageName>
                  <IsSupportIoOptimized>true</IsSupportIoOptimized>
                  <IsSelfShared>False</IsSelfShared>
                  <IsCopied>false</IsCopied>
                  <IsSubscribed>false</IsSubscribed>
                  <Platform>Windows Server 2016</Platform>
                  <Size>60</Size>
            </Image>
      </Images>
</DescribeImagesResponse>
```

`JSON`格式

```
{
	"PageNumber": 1,
	"TotalCount": 1,
	"PageSize": 1,
	"RegionId": "cn-hangzhou",
	"RequestId": "66189103-EDB2-43E2-BB60-BFF2B62F4EB8",
	"Images": {
		"Image": [
			{
				"ImageId": "m-bp1g7004ksh0oeuc****",
				"ImageFamily": "hangzhou-daily-update",
				"Description": "Archive log for Oracle",
				"OSNameEn": "Windows Server  2016 Data Center Edition 64bit Chinese Edition",
				"ProductCode": "",
				"ResourceGroupId": "",
				"OSType": "windows",
				"Architecture": "x86_64",
				"OSName": "Windows Server  2016 数据中心版 64位中文版",
				"DiskDeviceMappings": {
					"DiskDeviceMapping": [
						{
							"ImportOSSObject": "",
							"Format": "",
							"Device": "/dev/xvda",
							"Type": "system",
							"SnapshotId": "s-bp17ot2q7x72ggtw****",
							"ImportOSSBucket": "",
							"Progress": "",
							"Size": "60"
						}
					]
				},
				"ImageOwnerAlias": "self",
				"Progress": "100%",
				"IsSupportCloudinit": true,
				"Usage": "none",
				"CreationTime": "2019-11-15T06:07:05Z",
				"ImageVersion": "",
				"Tags": {
					"Tag": [
						{
							"TagValue": "Oracle",
							"TagKey": "DTS"
						}
					]
				},
				"Status": "Available",
				"ImageName": "testImageName",
				"IsSupportIoOptimized": true,
				"IsSelfShared": "False",
				"IsCopied": false,
				"IsSubscribed": false,
				"Platform": "Windows Server 2016",
				"Size": 60
			}
		]
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidImageOwnerAlias.ValueNotSupported|The specified ImageOwnerAlias value is not supported.|无效的镜像所有者别名，请您检查该参数是否正确。|
|400|InvalidParamter|Invalid Parameter|指定的参数不合法。|
|404|InvalidFilterKey.NotFound| |指定的起始时间或到期时间参数错误。|
|404|InvalidUsage|The specifed Usage is not valid|指定有引用关系的资源类型（image、disk、image\_disk、none）不合法。|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|指定的Tag.N.Key和Tag.N.Value不匹配。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|您指定的实例规格不存在，或者您没有权限操作此规格的实例。|
|404|InvalidOSType|The specifed OSType is not valid|不支持指定的操作系统。|
|404|InvalidArchitecture|The specifed Architecture is not valid|指定的架构不存在。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

