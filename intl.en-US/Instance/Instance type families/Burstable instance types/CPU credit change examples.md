# CPU credit change examples

After a burstable instance is created, its CPU credits change based on the relationship between its CPU utilization and the baseline performance. This topic describes how the CPU credits change for a burstable instance in different performance modes.

## Background information

The examples given in this topic are used to describe concepts such as baseline performance and CPU credits. Actual business scenarios may be more complex and variable than those provided in these examples. For example, the CPU utilization is unlikely to remain at a constant value for very long. We recommend that you select appropriate instances based on your understanding of burstable instance-related concepts and manage the performance modes or configurations of the instances to suit your needs. For more information, see [Switch the performance mode of a burstable instance](/intl.en-US/Instance/Instance type families/Burstable instance types/Switch the performance mode of a burstable instance.md) or [Change instance types](/intl.en-US/Instance/Instance type families/Burstable instance types/Overview.md).

Before you read the examples, take note of the following items:

-   After a burstable instance is created, each of its vCPUs can earn 30 initial CPU credits.
-   The consumption rate of CPU credits of a burstable instance is subject to the number of vCPUs, CPU utilization, and instance running hours. One CPU credit is equal to one vCPU at 100% utilization for one minute. When the actual performance is other values, the running time is converted proportionally.
-   When a burstable instance runs at the baseline performance level, the CPU credits it earns are equal to the CPU credits it consumes.

For more information, see [Baseline performance](/intl.en-US/Instance/Instance type families/Burstable instance types/Overview.md) and [CPU credits](/intl.en-US/Instance/Instance type families/Burstable instance types/Overview.md).

## Standard mode

A burstable instance in standard mode cannot burst above the performance baseline after its initial CPU credits and CPU credit balance are depleted.

The following figure shows how the CPU credits of an ecs.t6-c2m1.large instance that runs in standard mode change. The instance has 2 vCPUs and 1 GiB memory. Take note of the following items:

-   The instance has two vCPUs and can earn 60 initial CPU credits.
-   The performance baseline of the instance is 10%.
-   The instance earns 12 CPU credits per hour and has a CPU credit balance limit of 288. For more information about the instance type, see the "t6, burstable instance family" section of the [Overview](/intl.en-US/Instance/Instance type families/Burstable instance types/Overview.md) topic.
-   The instance has two vCPUs and consumes 12 CPU credits per hour when it runs at the baseline performance level.

![Standard mode](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3163416161/p45896.png)

The following section describes how CPU credits change in different phases shown in the preceding figure.

-   0 h ~ 24 h

    Phase A: 60 initial CPU credits are earned on instance startup. The CPU utilization is 0%. The CPU credit balance keeps increasing until it reaches the limit in a 24-hour period after startup.

    At the end of these hours, the instance has a CPU credit balance of 348, which is calculated based on the following formula: 60 initial credits + 288 maximum credit balance.

-   25 h ~ 48 h
    1.  Phase B: The CPU utilization is 10%, which is equal to the performance baseline. The initial CPU credits are consumed first. When the instance is running, 12 CPU credits are consumed per hour. After the 60 initial CPU credits are consumed, the instance cannot obtain more initial CPU credits.

        At the end of these hours, the instance has a CPU credit balance of 288, which is calculated based on the following formula: 348 available credits at the end of Phase A - 60 consumed initial credits.

    2.  Phase C: The CPU utilization is 5%, which is below the performance baseline. However, the CPU credit balance has reached the upper limit and remains constant.

        At the end of these hours, the credit balance is 288 and is equal to the maximum CPU credit balance.

    3.  Phase D: The CPU utilization is 10%, which is equal to the performance baseline. The instance earns and consumes equal CPU credits, and the CPU credit balance remains constant.

        At the end of these hours, the credit balance is 288 and is equal to the maximum CPU credit balance.

-   49 h ~ 72 h
    1.  Phase E: The CPU utilization is 100%. The instance runs for 2 hours and consumes 120 CPU credits per hour. In this case, the baseline performance cannot meet requirements, and the instance begins to consume the CPU credit balance.

        At the end of these hours, the instance has a CPU credit balance of 72, which is calculated based on the following formula: 288 maximum CPU credit balance - 2 × 120 credits consumed per hour + 2 × 12 credits earned per hour.

    2.  Phase F: The CPU utilization is 0%. The instance is idle for 4 hours and earns 12 CPU credits per hour. All earned credits are accrued in the credit balance.

        At the end of these hours, the instance has a CPU credit balance of 120, which is calculated based on the following formula: 72 credit balance at the end of Phase E + 4 × 12 credits earned per hour.

    3.  Phase G: The CPU utilization is 5%. The instance runs for 8 hours and consumes 6 CPU credits per hour. The unconsumed credits are accrued in the credit balance.

        At the end of these hours, the instance has a CPU credit balance of 168, which is calculated based on the following formula: 120 credit balance at the end of Phase F - 8 × 6 credits consumed per hour + 8 × 12 credits earned per hour.

    4.  Phase H: The CPU utilization is 80%, and the baseline performance cannot meet requirements. The instance runs for 2 hours and consumes 96 CPU credits per hour. The CPU credit balance is depleted. When the instance runs in standard mode and has no available CPU credits, it cannot burst beyond the performance baseline.

        **Note:** When the CPU credit balance is low, the instance gradually reduces performance to its baseline level within 15 minutes. This way, the instance does not experience a sharp performance drop-off when its accrued CPU credit balance is depleted.

        At the end of these hours, the instance has a CPU credit balance of zero, which is calculated based on the following formula: 168 credit balance at the end of Phase G - 2 × 96 credits consumed per hour + 2 × 12 credits earned per hour.

    5.  Phase I: The CPU utilization is 10%, which is equal to the performance baseline. The instance earns and consumes equal CPU credits, and the CPU credit balance remains constant.

        At the end of this these hours, the instance has a CPU credit balance of zero, which is calculated based on the following formula: 0 credit balance at the end of Phase H - 5 × 12 credits consumed per hour + 5 × 12 credits earned per hour.

    6.  Phase J: The CPU utilization is 0%. The instance is idle for 3 hours and earns 12 CPU credits per hour. All earned credits are accrued in the credit balance.

        At the end of these hours, the instance has a CPU credit balance of 36, which is calculated based on the following formula: 0 credit balance at the end of Phase I + 3 × 12 credits earned per hour.


