---
keyword: [subscription, pay-as-you-go, pay-by-bandwidth, pay-by-traffic, public IP address, outbound bandwidth, inbound bandwidth, bandwidth billing]
---

# Public bandwidth

This topic describes public bandwidth types, billing methods for network usage, and examples on how to calculate network usage fees.

## Billing overview

An Elastic Compute Service \(ECS\) instance can access the Internet by using the following methods:

-   Public IP address

    Public IP addresses are assigned by the system. You are not charged for retaining public IP addresses. You are charged only for the outbound public bandwidth. Two billing methods for network usage are available: pay-by-bandwidth and pay-by-traffic.

-   Elastic IP address \(EIP\)

    EIPs are public IP addresses that you can separately purchase and use. Only instances that are deployed in virtual private clouds \(VPCs\) support EIPs. For information about the billing details of EIPs, see [Overview](/intl.en-US/Pricing/Overview.md).

-   NAT gateway

    NAT gateways are Internet gateways that can be separately purchased. For information about the billing details of NAT gateways, see [Billing overview](/intl.en-US/Pricing/Billing overview.md).


This topic describes how to use public IP addresses to access the Internet and the billing methods for network usage. After an ECS instance is assigned a public IP address, you can use the instance to access the Internet and receive requests from the Internet. The following table describes the related public bandwidth types.

|Public bandwidth type|Charged|Description|Example|
|---------------------|-------|-----------|-------|
|outbound bandwidth|Yes|The bandwidth for traffic from ECS instances to the Internet.|FTP clients download resources from ECS instances by using public IP addresses.|
|inbound bandwidth|No|The bandwidth for traffic from the Internet to ECS instances.|FTP clients upload resources to ECS instances by using public IP addresses.|

**Note:** You are not charged for internal bandwidth usage. Within the same region, you are not charged for traffic generated when ECS instances communicate with each other or with other Alibaba Cloud services by using private IP addresses. For example, communication between Alibaba Cloud services that belong to the same VPC is free of charge. If an ECS instance communicates with other Alibaba Cloud services over the Internet, you are charged for the outbound bandwidth. For example, you are charged for communication between an instance from the China \(Hangzhou\) region and an instance from the China \(Shanghai\) region.

For information about the limits on the public bandwidth of ECS instances, see [Limits](/intl.en-US/Product Introduction/Limits.md).

## Billing methods for network usage

Two billing methods for network usage are available: pay-by-bandwidth and pay-by-traffic.

-   Pay-by-bandwidth: You are charged based on the bandwidth that you specify. The actual outbound bandwidth does not exceed the specified bandwidth.
-   Pay-by-traffic: a pay-as-you-go billing method. You are charged for the traffic that you actually used. You must configure a peak bandwidth for outbound traffic to avoid unmanageable fees incurred by outbound traffic bursts.

    **Note:** When the **pay-by-traffic** billing method for network usage is used, the peak inbound and outbound bandwidths are both the upper limits of bandwidths and are for reference only. In the event of resource contention, these peak bandwidths cannot be guaranteed. If you want guaranteed bandwidths for your instance, use the **pay-by-bandwidth** billing method for network usage.


**Note:** You can also purchase a data transfer plan to offset the network traffic fees. For more information, see the [Data Transfer Plan](https://www.alibabacloud.com/help/zh/product/55093.htm) documentation.

The pricing of bandwidth varies based on regions. For more information, see the [Pricing](https://www.alibabacloud.com/zh/product/ecs#pricing) tab on the Elastic Compute Service page. The following table describes the billing methods for network usage and their relationship with billing methods of ECS instances.

|Billing method for network usage|Billing method of ECS instances|Billing rule for network usage|
|--------------------------------|-------------------------------|------------------------------|
|Pay-by-bandwidth|Subscription|You must pay for the bandwidth and subscription duration that you purchased in advance. You are charged for the bandwidth \(Mbit/s\) based on a tiered billing system. Unit: USD/month. -   1-5 Mbit/s: Each bandwidth value corresponds to a unit price.
-   ≥ 6 Mbit/s: You are charged on a Mbit/s basis. |
|Pay-as-you-go|Bandwidth bills are accurate to seconds. The bills are generated on the hour every hour. You are charged for the bandwidth \(Mbit/s\) based on a tiered billing system. Unit: USD/hour. -   1-5 Mbit/s: Each bandwidth value corresponds to a unit price.
-   ≥ 6 Mbit/s: You are charged on a Mbit/s basis. |
|Pay-by-traffic|Subscription and pay-as-you-go|The bills are generated on the hour every hour. You are charged based on the volume of traffic \(GB\) that you used. Unit: USD/GB.|

## Billing examples

The following table describes how you are billed for network usage. Instances in the China \(Hangzhou\) region are used in the examples.

**Note:** The unit price is for reference only and the prices on the Pricing tab of the Elastic Compute Service page prevail.

|Billing method for network usage|Billing method of ECS instances|Example of billing conditions|Fee \(USD\)|
|:-------------------------------|-------------------------------|-----------------------------|-----------|
|Pay-by-bandwidth|Subscription|-   Usage period: one month
-   Bandwidth value: 2 Mbit/s
-   Unit price for 2 Mbit/s: USD 6.8 per month

|1 × 6.8 = 6.8|
|-   Usage period: one month
-   Bandwidth value: 7 Mbit/s
-   Unit price for 5 Mbit/s: USD 17 per month
-   Unit price for 6 Mbit/s or higher: USD 11.8 per month

|1 × \[17 + \(7 - 5\) × 11.8\] = 40.6|
|Pay-as-you-go|-   Usage period: one month
-   Bandwidth value: 2 Mbit/s
-   Unit price for 2 Mbit/s: USD 0.012 per hour

|24 × 30 × 0.012 = 8.64|
|-   Usage period: one month
-   Bandwidth value: 7 Mbit/s
-   Unit price for 5 Mbit/s: USD 0.03 per hour
-   Unit price for 6 Mbit/s or higher: USD 0.021 per hour

|24 × 30 × \[0.03 + \(7 - 5\) × 0.021\] = 51.84|
|Pay-by-traffic|Subscription and pay-as-you-go|-   Consumed traffic: 1 GB
-   Unit price: USD 0.123 per GB
-   Usage period: N/A. You are charged based on the amount of traffic that you actually used.

|1 × 0.123 = 0.123|

## References

You can change the billing method for network usage from pay-by-bandwidth to pay-by-traffic, or from pay-by-traffic to pay-by-bandwidth. For more information, see [Change the billing method for network usage](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Change the billing method for network usage.md).

If the current public bandwidth does not meet your business requirements, you can upgrade or downgrade the public bandwidth. For more information, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md).

