---
keyword: [resource assurance, resource reservation, elastic quota, elasticity assurance, immediate capacity reservation, private resource pool, private pool, pay-as-you-go]
---

# Overview of Resource Assurance

Resource Assurance is a service that guarantees resources to flexibly meet your business needs. It enables you to quantify the amount of available resources, reserve resources, plan private pools, and have a better experience when you query, reserve, purchase, and use resources.



## Introduction

Resource Assurance is in invitational preview. To use Resource Assurance, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

The following table describes the different services that Resource Assurance provide.

|Service|Feature|Description|
|-------|-------|-----------|
|Quota management|Elastic Quota|Allows you to view quotas on resources such as instance types, images, disks, and security groups, and guarantees the provision of instance resources to some extent.|
|Resource Reservation|-   Elasticity Assurance
-   Immediate Capacity Reservation

|Allows you to reserve resources for different scenarios. After resources are reserved, the system generates private pools in which to retain the resources.|
|Private Pool|Private Pool|Provides guaranteed resources for you to create instances.|

## Quota management

The following table describes the different types of elastic quotas.

|Elastic quota type|Description|
|------------------|-----------|
|Instance quota|Instance quotas are allocated based on zones, instance types, billing methods, and network types. Instance quotas are classified into the following types based on how well the provision of resources is guaranteed:-   Base quotas: specify the minimum amounts of guaranteed available instance resources. When you create instances within a base quota, the requested resources are guaranteed. Base quotas are automatically adjusted and allocated before the tenth day of each month based on your usage of ECS resources. You cannot apply to increase base quotas.
-   Reserved quotas: specify the amounts of instance resources reserved by resource reservations. When you create instances within a reserved quota, the requested resources are guaranteed. You can create the following resource reservations to increase reserved quotas:
    -   Elasticity assurances
    -   Immediate capacity reservations \(capacity reservations that take effect as soon as they are created\)
-   Total quotas: specify the maximum amounts of guaranteed available instance resources and include base quotas, reserved quotas, and other quotas. To ensure that the automatic increases in your total quotas match the increases in your daily resource usage, the system periodically adjusts your instance quotas based on your instance usage. If a total quota cannot meet your requirements, you can apply to increase it. For more information, see [View and increase instance quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase instance quotas.md). |
|Resource quota|Resource quotas are quotas on other ECS resources such as images, cloud disks, and security groups. You can apply to increase these quotas. For more information, see [View and increase resource quotas](/intl.en-US/Tag & Resource/Resource/Privileges & Quotas/View and increase resource quotas.md).|

## Resource Reservation

The following table describe the different types of resource reservations.

|Type|Description|Reference|
|----|-----------|---------|
|Elasticity assurance|Provides guaranteed pay-as-you-go instance resources to meet irregular resource requirements.|[Overview of Elasticity Assurance](/intl.en-US/Instance/Instance purchasing options/Resource assurances/Elasticity assurances/Overview of Elasticity Assurance.md)|
|Immediate capacity reservation|Provides guaranteed pay-as-you-go instance resources, and is typically used in conjunction with reserved instances or savings plans to meet large resource requirements.|[Overview of Immediate Capacity Reservation](/intl.en-US/Instance/Instance purchasing options/Resource assurances/Capacity reservations/Overview of Immediate Capacity Reservation.md)|

Resource reservation solutions are recommended based on the different types of resource reservations. These solutions are more flexible than the subscription model, and can provide resource reservations that the pay-as-you-go model lacks. The following table compares the solutions.

|Item|Combination of elasticity assurances and pay-as-you-go instances|Combination of immediate capacity reservations, savings plans or regional reserved instances, and pay-as-you-go instances|
|----|----------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
|Scenario|Some scenarios to which this solution is applicable:-   A financial SaaS service provider needs a large amount of resources to perform an account check at the beginning of each month.
-   A rendering enterprise needs to process a number of rendering tasks at the beginning of each week.
-   Internet media needs to report hot news that appears from time to time.

The resource usage in the preceding scenarios demonstrates discrete peaks over time, as shown in the following figure.

![spur](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9830482161/p189868.png)

|Some scenarios to which this solution is applicable:-   An internal office automation \(OA\) system is used.
-   Resources need to be reserved immediately or for a specified period of time to use together with regional reserved instances or savings plans.

The resource usage in the preceding scenarios is consistent over a specific period of time, as shown in the following figure.

![stable](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0930482161/p189867.png) |
|Flexibility in time|This solution allows for great flexibility in when resources are used. You do not need to plan when to use resources for an extended period of time but purchase resources when you need them.|This solution allows for limited flexibility in when resources are used. To make resources cost-effective, you need to plan when to use resources, and continuously use the resources over an extended period of time.|
|Resource reservation|Elasticity assurances provide resource reservations.|Immediate capacity reservations provide resource reservations.|
|Billing rule|Total price of resources reserved by an elasticity assurance = Assurance fee + Price of created pay-as-you-go instancesIf you have purchased regional reserved instances or savings plans, you can apply them to the created pay-as-you-go instances.

|Total price of resources reserved by an immediate capacity reservation = Price of unused reserved capacity \(billed at the pay-as-you-go instance rate\) + Price of created pay-as-you-go instances.**Note:** During the validity period of an immediate capacity reservation, you are charged for the capacity reservation at the pay-as-you-go instance rate regardless of whether the reserved resources are used to create pay-as-you-go instances.

If you have purchased regional reserved instances or savings plans, you can apply them to the unused reserved capacity and the created pay-as-you-go instances. |

## Private Pool

All the resources that are automatically allocated by the system constitute a public pool. All users have access to the resources in the public pool. Instances may fail to be created due to insufficient resources in the public pool.

When you use resource reservations, the system reserves resources that have matching attributes in the form of private pools to guarantee resource provision.

**Note:** The capacities in private pools are equal to reserved quotas. This makes it easy for you to have an overview of guaranteed resources.

The reservation and use of resources in private pools are separated. The system generates private pools to reserve resources. You can then use the resources reserved in the private pools to create instances. You can make the following configurations to reserve and use resources in private pools:

-   When you reserve resources, you can select one of the following private pool types:

    -   Open: suited to common business that requires guaranteed resources.
    -   Targeted: suited to key business for which you want to reserve resources. To use a targeted private pool, you must specify the pool ID.
    ![admin-side](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0930482161/p186143.png)

-   When you use resources, you can use the Private Pool parameter to specify whether to use private pools and which type of private pools to use. Valid values for the Private Pool parameter:

    -   Open: The capacity in open private pools is given priority over public pool resources. If no capacity is available in private pools, the system attempts to use public pool resources.
    -   Targeted: A specified targeted or open private pool is used. If you set Private Pool to Targeted, you must specify the ID of a targeted or open private pool. If no capacity is available in the specified private pool, the instances cannot be created.
    -   None: The capacity in private pools is not used.
    ![user-side](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0930482161/p186144.png)


The following section describes some best practices for using private pools:

-   Resources allocated based on business types

    A system administrator creates multiple targeted private pools and informs O&M personnel and developers of different pool IDs. This ensures that different pools are used to create instances for O&M and development purposes.

-   Resources allocated regardless of business types

    A system administrator creates open private pools. The O&M personnel and developers first use the capacity in the open private pools to create instances. When no capacity is available in the private pools, resources in the public pool are used.

-   Resources allocated exclusively to a specific business

    A system administrator creates targeted private pools and configures instances to be created by using these pools for the specified business. When no capacity is available in the private pools, instances cannot be created.


