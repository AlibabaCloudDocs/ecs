# DescribeInstanceAttachmentAttributes

You can call this operation to query information about the private pools from which instances are created.

## Description

A private pool is generated after an elasticity assurance or a capacity reservation is created. The private pool is associated with information about instances that are created by using the private pool. You can configure a private pool when you create an ECS instance, so that the instance can match the corresponding elasticity assurance or capacity reservation.

When a private pool expires, data about the association between instances and the private pool becomes invalid. In this case, a call to this operation returns empty values related to private pools.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceAttachmentAttributes&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInstanceAttachmentAttributes|The operation that you want to perform. Set the value to DescribeInstanceAttachmentAttributes. |
|InstanceIds|String|Yes|\["i-bp67acfmxazb4\*\*\*\*", "i-bp67acfmxazb5\*\*\*\*", "i-bp67acfmxazb6\*\*\*\*"\]|The IDs of instances. The value can be a JSON array that consists of up to 100 instance IDs. Separate multiple instance IDs with commas \(,\). |
|RegionId|String|Yes|cn-hangzhou|The region ID of the elasticity assurance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|PageNumber|Integer|No|1|The number of the page to return.

This value starts from 1.

Default value: 1. |
|PageSize|Integer|No|10|The number of entries to return on each page.

Maximum value: 100

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Instances|Array of Instance| |Details about the private pools from which the instances are created. |
|Instance| | | |
|InstanceId|String|i-bp67acfmxazb4\*\*\*\*|The ID of the instance. |
|PrivatePoolOptionsId|String|eap-bp67acfmxazb4\*\*\*\*|The ID of the private pool. When the value of `PrivatePoolOptionsMatchCriteria` is `Open`, the private pool ID is the ID that was allocated by the system for automatic match. |
|PrivatePoolOptionsMatchCriteria|String|Open|The match mode of the private pool. Valid values:

-   Open: Instances automatically match an open private pool.
-   Target: Instances match a specified private pool.
-   None: Instances do not use private pools. |
|PageNumber|Integer|1|The number of the page returned. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|1|The number of entries that meet the query criteria. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceAttachmentAttributes
&RegionId=cn-hangzhou
&InstanceIds=["i-bp67acfmxazb4****", "i-bp67acfmxazb5****", "i-bp67acfmxazb6****"]
&<Common request parameters>
```

Sample success responses

`XML` format

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

`JSON` format

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

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|The error message returned because the RegionId parameter is not specified.|
|404|InvalidInstanceIds.NotFound|The specified InstanceIds does not exist.|The error message returned because the specified InstanceIds parameter does not exist. Check whether the InstanceIds parameter is valid. You can call the DescribeInstances operation to query the most recent instance list.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

