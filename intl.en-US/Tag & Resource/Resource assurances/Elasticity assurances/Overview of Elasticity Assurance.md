---
keyword: [resource reservation, elasticity assurance, private resource pool, private pool, pay-as-you-go]
---

# Overview of Elasticity Assurance

Elasticity Assurance offers guaranteed resources to flexibly meet your daily requirements. If you have consistent resource requirements, we recommend that you use Capacity Reservation.

## Introduction

Elasticity Assurance allows you to pay a small assurance fee for guaranteed access to resources for a duration of 1 month up to 5 years. When you purchase an elasticity assurance, you must specify attributes such as zone and instance type. The system generates a private pool for the created elasticity assurance to reserve resources that match the specified attributes. For example, you can purchase an elasticity assurance to reserve resources of the ecs.c6.large instance type in Hangzhou Zone I. You can have guaranteed access to the reserved capacity in the private pool to create pay-as-you-go instances.

An elasticity assurance transitions through the following phases during its lifecycle:

1.  The elasticity assurance is created after you pay for its upfront costs \(assurance fee\).
2.  At any time during the assurance period \(the validity period of the elasticity assurance\), you can use the reserved capacity in the private pool associated with the elasticity assurance to create pay-as-you-go instances.
3.  The elasticity assurance is automatically released when it expires.

    **Note:** Created pay-as-you-go instances are not affected when the associated elasticity assurance is released, and continue to run properly. The instances are billed at the pay-as-you-go rate after they are created.


The following figure shows how an elasticity assurance that reserves resources for two instances is used.

![ea-process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1250482161/p187803.png)

## Benefits

-   Low-cost guaranteed provision of resources: You can purchase elasticity assurances at low costs to reserve resources for specified durations. During these durations, you can use the reserved resources to create pay-as-you-go instances that have matching attributes.
-   Flexibility in time of using resources: Elasticity assurances provide guaranteed access to resources and allow you to create and release pay-as-you-go instances within the reserved capacity at any time over an extended period of time.
-   Use in conjunction with discount plans: Pay-as-you-go instances created from reserved resources in private pools can match savings plans or regional reserved instances to benefit from the billing discounts.

## Billing

You cannot manually release the elasticity assurances that you purchased. When you use an elasticity assurance, you must pay the following fees:

-   Assurance fee generated when you create the elasticity assurance
-   Hourly fees of the pay-as-you-go instances that were created from the reserved resources of the elasticity assurance

    **Note:** If you have purchased applicable savings plans or regional reserved instances, you can apply them to the pay-as-you-go instances.


## Limits

-   Elasticity Assurance is available only for specific instance types in specific regions. For more information, see the buy page.
-   You cannot cancel elasticity assurances or release them before they expire.
-   Reserved resources in a private pool can be used to create only pay-as-you-go instances of the same instance type in the same zone as the associated elasticity assurance.
-   Zonal reserved instances cannot be applied to the pay-as-you-go instances that were created from reserved resources in private pools.

## Scenarios

-   Periodic short-term resource requirements: Elasticity Assurance guarantees the provision of resources when you need to scale your computing resources during a fixed period of time every day, week, or month. Your business is affected if no sufficient resources are available during that period of time. However, you have only small resource requirements during the other periods of time, and consume a small amount of resources in total. In this context, discount plans such as reserved Instances will be underused. For example, a financial SaaS service provider requires a large amount of resources to perform an account check at the beginning of each month, or a rendering enterprise needs to process a number of rendering tasks at the beginning of each week.

    ![short-term-need](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1250482161/p190569.png)

-   Occasional large resource requirements: Elasticity Assurance enables you to reserve resources for urgent use so that you can have fast access to resources to ensure business continuity in case of unexpected events. For example, Internet media needs to report hot news that appears from time to time, or an enterprise needs to reserve resources for disaster recovery.

    ![burst-need](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1250482161/p190570.png)

-   Resource guarantee during special periods: In high-traffic periods such as Double 11 and Spring Festival when resources are strained, Elasticity Assurance helps ensure the normal running of key business and avoid risks caused by resource contention. For example, resources required for key business such as live video streaming, ticket-grabbing, and giveaways need to be guaranteed.

    ![peak-assurance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1250482161/p198908.png)


## Best practices

If a company is attempting to run computing tasks while resources are insufficient, their business is significantly affected and they may encounter the following issues:

-   In use of preemptible instances, clusters may fail to be scaled out due to insufficient resources in a zone.
-   They use pay-as-you-go instances in place of preemptible instances for guaranteed provision of resources, which results in cost increases.
-   They worry that pay-as-you-go instances fail to be created due to unavailability of resources during high-traffic periods such as Double 11. This failure may affect their key business.

Solutions:

1.  Make a resource requirements plan and select zones where resources are sufficient.
2.  Purchase zonal reserved instances and elasticity assurances to reduce pay-as-you-go instance costs while guaranteeing the provision of resources.
    -   Zonal reserved instances can cover resources in consistent use to reduce pay-as-you-go instance costs.
    -   Elasticity assurances can be used to meet daily requirements for elastic resources and reserve resources at lower costs than reserved instances do. Elasticity assurances provide guaranteed resources for your exclusive use to create pay-as-you-go instances even when resources are strained.
    -   You can choose to create pay-as-you-go instances only for key business by using reserved resources in private pools.

