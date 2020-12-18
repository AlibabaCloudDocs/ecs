# DescribeRegions

You can call this operation to query available Alibaba Cloud regions.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates a sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeRegions&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRegions|The operation that you want to perform. Set the value to DescribeRegions. |
|InstanceChargeType|String|No|PrePaid|The billing method of the instance. For more information, see [Billing overview](~~25398~~). Valid values:

-   PrePaid: subscription. If this parameter is set to PrePaid, make sure that you have sufficient balance or credit in your account. Otherwise, the InvalidPayMethod error code is returned.
-   PostPaid: pay-as-you-go.

Default value: PostPaid. |
|ResourceType|String|No|instance|The resource type. Valid values:

-   instance: ECS instance
-   disk: disk
-   reservedinstance: reserved instance
-   scu: storage capacity unit \(SCU\)

Default value: instance. |
|AcceptLanguage|String|No|zh-CN|The natural language that is used to filter responses. For more information, visit [RFC 7231](https://tools.ietf.org/html/rfc7231). Valid values:

-   zh-CN: Chinese
-   en-US: English
-   ja: Japanese

Default value: zh-CN. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Regions|Array| |An array consisting of region data. |
|Region| | | |
|LocalName|String|China \(Qingdao\)|The name of the region. |
|RegionEndpoint|String|ecs.aliyuncs.com|The endpoint of the region. |
|RegionId|String|cn-qingdao-et2-bo1|The region ID. |
|Status|String|available|Indicates whether the cluster is sold out. Valid values:

-   available
-   soldOut |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeRegions
&RegionId=cn-qingdao
&InstanceChargeType=PrePaid
&ResourceType=Instance
&AcceptLanguage=en-US
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeRegionsResponse>
      <RequestId>38EC7366-F5A9-46B1-BDB1-0FDC2E296397</RequestId>
      <Regions>
            <Region>
                  <RegionId>cn-qingdao-et2-bo1</RegionId>
                  <RegionEndpoint>ecs.aliyuncs.com</RegionEndpoint>
                  <LocalName>China (Qingdao)</LocalName>
            </Region>
            <Region>
                  <RegionId>cn-qingdao-nebula</RegionId>
                  <RegionEndpoint>ecs.cn-qingdao-nebula.aliyuncs.com</RegionEndpoint>
                  <LocalName>cn-qingdao-nebula</LocalName>
            </Region>
      </Regions>
</DescribeRegionsResponse>
```

`JSON` format

```
{
    "RequestId": "38EC7366-F5A9-46B1-BDB1-0FDC2E296397",
    "Regions": {
        "Region": [
            {
                "RegionId": "cn-qingdao-et2-b01",
                "RegionEndpoint": "ecs.aliyuncs.com",
                "LocalName": "China (Qingdao)"
            },
            {
                "RegionId": "cn-qingdao-nebula",
                "RegionEndpoint": "ecs.cn-qingdao-nebula.aliyuncs.com",
                "LocalName": "cn-qingdao-nebula"
            }
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|Unauthorized.EmptyRegion|The specified account has no access authority to any region.|The error message returned because you are not authorized to access any regions. Apply for permissions and try again.|
|404|InvalidAcceptLanguage.NotFound|Only Chinese \(zh-CN\), English \(en-US\), and Japanese \(ja\) are allowed.|The error message returned because the selected language is not supported. Only Chinese, English, and Japanese are supported.|
|404|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|The error message returned because the specified resource type does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

