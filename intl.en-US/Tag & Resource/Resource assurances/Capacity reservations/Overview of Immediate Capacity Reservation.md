# Overview of Immediate Capacity Reservation

You can purchase immediate capacity reservations to reserve and lock down capacity for pay-as-you-go instances. Immediate capacity reservations take effect immediately after they are created, and are applicable to scenarios where resource requirements are large.

## Introduction

You can reserve capacity at any time by purchasing an immediate capacity reservation. After you purchase an immediate capacity reservation, the specified resources are reserved and locked down for your exclusive use. An immediate capacity reservation begins to be billed at the pay-as-you-go instance rate as soon as the capacity reservation takes effect. Billing continues regardless of whether the capacity reservation is actually used to create instances. Billing stops when the capacity reservation is released.

When you purchase an immediate capacity reservation, you must specify attributes such as zone, instance type, and operating system. The system generates a private pool in which to reserve resources that match the specified attributes. You have guaranteed access to the reserved capacity in the private pool to create pay-as-you-go instances.

**Note:** Savings plans and regional reserved instances can be applied to the pay-as-you-go instances associated with immediate capacity reservations, but zonal reserved instances cannot.

An immediate capacity reservation transitions through the following phases throughout its lifecycle:

1.  When the capacity reservation is purchased, it begins to be billed at the pay-as-you-go instance rate.
2.  At any time during the validity period of the capacity reservation, you can use the reserved capacity in the private pool associated with the capacity reservation to create pay-as-you-go instances.
3.  You can manually release the capacity reservation or wait for it to expire and be automatically released.

    **Note:** Created pay-as-you-go instances are not affected when the associated immediate capacity reservation is released and continue to run properly. The instances are billed based at the pay-as-you-go rates after they are created.


The following figure shows how an immediate capacity reservation that reserves resources for two instances is used.

![cr-process](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6570482161/p187808.png)

## Billing

An immediate capacity reservation begins to be billed at the pay-as-you-go instance rate as soon as the capacity reservation is purchased. Billing continues regardless of whether the capacity reservation is actually used to create instances. Billing stops when the capacity reservation is automatically released upon expiration or manually released.

**Note:** Before pay-as-you-go instances are created from the reserved resources of the capacity reservation, you are charged only the instance type price. After pay-as-you-go instances are created from the reserved instances of the capacity reservation, you are charged based on the instance configurations including the instance type, disks, and public bandwidth.

## Limits

-   Immediate Capacity Reservation is available only for specific instance types in specific regions. For more information, see the buy page.
-   The reserved capacity in a private pool can be used to create only pay-as-you-go instances that match the instance type, zone, and operating system attributes of the associated capacity reservation.
-   Zonal reserved instances cannot be applied to pay-as-you-go instances that were created from reserved resources in private pools.

## Scenarios

-   Large requirements for elastic resources: When an immediate capacity reservation is purchased, billing starts based on the pay-as-you-go rate of the instance type. To make resources cost-effective, you need to make continuous and full use of the reserved resources during the validity period of the capacity reservation.
-   Requirements for reserved resources in use of savings plans or reserved instances: Savings plans and regional reserved instances can significantly reduce costs but cannot provide resource reservations. To reserve resources when you have savings plans or reserved instances, you can purchase immediate capacity reservations.

## Usage examples

-   Manual release

    Requirements:

    -   Apply one regional reserved instance to offset the hourly bills of pay-as-you-go instances. The reserved instance is an ecs.g6.large Linux reserved instance that is scoped to the China \(Hangzhou\) region and can cover 10 ecs.g6.large instances.
    -   Immediately reserve resources in Hangzhou Zone H and Hangzhou Zone I.
    -   Switch to other zones to create pay-as-you-go instances based on business needs.
    Solution:

    -   Create an immediate capacity reservation that can be manually released in both Hangzhou Zone H and Hangzhou Zone I. Make sure that the created immediate capacity reservations match the instance type, instance quantity, and operating system attributes of the regional reserved instance.
    -   To reserve resources in other zones, manually release the immediate capacity reservations in Hangzhou Zone H and Hangzhou Zone I and create immediate capacity reservations within the zones where you want to reserve resources.
-   Scheduled release

    Requirements:

    -   Apply a general-purpose savings plan that you purchased to offset the hourly bills of pay-as-you-go instances.
    -   Reserve resources of different instance types for specific periods of time. Reserve resources of the ecs.c6e.large instance type for the first half of a month and resources of the ecs.c6.large instance type for the second half of a month.
    Solution:

    -   At the beginning of the month, purchase immediate capacity reservations for the ecs.c6e.large instance type that are to be released at the specified time.
    -   In the middle of the month, purchase immediate capacity reservations for the ecs.c6.large instance type that are to be released at the specified time.

