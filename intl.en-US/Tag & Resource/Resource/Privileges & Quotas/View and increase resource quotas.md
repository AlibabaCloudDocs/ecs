# View and increase resource quotas

This topic describes how to view quotas for resources such as images, disks, and security groups.

## Step 1: View resource quotas

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the upper-right corner of the **Overview** page, click **Privileges**.

    ![quota](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1454237061/p166801.png)

3.  On the **Privileges and Quotas** page, click the **Resource Quota** tab.

4.  Select a region and view the quota values.

    Resource quotas include quotas for resources such as images, disks, and security groups in the selected region.

    **Note:** Your resource quotas may change based on the usage of your ECS resources.

    ![res-quota](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2416237061/p166924.png)


## Step 2: Increase resource quotas

1.  Find the quota that you want to increase, and click **Increase Quota** in the **Actions** column.

    **Note:** You cannot apply to increase a quota while the previous increase request is in progress.

2.  On the Calculate Quotas and Request page, enter required information and then click **Submit**.

    ![increase-res-quota](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9407337061/p167165.png)

    The following table describes the information that you must enter.

    |Information|Description|
    |-----------|-----------|
    |**New Quota**|Enter your expected quota. The unit is based on the resource type.|
    |**Reason**|Enter the reason of your request. A proper reason makes it easier for your request to be approved.|
    |**Notify Adjustment Results**|If you select Yes, the system notifies you of the adjustment results by email.|

3.  Click **Quota Increase Requests** in the **Actions** column to view the status of your request.

    -   **Approved**: Your request is approved and cannot be revoked.
    -   **Forbid**: Your request is rejected. You can click **Submit Again** in the **Actions** column and select Manual Approval.

**Related topics**  


[DescribeAccountAttributes \(This operation queries only resource quotas and the zone-specific vCPU-based total quota for all instance types.](/intl.en-US/API Reference/Others/DescribeAccountAttributes.md)

