---
keyword: [quotas, quota, base quota, total quota, zone-specific vCPU-based total quota for all instance types, insufficient quota]
---

# View and increase instance quotas

Instance quotas are set based on the zones, instance types, billing methods, and network types of instances. This topic describes the types of instance quotas and how to view and increase instance quotas.

Instance quotas are classified into total quotas and base quotas based on resource supplies. A total quota indicates the maximum number of instances that can be created, whereas a base quota indicates the guaranteed number of instances to be created. The system periodically adjusts your instance quotas based on the usage of your instances to ensure that automatic increases in your total quota match increases in your daily resource usage. If a total quota cannot meet your requirements, you can apply to increase it.

Both the total and usage amounts of the total and base quotas are cumulative values of the last 15 days \(including the current day\). You do not have to worry about applying for additional quotas in the case of insufficient quotas due to a large number of instances in your account. Example:

-   When you query the total quota on August 16, the total amount displayed is the total quota for August 2 to August 16, and the displayed usage amount is the number of instances created and running from August 2 to August 16.
-   If you do not have the base quota automatically adjusted or manually apply for an increase to the total quota, the total quota remains unchanged when you query the total quota on August 17. The displayed usage amount is the number of instances created and running from August 3 to August 17.

**Note:** In some cases, refreshed usage data may be displayed with a delay of up to 24 hours. However, this does not affect whether you can create instances.

In addition, an instance quota can be classified into an instance type-specific quota and a zone-specific vCPU-based total quota for all instance types. Typically, you do not need to worry about the zone-specific vCPU-based total quota for all instance types, because this value is always greater than your demand.

## Step 1: View instance quotas

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the upper-right corner of the **Overview** page, click **Privileges**.

    ![quota](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1454237061/p166801.png)

3.  On the **Privileges and Quotas** page, click the **Instance Quota** tab.

4.  Select a region and view the quota values.

    The following figure shows the Instance Quota page.

    ![Instance quota](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1454237061/p166807.png)

    The following table describes the columns in the list shown in the preceding figure.

    |Column|Description|
    |------|-----------|
    |    -   **Region/Zone**
    -   **Instance Type**
    -   **Billing Method**
    -   **Network Type**
|You can filter and view instance quotas by region, zone, instance type, billing method, and network type. Instance quotas are classified into the following types:    -   Instance type-specific quota: the quota for instances of a specified instance type and a specified network type that use a specified billing method in a specified region and zone.

**Note:** Quotas for instances of the classic network type are displayed only when the classic network is available in the region. You can check whether the classic network is available in the region on the **Privileges** tab.

    -   Zone-specific vCPU-based total quota for all instance types: the maximum number of vCPUs that can be assigned to instances of all instance types and a specified network type that use a specified billing method in a specified region and zone. For example, you can view the maximum number of vCPUs that can be assigned to VPC-type subscription instances of all instance types in Hangzhou Zone H.

**Note:** By default, the zone-specific vCPU-based total quota for all instance types is not displayed. It is displayed only when you set Instance Type to **All**. |
    |**Quota Unit**|    -   Instance type-specific quota: The displayed value is the number of instances.
    -   Zone-specific vCPU-based total quota for all instance types: The displayed value is the number of vCPUs. |
    |**Total Quota**|A total quota consists of a base quota and other quotas. Therefore, the total quota is always greater than or equal to the base quota. Total quotas are automatically adjusted along with base quotas before the tenth day of each month. If the number of instances or vCPUs in your account reaches the total quota, you cannot purchase new instances. If you need more ECS instances, you can apply to increase the total quota.

After the total quota is increased to the specified value, the system keeps the total quota from falling below this value when the system automatically adjusts the total quota within at least three months.

**Note:** When you create ECS instances beyond the base quota, the availability of required resources is not guaranteed. |
    |**Base Quota**|Base quotas are automatically adjusted and allocated before the tenth day of each month based on the usage of your ECS resources. You cannot apply to increase the base quotas. **Note:** The base quota is used preferentially when you create instances. When you create instances within the base quota, the availability of required resources is guaranteed. |

    In the **Total Quota** and **Base Quota** columns, you can check the usage of quotas based on the color of the progress bar. Different colors convey different meanings:

    -   Green: The usage is less than 80% of the total.
    -   Yellow: The usage is greater than or equal to 80% but less than 100% of the total.
    -   Red: The usage is 100% of the total.

## Step 2: Increase instance quotas

1.  You can apply to increase quotas on demand.

    -   Increase a single quota: Find the quota that you want to increase, and click **Increase Quota** in the **Actions** column.
    -   Increase multiple quotas at a time: Select one or more quotas, and click **Calculate Quotas and Request** in the lower part of the page
    **Note:** You cannot apply to increase a quota while the previous increase application is in progress.

2.  On the Calculate Quotas and Request page, enter required information and then click **Submit**.

    Recommended quotas are displayed on the page. The request is submitted for fast and automatic approval first. If the request is rejected, it can be submitted again for manual approval.

    -   Typically, a requested quota that is less than the recommended value can pass automatic approval.
    -   A requested quota that is greater than the recommended value is likely to be rejected by automatic approval. If the request is rejected, you can submit it again for manual approval.
    Enter the required information based on your operation:

    -   The following table describes the information that you must enter when you request to increase a single quota.

        |Information|Description|
        |-----------|-----------|
        |**Target Quota**|Enter your expected quota in the number of instances or vCPUs.|
        |**Reason**|Enter the reason of your request. A proper reason makes it easier for your request to be approved.|
        |**Notify Adjustment Results**|If you select Yes, the system notifies you of the adjustment results by email.|

    -   The following table describes the information that you must enter when you request to increase multiple quotas at a time.

        |Information|Description|
        |-----------|-----------|
        |**Target Quota**|You can set a total expected quota for your selected quotas. The system allocates a recommended value in the number of instances for each quota.|
        |**New Quota**|You can also specify an expected value for each quota in the number of instances.|
        |**Reason**|Enter the reason of your request. A proper reason makes it easier for your request to be approved.|
        |**Notify Adjustment Results**|If you select Yes, the system notifies you of the adjustment results by email.|

3.  In the message that appears, confirm the result of the quota increase operation.

4.  Click **Quota Increase Requests** in the **Actions** column to view the status of your request.

    -   **Approved**: Your request is approved and cannot be revoked.
    -   **Forbid**: Your request is rejected. You can click **Submit Again** in the **Actions** column and select Manual Approval.

## Related FAQ

Is the zone-specific vCPU-based total quota for all instance types useful? Which one should I be concerned about: the instance type-specific quota or the zone-specific vCPU-based total quota for all instance types?

Typically, you do not need to worry about the zone-specific vCPU-based total quota for all instance types, because this value is always greater than your demand. In some cases, if your vCPU quota within a zone is insufficient, you must increase the zone-specific vCPU-based total quota for all instance types to create more instances.

![Capped quota in a single zone](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0210965061/p95306.png)

