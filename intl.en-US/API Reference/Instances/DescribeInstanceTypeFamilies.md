# DescribeInstanceTypeFamilies

You can call this operation to query the instance families provided by ECS.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceTypeFamilies&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInstanceTypeFamilies|The operation that you want to perform. Set the value to DescribeInstanceTypeFamilies. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Generation|String|No|ecs-5|The generation of the instance family. For more information, see [Instance families](~~25378~~). Valid values:

 -   ecs-1: Generation I, which consists of the earliest and cost-effective instance types
-   ecs-2: Generation II, which provides upgraded software and hardware and higher performance than Generation I
-   ecs-3: Generation III, which consists of high-performance instance families and is suitable for different business scenarios
-   ecs-4: Generation IV, which consists of enterprise-level instance families \(such as g5, c5, and r5\), Bare Metal Instance families \(such as ebmc5s, ebmg5s, and ebmr5s\), and burstable instance families \(such as t5\) that can meet a wide variety of business requirements with lower latency
-   ecs-5: Generation V, which consists of enterprise-level instance families \(such as g6, c6, and r6\), Bare Metal Instance families \(such as ebmg6, ebmg6e, and ebmc6\), and storage enhanced instance families \(such as g6e\) and delivers quick response and higher performance
-   ecs-6: Generation VI, which consists of enterprise-level instance families \(such as hfc7, hfg7, and hfr7\) and Bare Metal Instance families \(such as ebmhfg7\) and is in invitational preview |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|InstanceTypeFamilies|Array of InstanceTypeFamily| |Details about instance families. |
|InstanceTypeFamily| | | |
|Generation|String|ecs-5|The generation of the instance family. |
|InstanceTypeFamilyId|String|ecs.g6|The ID of the instance family. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceTypeFamilies
&RegionId=cn-hangzhou
&Generation=ecs-5
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeInstanceTypeFamiliesResponse>
      <InstanceTypeFamilies>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.g6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.ebmg6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.ebmg6e</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.g6e</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.c6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.r6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.t6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.hfc6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.hfg6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.hfr6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.ebmc6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
            <InstanceTypeFamily>
                  <InstanceTypeFamilyId>ecs.ebmr6</InstanceTypeFamilyId>
                  <Generation>ecs-5</Generation>
            </InstanceTypeFamily>
      </InstanceTypeFamilies>
      <RequestId>A66D039A-EC35-4130-B0D1-E9873C0742D2</RequestId>
</DescribeInstanceTypeFamiliesResponse>
```

`JSON` format

```
{
	"InstanceTypeFamilies": {
		"InstanceTypeFamily": [
			{
				"InstanceTypeFamilyId": "ecs.g6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.ebmg6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.ebmg6e",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.g6e",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.c6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.r6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.t6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.hfc6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.hfg6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.hfr6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.ebmc6",
				"Generation": "ecs-5"
			},
			{
				"InstanceTypeFamilyId": "ecs.ebmr6",
				"Generation": "ecs-5"
			}
		]
	},
	"RequestId": "A66D039A-EC35-4130-B0D1-E9873C0742D2"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

