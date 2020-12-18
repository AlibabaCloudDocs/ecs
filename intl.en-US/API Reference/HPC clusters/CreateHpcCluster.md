# CreateHpcCluster

You can call this operation to create an HPC cluster.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateHpcCluster&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateHpcCluster|The operation that you want to perform. Set the value to CreateHpcCluster. |
|Name|String|Yes|hpc-Cluster-01|The name of the HPC cluster. The name must be 2 to 128 characters in length. It must start with a letter but cannot start with http:// or https://. It can contain letters, digits, underscores \(\_\), and hyphens \(-\). |
|RegionId|String|Yes|cn-hangzhou|The region ID of the HPC cluster. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|Description|String|No|testHPCDescription|The description of the HPC cluster. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

This parameter is empty by default. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|HpcClusterId|String|hpc-pnlg1ds9rky4\*\*\*\*|The ID of the HPC cluster. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateHpcCluster
&RegionId=cn-hangzhou
&Name=hpc-Cluster-01
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateHpcClusterResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <HpcClusterId>hpc-pnlg1ds9rky4****</HpcClusterId>
</CreateHpcClusterResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "HpcClusterId": "hpc-pnlg1ds9rky4****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|The input parameter RegionId that is mandatory for processing this request is not supplied.|The error message returned because the RegionId parameter is not specified.|
|400|InvalidHpcClusterName.Malformed|Specified hpc cluster name is not valid.|The error message returned because the specified Name parameter is invalid.|
|400|InvalidHpcClusterDescription.Malformed|The specified parameter Description is not valid.|The error message returned because the specified Description parameter is invalid.|
|404|InvalidRegionId.NotFound|The specified parameter "RegionId" is not valid.|The error message returned because the specified RegionId parameter does not exist. Check whether the HPC cluster service is available in the region.|
|404|InternalError|Failed to create hpc cluster|The error message returned because the HPC cluster failed to be created.|
|400|Invalid.Parameter|Invalid parameters|The error message returned because a specified parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

