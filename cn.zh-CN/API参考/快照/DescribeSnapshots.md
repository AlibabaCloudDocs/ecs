# DescribeSnapshots

调用DescribeSnapshots查询一台ECS实例或一块云盘所有的快照列表。

## 接口说明

`InstanceId`、`DiskId`和`SnapshotIds`不是必需的请求参数，但是可以构建过滤器逻辑，参数之间为逻辑与（And）关系。

通过阿里云CLI调用API时，不同数据类型的请求参数取值必须遵循一定的格式要求，详情请参见[CLI参数格式说明](~~110340~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshots&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSnapshots|系统规定参数。取值：**DescribeSnapshots**。 |
|InstanceId|String|否|i-bp67acfmxazb4p\*\*\*\*|指定的实例ID。 |
|DiskId|String|否|d-bp67acfmxazb4p\*\*\*\*|指定的云盘设备ID。 |
|SnapshotLinkId|String|否|sp-bp67acfmxazb4p\*\*\*\*|快照链ID。 |
|RegionId|String|是|cn-hangzhou|云盘所属于的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|SnapshotIds|String|否|\["s-bp67acfmxazb4p\*\*\*\*", "s-bp67acfmxazb5p\*\*\*\*", … "s-bp67acfmxazb6p\*\*\*\*"\]|快照标识编码。取值可以由多个快照ID组成一个JSON数组，最多支持100个ID，ID之间用半角逗号（,）隔开。 |
|PageNumber|Integer|否|1|快照列表的页码。起始值：1

 默认值：1 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：100

 默认值：10 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0a4883|查询起始标志。由上一次的请求结果中获取。 |
|MaxResults|Integer|否|10|分页查询时每页行数。最大值：100

 默认值：10 |
|SnapshotName|String|否|testSnapshotName|快照名称。 |
|Status|String|否|all|快照状态。取值范围：

 -   progressing：正在创建的快照。
-   accomplished：创建成功的快照。
-   failed：创建失败的快照。
-   all（默认）：所有快照状态。 |
|SnapshotType|String|否|all|快照创建类型。取值范围：

 -   auto：自动创建快照。
-   user：手动创建快照。
-   all（默认）：所有的快照创建类型。 |
|Filter.1.Key|String|否|CreationStartTime|查询资源时的筛选键，取值必须为`CreationStartTime`。同时设置`Filter.1.Key`和`Filter.1.Value`可以查询在指定时间点后创建的资源信息。 |
|Filter.2.Key|String|否|CreationEndTime|查询资源时的筛选键，取值必须为`CreationEndTime`。同时设置`Filter.2.Key`和`Filter.2.Value`可以查询在指定时间点前创建的资源信息。 |
|Filter.1.Value|String|否|2019-12-13T17:00Z|查询资源时的筛选值。指定该参数时必须同时指定`Filter.1.Key`参数，格式为：`yyyy-MM-ddTHH:mmZ`，采用UTC +0时区。 |
|Filter.2.Value|String|否|2019-12-13T22:00Z|查询资源时的筛选值。指定该参数时必须同时指定`Filter.2.Key`参数，格式为：`yyyy-MM-ddTHH:mmZ`，采用UTC +0时区。 |
|Usage|String|否|none|快照是否被用作创建镜像或云盘。取值范围：

 -   image：使用快照创建了自定义镜像。
-   disk：使用快照创建了云盘。
-   image\_disk：使用快照创建了数据盘和自定义镜像。
-   none：暂未使用。 |
|SourceDiskType|String|否|Data|快照源云盘的云盘类型。取值范围：

 -   System：系统盘
-   Data：数据盘

 **说明：** 取值不区分大小写。 |
|Encrypted|Boolean|否|false|是否过滤加密快照。默认值：false |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|资源组ID。使用该参数过滤资源时，资源数量不能超过1000个。 |
|DryRun|Boolean|否|false|是否只预检此次请求。

 -   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码DryRunOperation。
-   false（默认）：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。 |
|KMSKeyId|String|否|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|数据盘对应的KMS密钥ID。 |
|Category|String|否|Standard|快照类型。取值范围：

 -   Standard：普通快照
-   Flash：本地快照

 原本地快照更替为快照极速可用功能。该参数说明如下：

 -   如果您在2020年12月14日之前使用过本地快照。您可以正常使用该参数。
-   如果您在2020年12月14日之前未使用过本地快照。您不能使用该参数。

 更多信息，请参见[12月14日阿里云快照服务升级与新增计费项通知](https://help.aliyun.com/noticelist/articleid/1060755542.html)。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用其他参数。 |
|Tag.N.Key|String|否|TestKey|快照的标签键。N的取值范围：1~20

 使用一个标签过滤资源，查询到该标签下的资源数量不能超过1000个；使用多个标签过滤资源，查询到同时绑定了多个标签的资源数量不能超过1000个。如果资源数量超过1000个，请使用[ListTagResources](~~110425~~)接口进行查询。 |
|Tag.N.Value|String|否|TestValue|快照的标签值。N的取值范围：1~20 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|下一个查询起始标志。 |
|PageSize|Integer|10|输入时设置的每页行数。 |
|PageNumber|Integer|1|快照列表的页码。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|1|快照总个数。 |
|Snapshots|Array of Snapshot| |快照详情集合。 |
|Snapshot| | | |
|Status|String|accomplished|快照状态。可能值：

 -   progressing
-   accomplished
-   failed |
|CreationTime|String|2020-08-20T14:52:28Z|创建时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|Progress|String|100%|快照创建进度，单位为百分比。 |
|InstantAccess|Boolean|false|是否开启了快照极速可用功能。可能值：

 -   true：开启。仅ESSD云盘支持开启该功能。
-   false：关闭。即快照为未开启快照极速可用功能的普通快照。 |
|RemainTime|Integer|38|正在创建的快照剩余完成时间，单位为秒。 |
|SourceDiskSize|String|40|源云盘容量，单位：GiB。 |
|RetentionDays|Integer|30|自动快照保留天数。 |
|SourceDiskType|String|system|源云盘属性。可能值：

 -   system
-   data |
|SourceStorageType|String|disk|原云盘类型。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用其他参数。 |
|Usage|String|image|快照是否被用作创建镜像或云盘。可能值：

 -   image
-   disk
-   image\_disk
-   none |
|LastModifiedTime|String|2020-08-25T14:18:09Z|快照的最后变更时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|Encrypted|Boolean|false|该快照是否加密。 |
|SnapshotType|String|all|快照创建类型。可能值：

 -   auto或者timer：自动创建快照。
-   user：手动创建快照。
-   all：所有的快照创建类型。 |
|SourceDiskId|String|d-bp67acfmxazb4ph\*\*\*\*|源云盘ID。如果快照的源云盘已经被释放，该字段仍旧保留。 |
|SnapshotName|String|testSnapshotName|快照显示名称。如果创建时指定了快照显示名称，则返回。 |
|InstantAccessRetentionDays|Integer|30|设置快照极速可用功能的保留时间，保留时间到期后自动关闭快照极速可用功能。

 默认与参数`RetentionDays`的值一致。 |
|Description|String|testDescription|描述信息。 |
|SnapshotId|String|s-bp67acfmxazb4p\*\*\*\*|快照ID。 |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|资源组ID。 |
|Category|String|standard|快照类型。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用参数`InstantAccess`。 |
|KMSKeyId|String|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|数据盘对应的KMS密钥ID。 |
|SnapshotSN|String|64472-116742336-61976\*\*\*\*|快照序列号。 |
|ProductCode|String|jxsc000\*\*\*\*|从镜像市场继承的产品编号。 |
|Tags|Array of Tag| |标签。 |
|Tag| | | |
|TagValue|String|TestValue|快照的标签值。 |
|TagKey|String|TestKey|快照的标签键。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeSnapshots
&RegionId=cn-hangzhou
&InstanceId=i-bp67acfmxazb4p****
&DiskId=d-bp67acfmxazb4p****
&SnapshotIds=["s-bp67acfmxazb4p****", "s-bp67acfmxazb5p****", … "s-bp67acfmxazb6p****"]
&PageNumber=1
&PageSize=10
&SnapshotName=testSnapshotName
&Status=all
&SnapshotType=all
&Usage=none
&SourceDiskType=Data
&Tag.1.Key=TestKey
&Tag.1.Value=TestValue
&Encrypted=false
&DryRun=false
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeSnapshotsResponse>
    <TotalCount>1</TotalCount>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
    <PageSize>10</PageSize>
    <NextToken>caeba0bbb2be03f84eb48b699f0a4883</NextToken>
    <PageNumber>1</PageNumber>
    <Snapshots>
        <Snapshot>
            <Status>accomplished</Status>
            <InstantAccess>false</InstantAccess>
            <Progress>100%</Progress>
            <Usage>image</Usage>
            <Description>testDescription</Description>
            <Category>standard</Category>
            <KMSKeyId>0e478b7a-4262-4802-b8cb-00d3fb40****</KMSKeyId>
            <ProductCode>jxsc000****</ProductCode>
            <Encrypted>false</Encrypted>
            <SnapshotName>testSnapshotName</SnapshotName>
            <SourceDiskId>d-bp67acfmxazb4ph****</SourceDiskId>
            <SourceStorageType>disk</SourceStorageType>
            <SnapshotId>s-bp67acfmxazb4p****</SnapshotId>
            <SnapshotSN>64472-116742336-61976****</SnapshotSN>
            <SourceDiskSize>40</SourceDiskSize>
            <CreationTime>2020-08-20T14:52:28Z</CreationTime>
            <LastModifiedTime>2020-08-25T14:18:09Z</LastModifiedTime>
            <SnapshotType>all</SnapshotType>
            <SourceDiskType>system</SourceDiskType>
            <Tags>
            </Tags>
        </Snapshot>
    </Snapshots>
</DescribeSnapshotsResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "TotalCount" : 1,
  "RequestId" : "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
  "PageSize" : 10,
  "NextToken" : "caeba0bbb2be03f84eb48b699f0a4883",
  "PageNumber" : 1,
  "Snapshots" : {
    "Snapshot" : [ {
      "Status" : "accomplished",
      "InstantAccess" : false,
      "Progress" : "100%",
      "Usage" : "image",
      "Description" : "testDescription",
      "Category" : "standard",
      "KMSKeyId" : "0e478b7a-4262-4802-b8cb-00d3fb40****",
      "ProductCode" : "jxsc000****",
      "Encrypted" : false,
      "SnapshotName" : "testSnapshotName",
      "SourceDiskId" : "d-bp67acfmxazb4ph****",
      "SourceStorageType" : "disk",
      "SnapshotId" : "s-bp67acfmxazb4p****",
      "SnapshotSN" : "64472-116742336-61976****",
      "SourceDiskSize" : 40,
      "CreationTime" : "2020-08-20T14:52:28Z",
      "LastModifiedTime" : "2020-08-25T14:18:09Z",
      "SnapshotType" : "all",
      "SourceDiskType" : "system",
      "Tags" : {
        "Tag" : [ ]
      }
    } ]
  }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|指定的Tag.N.Key和Tag.N.Value不匹配。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InvalidSnapshotIds.Malformed|The amount of specified specified snapshot Ids exceeds the limit.|快照ID参数格式不正确。|
|403|InvalidSnapshotIds.Malformed|The amount of specified specified snapshot Ids exceeds the limit.|快照ID参数格式不正确。|
|403|InvalidSnapshotCategory.Malformed|The specified Category is not valid.|指定的快照类型无效。请检查Category参数值是否正确。|
|404|InvalidFilterKey.NotFound| |指定的起始时间或到期时间参数错误。|
|404|InvalidUsage|The specifed Usage is not valid|指定有引用关系的资源类型（image、disk、image\_disk、none）不合法。|
|404|InvalidSourceDiskType|The specifed SourceDiskType is not valid|指定的快照源磁盘的磁盘类型不合法。|
|404|InvalidStatus.NotFound|The specified Status is not found|指定的资源状态不存在。|
|404|InvalidSnapshotType.NotFound|The specfied SnapshotType is not found|指定的快照类型不存在。|
|404|InvalidSnapshotLinkId.NotFound|The specified snapshot link is not found.|指定的快照链不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

