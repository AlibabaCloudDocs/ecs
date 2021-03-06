# DescribeElasticityAssuranceInstances

You can call this operation to query the running ECS instances that were created by using an elasticity assurance.

## Description

When an elasticity assurance expires, data about the association between instances and the private pool generated by the elasticity assurance becomes invalid. In this case, when you call this operation to query the expired elasticity assurance, no value is returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeElasticityAssuranceInstances&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeElasticityAssuranceInstances|The operation that you want to perform. Set the value to DescribeElasticityAssuranceInstances. |
|PrivatePoolOptions.Id|String|Yes|eap-bp67acfmxazb4\*\*\*\*|The ID of the elasticity assurance. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the elasticity assurance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|MaxResults|Integer|No|10|The number of entries to return on each page.

Maximum value: 100

Default value: 10. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the query. The token is obtained from the response of the previous request. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ElasticityAssuranceItem|Array of InstanceIdSet| |Details about the instances that were created by using the elasticity assurance. |
|InstanceIdSet| | | |
|InstanceId|String|i-bp67acfmxazb4\*\*\*\*|The ID of the instance. |
|MaxResults|Integer|10|The number of entries returned per page. |
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the next query. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|2|The number of entries that meet the query criteria. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeElasticityAssurances
&RegionId=cn-hangzhou
&PrivatePoolOptions.Ids=eap-bp67acfmxazb4****
&MaxResults=10
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|The error message returned because the RegionId parameter is not specified.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

