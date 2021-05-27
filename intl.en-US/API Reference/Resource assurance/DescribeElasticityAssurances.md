# DescribeElasticityAssurances

You can call this operation to query the details of elasticity assurances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeElasticityAssurances&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeElasticityAssurances|The operation that you want to perform. Set the value to DescribeElasticityAssurances. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the elasticity assurance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|MaxResults|Integer|No|10|The number of entries to return on each page.

 Maximum value: 100.

 Default value: 10. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the query. The token is obtained from the response of the previous request. |
|PrivatePoolOptions.Ids|String|No|\["eap-bp67acfmxazb4\*\*\*\*", "eap-bp67acfmxazb5\*\*\*\*"\]|The IDs of elasticity assurances. The value can be a JSON array that consists of up to 100 IDs. Separate multiple IDs with commas \(,\). |
|InstanceType|String|No|ecs.c6.large|The instance type to which the elasticity assurance applies. |
|ZoneId|String|No|cn-hangzhou-h|The zone ID of the elasticity assurance. |
|InstanceChargeType|String|No|PostPaid|The billing method of the instance to be created by using the elasticity assurance. Set the value to PostPaid. Only pay-as-you-go instances can be created by using elasticity assurances.

 Default value: PostPaid. |
|Status|String|No|Active|The status of the elasticity assurance. Valid values:

 -   Preparing
-   Active
-   Released

 Default value: Active. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ElasticityAssuranceSet|Array of ElasticityAssuranceItem| |Details about the elasticity assurances. |
|ElasticityAssuranceItem| | | |
|AllocatedResources|Array of AllocatedResource| |Details about the allocated resources. |
|AllocatedResource| | | |
|InstanceType|String|ecs.c6.large|The instance type to which the elasticity assurance applies. |
|TotalAmount|Integer|2|The total number of instances reserved for a single instance type. |
|UsedAmount|Integer|2|The number of instances that have been created by using the elasticity assurance. |
|zoneId|String|cn-hangzhou-h|The zone ID of the instance. |
|Description|String|This is description.|The description of the elasticity assurance. |
|EndTime|String|2021-10-30T06:32:00Z|The time when the elasticity assurance expires. |
|LatestStartTime|String|0|**Note:** This parameter is unavailable. |
|PrivatePoolOptionsId|String|eap-bp67acfmxazb4\*\*\*\*|The ID of the elasticity assurance. |
|PrivatePoolOptionsMatchCriteria|String|Open|The match mode of the private pool corresponding to the elasticity assurance. Valid values:

 -   Open: An open private pool is used.
-   Target: A specified private pool is used. |
|PrivatePoolOptionsName|String|eapTestName|The name of the elasticity assurance. |
|RegionId|String|cn-hangzhou|The region ID of the elasticity assurance. |
|StartTime|String|2020-10-30T06:32:00Z|The time when the elasticity assurance takes effect. |
|Status|String|Active|The status of the elasticity assurance. Valid values:

 -   Preparing
-   Active
-   Released |
|TotalAssuranceTimes|String|Unlimited|The total number of times that the elasticity assurance has been applied. |
|UsedAssuranceTimes|Integer|0|**Note:** This parameter is unavailable. |
|MaxResults|Integer|10|The number of entries returned per page. |
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the next query. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|10|The number of entries that meet the query criteria. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeElasticityAssurances
&RegionId=cn-hangzhou
&PrivatePoolOptions.Ids=["eap-bp67acfmxazb4****", "eap-bp67acfmxazb5****"]
&InstanceType=ecs.c6.large
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeElasticityAssurancesResponse>
      <ElasticityAssuranceSet>
            <ElasticityAssuranceItem>
                  <TotalAssuranceTimes>Unlimited</TotalAssuranceTimes>
                  <Status>Active</Status>
                  <UsedAssuranceTimes>0</UsedAssuranceTimes>
                  <Description>This is description.</Description>
                  <EndTime>2021-09-29T16:00Z</EndTime>
                  <PrivatePoolOptionsName>eapTestName</PrivatePoolOptionsName>
                  <LatestStartTime></LatestStartTime>
                  <StartTime>2020-09-29T08:00Z</StartTime>
                  <RegionId>cn-hangzhou</RegionId>
                  <PrivatePoolOptionsMatchCriteria>Open</PrivatePoolOptionsMatchCriteria>
                  <AllocatedResources>
                        <AllocatedResource>
                              <UsedAmount>0</UsedAmount>
                              <zoneId>cn-hangzhou-i</zoneId>
                              <TotalAmount>3</TotalAmount>
                              <InstanceType>ecs.c6.xlarge</InstanceType>
                        </AllocatedResource>
                  </AllocatedResources>
                  <PrivatePoolOptionsId>eap-bp1boncv6mbmv6wi****</PrivatePoolOptionsId>
            </ElasticityAssuranceItem>
      </ElasticityAssuranceSet>
      <TotalCount>1</TotalCount>
      <RequestId>45BF0929-A08F-49CA-A053-6FA3EC66B1BD</RequestId>
      <NextToken>caeba0bbb2be03f84eb48b699f0a4883</NextToken>
      <MaxResults>10</MaxResults>
</DescribeElasticityAssurancesResponse>
```

`JSON` format

```
{
"ElasticityAssuranceSet":
    {
    "ElasticityAssuranceItem":
        [{  
        "TotalAssuranceTimes":"Unlimited",
        "Status":"Active",
        "UsedAssuranceTimes":0,
        "Description":"This is description.",
        "EndTime":"2021-09-29T16:00Z",
        "PrivatePoolOptionsName":"eapTestName",
        "LatestStartTime":"",
        "StartTime":"2020-09-29T08:00Z",
        "RegionId":"cn-hangzhou",
        "PrivatePoolOptionsMatchCriteria":"Open",
        "AllocatedResources":
            {
            "AllocatedResource":[
                {"UsedAmount":0,
                "zoneId":"cn-hangzhou-i",
                "TotalAmount":3,
                "InstanceType":"ecs.c6.xlarge"}
                ]
            },
        "PrivatePoolOptionsId":"eap-bp1boncv6mbmv6wi****"
        }]
    },
    "TotalCount":1,
    "RequestId":"45BF0929-A08F-49CA-A053-6FA3EC66B1BD",
    "NextToken":"caeba0bbb2be03f84eb48b699f0a4883",
    "MaxResults":10
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|The error message returned because the RegionId parameter is not specified.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

