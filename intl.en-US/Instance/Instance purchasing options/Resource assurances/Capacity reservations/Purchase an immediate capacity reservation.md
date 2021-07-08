---
keyword: [capacity reservation, private pool, take effect immediately, pay-as-you-go, subscription, reserved instance, savings plan, RI, private resource pool]
---

# Purchase an immediate capacity reservation

This topic describes how to purchase an immediate capacity reservation. An immediate capacity reservation takes effect as soon as it is purchased. When you purchase an immediate capacity reservation, you must specify attributes such as private pool information. After the capacity reservation is purchased, you have guaranteed access to the resources in its associated private pool to create pay-as-you-go instances.

When you purchase an immediate capacity reservation, you must specify attributes such as instance type, zone, and operating system. After the capacity reservation is purchased, the provision of resources that have matching attributes is guaranteed.

## Procedure

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Resource Assurance**.

3.  In the top navigation bar, select a region.

4.  In the upper part of the Resource Assurance page, click the **Capacity Reservation** tab.

5.  Click **Purchase Capacity Reservation**.

6.  Configure the parameters of the capacity reservation in the **Query Solutions** step.

    The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Application Mode**|A value of **Effective Immediately** is available.|
    |**Expiration Method**|When an immediate capacity reservation is released, the reserved capacity is no longer billed but the instances created from the reserved resources are not affected. Valid values of this parameter:    -   **Manual Release**: The purchased immediate capacity reservation is effective until you manually release it.
    -   **Release Upon Expiration**: The purchased immediate capacity reservation is automatically released at the specified point in time. |
    |**Expires At**|If you set **Expiration Method** to **Release Upon Expiration**, you must specify expiration time, which must be at least 1 hour later than the current time.|
    |**Billing Method**|After an immediate capacity reservation is purchased, you can use the reserved capacity in the private pool associated with the capacity reservation to create only **pay-as-you-go** instances.**Note:** An immediate capacity reservation begins to be billed at the pay-as-you-go instance rate as soon as the capacity reservation takes effect. Billing continues regardless of whether the capacity reservation is actually used to create instances. Billing stops when the capacity reservation is automatically released upon expiration or manually released. |
    |**Region and Zone**|Specify the region and zone in which to reserve resources. In the Recommended Solution section, other zones may be recommended based on resource availability. Ultimately, the zones in the solution that you select prevail.|
    |**Instance Type**|Specify the instance type for which to reserve resources. In the Recommended Solution section, other alternative instance types may be recommended based on resource availability. Ultimately, the instance types in the solution that you select prevail.|
    |**Operating System**|Select an operating system type. To use this capacity reservation in conjunction with a regional reserved instance, you must select the operating system type of the regional reserved instance. Valid values of this parameter:    -   **linux**
    -   **windows** |
    |**Reserved Quantity**|Specify the number of instances for which to reserve resources.|
    |**Private Pool Type**|Select a private pool type. Valid values:    -   **Open**: When you create pay-as-you-go instances, the capacity in open private pools is used as long as the instances match the attributes of the reserved resources.
    -   **Targeted**: If you want to use the capacity in a targeted private pool to create pay-as-you-go instances, you must specify the pool ID.
We recommend that you prepare a number of open and targeted private pools based on your business types. For example, you can prepare targeted private pools dedicated to key business. For more information, see [Private Pool](/intl.en-US/Instance/Instance purchasing options/Resource assurances/Overview of Resource Assurance.md). |
    |**Private Pool Name**|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), periods \(.\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.|
    |**Description**|Enter a private pool description that makes the private pool easy to identify. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|

7.  Select a solution in the **Recommended Solution** section.

    The recommended solutions may deliver optimal performance, be backed by the most sufficient supply of resources, or provide multi-zone redundancy. You can select the solution that best suits your needs.

    ![recommended-cr](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6780482161/p187574.png)

    **Note:** If no recommended solutions are available or if the recommended solutions do not meet your requirements, you can **submit a ticket**.

8.  Click **Next: Confirm Information**.

    Each capacity reservation is applicable only to a specific instance type and a specific zone. If the solution that you select involves multiple instance types or zones, the solution is automatically split into multiple capacity reservations. You can select one or more capacity reservations in the **Confirm Information** step.

9.  Select the capacity reservations that you want to purchase. Then, read and select Notes. Verify that all configurations are correct, click **Purchase**, and then make payment as instructed.

    You can view the capacity reservations that you purchased on the Capacity Reservation tab. If **Active** is displayed in the Status column corresponding to a capacity reservation, the capacity reservation is created. You can then use the capacity in the private pool associated with the capacity reservation to create pay-as-you-go instances. For more information, see [Use a private pool](/intl.en-US/Instance/Instance purchasing options/Resource assurances/Use a private pool.md).


