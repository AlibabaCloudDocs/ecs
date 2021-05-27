---
keyword: [elasticity assurance, capacity reservation, private resource pool, private pool, pay-as-you-go]
---

# Use a private pool

After an elasticity assurance or a capacity reservation is created, the system generates a private pool to reserve resources for a specific number of instances that have specific attributes. During the validity period of elasticity assurance or a capacity reservation, you can always have access to the resources reserved in the private pool when you want to create instances. This topic describes how to use the reserved capacity in a private pool to create instances.

-   The elasticity assurance or capacity reservation to be used is in the **Active** state.
-   Reserved capacity is available in the private pool associated with the elasticity assurance or capacity reservation.

Elasticity assurances have the attributes of instance type and zone, whereas capacity reservations have the attributes of instance type, zone, and operating system. Only pay-as-you-go instances that have matching attributes can be created from the resources reserved by elasticity assurances or capacity reservations.

This topic focuses on the configurations related to private pools during the procedure to create instances. For other configurations involved in the procedure, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

## Procedure

1.  Go to the [Custom Launch](https://ecs-buy.aliyun.com/wizard/#/) tab of the instance buy page in the ECS console.

2.  Configure the settings in the Basic Configurations step and click **Next: Networking**.

    -   To create instances by using the private pool associated with an elasticity assurance, make sure that the instance type and zone selected for the instances match the instance type and zone of the elasticity assurance. Otherwise, the instances cannot be created.
    -   To create instances by using the private pool associated with a capacity reservation, make sure that the instance type, zone, and operating system selected for the instances match the instance type, zone, and operating system of the capacity reservation. Otherwise, the instances cannot be created.
3.  Configure the settings in the Networking step and click **Next: System Configurations**.

4.  Configure the settings in the System Configurations \(Optional\) step and click **Next: Grouping**.

5.  Configure the settings in the Grouping \(Optional\) step and click **Next: Preview**.

    The following table describes the private pool-related parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Private Pool**|    -   **Open**: The capacity in open private pools is given priority over public pool resources. If no capacity is available in private pools, the system attempts to use public pool resources.
    -   **None**: The capacity in private pools is not used.
    -   **Targeted**: A specified targeted or open private pool is used. If no capacity is available in the specified private pool, the instances cannot be created.
For more information, see [Private Pool](/intl.en-US/Tag & Resource/Resource assurances/Overview of Resource Assurance.md). |
    |**Private Pool ID**|If you set **Private Pool** to **Targeted**, you must specify the ID of a targeted or open private pool.**Note:** By default, each elasticity assurance or capacity reservation and its associated private pool have the same ID. |

6.  Verify that the instance configurations are correct, and read and select *ECS Terms of Service*. Then, click Create Instance and make payment.

    You can view the created instances on the details page of the specified elasticity assurance or capacity reservation. For more information, see [View elasticity assurances](/intl.en-US/Tag & Resource/Resource assurances/Elasticity assurances/View elasticity assurances.md) and [View capacity reservations](/intl.en-US/Tag & Resource/Resource assurances/Capacity reservations/View capacity reservations.md).


