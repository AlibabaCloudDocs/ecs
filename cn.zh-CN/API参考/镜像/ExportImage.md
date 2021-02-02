# ExportImage

调用ExportImage导出一份自定义镜像到与该自定义镜像同一地域的OSS Bucket里。

## 接口说明

-   如果您使用镜像市场的镜像创建了ECS实例并再次创建了系统盘快照时，不支持导出由该系统盘快照创建的自定义镜像。
-   支持导出镜像中包括数据盘快照的信息的自定义镜像，其中数据盘数不能超过4块，单块数据盘容量最大不能超过500GiB。
-   导出镜像前，您必须通过RAM授权云服务器ECS官方服务账号写入OSS的权限：

    1. 创建角色：`AliyunECSImageExportDefaultRole`（其他任何角色名称无效），为该角色设置以下角色策略：

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

    2. 在角色`AliyunECSImageExportDefaultRole`下加入默认的系统权限策略：`AliyunECSImageExportRolePolicy`，该策略是云服务器ECS提供导出镜像的默认策略。更多详情，请参见[云资源访问授权](https://ram.console.aliyun.com/?spm=5176.2020520101.0.0.64c64df5dfpmdY#/role/authorize?request=%7B%22Requests%22:%20%7B%22request1%22:%20%7B%22RoleName%22:%20%22AliyunECSImageImportDefaultRole%22,%20%22TemplateId%22:%20%22ECSImportRole%22%7D,%20%22request2%22:%20%7B%22RoleName%22:%20%22AliyunECSImageExportDefaultRole%22,%20%22TemplateId%22:%20%22ECSExportRole%22%7D%7D,%20%22ReturnUrl%22:%20%22https:%2F%2Fecs.console.aliyun.com%2F%22,%20%22Service%22:%20%22ECS%22%7D)。您也可以创建自定义策略，权限需要包含：

    ```
    
             {
               "Version": "1",
               "Statement": [
                 {
                   "Action": [
                     "oss:GetObject",
                     "oss:PutObject",
                     "oss:DeleteObject",
                     "oss:GetBucketLocation",
                     "oss:GetBucketInfo",
                     "oss:AbortMultipartUpload",
                     "oss:ListMultipartUploads",
                     "oss:ListParts"
                   ],
                   "Resource": "*",
                   "Effect": "Allow"
                 }
               ]
             }
            
    ```


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ExportImage&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ExportImage|系统规定参数。取值：ExportImage |
|ImageId|String|是|m-bp67acfmxazb4p\*\*\*\*|自定义镜像ID。 |
|OSSBucket|String|是|testexportImage|保存导出镜像的OSS bucket。 |
|RegionId|String|是|cn-hangzhou|自定义镜像的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|OSSPrefix|String|否|EcsExport|您的OSS Object的前缀。可以由数字或者字母组成，字符长度为1~30。 |
|ImageFormat|String|否|raw|镜像文件的导出格式。取值范围：

 -   raw
-   vhd
-   qcow2
-   vmdk
-   vdi

 默认值：raw |
|RoleName|String|否|AliyunECSImageExportDefaultRole|导出镜像时使用的RAM角色名称。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RegionId|String|cn-hangzhou|地域ID。 |
|RequestId|String|C8B26B44-0189-443E-9816-D951F59623A9|请求ID。 |
|TaskId|String|tsk-bp67acfmxazb4p\*\*\*\*|导出镜像任务ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ExportImage
&ImageId=m-bp67acfmxazb4p****
&OSSBucket=testexportImage
&RegionId=cn-hangzhou
&OSSPrefix=EcsExport
&ImageFormat=raw
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ExportImageResponse>
      <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
      <ExportTaskId>tsk-bp67acfmxazb4p****</ExportTaskId>
      <RegionId>cn-hangzhou</RegionId>
</ExportImageResponse>
```

`JSON`格式

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "ExportTaskId": "tsk-bp67acfmxazb4p****",
    "RegionId": "cn-hangzhou"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|参数RegionId不得为空。|
|400|MissingParameter|An input parameter "ImageId" that is mandatory for processing the request is not supplied.|参数ImageId不得为空。|
|400|MissingParameter|An input parameter "OSSBucket" that is mandatory for processing the request is not supplied.|参数OSSBucket不得为空。|
|400|InvalidImageName.Malformed|The specified Image name is wrongly formed.|镜像名称不合法。长度为2~128个字符，以英文字母或中文开头，可包含数字，点号（.），下划线（\_）或连字符（-）。 不能以http://和https://开头。|
|400|InvalidOSSPrefix.Malformed|The specified OSSPrefix format is wrongly formed.|参数OssPrefix格式错误。|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的地域ID不存在。|
|400|InvalidRegion.NotSupport|The specified region does not support image import or export.|指定的地域暂时不支持此操作。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像ID是否正确。|
|400|IncorrectImageStatus|The specified Image is not available.|指定的源镜像状态不正确。|
|403|ImageNotSupported|The specified image from the image market, do not support export image.|指定的镜像来自镜像市场，此镜像不能导出。|
|400|InvalidImageFormat.Malformed|The specified Image Format is wrongly formed.|指定的镜像格式错误。|
|403|ImageIsExporting|The specified Image is exporting.|正在导出指定的镜像中。|
|403|ExportImageFailed|Exporting image is failed, Please contact the administrator.|导出镜像失败，请联系系统管理员。|
|403|UserNotInTheWhiteList|The user is not in the white list of exporting image.|该用户不在导出镜像白名单中。|
|403|NoSetRoletoECSServiceAcount|ECS service account Have no right to access your OSS.please attach a role of access your oss to ECS service account.|ECS官网服务账号没有权限访问您指定的OSS的bucket和Object。|
|400|InvalidOSSBucket.NotFound|The specified OSS bucket does not exist in this region.|指定的bucket不存在。|
|400|OperationDenied|The specified image contains the snapshot of the data disk,does not support this operation.|包含了数据盘快照的镜像，不支持此操作。|
|400|InvalidImage.DiskAmountOrSize|%s|无效的镜像，导出的镜像限制数据盘数不能超过4块，单块数据盘容量最大不能超过500GiB。|
|400|ImageNotSupported|The specified Image contains encrypted snapshots, do not support export.|指定的镜像包含了加密快照，不支持导出。|
|400|ImageNotSupported|Image from image market does not support exporting.|不支持导出镜像市场里的镜像。|
|400|InvalidOSSBucket.NotMatched|The specified OSS bucket is incorrect, %s.|指定的OSSBucket有误，具体信息请参见错误信息%s占位符的实际返回结果。|
|403|ConcurrentQuotaExceed.ExportImage|%s|当前处理中的任务，已达到并发最大额度，请耐心等待一段时间再创建任务。|
|403|WeeklyQuotaExceed.ExportImage|%s|本周提交任务已经超出配额，请耐心等候再次分配可用额度。|
|403|InvalidImageLicense.NotSupported|%s|指定的镜像不支持导出。具体信息请参见错误信息%s占位符的实际返回值。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

