# DescribeElasticityAssuranceInstances

调用DescribeElasticityAssuranceInstances查询弹性保障服务已匹配的运行状态的实例列表。

## 接口说明

当弹性保障服务失效后，实例与弹性保障服务对应的私有池的匹配关联数据也会失效。此时调用该接口查询已失效的服务，返回值为空。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeElasticityAssuranceInstances&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeElasticityAssuranceInstances|系统规定参数。取值：DescribeElasticityAssuranceInstances |
|PrivatePoolOptions.Id|String|是|eap-bp67acfmxazb4\*\*\*\*|弹性保障服务ID。 |
|RegionId|String|是|cn-hangzhou|弹性保障服务所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|MaxResults|Integer|否|10|分页查询时每页行数。

 最大值：100

 默认值：10 |
|NextToken|String|否|caeba0bbb2be03f84eb48b699f0a4883|弹性保障服务查询起始标志。由上一次的请求结果中获取。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ElasticityAssuranceItem|Array of InstanceIdSet| |弹性保障服务已匹配的实例列表。 |
|InstanceIdSet| | | |
|InstanceId|String|i-bp67acfmxazb4\*\*\*\*|实例ID。 |
|MaxResults|Integer|10|分页查询时每页行数。 |
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|弹性保障服务下一个查询起始标志。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|2|符合查询条件的记录条数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeElasticityAssurances
&RegionId=cn-hangzhou
&PrivatePoolOptions.Ids=eap-bp67acfmxazb4****
&MaxResults=10
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeElasticityAssuranceInstancesResponse>
      <TotalCount>2</TotalCount>
      <RequestId>CAF995AD-487E-4A2F-A064-A209CBA9B4EC</RequestId>
      <NextToken>fdf5da380c6d6b48</NextToken>
      <MaxResults>10</MaxResults>
      <ElasticityAssuranceItem>
            <InstanceIdSet>
                  <InstanceId>i-bp67acfmxazb4****</InstanceId>
            </InstanceIdSet>
            <InstanceIdSet>
                  <InstanceId>i-bp67acfmxazb5****</InstanceId>
            </InstanceIdSet>
      </ElasticityAssuranceItem>
</DescribeElasticityAssuranceInstancesResponse>
```

`JSON`格式

```
{"TotalCount":2,
 "RequestId":"CAF995AD-487E-4A2F-A064-A209CBA9B4EC",
 "NextToken":"fdf5da380c6d6b48",
 "MaxResults":10,
 "ElasticityAssuranceItem":
    {"InstanceIdSet":
        [{"InstanceId":"i-bp67acfmxazb4****"},
         {"InstanceId":"i-bp67acfmxazb5****"}]
     }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|RegionId是必选参数。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

