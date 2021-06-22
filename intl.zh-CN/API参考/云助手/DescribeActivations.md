# DescribeActivations

调用DescribeActivations查询已创建的激活码以及激活码的使用情况。

****

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeActivations&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeActivations|系统规定参数。取值：DescribeActivations |
|RegionId|String|是|cn-hangzhou|地域ID。目前仅支持华东1（杭州）、华北2（北京）、华东2（上海）。 |
|ActivationId|String|否|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|激活码ID。 |
|InstanceName|String|否|test-InstanceName|默认的实例名称前缀。 |
|PageNumber|Long|否|1|当前页码。

 起始值：1

 默认值：1 |
|PageSize|Long|否|10|分页查询时设置的每页行数。

 最大值：50

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ActivationList|Array of Activation| |激活码及使用情况信息组成的集合。 |
|ActivationId|String|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|激活码ID。 |
|CreationTime|String|2021-01-20T06:00:00Z|创建时间。 |
|DeregisteredCount|Integer|1|已注销的实例数。 |
|Description|String|This is description.|激活码对应的描述。 |
|Disabled|Boolean|false|激活码是否被禁用。 |
|InstanceCount|Integer|1|激活码用于注册托管实例的使用次数上限。 |
|InstanceName|String|test-InstanceName|默认的实例名称前缀。 |
|IpAddressRange|String|0.0.0.0/0|允许使用该激活码的主机IP。 |
|RegisteredCount|Integer|1|已注册的实例数。 |
|TimeToLiveInHours|Long|4|激活码的有效时间。单位：小时 |
|PageNumber|Long|1|当前页码。 |
|PageSize|Long|10|分页查询时设置的每页行数。 |
|RequestId|String|4ECEEE12-56F1-4FBC-9AB1-890F74625134|请求ID。 |
|TotalCount|Long|1|符合查询条件的记录条数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeActivations
&RegionId=cn-hangzhou
&ActivationId=4ECEEE12-56F1-4FBC-9AB1-890F1234****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeActivationsResponse>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <RequestId>4ECEEE12-56F1-4FBC-9AB1-890F74942176</RequestId>
      <PageNumber>1</PageNumber>
      <ActivationList>
            <InstanceName>test-InstanceName</InstanceName>
            <DeregisteredCount>1</DeregisteredCount>
            <InstanceCount>1</InstanceCount>
            <Description>This is description.</Description>
            <CreationTime>2021-01-20T06:00:00Z</CreationTime>
            <ActivationId>4ECEEE12-56F1-4FBC-9AB1-890F1234****</ActivationId>
            <RegisteredCount>1</RegisteredCount>
            <TimeToLiveInHours>4</TimeToLiveInHours>
            <Disabled>false</Disabled>
            <IpAddressRange>0.0.0.0/0</IpAddressRange>
      </ActivationList>
</DescribeActivationsResponse>
```

`JSON`格式

```
{
    "TotalCount": "1", 
    "PageSize": "10", 
    "RequestId": "4ECEEE12-56F1-4FBC-9AB1-890F74942176", 
    "PageNumber": "1", 
    "ActivationList": [
        {
            "InstanceName": "test-InstanceName", 
            "DeregisteredCount": "1", 
            "InstanceCount": "1", 
            "Description": "This is description.", 
            "CreationTime": "2021-01-20T06:00:00Z", 
            "ActivationId": "4ECEEE12-56F1-4FBC-9AB1-890F1234****", 
            "RegisteredCount": "1", 
            "TimeToLiveInHours": "4", 
            "Disabled": "false", 
            "IpAddressRange": "0.0.0.0/0"
        }
    ]
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发送请求时发生错误，请稍后重试。|
|400|InvalidParam.PageNumber|The specified parameter is invalid.|指定的PageNumber参数无效。|
|400|InvalidParam.PageSize|The specified parameter is invalid.|指定的PageSize参数无效。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

