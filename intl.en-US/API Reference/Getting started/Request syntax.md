---
keyword: [endpoint, Alibaba Cloud endpoint, ECS endpoint]
---

# Request syntax

You can call ECS API operations by sending HTTP or HTTPS GET requests based on URLs. Each URL must include request parameters. This topic describes the syntax of HTTP or HTTPS GET requests and provides the endpoints of ECS API.

## Sample request

The following example shows an unencoded URL request to call the [CreateSnapshot](/intl.en-US/API Reference/Snapshots/CreateSnapshot.md) operation:

```
https://ecs.aliyuncs.com/?Action=CreateSnapshot
&DiskId=d-28m5zbu****
&<Common request parameters>
```

-   `https` specifies the protocol for transmitting the request.
-   `ecs.aliyuncs.com` specifies the endpoint of ECS.
-   `Action=CreateSnapshot` specifies the API operation to call. `DiskId=d-28m5zbu\*\*\*\*` is a request parameter for [CreateSnapshot](/intl.en-US/API Reference/Snapshots/CreateSnapshot.md).
-   `<Common request parameters>` are common parameters defined in the system.

## Protocols

You can send requests over HTTP or HTTPS. For a higher level of security, we recommend that you send requests over HTTPS.

If the request contains sensitive data such as the username, password, and Secure Shell \(SSH\) key pairs, we recommend that you use HTTPS. For example, you can specify the `Password` parameter when you call the [CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md) operation.

## Endpoints

The following table lists the endpoints of ECS API. To minimize the network latency, we recommend that you specify the endpoint based on the region where you make API requests.

-   The following table lists the optimal endpoints for making API requests from mainland China.

|Region|Endpoint|
|:-----|:-------|
|Default|ecs.aliyuncs.com|
|China \(Zhangjiakou\)|ecs.cn-zhangjiakou.aliyuncs.com|
|China \(Hohhot\)|ecs.cn-huhehaote.aliyuncs.com|
|China \(Ulanqab\)|ecs.cn-wulanchabu.aliyuncs.com|
|China \(Heyuan\)|ecs.cn-heyuan.aliyuncs.com|
|China \(Guangzhou\)|ecs.cn-guangzhou.aliyuncs.com|
|Japan \(Tokyo\)|ecs.ap-northeast-1.aliyuncs.com|
|Australia \(Sydney\)|ecs.ap-southeast-2.aliyuncs.com|
|Malaysia \(Kuala Lumpur\)|ecs.ap-southeast-3.aliyuncs.com|
|Indonesia \(Jakarta\)|ecs.ap-southeast-5.aliyuncs.com|
|India \(Mumbai\)|ecs.ap-south-1.aliyuncs.com|
|UAE \(Dubai\)|ecs.me-east-1.aliyuncs.com|
|Germany \(Frankfurt\)|ecs.eu-central-1.aliyuncs.com|
|UK \(London\)|ecs.eu-west-1.aliyuncs.com|

-   Global acceleration is enabled for `ecs.aliyuncs.com`. This can reduce the network latency caused by traffic forwarding across countries or regions. You can use this endpoint when you want to make API requests from countries or regions outside mainland China.


**Note:** ECS provides public endpoints. If your ECS instance does not have a public bandwidth or a public IP address, you cannot use tools such as Alibaba Cloud CLI or SDKs to make API requests for the instance. If you want to call API operations on VPC-type ECS instances that cannot access the Internet, you can call the API operations over the internal network. For more information, see [Call API operations over the internal network](/intl.en-US/API Reference/Appendix/Call API operations over the internal network.md).

## Request parameters

You must specify the `Action` parameter to specify the API operatoin that you want to call. For example, set Action to [StartInstance](/intl.en-US/API Reference/Instances/StartInstance.md). You must also specify other operation-specific request parameters and common request parameters. For more information, see [Common request parameters](/intl.en-US/API Reference/Getting started/Common parameters.md).

## Encoding

All requests and responses are encoded in `UTF-8`.

