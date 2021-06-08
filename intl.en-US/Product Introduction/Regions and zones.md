# Regions and zones

This topic provides a complete list of regions and zones of Alibaba Cloud.

Regions are completely independent. Zones are completely isolated. However, zones in the same region can be connected with low-latency links.

## Region

A region is a geographic area where a data center resides. The region of an Alibaba Cloud resource cannot be changed after the resource is created. The following table describes the information about all regions of Alibaba Cloud, including the region IDs and the cities where the regions reside.

-   Regions in mainland China

    |Region|City|Region ID|Number of zones|
    |------|----|---------|---------------|
    |China \(Qingdao\)|Qingdao|cn-qingdao|2|
    |China \(Beijing\)|Beijing|cn-beijing|10|
    |China \(Zhangjiakou\)|Zhangjiakou|cn-zhangjiakou|3|
    |China \(Hohhot\)|Hohhot|cn-huhehaote|2|
    |China \(Ulanqab\)|Ulanqab|cn-wulanchabu|3|
    |China \(Hangzhou\)|Hangzhou|cn-hangzhou|8|
    |China \(Shanghai\)|Shanghai|cn-shanghai|8|
    |China \(Shenzhen\)|Shenzhen|cn-shenzhen|6|
    |China \(Heyuan\)|Heyuan|cn-heyuan|2|
    |China \(Guangzhou\)|Guangzhou|cn-guangzhou|2|
    |China \(Chengdu\)|Chengdu|cn-chengdu|2|
    |China \(Nanjing\)|Nanjing \(in invitational preview\)|cn-nanjing|1|

-   Region outside mainland China

    |Region|City|Region ID|Number of zones|
    |------|----|---------|---------------|
    |China \(Hong Kong\)|Hong Kong|cn-hongkong|3|
    |Singapore \(Singapore\)|Singapore|ap-southeast-1|3|
    |Australia \(Sydney\)|Sydney|ap-southeast-2|2|
    |Malaysia \(Kuala Lumpur\)|Kuala Lumpur|ap-southeast-3|2|
    |Indonesia \(Jakarta\)|Jakarta|ap-southeast-5|3|
    |India \(Mumbai\)|Mumbai|ap-south-1|2|
    |Japan \(Tokyo\)|Tokyo|ap-northeast-1|2|
    |US \(Silicon Valley\)|Silicon Valley|us-west-1|2|
    |US \(Virginia\)|Virginia|us-east-1|2|
    |Germany \(Frankfurt\)|Frankfurt|eu-central-1|2|
    |UK \(London\)|London|eu-west-1|2|
    |UAE \(Dubai\)|Dubai|me-east-1|1|


When you select a region, you must consider the following factors:

-   Geographical location

    Select a region based on the geographical location and of you and your target users.

    -   Mainland China

        In mainland China, we recommend that you select a region that is the closest to the geographical location of your target users to speed up the access. However, in terms of network infrastructure, Border Gateway Protocol \(BGP\) network quality, quality of service \(QoS\), and ease of use and configuration on Elastic Compute Service \(ECS\) instances, Alibaba Cloud regions in mainland China are almost the same. BGP networks ensure fast access to all regions in mainland China.

    -   Outside mainland China
        -   If your target users are located in China \(Hong Kong\) or Southeast Asia, you can select the following regions: China \(Hong Kong\), Singapore \(Singapore\), Malaysia \(Kuala Lumpur\), and Indonesia \(Jakarta\).
        -   If your target users are located in Japan or Korea, you can select the Japan \(Tokyo\) region.
        -   If your target users are located in India, you can select the India \(Mumbai\) region.
        -   If your target users are located in Australia, you can select the Australia \(Sydney\) region
        -   If your target users are located in America, you can select the US \(Silicon Valley\) and US \(Virginia\) regions.
        -   If your target users are located in Continental Europe, you can select the Germany \(Frankfurt\) region.
        -   If your target users are located in Middle East, you can select the UAE \(Dubai\) region.
-   Connection between Alibaba Cloud products

    If you use multiple Alibaba Cloud products together, note the following items:

    -   ECS instances, ApsaraDB for RDS instances, and Object Service Storage \(OSS\) buckets that are created in different regions cannot communicate with each other through internal networks.
    -   Server Load Balancer \(SLB\) cannot balance requests from ECS instances deployed in different regions. ECS instances that you purchased in different regions cannot be deployed under the same SLB instance.
-   Resource price

    The price of resources may vary with regions. For more information, see [Pricing](https://www.alibabacloud.com/pricing).

-   ICP license filing

    When you select a region, you must consider the special requirements of some areas. For example, if you purchase an ECS instance in a region in mainland China and use the instance as a web server, you must apply for an ICP license.

    If you need to apply for an ICP license, note the following items:

    -   If you want to apply for an ICP license for services in Beijing, select the China \(Beijing\) region.
    -   If you want to apply for an ICP license for services in Guangdong, select the China \(Shenzhen\) region.
    **Note:** The Communications Administration of each province in China has specific approval requirements for ICP licenses. For the latest requirements, see the content published on the ICP license application website of the local Communications Administration.


## Zone

A zone is a physical area with independent power grids and networks in a region. The network latency for access between instances within the same zone is shorter.

Zones within the same region have access to each other, but faults within a single zone will not affect the others. We recommend that you choose a deployment method based on your business requirements for disaster recovery and network latency.

-   If your application requires high disaster recovery capabilities, we recommend that you choose multi-zone deployment to create your instances in different zones of the same region.
-   If your application requires low network latency, we recommend that you choose single-zone deployment to create your RDS instances in the same zone.

