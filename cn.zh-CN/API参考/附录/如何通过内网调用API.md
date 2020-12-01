# 如何通过内网调用API

如果专有网络VPC类型的ECS实例没有设置公网IP，则无法调用API。本文介绍该类实例如何通过阿里云内网调用API。

## 背景信息

由于云服务器ECS提供的接入地址（Endpoint）为公网服务地址，当您的ECS实例没有分配公网带宽或者不存在公网IP地址时，无法使用阿里云CLI或者SDK等工具发起API请求。此时，您可以通过以下两种方式实现阿里云内网调用API。

-   SDK：Java SDK核心库在4.5.3版本起，支持通过VPC内网调用API。
-   CLI：使用CLI时，只需将Endpoint修改为对应地域的接入地址，即可实现内网调用API。

使用说明如下：

-   两种方式仅适用于专有网络VPC类型ECS实例所在的地域，且仅能使用对应地域的接入地址（Endpoint）操作同地域资源，不支持跨地域操作。
-   建议您使用已部署了阿里云CLI或者SDK的自定义镜像创建ECS实例，避免实例在无公网访问的条件下无法加载相关依赖。

支持的内网调用API的ECS接入地址（Endpoint）如下表所示，请确保您使用的Endpoint在列举范围内。

|阿里云地域|地域ID|接入地址（Endpoint）|
|-----|----|--------------|
|华东 1（杭州）|cn-hangzhou|ecs-vpc.cn-hangzhou.aliyuncs.com|
|华东 2（上海）|cn-shanghai|ecs-vpc.cn-shanghai.aliyuncs.com|
|华北 1（青岛）|cn-qingdao|ecs-vpc.cn-qingdao.aliyuncs.com|
|华北 2（北京）|cn-beijing|ecs-vpc.cn-beijing.aliyuncs.com|
|华北 3（张家口）|cn-zhangjiakou|ecs-vpc.cn-zhangjiakou.aliyuncs.com|
|华北 5（呼和浩特）|cn-huhehaote|ecs-vpc.cn-huhehaote.aliyuncs.com|
|华北 6（乌兰察布）|cn-wulanchabu|ecs-vpc.cn-wulanchabu.aliyuncs.com|
|华南 1（深圳）|cn-shenzhen|ecs-vpc.cn-shenzhen.aliyuncs.com|
|华南 2（河源）|cn-heyuan|ecs-vpc.cn-heyuan.aliyuncs.com|
|华南 3（广州）|cn-guangzhou|ecs-vpc.cn-guangzhou.aliyuncs.com|
|西南 1（成都）|cn-chengdu|ecs-vpc.cn-chengdu.aliyuncs.com|
|中国（香港）|cn-hongkong|ecs-vpc.cn-hongkong.aliyuncs.com|
|新加坡|ap-southeast-1|ecs-vpc.ap-southeast-1.aliyuncs.com|
|澳大利亚（悉尼）|ap-southeast-2|ecs-vpc.ap-southeast-2.aliyuncs.com|
|马来西亚（吉隆坡）|ap-southeast-3|ecs-vpc.ap-southeast-3.aliyuncs.com|
|印度尼西亚（雅加达）|ap-southeast-5|ecs-vpc.ap-southeast-5.aliyuncs.com|
|日本（东京）|ap-northeast-1|ecs-vpc.ap-northeast-1.aliyuncs.com|
|德国（法兰克福）|eu-central-1|ecs-vpc.eu-central-1.aliyuncs.com|
|英国（伦敦）|eu-west-1|ecs-vpc.eu-west-1.aliyuncs.com|
|美国（硅谷）|us-west-1|ecs-vpc.us-west-1.aliyuncs.com|
|美国（弗吉尼亚）|us-east-1|ecs-vpc.us-east-1.aliyuncs.com|
|印度（孟买）|ap-south-1|ecs-vpc.ap-south-1.aliyuncs.com|
|阿联酋（迪拜）|me-east-1|ecs-vpc.me-east-1.aliyuncs.com|

## 方式一（推荐）：SDK内网调用API

使用SDK过程中，只需要简单配置，即可实现内网调用API。Java代码示例如下所示：

```
DefaultProfile profile = DefaultProfile.getProfile("<RegionId>", "<AccessKeyId>", "<AccessKeySecret>");
IAcsClient client = new DefaultAcsClient(profile);

// 全局生效配置。其中，<product>为产品名称，云服务器ECS的值为Ecs。
DefaultProfile.addEndpoint("<RegionId>", "<product>", "<Endpoint>");

// 只对当前请求生效配置。例如，调用DescribeRegions接口。
DescribeRegionsRequest regionsRequest = new DescribeRegionsRequest();
// 如设置下述productNetwork参数，则无需手动设置SysEndpoint。
regionsRequest.setSysEndpoint("<Endpoint>");
// 设置网络。productNetwork参数的取值范围：vpc、 public。
// vpc为内网调用接入地址选项；public为公网调用API的选项，即默认选项。
regionsRequest.productNetwork = "vpc";
DescribeRegionsResponse regionsResponse = client.getAcsResponse(regionsRequest);
```

## 方式二：CLI内网调用API

以接口[DescribeRegions](/cn.zh-CN/API参考/地域/DescribeRegions.md)为例，调用命令示例如下：

```
aliyun ecs DescribeRegions --endpoint ecs-vpc.cn-hangzhou.aliyuncs.com
```

