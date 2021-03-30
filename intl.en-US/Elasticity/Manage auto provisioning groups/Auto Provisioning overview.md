# Auto Provisioning overview

Auto Provisioning is a service that allows quick deployment of instance clusters. Auto Provisioning supports one-click deployment of instance clusters that use multiple billing methods across instance types and zones. You can use auto provisioning groups to provide stable computing power, alleviate the instability caused by the reclaiming of preemptible instances, and eliminate the need to manually create instances.

## Introduction to Auto Provisioning

To use Auto Provisioning, you must create auto provisioning groups. Auto provisioning groups can create instance clusters based on the specified target capacities, resource pools, and provisioning policies. Auto provisioning groups eliminate the need to track the creation processes or calculate costs of individual instances. If you select Continuous Delivery and Maintain Capacity when you create an auto provisioning group, the created group automatically compares the real-time and target capacities. When preemptible instances are reclaimed, the auto provisioning group creates instances to maintain the target capacity to meet your computing power needs at the lowest costs.

The following figure shows how an auto provisioning group works.

![Auto provisioning group](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0190707161/p48772.png)

## Scenarios

Similar to preemptible instances, auto provisioning groups are applicable to stateless application scenarios such as scalable website services, image rendering, big data analytics, and parallel computing.

Preemptible instances provide computing resources at lower costs. However, preemptible instances can be reclaimed. You must closely monitor for preemptible instances that are about to be reclaimed so that you can create new ones. The more preemptible instances you maintain, the higher the maintenance costs are.

To solve these issues, you can use an auto provisioning group to deploy an instance cluster with one click. You can configure computing power provisioning methods, resource pools, and provisioning policies for the auto provisioning group to meet your computing power needs at the lowest costs.

## Features

-   Flexible computing power delivery methods

    The target capacity for an auto provisioning group is set based on the number of instances or vCPUs. Auto Provisioning uses weights to indicate the capacity of a single instance in an auto provisioning group. For more information, see [Create an auto provisioning group](/intl.en-US/Elasticity/Manage auto provisioning groups/Create an auto provisioning group.md).

-   Multi-zone and multi-instance types

    Auto provisioning groups can create instances across multiple instance types and zones. After you specify instance types and zones, a resource pool is created for each specified instance type in each specified zone. To improve the success rate of creating instances and the disaster recovery capability of applications, we recommend that you select multiple instance types and zones to create multiple alternative resource pools. Auto provisioning groups attempt to create instance clusters based on your settings. When the resources of a resource pool is insufficient, the auto provisioning group automatically uses another resource pool that has sufficient resources to create instances.

    **Note:** If you select multiple vSwitches within one zone, only the first vSwitch takes effect.

    For example, if Balanced Distribution Policy is selected, the auto provisioning group first attempts to create instances across zones. However, if instances cannot be created due to insufficient resources in the resource pools of one zone, the auto provisioning group then attempts to create instances by using resource pools in another zone.

-   Flexible provisioning policies

    Preemptible instances support the capacity optimization policy, cost optimization policy, and balanced distribution policy. Pay-as-you-go instances support the cost optimization policy and priority-based policy.

    **Note:** You can specify the provisioning policy for preemptible instances by using the ECS console or by calling an API operation. You can specify the provisioning policy for pay-as-you-go instances by calling an API operation.

    -   When the capacity optimization policy is used, the auto provisioning group creates instance clusters that have high success rate of instance creation at a lower cost based on the prices and reclaim rates of preemptible ECS instances. This can effectively reduce the number of times preemptible instances that are reclaimed and ensure stable capacity.
    -   When the cost optimization policy is used, the auto provisioning group uses the most cost-effective resource pools to create instances. This can effectively reduce costs and eliminate the need to manually compare prices.

        If you create an auto provisioning group by calling the [CreateAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/CreateAutoProvisioningGroup.md) operation, you can specify to use the cost optimization policy by setting SpotAllocationStrategy and PayAsYouGoAllocationStrategy and specify the allowed number of resource pools by setting SpotInstancePoolsToUseCount. In this case, you can use the cost-effective resource pools to meet your capacity needs. For example, assume that the target capacity is 100 instances and SpotInstancePoolsToUseCount is set to 5. In this case, 20 instances are created in each resource pool. When the preemptible instances corresponding to a single resource pool are reclaimed, preemptible instances of other resource pools are still available. This can improve service availability.

    -   When the balanced distribution policy is used, the auto provisioning group attempts to create instances across multiple zones in a balanced manner to avoid instance creation failures caused by insufficient resources in a single zone. This can effectively improve the disaster recovery capabilities of applications.
    -   When the priority-based policy is used, the auto provisioning group attempts to create instances in descending order of the priorities of resource pools.

        If you create an auto provisioning group by calling the [CreateAutoProvisioningGroup](/intl.en-US/API Reference/Auto provisioning group/CreateAutoProvisioningGroup.md) operation, you can specify to use the priority-based policy by setting PayAsYouGoAllocationStrategy and specify the priorities of extended instance configurations by setting LaunchTemplateConfig.N.Priority.The low-priority resource pool is used to create instances only when resources of the high-priority resource pool are insufficient.

-   Multiple billing methods

    Preemptible instances are cost-effective, but are available only when resources are sufficient and can be reclaimed. Pay-as-you-go instances prevail preemptible instances in terms of guaranteeing the inventory. You can create and release pay-as-you-go instances at any time, but these instances are more costly than preemptible instances. Instance clusters created by the auto provisioning group can contain both preemptible instances and pay-as-you-go instances. You can use preemptible instances to reduce costs and use some pay-as-you-go instances to ensure that the minimum computing power is met.

-   Complete cost control

    Auto provisioning groups allow you to set the global maximum hourly price for preemptible instances and the maximum hourly price for a single instance type. You can set the prices based on your budget.

-   Practical protection mechanism

    Auto provisioning groups provide the instance shutdown settings. You can configure the settings to specify whether to stop the instances in the group when an auto provisioning group expires or when instances exceed the target capacity. Auto provisioning groups perform routine health checks on instances and replace unhealthy instances in a timely manner to ensure availability of instances.


## Billing

Auto Provisioning is available free of charge. However, you are charged for ECS instances created by auto provisioning groups. Auto Provisioning supports creating preemptible instances and pay-as-you-go instances. For more information about billing, see [Overview](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Overview.md) and [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md).

**Warning:** Make sure that you have sufficient balance in your account. If you have overdue payments, all pay-as-you-go instances and preemptible instances are stopped. For more information, see [Settlement cycle](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md). In this case, the auto provisioning group cannot create ECS instances. The group determines the stopped instances to be unhealthy based on the health check results and then removes and releases unhealthy instances.

## Limits

-   Auto provisioning groups cannot provide resources across regions.
-   An auto provisioning group can include a maximum of 20 resource pools, each of which is a combination of a zone and an instance type.
-   A maximum of 1,000 instances can be created in each auto provisioning group.
-   You can specify a single version of a specified launch template for each auto provisioning group but you cannot extend the template. For more information, see [Create an auto provisioning group](/intl.en-US/Elasticity/Manage auto provisioning groups/Create an auto provisioning group.md).

