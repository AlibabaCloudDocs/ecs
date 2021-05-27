# DescribeInstanceAttachmentAttributes

调用DescribeInstanceAttachmentAttributes查询实例匹配的私有池信息。

## 接口说明

私有池是弹性保障服务或容量预定服务在创建后生成的，关联了与私有池匹配的实例信息。您可以在创建实例时设置私有池，实例将会与弹性保障服务或容量预定服务进行匹配。

当私有池失效后，实例与私有池的匹配关联数据也会失效。此时调用该接口，返回值的私有池信息将为空。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceAttachmentAttributes&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeInstanceAttachmentAttributes|系统规定参数。取值：DescribeInstanceAttachmentAttributes |
|InstanceIds|String|是|\["i-bp67acfmxazb4\*\*\*\*", "i-bp67acfmxazb5\*\*\*\*", "i-bp67acfmxazb6\*\*\*\*"\]|实例ID。取值可以由多个实例ID组成一个JSON数组，最多支持100个ID，ID之间用半角逗号（,）隔开。 |
|RegionId|String|是|cn-hangzhou|弹性保障服务所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|PageNumber|Integer|否|1|实例状态列表的页码。

 起始值：1

 默认值：1 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。

 最大值：100

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Instances|Array of Instance| |实例匹配的私有池信息组成的集合。 |
|Instance| | | |
|InstanceId|String|i-bp67acfmxazb4\*\*\*\*|实例ID。 |
|PrivatePoolOptionsId|String|eap-bp67acfmxazb4\*\*\*\*|私有池ID。当`PrivatePoolOptionsMatchCriteria`返回值为`Open`时，私有池ID为系统自动匹配时所分配的私有池ID。 |
|PrivatePoolOptionsMatchCriteria|String|Open|实例的私有池匹配模式。可能值：

 -   Open：开放模式。实例自动匹配开放类型的私有池。
-   Target：指定模式。实例匹配指定的私有池。
-   None：不使用模式。实例不使用私有池。 |
|PageNumber|Integer|1|实例状态列表的页码。 |
|PageSize|Integer|10|分页查询时设置的每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|1|符合查询条件的记录条数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceAttachmentAttributes
&RegionId=cn-hangzhou
&InstanceIds=["i-bp67acfmxazb4****", "i-bp67acfmxazb5****", "i-bp67acfmxazb6****"]
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeInstanceAttachmentAttributesResponse>
      <Instances>
            <Instance>
                  <InstanceId>i-bp67acfmxazb4****</InstanceId>
                  <PrivatePoolOptionsMatchCriteria>Open</PrivatePoolOptionsMatchCriteria>
                  <PrivatePoolOptionsId>eap-bp67acfmxazb4****</PrivatePoolOptionsId>
            </Instance>
      </Instances>
      <TotalCount>1</TotalCount>
      <RequestId>395245CB-A6FD-4777-8F83-A0B0DFE43F23</RequestId>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
</DescribeInstanceAttachmentAttributesResponse>
```

`JSON`格式

```
{
    "Instances":
        {"Instance":
            [{"InstanceId":"i-bp67acfmxazb4****",
            "PrivatePoolOptionsMatchCriteria":"Open",
            "PrivatePoolOptionsId":"eap-bp67acfmxazb4****"}]
        },
    "TotalCount":1,
    "RequestId":"395245CB-A6FD-4777-8F83-A0B0DFE43F23",
    "PageSize":10,
    "PageNumber":1
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|RegionId是必选参数。|
|404|InvalidInstanceIds.NotFound|The specified InstanceIds does not exist.|指定的InstanceId不存在。请检查InstanceId参数值是否正确。您可以调用DescribeInstances查询指定实例的状态。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

