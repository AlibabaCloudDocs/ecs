# DescribeDisks

调用DescribeDisks查询一块或多块您已经创建的块存储（包括云盘以及本地盘）。

## 接口说明

-   请求参数`RegionId`、`ZoneId`、`DiskIds`和`InstanceId`等都是过滤器的概念，参数间是逻辑与（AND）关系。
-   请求参数`DiskIds`是一个JSON格式的数组（Array），如果参数为空，则过滤器不起作用，但是`DiskIds`如果是一个空数组，则视为该过滤器有效，且返回空。
-   支持以下两种方式查看返回数据：
    -   方式一：通过`NextToken`设置查询凭证（Token），其取值是上一次调用DescribeDisks返回的`NextToken`参数值，再通过`MaxResults`设置单页查询的最大条目数。
    -   方式二：通过`PageSize`设置单页返回的条目数，再通过`PageNumber`设置页码。

        以上两种方式只能任选其中之一。当返回的条目数较多时，推荐使用方式一。如果设置了`NextToken`，则请求参数`PageSize`和`PageNumber`将失效，且返回数据中的`TotalCount`无效。

-   开启多重挂载特性的云盘可以挂载到多个实例上，您可以根据返回结果的`Attachment`列表查看云盘涉及的所有挂载信息。

通过阿里云CLI调用API时，不同数据类型的请求参数取值必须遵循格式要求。更多信息，请参见[CLI参数格式说明](~~110340~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeDisks&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDisks|系统规定参数。取值：DescribeDisks |
|RegionId|String|是|cn-hangzhou|块存储所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ZoneId|String|否|cn-hangzhou-g|可用区ID。 |
|DiskIds|String|否|\["d-bp67acfmxazb4p\*\*\*\*", "d-bp67acfmxazb4g\*\*\*\*", … "d-bp67acfmxazb4d\*\*\*\*"\]|云盘或本地盘ID。一个带有格式的JSON数组，最多支持100个ID，用半角逗号（,）隔开。 |
|InstanceId|String|否|i-bp67acfmxazb4q\*\*\*\*|云盘或本地盘挂载的实例ID。 |
|DiskType|String|否|all|要查询的云盘或本地盘类型。取值范围：

 -   all：同时查询系统盘与数据盘。
-   system：只查询系统盘。
-   data：只查询数据盘。

 默认值：all |
|Category|String|否|all|云盘或本地盘种类。取值范围：

 -   all：所有云盘以及本地盘
-   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD盘
-   cloud\_essd：ESSD云盘
-   local\_ssd\_pro：I/O密集型本地盘
-   local\_hdd\_pro：吞吐密集型本地盘
-   ephemeral：（已停售）本地盘
-   ephemeral\_ssd：（已停售）本地SSD盘

 默认值：all |
|Status|String|否|All|云盘状态。更多信息，请参见[云盘状态](~~25689~~)。取值范围：

 -   In\_use
-   Available
-   Attaching
-   Detaching
-   Creating
-   ReIniting
-   All

 默认值：All |
|SnapshotId|String|否|s-bp67acfmxazb4p\*\*\*\*|创建云盘时使用的快照ID。 |
|Portable|Boolean|否|false|云盘或本地盘是否支持卸载。取值范围：

 -   true：支持。可以独立存在，且可以在可用区内自由挂载和卸载。
-   false：不支持。不可以独立存在，且不可以在可用区内自由挂载和卸载。

 以下类型块存储的`Portable`属性都为`false`，生命周期与实例等同：

 -   本地盘
-   本地SSD盘
-   包年包月数据盘 |
|DeleteWithInstance|Boolean|否|false|云盘是否设置了随实例释放。取值范围：

 -   true：云盘随实例一起释放。
-   false：云盘保留不释放，转为按量付费数据盘而保留下来。

 默认值：false |
|DeleteAutoSnapshot|Boolean|否|false|释放云盘时，是否会同时释放自动快照。

 默认值：false |
|PageNumber|Integer|否|1|云盘或本地盘状态列表的页码。

 起始值：1

 默认值：1 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。

 最大值：100

 默认值：10 |
|NextToken|String|否|AAAAAdDWBF2\*\*\*\*|查询凭证（Token），取值为上一次API调用返回的`NextToken`参数值。

 有关本接口查看返回数据的设置方式，请参见上文接口说明。 |
|MaxResults|Integer|否|50|返回的最大数。取值范围：1~500

 默认值：10。 |
|DiskName|String|否|testDiskName|云盘或本地盘名称。 |
|AutoSnapshotPolicyId|String|否|sp-m5e2w2jutw8bv31\*\*\*\*|根据自动快照策略ID查询云盘。 |
|EnableAutoSnapshot|Boolean|否|true|云盘是否启用自动快照策略功能。

 -   true：启用
-   false：未启用

 **说明：** 创建后的云盘默认启用自动快照策略功能，您只需要为云盘绑定自动快照策略即可正常使用。 |
|EnableAutomatedSnapshotPolicy|Boolean|否|false|云盘是否设置了自动快照策略。

 -   true：已设置
-   false：未设置

 默认值：false |
|DiskChargeType|String|否|PostPaid|云盘或本地盘的计费方式。取值范围：

 -   PrePaid：包年包月
-   PostPaid：按量付费 |
|LockReason|String|否|recycling|云盘或本地盘被锁定的原因。取值范围：

 -   financial：因欠费被锁定。
-   security：因安全原因被锁定。
-   recycling：抢占式实例的待释放锁定状态。
-   dedicatedhostfinancial：因为专有宿主机欠费导致ECS实例被锁定。 |
|Filter.1.Key|String|否|CreationStartTime|查询资源时的筛选键，取值必须为`CreationStartTime`。同时设置`Filter.1.Key`和`Filter.1.Value`可以查询在指定时间点后创建的资源信息。 |
|Filter.2.Key|String|否|CreationEndTime|查询资源时的筛选键，取值必须为`CreationEndTime`。同时设置`Filter.2.Key`和`Filter.2.Value`可以查询在指定时间点前创建的资源信息。 |
|Filter.1.Value|String|否|2017-12-05T22:40Z|查询资源时的筛选值。指定该参数时必须同时指定`Filter.1.Key`参数，格式为：`yyyy-MM-ddTHH:mmZ`，采用UTC +0时区。 |
|Filter.2.Value|String|否|2017-12-06T22:40Z|查询资源时的筛选值。指定该参数时必须同时指定`Filter.2.Key`参数，格式为：`yyyy-MM-ddTHH:mmZ`，采用UTC +0时区。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|云盘或本地盘所在的企业资源组ID。使用该参数过滤资源时，资源数量不能超过1000个。 |
|EnableShared|Boolean|否|false|是否是共享块存储。 |
|Encrypted|Boolean|否|false|是否只筛选出加密云盘。

 默认值：false |
|DryRun|Boolean|否|false|是否只预检此次请求。取值范围：

 -   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

 默认值：false |
|KMSKeyId|String|否|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|云盘使用的KMS密钥ID。 |
|MultiAttach|String|否|Disabled|是否开启了多重挂载特性。取值范围：

 -   Disabled：未开启
-   Enabled：已开启
-   LegacyShared：用于查询共享块存储

 多重挂载功能正在邀测中，如需使用，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。 |
|Tag.N.key|String|否|null|云盘或本地盘的标签键。

 **说明：** 为提高代码兼容性，请尽量使用Tag.N.Key参数。 |
|Tag.N.Key|String|否|TestKey|云盘或本地盘的标签键。N的取值范围：1~20

 使用一个标签过滤资源，查询到该标签下的资源数量不能超过1000个；使用多个标签过滤资源，查询到同时绑定了多个标签的资源数量不能超过1000个。如果资源数量超过1000个，请使用[ListTagResources](~~110425~~)接口进行查询。 |
|Tag.N.Value|String|否|TestValue|云盘或本地盘的标签值。N的取值范围：1~20 |
|Tag.N.value|String|否|null|云盘或本地盘的标签值。

 **说明：** 为提高代码兼容性，请尽量使用Tag.N.Value参数。 |
|AdditionalAttributes.N|RepeatList|否|IOPS|其他属性值。目前仅支持传入值为IOPS，表示查询当前磁盘的IOPS上限。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Disks|Array of Disk| |云盘或本地盘信息组成的集合。 |
|Disk| | | |
|AttachedTime|String|2021-06-07T06:08:56Z|该云盘最后一次挂载的时间。按照ISO8601标准表示，使用UTC+0时间。格式为：yyyy-MM-ddThh:mmZ。 |
|Attachments|Array of Attachment| |云盘所涉及的挂载信息。由`Attachment`对象组成的列表，查询共享块存储时不返回该列表。 |
|Attachment| | | |
|AttachedTime|String|2021-06-07T06:08:56Z|挂载的时间，以UTC +0时间为准。 |
|Device|String|/dev/xvda|设备名称。 |
|InstanceId|String|i-bp67acfmxazb4q\*\*\*\*|所挂载的实例ID。 |
|AutoSnapshotPolicyId|String|sp-bp67acfmxazb4p\*\*\*\*|云盘采用的自动快照策略ID。 |
|BdfId|String|null|该参数正在邀测中，暂未开放使用。 |
|Category|String|cloud\_ssd|云盘或本地盘种类。可能值：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD盘
-   cloud\_essd：ESSD云盘
-   local\_ssd\_pro：I/O密集型本地盘
-   local\_hdd\_pro：吞吐密集型本地盘
-   ephemeral：（已停售）本地盘
-   ephemeral\_ssd：（已停售）本地SSD盘 |
|CreationTime|String|2021-06-07T06:08:54Z|创建时间。 |
|DedicatedBlockStorageClusterId|String|dbsc-f8zfynww0vzuhg4w\*\*\*\*|云盘所属的专属块存储集群ID。如果您的云盘在公共云块存储集群中，此参数为空。 |
|DeleteAutoSnapshot|Boolean|false|是否同时删除自动快照。可能值：

 -   true：删除云盘上的快照。
-   false：保留云盘上的快照。

 通过[CreateSnapshot](~~25524~~)或者在控制台创建的快照，不受这个参数的影响，会始终保留。 |
|DeleteWithInstance|Boolean|true|是否随实例释放。可能值：

 -   true：释放实例时，这块云盘随实例一起释放。
-   false：释放实例时，这块云盘保留不释放。 |
|Description|String|testDescription|云盘或本地盘描述。 |
|DetachedTime|String|2021-06-07T21:01:22Z|该云盘最后一次卸载时间。 |
|Device|String|/dev/xvda|云盘或本地盘挂载的实例的设备名，例如/dev/xvdb。您需要注意：

 -   该参数仅在`Status`参数值为`In_use`时才有值，其他状态时为空。
-   对于开启多重挂载特性的云盘，该值始终为空。您可以通过返回的`Attachment`对象组成的列表，查看云盘所涉及的所有挂载信息。

 **说明：** 该参数即将停止使用，为提高代码兼容性，建议您尽量不要使用该参数。 |
|DiskChargeType|String|PrePaid|云盘或本地盘的计费方式。可能值：

 -   PrePaid：包年包月
-   PostPaid：按量付费 |
|DiskId|String|d-bp18um4r4f2fve24\*\*\*\*|云盘或本地盘ID。 |
|DiskName|String|testDiskName|云盘或本地盘名称。 |
|EnableAutoSnapshot|Boolean|false|云盘是否启用自动快照策略功能。 |
|EnableAutomatedSnapshotPolicy|Boolean|false|云盘是否设置了自动快照策略。 |
|Encrypted|Boolean|false|是否为加密云盘。 |
|ExpiredTime|String|2021-07-07T16:00Z|包年包月云盘的过期时间。 |
|IOPS|Integer|4000|每秒读写（I/O）操作的次数，单位：次/s。 |
|IOPSRead|Integer|2000|每秒读操作的次数，单位：次/s。 |
|IOPSWrite|Integer|2000|每秒写操作的次数，单位：次/s。 |
|ImageId|String|m-bp13aqm171qynt3u\*\*\*|创建ECS实例时使用的镜像ID，只有通过镜像创建的云盘才有值，否则为空。这个值在云盘的生命周期内始终不变。 |
|InstanceId|String|i-bp67acfmxazb4q\*\*\*\*|云盘或本地盘挂载的实例ID。您需要注意：

 -   该参数值仅在`Status`参数值为`In_use`时才有值，其他状态时为空。
-   对于开启多重挂载特性的云盘，该值始终为空。您可以通过返回的`Attachment`对象组成的列表，查看云盘所涉及的所有挂载信息。 |
|KMSKeyId|String|0e478b7a-4262-4802-b8cb-00d3fb408\*\*\*|云盘使用的KMS密钥ID。 |
|MountInstanceNum|Integer|1|共享存储挂载的实例数量。 |
|MountInstances|Array of MountInstance| |共享存储挂载到实例上的信息集合。 |
|MountInstance| | | |
|AttachedTime|String|2017-12-05T2340:00Z|挂载时间。按照[ISO8601](~~25696~~)标准表示，使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|Device|String|/dev/xvda|云盘或本地盘的挂载点。 |
|InstanceId|String|i-bp1j4i2jdf3owlhe\*\*\*\*|云盘或本地盘挂载的实例ID。 |
|MultiAttach|String|Disabled|云盘是否开启了多重挂载特性。 |
|OperationLocks|Array of OperationLock| |云盘或本地盘锁定原因类型。 |
|OperationLock| | | |
|LockReason|String|security|云盘或本地盘被安全锁定的原因。 |
|PerformanceLevel|String|PL0|ESSD云盘的性能等级。可能值：

 -   PL0：单盘最高随机读写IOPS 1万。
-   PL1：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。 |
|Portable|Boolean|false|云盘或本地盘是否可卸载。 |
|ProductCode|String|jxsc000204|云市场的商品标识。 |
|RegionId|String|cn-hangzhou|云盘或本地盘所属的地域ID。 |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|云盘或本地盘所在的企业资源组ID。 |
|SerialNumber|String|bp18um4r4f2fve2\*\*\*\*|云盘或本地盘的序列号。 |
|Size|Integer|60|云盘或本地盘大小，单位GiB。 |
|SourceSnapshotId|String|s-bp67acfmxazb4p\*\*\*\*|创建云盘使用的快照ID。

 如果创建云盘时，没有指定快照，则该参数值为空。该参数值在云盘的生命周期内始终不变。 |
|Status|String|In\_use|云盘状态。可能值：

 -   In\_use
-   Available
-   Attaching
-   Detaching
-   Creating
-   ReIniting |
|StorageSetId|String|ss-i-bp1j4i2jdf3owlhe\*\*\*\*|存储集ID。 |
|StorageSetPartitionNumber|Integer|11|存储集中的最大分区数量。 |
|Tags|Array of Tag| |云盘或本地盘的标签集合。 |
|Tag| | | |
|TagKey|String|TestKey|标签键。 |
|TagValue|String|TestValue|标签值。 |
|Type|String|system|云盘或本地盘类型。可能值：

 -   system：系统盘
-   data：数据盘 |
|ZoneId|String|cn-hangzhou-i|云盘或本地盘所属的可用区ID。 |
|NextToken|String|AAAAAdDWBF2\*\*\*\*|本次调用返回的查询凭证值。 |
|PageNumber|Integer|1|云盘或本地盘列表的页码。 |
|PageSize|Integer|1|输入时设置的每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|15|查询结果总条数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeDisks
&RegionId=cn-hangzhou
&PageNumber=1
&PageSize=1
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeDisksResponse>
      <TotalCount>15</TotalCount>
      <NextToken>AAAAAdDWBF2****</NextToken>
      <PageSize>1</PageSize>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PageNumber>1</PageNumber>
      <Disks>
            <Disk>
                  <DetachedTime></DetachedTime>
                  <Category>cloud_ssd</Category>
                  <Description>testDescription</Description>
                  <KMSKeyId></KMSKeyId>
                  <ResourceGroupId></ResourceGroupId>
                  <DedicatedBlockStorageClusterId></DedicatedBlockStorageClusterId>
                  <Encrypted>false</Encrypted>
                  <Size>40</Size>
                  <DeleteAutoSnapshot>false</DeleteAutoSnapshot>
                  <DiskChargeType>PrePaid</DiskChargeType>
                  <MultiAttach>Disabled</MultiAttach>
                  <Attachments>
                        <Attachment>
                              <AttachedTime>2021-06-07T06:08:56Z</AttachedTime>
                              <InstanceId>i-bp67acfmxazb4q****</InstanceId>
                              <Device>/dev/xvda</Device>
                        </Attachment>
                  </Attachments>
                  <ExpiredTime>2021-07-07T16:00Z</ExpiredTime>
                  <ImageId>m-bp13aqm171qynt3u***</ImageId>
                  <StorageSetId></StorageSetId>
                  <Tags>
            </Tags>
                  <Status>In_use</Status>
                  <AttachedTime>2021-06-07T06:08:56Z</AttachedTime>
                  <ZoneId>cn-hangzhou-i</ZoneId>
                  <InstanceId>i-bp67acfmxazb4q****</InstanceId>
                  <SourceSnapshotId></SourceSnapshotId>
                  <ProductCode></ProductCode>
                  <PerformanceLevel>PL0</PerformanceLevel>
                  <Device>/dev/xvda</Device>
                  <DeleteWithInstance>true</DeleteWithInstance>
                  <EnableAutomatedSnapshotPolicy>false</EnableAutomatedSnapshotPolicy>
                  <EnableAutoSnapshot>false</EnableAutoSnapshot>
                  <AutoSnapshotPolicyId>sp-bp67acfmxazb4p****</AutoSnapshotPolicyId>
                  <DiskName>testDiskName</DiskName>
                  <OperationLocks>
            </OperationLocks>
                  <BdfId></BdfId>
                  <Portable>false</Portable>
                  <Type>system</Type>
                  <SerialNumber>bp18um4r4f2fve2****</SerialNumber>
                  <CreationTime>2021-06-07T06:08:54Z</CreationTime>
                  <RegionId>cn-hangzhou</RegionId>
                  <DiskId>d-bp18um4r4f2fve24****</DiskId>
            </Disk>
      </Disks>
</DescribeDisksResponse>
```

`JSON`格式

```
{
	"TotalCount": 15,
	"NextToken": "AAAAAdDWBF2****",
	"PageSize": 1,
	"RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"PageNumber": 1,
	"Disks": {
		"Disk": [
			{
				"DetachedTime": "",
				"Category": "cloud_ssd",
				"Description": "testDescription",
				"KMSKeyId": "",
				"ResourceGroupId": "",
				"DedicatedBlockStorageClusterId": "",
				"Encrypted": false,
				"Size": 40,
				"DeleteAutoSnapshot": false,
				"DiskChargeType": "PrePaid",
				"MultiAttach": "Disabled",
				"Attachments": {
					"Attachment": [
						{
							"AttachedTime": "2021-06-07T06:08:56Z",
							"InstanceId": "i-bp67acfmxazb4q****",
							"Device": "/dev/xvda"
						}
					]
				},
				"ExpiredTime": "2021-07-07T16:00Z",
				"ImageId": "m-bp13aqm171qynt3u***",
				"StorageSetId": "",
				"Tags": {
					"Tag": []
				},
				"Status": "In_use",
				"AttachedTime": "2021-06-07T06:08:56Z",
				"ZoneId": "cn-hangzhou-i",
				"InstanceId": "i-bp67acfmxazb4q****",
				"SourceSnapshotId": "",
				"ProductCode": "",
				"PerformanceLevel": "PL0",
				"Device": "/dev/xvda",
				"DeleteWithInstance": true,
				"EnableAutomatedSnapshotPolicy": false,
				"EnableAutoSnapshot": false,
				"AutoSnapshotPolicyId": "sp-bp67acfmxazb4p****",
				"DiskName": "testDiskName",
				"OperationLocks": {
					"OperationLock": []
				},
				"BdfId": "",
				"Portable": false,
				"Type": "system",
				"SerialNumber": "bp18um4r4f2fve2****",
				"CreationTime": "2021-06-07T06:08:54Z",
				"RegionId": "cn-hangzhou",
				"DiskId": "d-bp18um4r4f2fve24****"
			}
		]
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidDiskType.ValueNotSupported|The specified disk type is not supported.|指定的磁盘属性不支持。|
|400|InvalidCategory.ValueNotSupported|The specified disk category is not supported.|不支持指定的磁盘种类。|
|400|InvalidStatus.ValueNotSupported|The specified disk status is not supported.|指定的磁盘状态不支持此类操作。|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|指定的Tag.N.Key和Tag.N.Value不匹配。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|400|InvalidRegion.NotFound|The specified parameter RegionId is not valid.|RegionId参数不合法。|
|400|InvalidZoneId.NotFound|The zoneId provided does not exist in our records.|指定的可用区ID不存在。|
|400|MissingParamter.RegionId|The regionId should not be null.|参数RegionId不得为空。|
|400|InvalidParameter.DiskIds|The specified parameter diskIds is not valid.|指定的参数diskIds无效。|
|400|IncompleteParamter|Some fields can not be null in this request.|请求中缺失参数。|
|400|InvalidParamter|Some parameters are invalid in this request.|请求中包含非法参数。|
|400|InvalidSnapshot.NotFound|The specified parameter SnapshotId is not valid.|指定的SnapshotId不合法。|
|403|InvalidDiskIds.Malformed|The amount of specified disk Ids exceeds the limit.|指定的磁盘ID格式不正确。|
|403|UserNotInTheWhiteList|The user is not in volume white list.|用户不在共享块存储白名单中，请您提交工单申请白名单。|
|403|InvalidParameter.MultiAttachAndEnableSharedNotMatch|The parameter MultiAttach and EnableShared are not match.|设置的MultiAttach参数和EnableShared参数的值不兼容。|
|403|InvalidParameter.MultiAttach|The specified param MultiAttach is not valid.|MultiAttach参数的取值有误。|
|404|InvalidDiskChargeType.NotFound|The DiskChargeType does not exist in our records|指定的磁盘计费方式不存在。|
|404|InvalidLockReason.NotFound|The specified LockReason is not found|指定的锁定类型不存在。|
|404|InvalidDiskIds.ValueNotSupported|The specified parameter "DiskIds" is not supported.|指定的磁盘ID无效。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

