# CreateActivation

You can call this operation to create an activation code. This activation code is used to register servers that are not provided by Alibaba Cloud as an Alibaba Cloud managed instance.

## Description

After you use an activation code to register a server that is not provided by Alibaba Cloud as an Alibaba Cloud managed instance, you can use a variety of online services provided by Alibaba Cloud, such as Cloud Assistant, Operation Orchestration Service \(OOS\), and Apsara Devops in the managed instance.

If a server is not provided by Alibaba Cloud, it can be registered as an Alibaba Cloud managed instance only when the server can access the Internet and runs an operating system of one of the following versions:

-   Alibaba Cloud Linux 2
-   CentOS 6, CentOS 7, CentOS 8, and later
-   Debian 8, Debian 9, Debian 10, and later
-   Ubuntu 12, Ubuntu 14, Ubuntu 16, Ubuntu 18, and later
-   CoreOS
-   OpenSUSE
-   RedHat 5, RedHat 6, RedHat 7, and later
-   SUSE Linux Enterprise Server \(SLES\) 11, SLES 12, SLES 15, and later
-   Windows Server 2012, Windows Server 2016, Windows Server 2019, and later

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateActivation&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateActivation|The operation that you want to perform. Set the value to CreateActivation. |
|InstanceName|String|Yes|test-InstanceName|The default instance name prefix. The instance name prefix must be 1 to 50 characters in length. It must start with a letter but cannot start with `http://` or `https://`. The instance name prefix can only contain letters, periods \(.\), underscores \(\_\), hyphens \(-\), and colons \(:\).

If you register instances by using the activation code created by the CreateActivation operation, the instances are assigned sequential names that are prefixed by the value of this parameter. You can also specify a new instance name to override this default name when you register a managed instance.

If you did not specify the InstanceName parameter when you register a managed instance, an instance name in the format of `<InstanceName>-<Number>` is generated. The digits of <Number\> depend on the digits of the value of `InstanceCount`. Example: `001`. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the activation code. Only the China \(Hangzhou\), China \(Beijing\), and China \(Shanghai\) regions are supported. |
|Description|String|No|This is description.|The description of the activation code. The description can be 1 to 100 characters in length and cannot start with `http://` or `https://`. |
|InstanceCount|Integer|No|10|The maximum number of times that the activation code can be used to register managed instances. Valid values: 1 to 1000.

Default value: 10 |
|TimeToLiveInHours|Long|No|4|The validity period of the activation code. The activation code cannot be used to register a new instance when the validity period expires. Unit: hours. Valid values: 1 to 24.

Default value: 4 |
|IpAddressRange|String|No|0.0.0.0/0|The IP addresses of hosts that are allowed to use the activation code. The values are the corresponding IPv4 addresses, IPv6 addresses, or CIDR blocks. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ActivationCode|String|a-hz0ch3SwhOlE1234+Xo32lAZC\*\*\*\*|The value of the activation code. The value is returned only once after the CreateActivation operation is called and cannot be queried subsequently. Be sure to properly save the return value. |
|ActivationId|String|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|The ID of the activation code. |
|RequestId|String|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateActivation
&InstanceName=test-InstanceName
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateActivationResponse>
      <RequestId>4ECEEE12-56F1-4FBC-9AB1-890F1234****</RequestId>
      <ActivationId>4ECEEE12-56F1-4FBC-9AB1-890F1234****</ActivationId>
      <ActivationCode>a-hz0ch3SwhOlE1234+Xo32lAZC****</ActivationCode>
</CreateActivationResponse>
```

`JSON` format

```
{
    "RequestId": "4ECEEE12-56F1-4FBC-9AB1-890F1234****",
    "ActivationId": "4ECEEE12-56F1-4FBC-9AB1-890F1234****",
    "ActivationCode": "a-hz0ch3SwhOlE1234+Xo32lAZC****"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

