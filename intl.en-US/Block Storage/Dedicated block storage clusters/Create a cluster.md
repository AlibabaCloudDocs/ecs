# Create a cluster

This topic describes how to create a dedicated block storage cluster.

For more information about the billing of dedicated block storage clusters, see [Purchase](/intl.en-US/Block Storage/Dedicated block storage clusters/Billing.md).

**Note:** The dedicated block storage cluster feature is available in the China \(Heyuan\), China \(Ulanqab\), and Indonesia \(Jakarta\) regions. The number of supported regions is increasing.

1.  Go to the Dedicated block storage cluster page.

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Dedicated Block Storage Cluster**.

    3.  In the top navigation bar, select a region.

2.  Click **Create a dedicated block storage cluster**.

3.  On the **Create a dedicated block storage cluster** page, configure the parameters described in the following table for the dedicated block storage cluster.

    |Parameter|Description|
    |---------|-----------|
    |Billing Method|Only the **Subscription** billing method is supported.|
    |Region and Zone|Select the region and zone in which to create the dedicated block storage cluster. The region and zone of the dedicated block storage cluster must be the same as those of the ECS instance to which you want to attach the cloud disks in the cluster. **Note:** After a dedicated block storage cluster is created, you cannot change its region or zone. |
    |Cluster capacity|Set the capacity of the dedicated block storage cluster.|
    |Propriety block storage cluster name|Set the name of the dedicated block storage cluster for subsequent management.|
    |Cluster performance type|Set the category of disks to create in the cluster. You can create only PL1 enhanced SSDs \(ESSDs\).|
    |Duration|Set the subscription duration of the dedicated block storage cluster.|

4.  Check the configuration fees, read and select the terms of service, and then click **Confirm the order**.

    The dedicated block storage cluster is delivered within 21 business days after the payment is made.


After the dedicated block storage cluster is created, you can choose **Storage & Snapshots** \> **Dedicated Block Storage Cluster** in the left-side navigation pane to view the information about the cluster.

After the dedicated block storage cluster is deployed, you can create data disks in the cluster. For more information, see [Create a cloud disk in a dedicated block storage cluster](/intl.en-US/Block Storage/Dedicated block storage clusters/Create a cloud disk in a dedicated block storage cluster.md).

