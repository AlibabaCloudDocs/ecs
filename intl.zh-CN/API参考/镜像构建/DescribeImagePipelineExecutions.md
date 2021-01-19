# DescribeImagePipelineExecutions

调用DescribeImagePipelineExecutions查询一个镜像构建任务的详细信息。

## 接口说明

-   指定的镜像模板ID`ImagePipelineId`不能是已删除的镜像模板，已删除的镜像模板会同步删除对应的构建任务。
-   镜像模板ID`ImagePipelineId`和构建任务ID`ExecutionId`不能同时为空。
-   您可以设置`NextToken`查询凭证（Token），其取值是上一次调用`DescribeImagePipelineExecutions`返回的`NextToken`参数值，再通过`MaxResults`设置单页查询的最大条目数进行查询。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeImagePipelineExecutions&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeImagePipelineExecutions|系统规定参数。取值：DescribeImagePipelineExecutions |
|RegionId|String|是|cn-hangzhou|所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ImagePipelineId|String|否|ip-2ze5tsl5bp6nf2b3\*\*\*\*|镜像模板ID。 |
|ExecutionId|String|否|exec-5fb8facb8ed7427c\*\*\*\*|镜像构建任务ID。 |
|Status|String|否|BUILDING|镜像构建任务的状态。支持同时设置多个值，每个值之间以半角逗号（,）间隔，格式示例为`BUILDING,DISTRIBUTING`。取值范围：

 -   BUILDING：构建中
-   DISTRIBUTING：分发中
-   RELEASING：资源回收中
-   SUCCESS：成功
-   FAILED：失败
-   CANCELLING：取消中
-   CANCELLED：已取消

 **说明：** 目前不支持参数值为空时默认查询所有状态的镜像构建任务。 |
|NextToken|String|否|AAAAAdDWBF2\*\*\*\*|查询凭证（Token）。取值为上一次调用该接口返回的`NextToken`参数值，初次调用接口时无需设置该参数。 |
|MaxResults|Integer|否|50|分页查询时每页行数。取值范围：1~500

 默认值：50。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ImagePipelineExecution|Array of ImagePipelineExecutionSet| |镜像构建任务的详细信息组成的列表。 |
|ImagePipelineExecutionSet| | | |
|CreationTime|String|2020-11-24T06:00:00Z|镜像构建任务的创建时间。 |
|ExecutionId|String|exec-5fb8facb8ed7427c\*\*\*\*|构建任务ID。 |
|ImageId|String|m-bp67acfmxazb4p\*\*\*\*|目标镜像ID。 |
|ImagePipelineId|String|ip-2ze5tsl5bp6nf2b3\*\*\*\*|镜像模板ID。 |
|Message|String|Create transition vpc "vpc-2ze70rc7093j9idu6\*\*\*\*" success!|执行结果信息。 |
|ModifiedTime|String|2020-11-25T06:00:00Z|任务最近一次更新的时间。 |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|企业资源组ID。 |
|Status|String|BUILDING|镜像构建任务的状态。可能值：

 -   BUILDING：构建中
-   DISTRIBUTING：分发中
-   RELEASING：资源回收中
-   SUCCESS：成功
-   FAILED：失败
-   CANCELLING：取消中
-   CANCELLED：已取消 |
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
https://ecs.aliyuncs.com/?Action=DescribeImagePipelineExecutions
&RegionId=cn-hangzhou
&ExecutionId=exec-5fb8facb8ed7427c****
&Status=BUILDING
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeImagePipelineExecutionsResponse>
      <TotalCount>1</TotalCount>
      <NextToken>AAAAAdDWBF2****</NextToken>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <MaxResults>50</MaxResults>
      <ImagePipelineExecution>
            <ImagePipelineExecutionSet>
                  <Status>BUILDING</Status>
                  <ResourceGroupId>rg-bp67acfmxazb4p****</ResourceGroupId>
                  <Message>Create transition vpc "vpc-2ze70rc7093j9idu6****" success!</Message>
                  <ModifiedTime>2020-11-25T06:00:00Z</ModifiedTime>
                  <ImagePipelineId>ip-2ze5tsl5bp6nf2b3****</ImagePipelineId>
                  <ImageId>m-bp67acfmxazb4p****</ImageId>
                  <CreationTime>2020-11-24T06:00:00Z</CreationTime>
                  <ExecutionId>exec-5fb8facb8ed7427c****</ExecutionId>
            </ImagePipelineExecutionSet>
            <ImagePipelineExecutionSet>
                  <Tags>
                        <Tag>
                              <TagKey>TestKey</TagKey>
                              <TagValue>TestValue</TagValue>
                        </Tag>
                  </Tags>
            </ImagePipelineExecutionSet>
      </ImagePipelineExecution>
</DescribeImagePipelineExecutionsResponse>
```

`JSON` 格式

```
{
    "TotalCount": "1", 
    "NextToken": "AAAAAdDWBF2****", 
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E", 
    "MaxResults": "50", 
    "ImagePipelineExecution": {
        "ImagePipelineExecutionSet": [
            {
                "Status": "BUILDING", 
                "ResourceGroupId": "rg-bp67acfmxazb4p****", 
                "Message": "Create transition vpc \"vpc-2ze70rc7093j9idu6****\" success!", 
                "ModifiedTime": "2020-11-25T06:00:00Z", 
                "ImagePipelineId": "ip-2ze5tsl5bp6nf2b3****", 
                "ImageId": "m-bp67acfmxazb4p****", 
                "CreationTime": "2020-11-24T06:00:00Z", 
                "ExecutionId": "exec-5fb8facb8ed7427c****"
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
    }
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

