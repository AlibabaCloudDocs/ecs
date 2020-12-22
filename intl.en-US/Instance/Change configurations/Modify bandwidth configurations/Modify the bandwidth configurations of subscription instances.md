---
keyword: [Alibaba Cloud, ECS, upgrade and downgrade, subscription, modify bandwidth configurations]
---

# Modify the bandwidth configurations of subscription instances

If the bandwidth configurations of a subscription instance that uses a public IP address are not suitable for your business requirements, you can modify the bandwidth configurations.

If you want to downgrade the bandwidth configurations or modify the maximum bandwidth of an instance, make sure that your account has the configuration downgrade privilege.

**Note:** You can click **Privileges & Quota** on the **Overview** page. On the Privileges & Quota Management page, you can check whether your account has the configuration downgrade privilege.

You can modify the public bandwidth or the maximum bandwidth of an instance based on its billing method for network usage.

-   If instances use the pay-by-bandwidth billing method for network usage, you can upgrade or downgrade the public bandwidth. For more information, see [Upgrade public bandwidths](#section_bkh_ae1_b9z) or [Downgrade public bandwidths](#section_kyj_eqr_tlx).

    **Note:** A bandwidth configuration downgrade may result in a refund. The following formula is used to calculate the refund amount: Refund amount = Remaining amount of the configuration price before the downgrade - Price of the new configurations. Up to three refunds can be made for each subscription instance. A refund is made if you downgrade the instance type or bandwidth or change the billing method of a disk from subscription to pay-as-you-go.

-   If the billing method for network usage is pay-by-traffic, you can change the maximum bandwidth. For more information, see [Modify the maximum bandwidth](#section_6xv_wol_5qb).

When you modify the bandwidth configurations of an ECS instance, take note of the following limits:

-   The use of your ECS instances determines whether the configuration downgrade feature is supported.
-   You can modify the bandwidth configurations of an instance multiple times, but you must wait at least five minutes between two consecutive operations.

This topic describes how to modify the bandwidth configurations of a subscription instance that uses a public IP address. For more information about how to modify the bandwidth configurations of a subscription instance that uses an elastic IP address \(EIP\), see [Modify the bandwidth of an EIP](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Modify the bandwidth of an EIP.md).

## Upgrade public bandwidths

If instances use the pay-by-bandwidth billing method for network usage, you can perform the following operations to upgrade the public bandwidth.

**Note:** If you do not assign a public IP address when you create an instance, the instance has no public bandwidth. You can change the public bandwidth from 0 Mbit/s to a non-zero value by using the bandwidth upgrade feature to assign a public IP address to the instance.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Select one of the following methods to go to the bandwidth configuration page based on the number of instances for which you want to upgrade public bandwidths:

    -   Upgrade the public bandwidth of a single instance
        1.  Find the subscription instance for which you want to upgrade the public bandwidth and click **Upgrade/Downgrade** in the **Actions** column.
        2.  In the dialog box that appears, select **Upgrade** and click **Continue**.
    -   Upgrade the public bandwidths of multiple instances
        1.  Select the subscription instances for which you want to upgrade the public bandwidths. In the lower part of the page, choose **More** \> **Configuration Change** \> **Change Subscription Instance Bandwidth**.
        2.  In the dialog box that appears, select **Upgrade Bandwidth** and click **Continue**.
5.  On the page that appears, modify the bandwidth in the Bandwidth section.

    When you upgrade the public bandwidths of multiple instances, instances are filtered out if they are not associated with a public IP address or if their billing method for network usage is not pay-by-bandwidth. You can continue to perform operations only on the qualified instances, as shown in the following figure.

    ![Upgrade the public bandwidths of multiple instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6775240061/p135172.png)

6.  Read the notes and terms of service. If you do not have any questions, select *ECS Service Terms*.

7.  Check the configuration costs, click Upgrade or Create Order in the lower part of the page, and then perform the subsequent operations as instructed on the page.

    **Note:** If you change the public bandwidth of a classic network-type instance from 0 Mbit/s to a non-zero value for the first time, you must restart the instance by using the console or calling the RebootInstance operation to make the new configurations take effect.


## Downgrade public bandwidths

If instances use the pay-by-bandwidth billing method for network usage, you can perform the following operations to downgrade the public bandwidth.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Select one of the following methods to go to the bandwidth configuration page based on the number of instances for which you want to upgrade public bandwidths:

    -   Downgrade the public bandwidth of a single instance
        1.  Find the subscription instance for which you want to downgrade the public bandwidth and click **Upgrade/Downgrade** in the **Actions** column.
        2.  In the dialog box that appears, select **Downgrade** and **Bandwidth Configuration**, and then click **Continue**.
    -   Downgrade the public bandwidths of multiple instances
        1.  Select the subscription instances for which you want to downgrade the public bandwidths. In the lower part of the page, choose **More** \> **Configuration Change** \> **Change Subscription Instance Bandwidth**.
        2.  In the dialog box that appears, select **Downgrade Bandwidth** and click **Continue**.
5.  On the page that appears, find the bandwidth configuration items and modify the bandwidth.

    When you downgrade the public bandwidths of multiple instances, instances are filtered out if they are not associated with a public IP address or if their billing method for network usage is not pay-by-bandwidth. You can continue to perform operations on only the qualified instances, as shown in the following figure.

    ![Downgrade the public bandwidths of multiple instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5495240061/p135021.png)

    **Note:**

    -   If you downgrade the bandwidth of a classic network-type instance to 0 Mbit/s, the public IP address of the instance is retained. If you downgrade the bandwidth of a VPC-type instance to 0 Mbit/s, the public IP address of the instance is released.
    -   You can select **Pay-By-Traffic** to change the billing method for network usage to pay-by-traffic and set the maximum bandwidth.
6.  Read the notes and terms of service. If you do not have any questions, select *ECS Service Terms*.

7.  Check the refund amount, click Downgrade Now, and then perform the subsequent operations as instructed on the page.

    **Note:** After you downgrade the bandwidth, you do not need to restart the instance for the new configurations to take effect immediately.


## Modify the maximum bandwidth

If instances use the pay-by-traffic billing method for network usage, you can perform the following operations to modify the maximum bandwidth.

**Note:** If you select pay-by-traffic as the billing method for network usage, you are charged based on the actual volume of traffic. If you modify only the maximum bandwidth, the configuration costs remain unchanged. The specified maximum bandwidth is the maximum outbound bandwidth and can help avoid the high costs caused by bursts in outbound traffic.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Select one of the following methods to modify the maximum bandwidth based on the number of instances for which you want to modify maximum bandwidths:

    -   Modify the maximum bandwidth of a single instance
        1.  Find the subscription instance for which you want to modify the maximum bandwidth and click **Upgrade/Downgrade** in the **Actions** column.
        2.  In the dialog box that appears, select one of the following methods and click **Continue**.
            -   Select **Upgrade** to modify the maximum bandwidth or change the billing method for network usage to pay-by-bandwidth.
            -   Click **Downgrade** and **Bandwidth Configuration** to modify only the maximum bandwidth.
    -   Modify the maximum bandwidths of multiple instances
        1.  Select the subscription instances for which you want to modify the maximum bandwidths. In the lower part of the page, choose **More** \> **Configuration Change** \> **Change Subscription Instance Bandwidth**.
        2.  In the dialog box that appears, select **Modify Peak Bandwidth Value** and click **Continue**.
5.  On the page that appears, find the bandwidth configuration items and modify the maximum bandwidth.

    When you modify the maximum bandwidths of multiple instances, instances are filtered out if they are not associated with a public IP address or if their billing method for network usage is not pay-by-traffic. You can continue to perform operations on only the qualified instances, as shown in the following figure.

    ![Modify the maximum bandwidths of multiple instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6775240061/p135057.png)

    **Note:**

    -   If you downgrade the maximum bandwidth of a classic network-type instance to 0 Mbit/s, the public IP address of the instance is retained. If you downgrade the maximum bandwidth of a VPC-type instance to 0 Mbit/s, the public IP address of the instance is released.
    -   You can select **Pay-By-Bandwidth** to change the billing method for network usage to pay-by-bandwidth and set a bandwidth.
6.  Read the notes and terms of service. If you do not have any questions, select *ECS Service Terms*.

7.  Click the button in the lower part of the page and perform the subsequent operations as instructed on the page.

    **Note:**

    -   If you change the billing method for network usage from pay-by-traffic to pay-by-bandwidth, you must pay for the bandwidth upfront.
    -   If you change the public bandwidth of a classic network-type instance from 0 Mbit/s to a non-zero value for the first time, you must restart the instance by using the console or calling the RebootInstance operation to make the new configurations take effect.

**Related topics**  


[DescribeResourcesModification](/intl.en-US/API Reference/Regions/DescribeResourcesModification.md)

[ModifyInstanceNetworkSpec](/intl.en-US/API Reference/Networks/ModifyInstanceNetworkSpec.md)

