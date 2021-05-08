# ImportImage

调用ImportImage导入一份您的本地镜像文件到云服务器ECS，作为自定义镜像出现在相应地域中。您可以使用导入的镜像创建ECS实例（RunInstances），或者更换实例的系统盘（ReplaceSystemDisk）。

## 接口说明

调用该接口时，您需要注意：

-   您必须提前上传镜像文件到对象存储OSS。具体步骤请参见[上传文件](~~31886~~)。
-   首次导入镜像时，您必须提前通过访问控制RAM授权ECS访问您的OSS Bucket，否则会报错`NoSetRoletoECSServiceAcount`，具体步骤请参见[账号访问控制](~~25481~~)，其中部分步骤策略如下所示。

    1. 创建角色`AliyunECSImageImportDefaultRole`（必须是这个名称，否则导入镜像会失败），角色的策略为：

    ```
    
            {
    			"Statement": [
    			{
    				"Action": "sts:AssumeRole",
    				"Effect": "Allow",
    				"Principal": {
    				"Service": [
    					"ecs.aliyuncs.com"
    				]
    				}
    			}
            ],
    			"Version": "1"
            }
            
    ```

    2. 在该角色下，添加系统策略`AliyunECSImageImportRolePolicy`，更多详情，请参见[云资源访问授权](https://ram.console.aliyun.com/?spm=5176.2020520101.0.0.64c64df5dfpmdY#/role/authorize?request=%7B%22Requests%22:%20%7B%22request1%22:%20%7B%22RoleName%22:%20%22AliyunECSImageImportDefaultRole%22,%20%22TemplateId%22:%20%22ECSImportRole%22%7D,%20%22request2%22:%20%7B%22RoleName%22:%20%22AliyunECSImageExportDefaultRole%22,%20%22TemplateId%22:%20%22ECSExportRole%22%7D%7D,%20%22ReturnUrl%22:%20%22https:%2F%2Fecs.console.aliyun.com%2F%22,%20%22Service%22:%20%22ECS%22%7D)。或者您也可以创建自定义策略，权限必须包含：

    ```
    
            {
    			"Version": "1",
    			"Statement": [
    			{
    				"Action": [
            				"oss:GetObject",
            				"oss:GetBucketLocation",
            				"oss:GetBucketInfo"
    			],
            			"Resource": "*",
            			"Effect": "Allow"
            			}
    			]
            }
            
    ```

-   不能删除正在导入的镜像，只能取消导入镜像任务（[CancelTask](~~25624~~)）。
-   导入镜像的地域必须跟镜像文件上传的OSS Bucket的地域相同。
-   参数`DiskDeviceMapping.N`中N的取值范围为1~17。N为1时表示系统盘，N为2~17时表示数据盘。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ImportImage&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ImportImage|系统规定参数。取值：**ImportImage**。 |
|RegionId|String|是|cn-hangzhou|镜像上传至OSS Bucket后，Bucket所属的地域ID。

 您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ImageName|String|否|ImageTestName|镜像名称。长度为2~128个字符。必须以大小字母或中文开头，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。可以包含数字、半角句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。

 默认值：空。 |
|Description|String|否|TestDescription|镜像的描述信息。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。

 默认值：空。 |
|Architecture|String|否|x86\_64|系统架构。取值范围：

 -   i386
-   x86\_64

 默认值：x86\_64 |
|OSType|String|否|linux|操作系统平台类型。取值范围：

 -   windows
-   linux

 默认值：linux |
|Platform|String|否|Aliyun|操作系统发行版。取值范围：

 -   CentOS
-   Ubuntu
-   SUSE
-   OpenSUSE
-   Debian
-   CoreOS
-   Aliyun
-   Windows Server 2003
-   Windows Server 2008
-   Windows Server 2012
-   Others Linux
-   Customized Linux

 默认值：Others Linux |
|BootMode|String|否|BIOS|修改镜像的启动模式。取值范围：

 -   BIOS：BIOS启动模式。
-   UEFI：UEFI启动模式。

 默认值：BIOS

 **说明：** 您需要了解指定的镜像支持的启动模式，当通过该参数修改启动模式后，必须与镜像本身支持的启动模式匹配，实例才能正常启动。 |
|RoleName|String|否|AliyunECSImageImportDefaultRole|导入镜像时，使用的RAM角色名称。 |
|LicenseType|String|否|Auto|导入镜像后，激活操作系统采用的许可证类型。取值范围：

 -   Auto（默认）：由阿里云检测源操作系统并分配许可证。自动模式下，系统优先搜索您设置的`Platform`是否有阿里云官方渠道的许可证并分配给导入的镜像，如果缺乏该类许可，会切换成BYOL（Bring Your Own License）方式。
-   Aliyun：根据您设置的`Platform`采用阿里云官方渠道的许可证。
-   BYOL：源操作系统自带的许可证。采用BYOL时，您必须确保您的许可证密钥支持在阿里云使用。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|导入镜像所在的企业资源组ID。 |
|DiskDeviceMapping.N.DiskImSize|Integer|否|80|导入镜像后，自定义镜像的空间大小。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用`DiskDeviceMapping.N.DiskImageSize`参数。 |
|DiskDeviceMapping.N.Device|String|否|null|指定DiskDeviceMapping.N.Device在自定义镜像中的设备名。

 **说明：** 该参数即将停止使用，为提高代码兼容性，建议您尽量不要使用该参数。 |
|DiskDeviceMapping.N.OSSBucket|String|否|ecsimageos|镜像文件所在的OSS Bucket。

 **说明：** 首次导入镜像到该OSS Bucket前，请参见接口说明章节添加RAM授权策略，否则会报错`NoSetRoletoECSServiceAcount`。 |
|DiskDeviceMapping.N.Format|String|否|QCOW2|镜像格式。取值范围：

 -   RAW
-   VHD
-   QCOW2

 默认值：无，表示阿里云自动检测镜像格式，以检测格式为准。 |
|DiskDeviceMapping.N.OSSObject|String|否|CentOS\_5.4\_32.raw|镜像上传至OSS Bucket后，保存在Bucket中的镜像文件的文件名（key）。 |
|DiskDeviceMapping.N.DiskImageSize|Integer|否|80|导入镜像后，自定义镜像的空间大小。

 该空间由系统盘和数据盘组成，当N=1时，表示系统盘，当N=2~17时，表示数据盘。您必须保证系统盘的空间大小大于等于导入的镜像文件大小。取值范围：

 -   N = 1时，取值范围：5 GiB~500 GiB
-   N = 2~17时，取值范围：5 GiB~1000 GiB

 当您将源镜像文件上传至OSS后，可以在OSS Bucket中查看镜像文件的大小。 |
|Tag.N.Key|String|否|TestKey|镜像的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |
|Tag.N.Value|String|否|TestValue|镜像的标签值。N的取值范围：1~20。一旦传入该值，允许为空字符串。最多支持128个字符，不能以`acs:`开头，不能包含`http://`或者`https://`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|ImageId|String|m-bp67acfmxazb4p\*\*\*\*|镜像ID。 |
|TaskId|String|t-bp67acfmxazb4p\*\*\*\*|导入镜像任务ID。 |
|RegionId|String|cn-hangzhou|地域ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ImportImage
&RegionId=cn-hangzhou
&DiskDeviceMapping.1.Format=QCOW2
&DiskDeviceMapping.1.OSSBucket=ecsimageos
&DiskDeviceMapping.1.OSSObject=CentOS_5.4_32.raw
&DiskDeviceMapping.1.DiskImageSize=80
&ImageName=Test
&Description=Test
&Architecture=x86_64
&OSType=linux
&Platform=Aliyun
&LicenseType=Aliyun
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ImportImageResponse>
    <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
    <ImageId>m-bp67acfmxazb4p****</ImageId>
    <RegionId>cn-hangzhou</RegionId>
    <ImportTaskId>t-bp67acfmxazb4p****</ImportTaskId>
</ImportImageResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "C8B26B44-0189-443E-9816-D951F59623A9",
  "ImageId" : "m-bp67acfmxazb4p****",
  "RegionId" : "cn-hangzhou",
  "ImportTaskId" : "t-bp67acfmxazb4p****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|参数RegionId不得为空。|
|400|MissingParameter|An input parameter "DiskDeviceMapping.1.OSSBucket" that is mandatory for processing the request is not supplied.|导入镜像的OSS的bucket不得为空。|
|400|MissingParameter|An input parameter "DiskDeviceMapping.1.OSSObject" that is mandatory for processing the request is not supplied.|导入镜像的OSS的bucket不得为空。|
|400|InvalidImageName.Malformed|The specified Image name is wrongly formed.|镜像名称格式错误。长度为2~128个字符。必须以大小字母或中文开头，不能以aliyun和acs:开头，不能包含http://或者https://。可以包含数字、半角句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。|
|400|InvalidOSSObject.Malformed|The specified OSS object is wrongly formed.|指定的OSS Object不合法。|
|400|InvalidDescription.Malformed|The specified Image description is wrongly formed.|镜像描述格式错误。|
|400|InvalidArchitecture.Malformed|The specified Architecture is wrongly formed.|参数Architecture格式错误。|
|400|InvalidPlatform.Malformed|The specified Platform is wrongly formed.|指定的镜像操作系统发行版不合法。|
|400|InvalidOSType.Malformed|The specified OSType is wrongly formed.|格式不对。|
|400|InvalidImageName.Duplicated|The destination image is exist.|指定的镜像名已存在。|
|400|InvalidImageSize|%s|镜像大小不符合要求。|
|400|InvalidDataDiskSize|The specified DiskDeviceMapping.N.DiskImSize should be in the specified range.|指定的DiskDeviceMapping.N.DiskImSize超出取值范围。|
|400|InvalidImageFormat.Malformed|The specified Image Format is wrongly formed.|指定的镜像格式错误。|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的地域ID不存在。|
|400|InvalidRegion.NotSupport|The specified region does not support image import or export.|指定的地域暂时不支持此操作。|
|400|InvalidOSSBucket.NotFound|The specified OSS bucket does not exist in this region.|指定的bucket不存在。|
|400|InvalidOSSObject.NotFound|The specified OSS object does not exist in this region.|指定的object不存在。|
|400|InvalidOSSObject.NotFound|The specified OSS object cannot be retrieved.|指定的OSS对象无法检索。|
|400|InvalidRegion.NotSupport|The specified region does not support image import or export.|指定的地域暂时不支持此操作。|
|400|InvalidOSSBucket.NotMatched|The specified OSS bucket is incorrect, %s.|指定的OSSBucket有误，具体信息请参见错误信息%s占位符的实际返回结果。|
|400|InvalidLicenseType.NotSupported|The specified LicenseType is not supported|指定的许可证类型不支持。|
|400|InvalidLicenseType.BYOLOnly|Only BYOL LicenseType is supported for the current platform provided|当前提供的平台仅支持BYOL类型的许可证。|
|403|ImageIsImporting|The specified Image is importing.|指定镜像正在导入，无法执行操作。|
|403|QuotaExceed.Image|The Image Quota exceeds.|自定义镜像额度已用完。|
|403|ImportImageFailed|Importing image is failed, Please contact the administrator.|导入镜像失败，请联系系统管理员排查。|
|403|UserNotInTheWhiteList|The user is not in the white list of importing image.|用户未被授权导入镜像。|
|403|NoSetRoletoECSServiceAcount|ECS service account Have no right to access your OSS.please attach a role of access your oss to ECS service account.|ECS官网服务账号没有权限访问您指定的OSS的bucket和Object。|
|403|InvalidParameter.Malformed|The specified parameter "DiskDeviceMapping.n.Device " is not valid.|指定的参数DiskDeviceMapping.n.Device无效。|
|403|MissingParameter.DiskDeviceMapping|The specified parameter DiskDeviceMapping is not supplied.|参数DiskDeviceMapping不能为空。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

