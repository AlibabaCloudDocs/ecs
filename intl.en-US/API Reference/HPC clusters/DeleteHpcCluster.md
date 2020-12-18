# DeleteHpcCluster

You can call this operation to delete an HPC cluster.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DeleteHpcCluster&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteHpcCluster|The operation that you want to perform. Set the value to DeleteHpcCluster. |
|HpcClusterId|String|Yes|hpc-cxvr5uzy54j0ya\*\*\*\*|The ID of the HPC cluster. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the HPC cluster. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DeleteHpcCluster
&RegionId=cn-hangzhou
&HpcClusterId=hpc-cxvr5uzy54j0ya****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteHpcClusterResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</DeleteHpcClusterResponse>
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter.RegionId|The input parameter RegionId that is mandatory for processing this request is not supplied.|The error message returned because the required RegionId parameter is not specified.|
|404|InvalidRegionId.NotFound|The specified parameter "RegionId" is not valid.|The error message returned because the specified RegionId parameter does not exist. Check whether the HPC cluster service is available in the region.|
|400|MissingParameter.HpcClusterId|The input parameter HpcClusterId that is mandatory for processing this request is not supplied.|The error message returned because the HpcClusterId parameter is not specified.|
|400|Invalid.Parameter|Invalid parameters.|The error message returned because a specified parameter is invalid.|
|400|NotExists.HpcCluster|The specified hpc cluster does not exist.|The error message returned because the specified HPC cluster does not exist.|
|400|NotEmpty.HpcCluster|The specified hpc cluster is not empty, still contains instances.|The error message returned because the specified HPC cluster contains instances. Release the instances and try again.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

