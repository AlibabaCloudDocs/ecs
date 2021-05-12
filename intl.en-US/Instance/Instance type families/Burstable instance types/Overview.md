---
keyword: [What are burstable instances, t5 burstable instances, t6 burstable instances, vCPU credits, distribution, accrual, cumulation, accumulation, standard instances, unlimited instances]
---

# Overview

Burstable instances are an economical instance type that is intended to meet burstable performance requirements in entry-level computing scenarios. This topic describes the features, application scenarios, specific instance families and instance types, baseline performance, CPU credits, and performance modes of burstable instances.

## What are burstable instances?

Burstable instances use CPU credits to ensure computing performance and are suited for scenarios where CPU utilization is typically low but bursts in CPU utilization occur on occasion. You can accumulate CPU credits that can be used to increase the computing performance of burstable instances required by your workloads. This consumption pattern does not affect the environments or applications that are running on your instances. Burstable instances are more flexible and less expensive than other types of instances in terms of CPU utilization.

The CPU credit mechanism allows you to minimize the consumption of resources during off-peak hours and scale resources out during peak hours at no extra cost. If you have unplanned performance requirements, you can enable the unlimited mode for your burstable instances.

Burstable instances include the following instance families:

-   [t6, burstable instance family](#section_6gl_pk7_f56)
-   [t5, burstable instance family](#section_mq2_x7y_0jl)

**Note:** Burstable instances are special shared instances. For more information about other shared instance families, see [Shared instance families](/intl.en-US/Instance/Instance type families/Shared instance families.md).

The following table describes the baseline performance, CPU credits, and performance modes of burstable instances.

|Term|Description|References|
|----|-----------|----------|
|baseline performance|The amount of vCPU capacity that is continuously provisioned to a burstable instance. Baseline performance varies with instance types.|[Baseline performance](#section_dpw_65z_7kv)|
|initial CPU credit|The CPU credits that are provisioned when you create a burstable instance. You can earn 30 initial credits for each vCPU. These credits cannot be replenished after they are used up.|[CPU credits](#section_h4n_jgr_6b4)|
|CPU credit balance|The net credits that are accrued when the earned CPU credits exceed the consumed credits. You can use these credits to run instances above their baseline performance.|[CPU credits](#section_h4n_jgr_6b4)|
|max CPU credit balance|The maximum amount of CPU credits that can be earned by a burstable instance within a 24-hour period. Your CPU credit balance is valid for 24 hours to ensure the availability of CPU credits. A specific instance type earns CPU credits at a fixed rate. Therefore, its CPU credit balance has upper limits.|[CPU credits](#section_h4n_jgr_6b4)|
|performance mode|A burstable instance can run in standard or unlimited mode.

-   A burstable instance in standard mode runs below its baseline performance if its CPU credits are depleted.
-   A burstable instance in unlimited mode allows you to overdraw or pay for additional CPU credits and utilize the CPU above its baseline performance at any time. In this case, you may be charged for using these additional CPU credits.

|[Performance modes](#section_svb_w9d_dju)|
|advance CPU credit|The CPU credits that you can pay for in advance and can receive within 24 hours after you make the payment. You can use advance CPU credits only when you enable the unlimited mode.|[Performance modes](#section_svb_w9d_dju)|
|overdrawn CPU credit|The CPU credits that you use when you have consumed all advance CPU credits to ensure that the instance is running above the baseline performance. You are charged for using these credits. You can use overdrawn CPU credits only when you enable the unlimited mode.|[Performance modes](#section_svb_w9d_dju)|

## Scenarios

When you purchase an enterprise-level instance, its vCPUs are exclusively reserved for you. In this case, you are charged for the vCPU resources regardless of whether you fully utilize the performance of the vCPUs. Even if you require high levels of computing power only for a specific period during a day, you are charged for the remainder of the entire day. To avoid this situation, you can use burstable instances to better suit your business requirements.

Burstable instances apply to scenarios where you require higher-than-normal performance for a specific period, such as stress testing service applications, lightweight applications, microservices, and web application servers. We recommend that you evaluate your business requirements to determine the performance levels required during off-peak and peak hours before you make a purchase. The baseline performance of the instances that you purchase must meet your business requirements during off-peak hours. This way, you can achieve the required performance at significantly lower costs.

**Note:** If the purchased burstable instances cannot meet your requirements, you can change the configurations. For more information, see [Change instance types](#section_vg2_yxn_ore).

## Baseline performance

Baseline performance is the amount of vCPU capacity that is continuously provisioned to a burstable instance. Baseline performance varies based on instance types. You can view the baseline performance of different instance types from the Baseline CPU computing performance column of the instance type tables.

## CPU credits

CPU credits can be described as computing resources that are available for you to use. These computing resources determine the computing performance of your burstable instances. The following section describes the terms and examples related to CPU credits:

-   Initial CPU credits

    When you create a burstable instance, 30 CPU credits are provisioned for each vCPU of the instance, which are initial CPU credits. These credits enable you to complete deployment tasks after you start the instance.

    For example, an ecs.t5-lc1m2.large instance has two vCPUs. You can earn 60 initial CPU credits when you create an instance of this instance type. An ecs.t5-c1m1.xlarge instance has four vCPUs. You can earn 120 initial CPU credits when you create an instance of this instance type.

-   Rate of earning CPU credits

    When a burstable instance is started, it starts to consume CPU credits to maintain its computing performance. At the same time, the instance also earns CPU credits at a fixed rate that is determined by the instance type. The amount of CPU credits that a vCPU can earn per hour varies based on the instance types. The CPU credits per hour column in the instance type tables indicates the CPU credits that all the vCPUs of an instance can earn per hour.

    For example, 25% baseline performance of an ecs.t5-c1m1.large instance indicates that the CPU credits that a vCPU of the instance earns per hour can keep the vCPU running at 25% utilization for 1 hour or at 100% utilization for 15 minutes \(60 × 25%\). In response to its baseline performance, each vCPU earns 15 CPU credits per hour. Therefore, an ecs.t5-c1m1.large instance that has two vCPUs earns 30 CPU credits per hour.

-   CPU credit balance

    If the earned CPU credits exceed the consumed credits, the net credits are accrued as CPU credit balance. Your CPU credit balance is valid for 24 hours to ensure the availability of CPU credits. A specific instance type earns CPU credits at a fixed rate. Therefore, its CPU credit balance is limited. The maximum CPU credit balance of a specific instance type is the number of CPU credits that the instance can earn within 24 hours. For more information, see the Max CPU credit balance column in the instance type tables.

    For example, an ecs.t5-c1m1.large instance can earn 30 CPU credits per hour. The maximum CPU credit balance that the instance can earn is 720 \(30 × 24\) credits.

-   Rate of consuming CPU credits

    The rate of CPU credit consumption of a burstable instance is based on the number of vCPUs, CPU utilization, and operating hours. For example, you consume one CPU credit in the following scenarios:

    -   One vCPU runs at 100% utilization for 1 minute.
    -   One vCPU runs at 50% utilization for 2 minutes.
    -   Two vCPUs run at 25% utilization for 2 minutes.
    When a burstable instance is started, it starts to consume CPU credits to maintain its computing performance. Initial credits that cannot be replenished are consumed first. When the initial credits are used up, the instance consumes the accumulated CPU credits.

    -   When your vCPUs run below the baseline performance, the earned credits are greater than the consumed credits. In this case, the CPU credit balance increases.
    -   When your vCPUs run at the baseline performance, the earned credits are equal to the consumed credits. In this case, the CPU credit balance remains unchanged.
    -   When your vCPUs run above the baseline performance, the earned credits are less than the consumed credits. In this case, the CPU credit balance decreases.

In different scenarios, the operation of stopping your instances may have different impacts on your CPU credits:

-   If a pay-as-you-go instance is stopped while the No Fees for Stopped Instances \(VPC-Connected\) feature is disabled, the current CPU credit balance of the instance is retained, and the instance continues to earn CPU credits.
-   If a pay-as-you-go instance is stopped while the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled, the current CPU credit balance of the instance becomes invalid, and the instance cannot continue to earn credits. When you restart the instance, the instance receives initial credits and starts to earn credits again.
-   If a pay-as-you-go instance is stopped due to overdue payments, its current CPU credit balance is retained, but the instance cannot continue to earn credits until you complete the payment.
-   If a subscription instance expires and is stopped, its current CPU credit balance is retained, but the instance cannot continue to earn credits. When the instance is restarted, it starts to earn credits again.

## Performance modes

A burstable instance can run in standard or unlimited mode.

-   Standard mode

    The performance of a burstable instance in standard mode is based on the availability of CPU credits. After the instance consumes all of its initial credits and accrued CPU credits, the instance cannot run above its baseline performance. When the CPU credit balance is low, the instance gradually reduces performance to its baseline performance within 15 minutes. This way, the instance does not experience a sharp performance drop-off when its accrued CPU credit balance is depleted.

    The standard mode applies to scenarios such as lightweight web servers, development and testing environments, and databases that have low and medium performance. In these scenarios, you have stable workloads, do not need instances to run above the baseline performance for an extended period of time, and may occasionally need burst performance.

-   Unlimited mode

    The performance of a burstable instance in unlimited mode is not limited by the availability of CPU credits. You can overdraw or pay for additional CPU credits to utilize the CPU above the baseline performance at any time. If your instances continue to run above the baseline performance after the initial CPU credits and accrued credits are consumed, the CPU credits change, as shown in the following figure. The following section describes the two concepts involved in the figure:

    -   Advance CPU credits: Advance CPU credits are credits that you can pay for in advance and can receive within 24 hours after you make the payment.
    -   Overdrawn CPU credits: When you have consumed all the advance CPU credits, overdrawn CPU credits are used to ensure that the instance can run above the baseline performance. You are charged for using overdrawn CPU credits.
    **Note:** For more information about the billing of burstable instances, see [Impact of performance modes on billing](/intl.en-US/Instance/Instance type families/Burstable instance types/Billing.md).

    ![Advance CPU credits and overdrawn CPU credits](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7690359951/p45325.png)

    You can enable the unlimited mode for your burstable instances if you need to consume advance CPU credits or overdrawn CPU credits in addition to your credit balance to meet burstable performance requirements. Examples:

    -   Some events such as new feature releases, e-commerce promotions, and website promotions cause a substantial increase to your workloads. High CPU performance is required during this period of time. In this case, you can enable the unlimited mode for your burstable instances. You can disable the mode to save costs when the workload peak ends.
    -   Some web applications may require CPU bursts for a specific period during a day, but the daily average CPU utilization is below the baseline CPU utilization. In this case, you can enable the unlimited mode for your instances during peak hours to ensure a positive customer experience. If the CPU credits that you have earned during off-peak hours can offset the advance CPU credits that you consumed during peak hours, you can ensure a positive customer experience at no additional costs.

By default, when you create a burstable instance, the standard mode is enabled. For more information about how to enable the unlimited mode, see [Enable the unlimited mode](/intl.en-US/Instance/Instance type families/Burstable instance types/Switch the performance mode of a burstable instance.md).

For more information about how the CPU credits change when an instance is running in different performance modes, see [CPU credit change examples](/intl.en-US/Instance/Instance type families/Burstable instance types/CPU credit change examples.md).

## Change instance types

When you monitor a burstable instance, you may find that the vCPUs are running above or below their baseline performance on a constant basis. This indicates that the instance type is not suitable for your business. We recommend that you re-evaluate the instance type to decide whether to select another burstable or enterprise-level instance type. For more information, see [Instance families that support instance type changes](/intl.en-US/Instance/Change configurations/Instance families that support instance type changes.md).

The operation of changing instance types varies based on the billing methods. For more information, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md).

## t6, burstable instance family

Features

-   Provides baseline CPU performance and is burstable but limited by accrued CPU credits.
-   Is more cost-effective when compared with the t5 burstable instance family.
-   Compute:
    -   Uses 2.5 GHz Intel® Xeon® Cascade Lake processors that deliver a turbo frequency of 3.2 GHz.
    -   Uses the DDR4 memory.
-   Storage:
    -   Supports enhanced SSDs \(ESSD\), standard SSDs, and ultra disks.

        **Note:** PL2 and PL3 ESSDs cannot provide maximum performance due to the specification limits of burstable instances. We recommend that you use enterprise-level instances or ESSDs that are at lower performance levels.

-   Network:
    -   Supports IPv6.
    -   Supports only VPCs.
    -   Delivers a bandwidth of up to 4 Gbit/s.
-   Suits the following scenarios:
    -   Web application servers
    -   Lightweight applications and microservices
    -   Development and testing environments

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline CPU computing performance|CPU credits per hour|Max CPU credit balance|Base bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|--------------|:---------------------------------|:-------------------|:---------------------|-------------------------|-------------------------------|----------|:---|----------------------------|
|ecs.t6-c4m1.large|2|0.5|5%|6|144|0.08|40|1|2|2|
|ecs.t6-c2m1.large|2|1.0|10%|12|288|0.08|60|1|2|2|
|ecs.t6-c1m1.large|2|2.0|20%|24|576|0.08|100|1|2|2|
|ecs.t6-c1m2.large|2|4.0|20%|24|576|0.08|100|1|2|2|
|ecs.t6-c1m4.large|2|8.0|30%|36|864|0.08|100|1|2|2|
|ecs.t6-c1m4.xlarge|4|16.0|40%|96|2,304|0.16|200|1|2|6|
|ecs.t6-c1m4.2xlarge|8|32.0|40%|192|4,608|0.32|400|1|2|6|

**Note:**

-   When you bind elastic network interfaces \(ENIs\) to or unbind ENIs from instances of the following instance types, the instances must be in the Stopped state: ecs.t6-c1m1.large, ecs.t6-c1m2.large, ecs.t6-c1m4.large, ecs.t6-c2m1.large, and ecs.t6-c4m1.large.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

## t5, burstable instance family

Features

-   Provides baseline CPU performance and is burstable but limited by accrued CPU credits.
-   Offers a balance between compute, memory, and network resources.
-   Compute:
    -   Offers multiple CPU-to-memory ratios.
    -   Uses 2.5 GHz Intel® Xeon® processors.
    -   Uses the DDR4 memory.
-   Network:
    -   Supports IPv6.
    -   Supports only VPCs.
-   Suits the following scenarios:
    -   Web application servers
    -   Lightweight applications and microservices
    -   Development and testing environments

Instance types

|Instance type|vCPUs|Memory \(GiB\)|Baseline CPU computing performance|CPU credits per hour|Max CPU credit balance|Disk bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|NIC queues|ENIs|Private IP addresses per ENI|
|:------------|:----|--------------|:---------------------------------|:-------------------|:---------------------|-------------------------|-------------------------------|----------|:---|----------------------------|
|ecs.t5-lc2m1.nano|1|0.5|20%|12|288|0.1|40|1|2|2|
|ecs.t5-lc1m1.small|1|1.0|20%|12|288|0.2|60|1|2|2|
|ecs.t5-lc1m2.small|1|2.0|20%|12|288|0.2|60|1|2|2|
|ecs.t5-lc1m2.large|2|4.0|20%|24|576|0.4|100|1|2|2|
|ecs.t5-lc1m4.large|2|8.0|20%|24|576|0.4|100|1|2|2|
|ecs.t5-c1m1.large|2|2.0|25%|30|720|0.5|100|1|2|2|
|ecs.t5-c1m2.large|2|4.0|25%|30|720|0.5|100|1|2|2|
|ecs.t5-c1m4.large|2|8.0|25%|30|720|0.5|100|1|2|2|
|ecs.t5-c1m1.xlarge|4|4.0|25%|60|1440|0.8|200|1|2|6|
|ecs.t5-c1m2.xlarge|4|8.0|25%|60|1440|0.8|200|1|2|6|
|ecs.t5-c1m4.xlarge|4|16.0|25%|60|1440|0.8|200|1|2|6|
|ecs.t5-c1m1.2xlarge|8|8.0|25%|120|2,880|1.2|400|1|2|6|
|ecs.t5-c1m2.2xlarge|8|16.0|25%|120|2,880|1.2|400|1|2|6|
|ecs.t5-c1m4.2xlarge|8|32.0|25%|120|2,880|1.2|400|1|2|6|
|ecs.t5-c1m1.4xlarge|16|16.0|25%|240|5,760|1.2|600|1|2|6|
|ecs.t5-c1m2.4xlarge|16|32.0|25%|240|5,760|1.2|600|1|2|6|

**Note:**

-   When you bind ENIs to or unbind ENIs from instances of the following instance types, the instances must be in the Stopped state: ecs.t5-lc2m1.nano, ecs.t5-c1m1.large, ecs.t5-c1m2.large, ecs.t5-c1m4.large, ecs.t5-lc1m1.small, ecs.t5-lc1m2.large, ecs.t5-lc1m2.small, and ecs.t5-lc1m4.large.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Description of instance specifications](/intl.en-US/Instance/Instance families.md).

