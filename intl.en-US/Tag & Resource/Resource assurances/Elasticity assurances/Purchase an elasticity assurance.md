---
keyword: [resource reservation, elasticity assurance, private resource pool, private pool, pay-as-you-go]
---

# Purchase an elasticity assurance

When you purchase an elasticity assurance, you must specify attributes such as instance type, zone, reserved quantity, and duration. After the elasticity assurance is purchased, you have guaranteed access to the resources in the private pool associated with the elasticity assurance to create pay-as-you-go instances.

You can guarantee access to resources by paying a small assurance fee to purchase an elasticity assurance. After you create pay-as-you-go instances from the reserved resources in the private pool, you are charged for the instances on an hourly basis at the pay-as-you-go rate.

**Note:** Resource Assurance is in invitational preview. To use Resource Assurance, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).

When you purchase an elasticity assurance, you must specify an instance type and a zone. After the elasticity assurance is purchased, it guarantees the provision of resources only of the specified instance type within the specified zone.

## Procedure

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Resource Assurance**.

3.  In the top navigation bar, select a region.

4.  In the upper part of the Resource Assurance page, click the **Elasticity Assurance** tab.

5.  Click **Purchase Elasticity Assurance**.

6.  Configure the parameters of the elasticity assurance in the **Query Solutions** step.

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Region and Zone**|Specify the region and zone in which to reserve resources. In the Recommended Solution section, other zones may be recommended based on resource availability. Ultimately, the zones in the solution that you select prevail.|
    |**Instance Type**|Specify the instance type for which to reserve resources. In the Recommended Solution section, other alternative instance types may be recommended based on resource availability. Ultimately, the instance types in the solution that you select prevail.|
    |**Reserved Quantity**|Specify the number of instances for which to reserve resources.|
    |**Billing Method**|After an elasticity assurance is purchased, you can use the reserved capacity in the private pool associated with the elasticity assurance to create only **pay-as-you-go** instances.|
    |**Effective At**|Specify the time at which the elasticity assurance takes effect. The end time of the validity period cannot be specified but is automatically changed with the specified **Duration** value.|
    |**Duration**|You can select a duration of one month up to five years. For the durations available for selection, see the elasticity assurance buy page.|
    |**Private Pool Type**|Select a private pool type. Valid values:    -   **Open**: When you create pay-as-you-go instances, the capacity in open private pools is used as long as the instances match the attributes of the reserved resources.
    -   **Targeted**: If you want to use the capacity in a targeted private pool to create pay-as-you-go instances, you must specify the pool ID.
We recommend that you prepare a number of open and targeted private pools based on your business types. For example, you can prepare targeted private pools dedicated to key business. For more information, see [Private Pool](/intl.en-US/Tag & Resource/Resource assurances/Overview of Resource Assurance.md). |
    |**Private Pool Name**|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), periods \(.\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.|
    |**Description**|Enter a private pool description that makes the private pool easy to identify. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|

7.  Select a solution in the **Recommended Solution** section.

    The recommended solutions may deliver optimal performance, be backed by the most sufficient supply of resources, or provide multi-zone redundancy. You can select the solution that best suits your needs.

    ![ea-recommended](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6560482161/p185062.png)

    **Note:** If no recommended solutions are available or if the recommended solutions do not meet your requirements, you can **submit a ticket**.

8.  Click **Next: Confirm Information**.

    Each elasticity assurance is applicable only to a specific instance type and a specific zone. If the solution that you select involves multiple instance types or zones, the solution is automatically split into multiple elasticity assurances. You can select one or more elasticity assurances in the **Confirm Information** step.

9.  Select the elasticity assurances that you want to purchase. Then, read and select Notes. Verify that all configurations are correct, click **Purchase**, and then make payment as instructed.

    You can view the elasticity assurances that you purchased on the Elasticity Assurance tab. If **Active** is displayed in the Status column corresponding to an elasticity assurance, the elasticity assurance is created. You can then use the capacity in the private pool associated with the elasticity assurance to create pay-as-you-go instances. For more information, see [Use a private pool]().


