# ModifyElasticityAssurance

You can call this operation to modify the name and description of an elasticity assurance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyElasticityAssurance&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|ModifyElasticityAssurance|The operation that you want to perform. Set the value to ModifyElasticityAssurance. |
|PrivatePoolOptions.Id|String|Yes|eap-bp67acfmxazb4\*\*\*\*|The ID of the elasticity assurance. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the elasticity assurance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|PrivatePoolOptions.Name|String|No|eapTestName|The name of the elasticity assurance. The name must be 2 to 128 characters in length. It must start with a letter but cannot start with http:// or https://. The name can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|Description|String|No|This is description.|The description of the elasticity assurance. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|8455DD10-84F8-43C9-8365-5F448EB169B6|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyElasticityAssurance
&PrivatePoolOptions.Id=eap-bp67acfmxazb4****
&RegionId=cn-hangzhou
&PrivatePoolOptions.Name=eapTestName
&Description=This is description.
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyElasticityAssuranceResponse>
      <RequestId>8455DD10-84F8-43C9-8365-5F448EB169B6</RequestId>
</ModifyElasticityAssuranceResponse>
```

`JSON` format

```
{
    "RequestId": "8455DD10-84F8-43C9-8365-5F448EB169B6"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|401|InvalidUser.Unauthorized|The user is not authorized|The error message returned because you are not authorized to perform this operation.|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|The error message returned because resources are insufficient in the specified zone. Try other types of resources, or select other regions and zones.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

