# DescribeAutoProvisioningGroupInstances

You can call this operation to query instances in an auto provisioning group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeAutoProvisioningGroupInstances&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAutoProvisioningGroupInstances|The operation that you want to perform. Set the value to DescribeAutoProvisioningGroupInstances. |
|AutoProvisioningGroupId|String|Yes|apg-uf6jel2bbl62wh13\*\*\*\*|The ID of the auto provisioning group. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the auto provisioning group. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|PageNumber|Integer|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1. |
|PageSize|Integer|No|10|The number of entries to return on each page.

Maximum value: 100.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Instances|Array| |An array consisting of Instance data. |
|Instance| | | |
|CPU|Integer|2|The number of vCPUs. |
|CreationTime|String|2017-12-10T04:04Z|The time when the instance was created. |
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|InstanceType|String|ecs.g5.large|The instance type of the ECS instance. |
|IoOptimized|Boolean|true|Indicates whether the instance is I/O optimized. |
|IsSpot|Boolean|True|Indicates whether the instance is a preemptible instance. |
|Memory|Integer|1024|The memory size of the instance. Unit: MiB. |
|NetworkType|String|vpc|The network type of the instance. Valid values:

-   vpc
-   classic |
|OsType|String|linux|The operating system type of the instance. Valid values:

-   windows
-   linux |
|RegionId|String|cn-hangzhou|The region ID of the instance. |
|Status|String|Running|The status of the instance. |
|ZoneId|String|cn-hangzhou-g|The zone ID of the instance. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*|The ID of the request. |
|TotalCount|Integer|2|The number of queried instances in the auto provisioning group. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeAutoProvisioningGroupInstances
&AutoProvisioningGroupId=apg-uf6jel2bbl62wh13****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeAutoProvisioningGroupInstancesResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>2</TotalCount>
      <PageSize>2</PageSize>
      <RequestId>A43735F7-30BD-4D89-AB8A-030EB24B****</RequestId>
      <Instances>
            <Instance>
                  <CreationTime>2019-06-17T15:25Z</CreationTime>
                  <IoOptimized>true</IoOptimized>
                  <OsType>linux</OsType>
                  <NetworkType>vpc</NetworkType>
                  <Status>Running</Status>
                  <Memory>8192</Memory>
                  <RegionId>cn-shanghai</RegionId>
                  <InstanceId>i-bp67acfmxazb4p****</InstanceId>
                  <CPU>2</CPU>
                  <ZoneId>cn-shanghai-a</ZoneId>
                  <InstanceType>ecs.g5.large</InstanceType>
            </Instance>
            <Instance>
                  <CreationTime>2019-06-17T15:25Z</CreationTime>
                  <IoOptimized>true</IoOptimized>
                  <OsType>linux</OsType>
                  <NetworkType>vpc</NetworkType>
                  <Status>Running</Status>
                  <Memory>8192</Memory>
                  <RegionId>cn-shanghai</RegionId>
                  <InstanceId>i-bp67acfmxazb5p****</InstanceId>
                  <CPU>2</CPU>
                  <ZoneId>cn-shanghai-a</ZoneId>
                  <InstanceType>ecs.g5.large</InstanceType>
            </Instance>
      </Instances>
</DescribeAutoProvisioningGroupInstancesResponse>
```

`JSON` format

```
{
    "PageNumber": 1,
    "TotalCount": 2,
    "PageSize": 2,
    "RequestId":"A43735F7-30BD-4D89-AB8A-030EB24B****",
    "Instances": {
        "Instance": [
            {
                "CreationTime": "2019-06-17T15:25Z",
                "IoOptimized": true,
                "OsType": "linux",
                "NetworkType": "vpc",
                "Status": "Running",
                "Memory": 8192,
                "RegionId": "cn-shanghai",
                "InstanceId": "i-bp67acfmxazb4p****",
                "CPU": 2,
                "ZoneId": "cn-shanghai-a",
                "InstanceType": "ecs.g5.large"
            },
            {
                "CreationTime": "2019-06-17T15:25Z",
                "IoOptimized": true,
                "OsType": "linux",
                "NetworkType": "vpc",
                "Status": "Running",
                "Memory": 8192,
                "RegionId": "cn-shanghai",
                "InstanceId": "i-bp67acfmxazb5p****",
                "CPU": 2,
                "ZoneId": "cn-shanghai-a",
                "InstanceType": "ecs.g5.large"
            }
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|The error message returned because you are not authorized to manage this resource, or this API operation does not support RAM roles.|
|400|MissingParamter.RegionId|The regionId should not be null.|The error message returned because the RegionId parameter is not specified.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

