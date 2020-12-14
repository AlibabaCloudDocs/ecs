# DescribeAccountAttributes

You can call this operation to query the quotas of ECS resources that you can create in an Alibaba Cloud region. The resources that you can query include the numbers of security groups, elastic network interfaces \(ENIs\), pay-as-you-go instance vCPUs, preemptible instance vCPUs, dedicated hosts, and capacity quotas of all pay-as-you-go disks. You can also query the information such as the network type or whether an account has passed the real-name verification.

## Description

After you[register](https://account.alibabacloud.com/register/intl_register.htm) for an Alibaba Cloud account, you can create a specific number of ECS resources in different regions. For more information, see [Limits](~~25412~~).

You can also [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to increase the resource usage quota.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeAccountAttributes&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAccountAttributes|The operation that you want to perform. Set the value to DescribeAccountAttributes. |
|RegionId|String|Yes|cn-hangzhou|The region ID. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ZoneId|String|No|cn-hangzhou-b|The zone ID. |
|AttributeName.N|RepeatList|No|max-security-groups|The type of resource quota N to be queried in the specified region. Valid values of N: 1 to 8. Valid values:

-   instance-network-type: available network types
-   max-security-groups: the maximum number of security groups
-   max-elastic-network-interfaces: the maximum number of ENIs
-   max-postpaid-instance-vcpu-count: the maximum number of pay-as-you-go instance vCPUs
-   max-spot-instance-vcpu-count: the maximum number of preemptible instance vCPUs
-   used-postpaid-instance-vcpu-count: the number of pay-as-you-go instance vCPUs that have been used
-   used-spot-instance-vcpu-count: the number of preemptible instance vCPUs that have been used
-   max-postpaid-yundisk-capacity: the maximum capacity of pay-as-you-go data disks
-   used-postpaid-yundisk-capacity: the capacity of pay-as-you-go data disks that have been used
-   max-dedicated-hosts: the maximum number of dedicated hosts
-   supported-postpaid-instance-types: the instance types of pay-as-you-go I/O optimized instances
-   max-axt-command-count: the maximum number of Cloud Assistant scripts
-   max-axt-invocation-daily: the maximum number of Cloud Assistant scripts that can be run each day
-   real-name-authentication: whether the account has passed the real-name verification

**Note:** You must pass the real-name verification before you create an ECS instance in mainland China regions.


This parameter is empty by default. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AccountAttributeItems|Array of AccountAttributeItem| |The collection of AccountAttributeItem information in the specified region. |
|AccountAttributeItem| | | |
|AttributeName|String|max-security-groups|The type of the resource quota in the specified region. Valid values:

-   instance-network-type: available network types
-   max-security-groups: the maximum number of security groups
-   max-elastic-network-interfaces: the maximum number of ENIs
-   max-postpaid-instance-vcpu-count: the maximum number of pay-as-you-go instance vCPUs
-   max-spot-instance-vcpu-count: the maximum number of preemptible instance vCPUs
-   used-postpaid-instance-vcpu-count: the number of pay-as-you-go instance vCPUs that have been used
-   used-spot-instance-vcpu-count: the number of preemptible instance vCPUs that have been used
-   max-postpaid-yundisk-capacity: the maximum capacity of pay-as-you-go data disks
-   used-postpaid-yundisk-capacity: the capacity of pay-as-you-go data disks that have been used
-   max-dedicated-hosts: the maximum number of dedicated hosts
-   supported-postpaid-instance-types: the instance types of pay-as-you-go I/O optimized instances
-   max-axt-command-count: the maximum number of Cloud Assistant scripts
-   max-axt-invocation-daily: the maximum number of Cloud Assistant scripts that can be run each day
-   real-name-authentication: whether the account has passed the real-name verification |
|AttributeValues|Array of ValueItem| |The specific values of resource quotas. |
|ValueItem| | | |
|Count|Integer|3|The number of privilege attribute types. |
|DiskCategory|String|cloud\_ssd|The category of the data disk. Valid values:

-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\) |
|ExpiredTime|String|2019-01-01T12:30:00Z|The expiration time of a privilege. This parameter is returned only when the account privilege has an expiration time. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|InstanceChargeType|String|PrePaid|The billing method of the instance. |
|InstanceType|String|ecs.g5.large|The instance type. |
|Value|String|800|The specific quota of the specified resource in the current region or all regions. Valid values:

The return values of the following parameters are 0 or positive integers:

-   max-security-groups
-   max-elastic-network-interfaces
-   max-postpaid-instance-vcpu-count
-   max-spot-instance-vcpu-count
-   used-postpaid-instance-vcpu-count
-   used-spot-instance-vcpu-count
-   max-postpaid-yundisk-capacity
-   used-postpaid-yundisk-capacity
-   max-dedicated-hosts
-   max-axt-command-count
-   max-axt-invocation-daily

When the AttributeName parameter is set to supported-postpay-instance-types, an instance type is returned. For more information, see [Instance families](~~25378~~).

When the AttributeName parameter is set to real-name-authentications, the following values are returned:

-   yes
-   none
-   unnecessary

When the AttributeName parameter is set to instance-network-type, the following values are returned:

-   vpc
-   classic |
|ZoneId|String|cn-hangzhou-b|The zone ID. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeAccountAttributes
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-b
&AttributeName.1=max-security-groups
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeAccountAttributesResponse>
      <AccountAttributeItems>
            <AccountAttributeItem>
                  <AttributeValues>
                        <ValueItem>
                              <Value>100</Value>
                        </ValueItem>
                  </AttributeValues>
                  <AttributeName>max-security-groups</AttributeName>
            </AccountAttributeItem>
            <AccountAttributeItem>
                  <AttributeValues>
                        <ValueItem>
                              <Value>2</Value>
                        </ValueItem>
                  </AttributeValues>
                  <AttributeName>max-dedicated-hosts</AttributeName>
            </AccountAttributeItem>
            <AccountAttributeItem>
                  <AttributeValues>
                        <ValueItem>
                              <Value>1000</Value>
                        </ValueItem>
                  </AttributeValues>
                  <AttributeName>max-postpaid-instance-vcpu-count</AttributeName>
            </AccountAttributeItem>
            <AccountAttributeItem>
                  <AttributeValues>
                        <ValueItem>
                              <Value>1000</Value>
                        </ValueItem>
                  </AttributeValues>
                  <AttributeName>max-spot-instance-vcpu-count</AttributeName>
            </AccountAttributeItem>
            <AccountAttributeItem>
                  <AttributeValues>
                        <ValueItem>
                              <Value>5000</Value>
                        </ValueItem>
                  </AttributeValues>
                  <AttributeName>max-elastic-network-interfaces</AttributeName>
            </AccountAttributeItem>
            <AccountAttributeItem>
                  <AttributeValues>
                        <ValueItem>
                              <Value>yes</Value>
                        </ValueItem>
                  </AttributeValues>
                  <AttributeName>real-name-authentication</AttributeName>
            </AccountAttributeItem>
            <AccountAttributeItem>
                  <AttributeValues>
                        <ValueItem>
                              <Value>vpc</Value>
                        </ValueItem>
                  </AttributeValues>
                  <AttributeName>instance-network-type</AttributeName>
            </AccountAttributeItem>
            <AccountAttributeItem>
                  <AttributeValues>
                        <ValueItem>
                              <Value>229376</Value>
                              <DiskCategory>cloud_efficiency</DiskCategory>
                        </ValueItem>
                        <ValueItem>
                              <Value>204800</Value>
                              <DiskCategory>cloud_ssd</DiskCategory>
                        </ValueItem>
                        <ValueItem>
                              <Value>204800</Value>
                              <DiskCategory>cloud_essd</DiskCategory>
                        </ValueItem>
                  </AttributeValues>
                  <AttributeName>max-postpaid-yundisk-capacity</AttributeName>
            </AccountAttributeItem>
            <AccountAttributeItem>
                  <AttributeValues>
                        <ValueItem>
                              <Value>ecs.f3-c16f1.4xlarge</Value>
                        </ValueItem>
                        <ValueItem>
                              <Value>ecs.g5.2xlarge</Value>
                        </ValueItem>
                  </AttributeValues>
                  <AttributeName>supported-postpaid-instance-types</AttributeName>
            </AccountAttributeItem>
      </AccountAttributeItems>
      <RequestId>8CE45CD5-31FB-47C2-959D-CA8144CE9F42</RequestId>
</DescribeAccountAttributesResponse>
```

`JSON` format

```
{
    "AccountAttributeItems": {
        "AccountAttributeItem": [
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "100"
                        }
                    ]
                },
                "AttributeName": "max-security-groups"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "2"
                        }
                    ]
                },
                "AttributeName": "max-dedicated-hosts"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "1000"
                        }
                    ]
                },
                "AttributeName": "max-postpaid-instance-vcpu-count"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "1000"
                        }
                    ]
                },
                "AttributeName": "max-spot-instance-vcpu-count"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "5000"
                        }
                    ]
                },
                "AttributeName": "max-elastic-network-interfaces"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "yes"
                        }
                    ]
                },
                "AttributeName": "real-name-authentication"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "vpc"
                        }
                    ]
                },
                "AttributeName": "instance-network-type"
            },        
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "229376",
                            "DiskCategory": "cloud_efficiency"
                        },
                        {
                            "Value": "204800",
                            "DiskCategory": "cloud_ssd"
                        },
                        {
                            "Value": "204800",
                            "DiskCategory": "cloud_essd"
                        }
                    ]
                },
                "AttributeName": "max-postpaid-yundisk-capacity"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "ecs.f3-c16f1.4xlarge"
                        },
                        {
                            "Value": "ecs.g5.2xlarge"
                        }
                    ]
                },
                "AttributeName": "supported-postpaid-instance-types"
            }
        ]
    },
    "RequestId": "8CE45CD5-31FB-47C2-959D-CA8144CE9F42"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|Invalid.Parameter|The required parameter regionId must be not null.|The error message returned because the RegionId parameter is not specified.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

