# DescribeImageFromFamily

调用DescribeImageFromFamily查询指定镜像族系内最新创建的可用自定义镜像。

## 接口说明

-   该接口只查询当前镜像族系内最新创建的可用自定义镜像，不包括公共镜像、云市场镜像、共享镜像。
-   指定查询的镜像族系如果不存在可用的自定义镜像，则返回结果为空。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeImageFromFamily&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeImageFromFamily|系统规定参数。取值：DescribeImageFromFamily |
|ImageFamily|String|是|hangzhou-daily-update|镜像族系名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://、https://、acs:和aliyun开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|RegionId|String|是|cn-hangzhou|镜像所在的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Image|Struct| |返回的镜像信息。 |
|Architecture|String|x86\_64|镜像系统架构类型。可能值：

 -   i386
-   x86\_64 |
|CreationTime|String|2018-01-10T01:01:10Z|镜像的创建时间。 |
|Description|String|testDescription|描述信息。 |
|DiskDeviceMappings|Array of DiskDeviceMapping| |镜像下包含云盘和快照的映射关系。 |
|DiskDeviceMapping| | | |
|Device|String|/dev/xvdb|云盘的设备信息，例如/dev/xvdb。

 **说明：** 该参数即将停止使用，为提高代码的兼容性，建议您尽量不要使用该参数。 |
|Format|String|qcow2|镜像格式。 |
|ImportOSSBucket|String|testEcsImport|导入镜像所属OSS的Bucket。 |
|ImportOSSObject|String|imageImport|导入镜像所属OSS的Object。 |
|Size|String|80|云盘大小，单位GiB。 |
|SnapshotId|String|s-bp17ot2q7x72ggtw\*\*\*\*|快照ID。 |
|Type|String|custom|镜像的类型。 |
|ImageFamily|String|testImageFamily|镜像族系。 |
|ImageId|String|m-bp1g7004ksh0oeuc\*\*\*\*|镜像ID。 |
|ImageName|String|testImageName|镜像的名称。 |
|ImageOwnerAlias|String|self|镜像所有者别名。可能值：

 -   system：公共镜像。
-   self：您的自定义镜像。
-   others：其他用户的公开镜像。
-   marketplace：云市场镜像。 |
|ImageVersion|String|2|镜像版本。 |
|IsCopied|Boolean|false|是否是复制的镜像。 |
|IsSelfShared|String|true|是否共享过该自定义镜像给其他用户。 |
|IsSubscribed|Boolean|false|是否订阅了该镜像商品码对应的镜像商品服务条款。 |
|IsSupportCloudinit|Boolean|true|是否支持cloud-init。 |
|IsSupportIoOptimized|Boolean|true|是否可以在I/O优化实例上运行。 |
|OSName|String|Alibaba Cloud Linux 2.1903|操作系统的中文显示名称。 |
|OSType|String|linux|操作系统类型。可能值：

 -   windows
-   linux |
|Platform|String|Aliyun|操作系统平台。 |
|ProductCode|String|jxsc00\*\*\*\*|镜像市场的镜像商品标示。 |
|Progress|String|100|镜像完成的进度，单位为百分比。 |
|Size|Integer|80|镜像大小，单位GiB。 |
|Status|String|Available|镜像的状态。可能值：

 -   UnAvailable：不可用
-   Available：可用
-   Creating：创建中
-   CreateFailed：创建失败 |
|Tags|Array of Tag| |镜像的标签对信息。 |
|Tag| | | |
|TagKey|String|TestKey|自定义镜像的标签键。 |
|TagValue|String|TestValue|自定义镜像的标签值。 |
|Usage|String|none|有引用关系的资源类型。可能值：

 -   instance：创建了一台或多台ECS实例。
-   none：未创建过ECS实例。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeImageFromFamily
&RegionId=cn-hangzhou
&ImageFamily=as-hangzhou-game-01
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeImageFromFamilyResponse>
      <RequestId>E39053A7-C3E6-41FA-8F8D-F5BD8063E61C</RequestId>
      <Image>
            <ImageOwnerAlias>self</ImageOwnerAlias>
            <Status>Available</Status>
            <Progress></Progress>
            <Usage></Usage>
            <Description>testDescription</Description>
            <IsSelfShared></IsSelfShared>
            <Architecture>x86_64</Architecture>
            <Platform>CentOS</Platform>
            <ProductCode></ProductCode>
            <Size>40</Size>
            <IsSubscribed>false</IsSubscribed>
            <IsCopied>false</IsCopied>
            <ImageFamily>testImageFamily</ImageFamily>
            <OSName>CentOS 8.0 64位</OSName>
            <IsSupportIoOptimized>true</IsSupportIoOptimized>
            <IsSupportCloudinit>true</IsSupportCloudinit>
            <ImageName>testImageName</ImageName>
            <DiskDeviceMappings>
                  <DiskDeviceMapping>
                        <SnapshotId>s-bp1ejhb4r1lyu55t****</SnapshotId>
                        <Type>system</Type>
                        <Format></Format>
                        <Size>40</Size>
                        <Device>/dev/xvda</Device>
                        <ImportOSSBucket></ImportOSSBucket>
                        <ImportOSSObject></ImportOSSObject>
                  </DiskDeviceMapping>
            </DiskDeviceMappings>
            <ImageVersion></ImageVersion>
            <OSType>linux</OSType>
            <ImageId>m-bp1ejhb4r1lyu55t****</ImageId>
            <CreationTime>2020-03-17T06:19:19Z</CreationTime>
            <Tags>
        </Tags>
      </Image>
</DescribeImageFromFamilyResponse>
```

`JSON` 格式

```
{
	"RequestId": "E39053A7-C3E6-41FA-8F8D-F5BD8063E61C",
	"Image": {
		"ImageOwnerAlias": "self",
		"Status": "Available",
		"Progress": "",
		"Usage": "",
		"Description": "testDescription",
		"IsSelfShared": "",
		"Architecture": "x86_64",
		"Platform": "CentOS",
		"ProductCode": "",
		"Size": 40,
		"IsSubscribed": false,
		"IsCopied": false,
		"ImageFamily": "testImageFamily",
		"OSName": "CentOS 8.0 64位",
		"IsSupportIoOptimized": true,
		"IsSupportCloudinit": true,
		"ImageName": "testImageName",
		"DiskDeviceMappings": {
			"DiskDeviceMapping": [
				{
					"SnapshotId": "s-bp1ejhb4r1lyu55t****",
					"Type": "system",
					"Format": "",
					"Size": "40",
					"Device": "/dev/xvda",
					"ImportOSSBucket": "",
					"ImportOSSObject": ""
				}
			]
		},
		"ImageVersion": "",
		"OSType": "linux",
		"ImageId": "m-bp1ejhb4r1lyu55t****",
		"CreationTime": "2020-03-17T06:19:19Z",
		"Tags": {
			"Tag": []
		}
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidRegionId.NotFound|The RegionId provided does not exist.|指定的地域不存在，请确认该参数是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

