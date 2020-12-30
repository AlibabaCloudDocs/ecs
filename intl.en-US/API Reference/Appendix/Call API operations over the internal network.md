# Call API operations over the internal network

You cannot call API operations on VPC-type ECS instances that do not have public IP addresses. This topic describes how to call API operations on VPC-type ECS instances over the Alibaba Cloud internal network.

## Background information

ECS provides public endpoints. If your ECS instance does not have a public bandwidth or a public IP address, you cannot make API requests by using tools such as Alibaba Cloud CLI or SDKs. You can use one of the following methods to call API operations over the Alibaba Cloud internal network:

-   SDK: Use the SDK for Java core library v4.5.3 or later to call API operations over the internal network in a VPC.
-   CLI: Use CLI to call API operations over the internal network by specifying the endpoint of a specific region.

Take note of the following items:

-   These methods are applicable only in regions where VPC-type ECS instances are deployed. The endpoint of a region can be used to manage resources only within that region. Cross-region operations are not supported.
-   We recommend that you use custom images that have Alibaba Cloud CLI or SDKs deployed to create ECS instances. The ECS instances must load related dependencies with access to the Internet.

The following table describes the endpoints that support API calls over the internal network. Make sure that you use an endpoint listed in the table.

|Alibaba Cloud region|Region ID|Endpoint|
|--------------------|---------|--------|
|China \(Hangzhou\)|cn-hangzhou|ecs-vpc.cn-hangzhou.aliyuncs.com|
|China \(Shanghai\)|cn-shanghai|ecs-vpc.cn-shanghai.aliyuncs.com|
|China \(Qingdao\)|cn-qingdao|ecs-vpc.cn-qingdao.aliyuncs.com|
|China \(Beijing\)|cn-beijing|ecs-vpc.cn-beijing.aliyuncs.com|
|China \(Zhangjiakou\)|cn-zhangjiakou|ecs-vpc.cn-zhangjiakou.aliyuncs.com|
|China \(Hohhot\)|cn-huhehaote|ecs-vpc.cn-huhehaote.aliyuncs.com|
|China \(Ulanqab\)|cn-wulanchabu|ecs-vpc.cn-wulanchabu.aliyuncs.com|
|China \(Shenzhen\)|cn-shenzhen|ecs-vpc.cn-shenzhen.aliyuncs.com|
|China \(Heyuan\)|cn-heyuan|ecs-vpc.cn-heyuan.aliyuncs.com|
|China \(Guangzhou\)|cn-guangzhou|ecs-vpc.cn-guangzhou.aliyuncs.com|
|China \(Chengdu\)|cn-chengdu|ecs-vpc.cn-chengdu.aliyuncs.com|
|China \(Hong Kong\)|cn-hongkong|ecs-vpc.cn-hongkong.aliyuncs.com|
|Singapore|ap-southeast-1|ecs-vpc.ap-southeast-1.aliyuncs.com|
|Australia \(Sydney\)|ap-southeast-2|ecs-vpc.ap-southeast-2.aliyuncs.com|
|Malaysia \(Kuala Lumpur\)|ap-southeast-3|ecs-vpc.ap-southeast-3.aliyuncs.com|
|Indonesia \(Jakarta\)|ap-southeast-5|ecs-vpc.ap-southeast-5.aliyuncs.com|
|Japan \(Tokyo\)|ap-northeast-1|ecs-vpc.ap-northeast-1.aliyuncs.com|
|Germany \(Frankfurt\)|eu-central-1|ecs-vpc.eu-central-1.aliyuncs.com|
|UK \(London\)|eu-west-1|ecs-vpc.eu-west-1.aliyuncs.com|
|US \(Silicon Valley\)|us-west-1|ecs-vpc.us-west-1.aliyuncs.com|
|US \(Virginia\)|us-east-1|ecs-vpc.us-east-1.aliyuncs.com|
|India \(Mumbai\)|ap-south-1|ecs-vpc.ap-south-1.aliyuncs.com|
|UAE \(Dubai\)|me-east-1|ecs-vpc.me-east-1.aliyuncs.com|

## Method 1: \(Recommended\) Use SDKs to call API operations over the internal network

Simple configurations are required when you use SDKs to call API operations over the internal network. The following code provides an example on how to use SDK for Java to call an API operation over the internal network:

```
DefaultProfile profile = DefaultProfile.getProfile("<RegionId>", "<AccessKeyId>", "<AccessKeySecret>");
IAcsClient client = new DefaultAcsClient(profile);

// Make the configurations take effect globally. <product> refers to the service. For example, you can enter Ecs for ECS.
DefaultProfile.addEndpoint("<RegionId>", "<product>", "<Endpoint>");

// Make the configurations take effect only for the request. For example, when you call the DescribeRegions operation, you can make the following configurations:
DescribeRegionsRequest regionsRequest = new DescribeRegionsRequest();
// If you set the productNetwork parameter, you do not need to set SysEndpoint.
regionsRequest.setSysEndpoint("<Endpoint>");
// Configure the network. Valid values of productNetwork: vpc and public.
// Set the parameter to vpc when you call the operation over the internal network. Set the parameter to public when you call the operation over the Internet. Default value: public.
regionsRequest.productNetwork = "vpc";
DescribeRegionsResponse regionsResponse = client.getAcsResponse(regionsRequest);
```

## Method 2: Use CLI to call API operations over the internal network

The [DescribeRegions](/intl.en-US/API Reference/Regions/DescribeRegions.md) operation is used in this example. Sample command:

```
aliyun ecs DescribeRegions --endpoint ecs-vpc.cn-hangzhou.aliyuncs.com
```

