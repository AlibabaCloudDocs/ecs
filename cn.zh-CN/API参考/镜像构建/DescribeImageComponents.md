# DescribeImageComponents

调用DescribeImageComponents查询一个或多个镜像组件的详细信息。

## 接口说明

默认查询您创建的自定义镜像组件列表。

您可以设置`NextToken`查询凭证（Token），其取值是上一次调用DescribeImageComponents返回的`NextToken`参数值，再通过`MaxResults`设置单页查询的最大条目数进行查询。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeImageComponents&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeImageComponents|系统规定参数。取值：DescribeImageComponents |
|RegionId|String|是|cn-hangzhou|所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Tag.N.Key|String|否|TestKey|标签键。N的取值范围：1~20 |
|Tag.N.Value|String|否|TestValue|标签值。N的取值范围：1~20 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|企业资源组ID。 |
|Name|String|否|testComponent|镜像组件名称。仅支持精确查找。 |
|ImageComponentId.N|RepeatList|否|ic-bp67acfmxazb4p\*\*\*\*|待查询的镜像组件ID。N取值范围：1~20 |
|NextToken|String|否|AAAAAdDWBF2\*\*\*\*|查询凭证（Token）。取值为上一次调用该接口返回的`NextToken`参数值，初次调用接口时无需设置该参数。 |
|MaxResults|Integer|否|50|分页查询时每页行数。取值范围：1~500

 默认值：50。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ImageComponent|Array of ImageComponentSet| |镜像组件的详细信息组成的列表。 |
|ImageComponentSet| | | |
|ComponentType|String|Build|组件类型。 |
|Content|String|RUN yum update -y|组件内容。 |
|CreationTime|String|2020-11-24T06:00:00Z|组件创建时间。 |
|Description|String|This is description.|描述信息。 |
|ImageComponentId|String|ic-bp67acfmxazb4p\*\*\*\*|镜像组件ID。 |
|Name|String|testComponent|组件名称。 |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|企业资源组ID。 |
|SystemType|String|Linux|组件支持的操作系统。 |
|Tags|Array of Tag| |标签键值对列表。 |
|Tag| | | |
|TagKey|String|TestKey|标签键。 |
|TagValue|String|TestValue|标签值。 |
|MaxResults|Integer|50|分页查询时每页行数。 |
|NextToken|String|AAAAAdDWBF2\*\*\*\*|本次调用返回的查询凭证（Token）。具体使用方式请参见接口说明。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|1|返回的镜像组件数量。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeImageComponents
&RegionId=cn-hangzhou
&ImageComponentId.1=ic-bp67acfmxazb4p****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeImageComponentsResponse>
      <TotalCount>1</TotalCount>
      <NextToken>AAAAAdDWBF2****</NextToken>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ImageComponent>
            <ImageComponentSet>
                  <ComponentType>Build</ComponentType>
                  <Description>This is description.</Description>
                  <ResourceGroupId>rg-bp67acfmxazb4p****</ResourceGroupId>
                  <Content>RUN yum update -y</Content>
                  <CreationTime>2020-11-24T06:00:00Z</CreationTime>
                  <SystemType>Linux</SystemType>
                  <ImageComponentId>ic-bp67acfmxazb4p****</ImageComponentId>
                  <Name>testComponent</Name>
            </ImageComponentSet>
            <ImageComponentSet>
                  <Tags>
                        <Tag>
                              <TagKey>TestKey</TagKey>
                              <TagValue>TestValue</TagValue>
                        </Tag>
                  </Tags>
            </ImageComponentSet>
      </ImageComponent>
      <MaxResults>50</MaxResults>
</DescribeImageComponentsResponse>
```

`JSON`格式

```
{
    "TotalCount": "1", 
    "NextToken": "AAAAAdDWBF2****", 
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E", 
    "ImageComponent": {
        "ImageComponentSet": [
            {
                "ComponentType": "Build", 
                "Description": "This is description.", 
                "ResourceGroupId": "rg-bp67acfmxazb4p****", 
                "Content": "RUN yum update -y", 
                "CreationTime": "2020-11-24T06:00:00Z", 
                "SystemType": "Linux", 
                "ImageComponentId": "ic-bp67acfmxazb4p****", 
                "Name": "testComponent"
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
            }
        ]
    }, 
    "MaxResults": "50"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