## Unlimited mode

The performance of a burstable instance in unlimited mode is not limited by the availability of CPU credits. You can overdraw or pay for additional CPU credits to obtain performance boosts at any time.

The following figure shows how the CPU credits of an ecs.t6-c1m1.large instance that runs in unlimited mode change. The instance has 2 vCPUs and 2 GiB memory. Take note of the following items:

-   The instance has two vCPUs and can earn 60 initial CPU credits.
-   The instance has a performance baseline of 20%.
-   The instance earns 24 CPU credits per hour and has a CPU credit balance limit of 576. For more information about the instance type, see the "t6, burstable instance family" section of the [Overview](/intl.en-US/Instance/Instance type families/Burstable instance types/Overview.md) topic.
-   The instance has two vCPUs and consumes 24 CPU credits per hour when it runs at the baseline performance level.

![Unlimited mode](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3163416161/p46048.png)

The following section describes how CPU credits change in different phases shown in the preceding figure.

-   0 h ~ 24 h

    Phase A: 60 initial CPU credits are earned on instance startup. The CPU utilization is 0%. The CPU credit balance keeps increasing until it reaches the limit in a 24-hour period after startup.

    At the end of these hours, the instance has a CPU credit balance of 636, which is calculated based on the following formula: 60 initial credits + 576 maximum CPU credit balance.

-   25 h ~ 48 h
    1.  Phase B: The CPU utilization is 20%, which is equal to the performance baseline. The initial CPU credits are consumed first. When the instance is running, 24 CPU credits are consumed per hour. After the 60 initial CPU credits are consumed, the instance cannot obtain more initial CPU credits.

        At the end of these hours, the instance has a CPU credit balance of 576, which is calculated based on the following formula: 636 credits at the end of Phase A - 60 consumed initial credits.

    2.  Phase C: The CPU utilization is 20%, which is equal to the performance baseline. The instance earns and consumes equal CPU credits, and the CPU credit balance remains constant.

        At the end of these hours, the CPU credit balance of the instance is 576 and is equal to the maximum CPU credit balance.

    3.  Phase D: The CPU utilization is 10%, which is below the performance baseline. However, the CPU credit balance has reached the upper limit and remains constant.

        At the end of these hours, the CPU credit balance of the instance is 576 and is equal to the maximum CPU credit balance.

    4.  Phase E: The CPU utilization is 100%. When the instance is running, it consumes 120 CPU credits per hour. In this case, the baseline performance cannot meet requirements, and the instance begins to consume the CPU credit balance.

        At the end of these hours, the CPU credit balance is depleted.

    5.  Phase F: The CPU utilization is 100%. When the instance is running, it consumes 120 CPU credits per hour. In this case, the baseline performance cannot meet requirements, and the instance begins to consume the advance CPU credits. For more information, see the "performance modes" section of the [Overview](/intl.en-US/Instance/Instance type families/Burstable instance types/Overview.md) topic.

        At the end of these hours, the advance CPU credits are depleted, and a total of 576 CPU credits are overdrawn.

    6.  Phase G: The CPU utilization is 100%. When the instance is running, it consumes 120 CPU credits per hour. In this case, the baseline performance cannot meet requirements, and the instance begins to consume the overdrawn CPU credits. For more information, see the "performance modes" section in [Overview](/intl.en-US/Instance/Instance type families/Burstable instance types/Overview.md).

        At the end of these hours, the CPU credit balance remain constant, and 576 CPU credits are overdrawn.

-   49 h ~ 72 h

    Phase H: The CPU utilization is 0%. The earned CPU credits preferentially pay down the consumed advance CPU credits and can pay off the advanced CPU credits in 72 hours.

    At the end of these hours, no overdrawn CPU credits are available, but the CPU credit balance is still 0.

-   73 h ~ 96 h

    Phase H: The CPU utilization is 0%. The instance is idle for 24 hours and earns 24 CPU credits per hour. All earned credits are accrued in the credit balance until the credit balance reaches the limit in a 96-hour period.

    At the end of these hours, the CPU credit balance is 576 and is equal to the maximum CPU credit balance.


