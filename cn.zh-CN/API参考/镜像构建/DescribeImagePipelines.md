# DescribeImagePipelines

调用DescribeImagePipelines查询一个或多个镜像模板的详细信息。

## 接口说明

您可以设置`NextToken`查询凭证（Token），其取值是上一次调用`DescribeImagePipelines`返回的`NextToken`参数值，再通过`MaxResults`设置单页查询的最大条目数进行查询。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeImagePipelines&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeImagePipelines|系统规定参数。取值：DescribeImagePipelines |
|RegionId|String|是|cn-hangzhou|所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Tag.N.Key|String|否|TestKey|标签键。N的取值范围：1~20 |
|Tag.N.Value|String|否|TestValue|标签值。N的取值范围：1~20 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|企业资源组ID。 |
|Name|String|否|testImagePipeline|模板名称。 |
|ImagePipelineId.N|RepeatList|否|ip-2ze5tsl5bp6nf2b3\*\*\*\*|镜像模板ID。N取值范围：1~20 |
|NextToken|String|否|AAAAAdDWBF2\*\*\*\*|查询凭证（Token）。取值为上一次调用该接口返回的`NextToken`参数值，初次调用接口时无需设置该参数。 |
|MaxResults|Integer|否|50|分页查询时每页行数。取值范围：1~500

 默认值：50。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ImagePipeline|Array of ImagePipelineSet| |镜像模板的详细信息组成的列表。 |
|ImagePipelineSet| | | |
|AddAccounts|List|\["1234567890"\]|目标镜像共享的阿里云账号ID。 |
|BaseImage|String|m-bp67acfmxazb4p\*\*\*\*|源镜像。

 -   当`BaseImageType=IMAGE`时，该参数值为自定义镜像ID。
-   当`BaseImageType=IMAGE_FAMILY`时，该参数值为镜像族系名称。 |
|BaseImageType|String|IMAGE|源镜像类型。可能值：

 -   IMAGE：自定义镜像。
-   IMAGE\_FAMILY：镜像族系。 |
|BuildContent|String|FROM IMAGE:m-bp67acfmxazb4p\*\*\*\*|镜像模板内容。 |
|CreationTime|String|2020-11-24T06:00:00Z|模板创建时间。 |
|DeleteInstanceOnFailure|Boolean|true|镜像构建失败后是否释放中转实例。 |
|Description|String|This is description.|描述信息。 |
|ImageName|String|testImageName|目标镜像名称前缀。 |
|ImagePipelineId|String|ip-2ze5tsl5bp6nf2b3\*\*\*\*|镜像模板ID。 |
|InstanceType|String|ecs.g6.large|实例规格。 |
|InternetMaxBandwidthOut|Integer|0|中转实例的公网出带宽大小。单位：Mbit/s |
|Name|String|testImagePipeline|模板名称。 |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|企业资源组ID。 |
|SystemDiskSize|Integer|40|中转实例的系统盘大小。单位：GiB |
|Tags|Array of Tag| |标签键值对列表。 |
|Tag| | | |
|TagKey|String|TestKey|标签键。 |
|TagValue|String|TestValue|标签值。 |
|ToRegionIds|List|\["cn-hangzhou"\]|目标镜像待分发的地域列表。 |
|VSwitchId|String|vsw-bp67acfmxazb4p\*\*\*\*|VPC的交换机ID。 |
|MaxResults|Integer|50|分页查询时每页行数。 |
|NextToken|String|AAAAAdDWBF2\*\*\*\*|本次调用返回的查询凭证（Token）。具体使用方式请参见接口说明。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|1|返回的镜像模板数量。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeImagePipelines
&RegionId=cn-hangzhou
&ImagePipelineId.1=ip-2ze5tsl5bp6nf2b3****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateDiskResponse>
      <TotalCount>1</TotalCount>
      <NextToken>AAAAAdDWBF2****</NextToken>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <MaxResults>50</MaxResults>
      <ImagePipeline>
            <ImagePipelineSet>
                  <BaseImageType>IMAGE</BaseImageType>
                  <Description>This is description.</Description>
                  <ResourceGroupId>rg-bp67acfmxazb4p****</ResourceGroupId>
                  <SystemDiskSize>40</SystemDiskSize>
                  <ImagePipelineId>ip-2ze5tsl5bp6nf2b3****</ImagePipelineId>
                  <VSwitchId>vsw-bp67acfmxazb4p****</VSwitchId>
                  <Name>testImagePipeline</Name>
                  <DeleteInstanceOnFailure>true</DeleteInstanceOnFailure>
                  <ImageName>testImageName</ImageName>
                  <InternetMaxBandwidthOut>0</InternetMaxBandwidthOut>
                  <CreationTime>2020-11-24T06:00:00Z</CreationTime>
                  <InstanceType>ecs.g6.large</InstanceType>
                  <BuildContent>FROM IMAGE:m-bp67acfmxazb4p****</BuildContent>
                  <BaseImage>m-bp67acfmxazb4p****</BaseImage>
            </ImagePipelineSet>
            <ImagePipelineSet>
                  <Tags>
                        <Tag>
                              <TagKey>TestKey</TagKey>
                              <TagValue>TestValue</TagValue>
                        </Tag>
                  </Tags>
            </ImagePipelineSet>
            <ImagePipelineSet>
                  <AddAccounts>
                        <AddAccount>["1234567890"]</AddAccount>
                  </AddAccounts>
                  <ToRegionIds>
                        <ToRegionId>["cn-hangzhou"]</ToRegionId>
                  </ToRegionIds>
            </ImagePipelineSet>
      </ImagePipeline>
</CreateDiskResponse>
```

`JSON`格式

```
{
    "TotalCount": "1", 
    "NextToken": "AAAAAdDWBF2****", 
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E", 
    "MaxResults": "50", 
    "ImagePipeline": {
        "ImagePipelineSet": [
            {
                "BaseImageType": "IMAGE", 
                "Description": "This is description.", 
                "ResourceGroupId": "rg-bp67acfmxazb4p****", 
                "SystemDiskSize": "40", 
                "ImagePipelineId": "ip-2ze5tsl5bp6nf2b3****", 
                "VSwitchId": "vsw-bp67acfmxazb4p****", 
                "Name": "testImagePipeline", 
                "DeleteInstanceOnFailure": "true", 
                "ImageName": "testImageName", 
                "InternetMaxBandwidthOut": "0", 
                "CreationTime": "2020-11-24T06:00:00Z", 
                "InstanceType": "ecs.g6.large", 
                "BuildContent": "FROM IMAGE:m-bp67acfmxazb4p****", 
                "BaseImage": "m-bp67acfmxazb4p****"
            }, 
            {
                "Tags": {
                    "Tag": [
                        {
                            "TagKey": "TestKey", 
                            "TagValue": "TestValue"
                        }
                    ]
                }
            }, 
            {
                "AddAccounts": {
                    "AddAccount": "[\"1234567890\"]"
                }, 
                "ToRegionIds": {
                    "ToRegionId": "[\"cn-hangzhou\"]"
                }
            }
        ]
    }
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

