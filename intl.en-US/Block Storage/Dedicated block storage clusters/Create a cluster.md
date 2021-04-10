# Create a cluster

This topic describes how to create a dedicated block storage cluster.

For information about the billing of the Dedicated Block Storage Cluster feature, see [Purchase](/intl.en-US/Block Storage/Dedicated block storage clusters/Billing.md).

**Note:** The dedicated block storage cluster feature is available in the China \(Heyuan\), China \(Ulanqab\), and Indonesia \(Jakarta\) regions. The number of supported regions is increasing.

1.  Go to the Dedicated Block Storage Cluster page.

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Dedicated Block Storage Cluster**.

    3.  In the top navigation bar, select a region.

2.  Click **Create**.

3.  On the buy page, configure the parameters described in the following table for the dedicated block storage cluster.

    |Parameter|Description|
    |---------|-----------|
    |Billing Method|Only the **Subscription** billing method is supported.|
    |Region and Zone|Select the region and zone in which to create the dedicated block storage cluster. The region and zone of the dedicated block storage cluster must be the same as those of the ECS instance to which you want to attach the cloud disks in the cluster.**Note:** After a dedicated block storage cluster is created, you cannot change the region and zone. |
    |Cluster Capacity|Set the capacity of the dedicated block storage cluster.|
    |Cluster Name|Set the name of the dedicated block storage cluster for subsequent management.|
    |Duration|Set the subscription duration of the dedicated block storage cluster.|

4.  Check the configuration fees, read and select the service agreement, and then click **Confirm Order**.

    The dedicated block storage cluster is delivered within 21 business days after the payment is made.


After the dedicated block storage cluster is created, you can choose **Storage & Snapshots** \> **Dedicated Block Storage Cluster** to view the information about the cluster.

After the dedicated block storage cluster is deployed, you can create data disks in the cluster. For more information, see [Create a cloud disk in a dedicated block storage cluster](/intl.en-US/Block Storage/Dedicated block storage clusters/Create a cloud disk in a dedicated block storage cluster.md).

