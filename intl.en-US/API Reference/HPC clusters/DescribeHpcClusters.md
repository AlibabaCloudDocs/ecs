# DescribeHpcClusters

You can call this operation to query available HPC clusters. The request parameters are used as filters. Specified parameters have logical AND relations. The request parameters are not dependent on each other.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeHpcClusters&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeHpcClusters|The operation that you want to perform. Set the value to DescribeHpcClusters. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the HPC cluster. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|HpcClusterIds|String|No|\["hpc-xxxxxxxxx", "hpc-yyyyyyyyy", ... "hpc-zzzzzzzzz"\]|The IDs of the HPC clusters.

You can specify a JSON array that consists of up to 100 HPC cluster IDs. Separate multiple HPC cluster IDs with commas \(,\). |
|PageNumber|Integer|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1. |
|PageSize|Integer|No|10|The number of entries to return on each page.

Maximum value: 100

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|HpcClusters|Array of HpcCluster| |Details about the HPC clusters. The value is an array that consists of the information of each HPC cluster. |
|HpcCluster| | | |
|Description|String|testDescription|The description of the HPC cluster. |
|HpcClusterId|String|hpc-bp1a5zr3u7nq9cx\*\*\*\*|The ID of the HPC cluster. |
|Name|String|testName|The name of the HPC cluster. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|2|The total number of queried HPC clusters. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeHpcClusters
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeHpcClustersResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>2</TotalCount>
      <HpcClusters>
            <HpcCluster>
                  <Name>chuatest1</Name>
                  <Description>testDescription1</Description>
                  <HpcClusterId>hpc-bp1a5zr3u7nq9cx****</HpcClusterId>
            </HpcCluster>
            <HpcCluster>
                  <Name>chuatest2</Name>
                  <Description>testDescription2</Description>
                  <HpcClusterId>hpc-l6aam7fivcfd21fu****</HpcClusterId>
            </HpcCluster>
      </HpcClusters>
      <PageSize>10</PageSize>
      <RequestId>382960A6-C535-4705-B6EA-8338466270C4</RequestId>
</DescribeHpcClustersResponse>
```

`JSON` format

```
{
    "PageNumber": 1,
    "TotalCount": 2,
    "HpcClusters": {
        "HpcCluster": [
            {
                "Name": "chuatest1",
                "Description": "testDescription1",
                "HpcClusterId": "hpc-bp1a5zr3u7nq9cx****"
            },
            {
                "Name": "chuatest2",
                "Description": "testDescription2",
                "HpcClusterId": "hpc-l6aam7fivcfd21fu****"
            }
        ]
    },
    "PageSize": 10,
    "RequestId": "382960A6-C535-4705-B6EA-8338466270C4"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRegionId.NotFound|The specified parameter "RegionId" is not valid.|The error message returned because the specified RegionId parameter does not exist. Check whether the HPC cluster service is available in the region.|
|400|MissingParameter.HpcClusterId|The input parameter HpcClusterId that is mandatory for processing this request is not supplied.|The error message returned because the HpcClusterIds parameter is not specified.|
|400|InvalidHpcClusterIds.ExceedLimit|The amount of specified specified hpc cluster ids exceeds the limit.|The error message returned because the maximum number of HPC cluster IDs has been reached.|
|400|InvalidHpcClusterIds.Malformed|The amount of specified specified hpc cluster ids is invalid.|The error message returned because the maximum number of HPC cluster IDs has been reached.|
|400|Invalid.Parameter|Invalid parameters.|The error message returned because a specified parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

