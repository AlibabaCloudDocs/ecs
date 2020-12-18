# CreateDeploymentSet

You can call this operation to create a deployment set in a specified region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateDeploymentSet&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateDeploymentSet|The operation that you want to perform. Set the value to CreateDeploymentSet. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region in which to create the deployment set. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|OnUnableToRedeployFailedInstance|String|No|CancelMembershipAndStart|The emergency solution to be used in the following situation: Instances in the deployment set cannot be evenly distributed to different zones due to resource insufficiency after the instances are failed over from faulty physical machines to normal physical machines. Default value: CancelMembershipAndStart. Valid values:

-   CancelMembershipAndStart: removes the instances from the deployment set and restarts the instances immediately after the failover is complete.
-   KeepStopped: keeps the instances in the abnormal state and restarts them after ECS resources are replenished. |
|Description|String|No|testDescription|The description of the deployment set. The description must be 2 to 256 characters in length and cannot start with http:// or https://. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [Ensure idempotence](~~25693~~). |
|DeploymentSetName|String|No|testDeploymentSetName|The name of the deployment set. The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://. |
|Strategy|String|No|Availability|The deployment strategy. Set the value to Availability. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DeploymentSetId|String|ds-bp1frxuzdg87zh4pzq\*\*\*\*|The ID of the deployment set. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateDeploymentSet
&RegionId=cn-hangzhou
&DeploymentSetName=testDeploymentSetName
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateDeploymentSetResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
      <DeploymentSetId>ds-bp1frxuzdg87zh4pzq****</DeploymentSetId>
</CreateDeploymentSetResponse>
```

`JSON` format

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "DeploymentSetId": "ds-bp1frxuzdg87zh4pzq****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|The input parameter RegionId that is mandatory for processing this request is not supplied.|The error message returned because the required RegionId parameter is not specified.|
|400|InvalidDeploymentSetName.Malformed|Specified deployment set name is not valid.|The error message returned because the specified DeploymentSetName parameter is invalid.|
|400|InvalidDescription.Malformed|The specified parameter Description is not valid.|The error message returned because the specified Description parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|InvalidParameter.Domain|The specified parameter Domain is not valid.|The error message returned because the specified Domain parameter is invalid.|
|400|InvalidParameter.Strategy|The specified parameter Strategy is not valid|The error message returned because the specified Strategy parameter is invalid.|
|400|InvalidParameter.granularity|The specified parameter Granularity is not valid.|The error message returned because the specified Granularity parameter is invalid.|
|400|DependencyViolation.domain.granularity|The DeploymentSet domain and granularity is violation.|The error message returned because the specified Domain and Granularity parameters do not correspond to each other.|
|400|DependencyViolation.strategy.granularity|The DeploymentSet strategy and granularity is violation.|The error message returned because the specified Strategy and Granularity parameters do not correspond to each other.|
|400|DEPLOYMENTSET.QUOTA\_FULL|The deploymentSet quota is full|The error message returned because the maximum number of deployment sets has been reached. Reduce the number of deployment sets.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

