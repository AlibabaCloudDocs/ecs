---
keyword: [billing method, subscription, pay-as-you-go, comparison of billing methods]
---

# Billing method overview

You can choose an appropriate billing method based on ECS resource types. This topic describes all types of billing methods and the comparison between subscription and pay-as-you-go.

## Major billing methods

The following table describes the major billing methods of ECS resources: subscription and pay-as-you-go.

|Billing method|Applicable resource|Description|Reference|
|--------------|-------------------|-----------|---------|
|Subscription|-   Computing resource \(vCPUs and memory\)
-   Image
-   Cloud disk
-   Public bandwidth

|A billing method that allows you to use ECS resources only after you pay for them. Subscription is applicable to services that run for 24 hours a day and 7 days a week, such as web services. You must pay for subscription resources before you can use them.|[Subscription](/intl.en-US/Pricing/Billing methods/Subscription.md)|
|Pay-as-you-go|-   Computing resource \(vCPUs and memory\)
-   Image
-   Cloud disk
-   Public bandwidth
-   Snapshot

|A billing method that allows you to use ECS resources before you pay for them. Pay-as-you-go is applicable to applications or services that experience traffic spikes, such as temporary scaling, interim testing, and scientific computing. You can activate and use pay-as-you-go resources before you pay for them. The system generates bills in each billing cycle and deducts corresponding fees from your account.|[Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md)|

Subscription ECS instances and pay-as-you-go ECS instances support different features. The following table lists the differences.

|Feature|Subscription|Pay-as-you-go|
|-------|------------|-------------|
|Release instances at any time|-   To release an instance before it expires, you must first change its billing method from subscription to pay-as-you-go.
-   After an instance expires, if you do not renew the instance within the required period of time, the instance is automatically released.

|Supported.Release pay-as-you-go instances that you no longer need as soon as possible. If you do not release them, the ECS resources are continuously charged until the instances are stopped and released due to overdue payments. |
|Change instance types|Supported.|Supported.|
|Change bandwidth configurations|Supported.|Supported.|
|Change billing methods|Supported.|Supported.|
|Use subscription images from Alibaba Cloud Marketplace|Supported.|Not supported.|
|Apply for ICP filings for websites that are deployed on ECS instances in mainland China|Supported.You can apply for ICP filings only for ECS instances that have a subscription period of at least three months.

|Not supported.|
|Create instances by calling API operations|Supported.|Supported.|
|Use Alibaba Cloud Security, Cloud Monitor, and Server Load Balancer \(SLB\) for free|Supported.|Supported.|

## Other billing methods

In addition to subscription and pay-as-you-go, Alibaba Cloud provides other billing methods for different ECS resources. You can use these billing methods to reduce costs.

|Billing method|Applicable resource|Description|Reference|
|--------------|-------------------|-----------|---------|
|Reserved instance|-   Computing resource \(vCPUs and memory\)
-   Image

|Reserved instances are coupons that can be used to offset bills of pay-as-you-go instances.|[Reserved instances](/intl.en-US/Pricing/Billing methods/Reserved instances.md)|
|Preemptible instance|Computing resource \(vCPUs and memory\)|Preemptible instances are on-demand instances that you can use before you pay. Preemptible instances offer some discounts compared with pay-as-you-go instances and are charged based on the actual usage duration. Prices of preemptible instances fluctuate based on the changes to supply and demand.|[Preemptible instances](/intl.en-US/Pricing/Billing methods/Preemptible instances.md)|
|SCU|Cloud disk and snapshot|Storage capacity units \(SCUs\) are storage resource plans that can be used to offset bills of different pay-as-you-go storage resources.|[SCU billing methods](/intl.en-US/Pricing/Billing methods/SCU billing methods.md)|
|Data transfer plan|Public bandwidth|Data transfer plans are effective and economical solutions that can be used to offset bills of IPv4 traffic on a pay-as-you-go basis.|[Data Transfer Plan](https://www.alibabacloud.com/help/zh/product/55093.htm)|

