---
keyword: [Alibaba Cloud, ECS, billing method for network usage, change the billing method for network usage, pay-by-bandwidth, pay-by-traffic, change from pay-by-bandwidth to pay-by-traffic, change from pay-by-traffic to pay-by-bandwidth]
---

# Change the billing method for network usage

If the billing method for network usage of an instance that uses a public IP address does not meet your business requirements, you can change the billing method.

Before you change the billing method for network usage of a subscription instance from pay-by-bandwidth to pay-by-traffic, make sure that your account has the configuration downgrade privilege.

**Note:** You can click **Privileges & Quotas** on the **Overview** page to go to the Privileges and Quotas page and check whether your account has the configuration downgrade privilege.

The billing methods available for network usage are pay-by-bandwidth and pay-by-traffic. You can change the billing method based on your needs.

-   Pay-by-bandwidth: You are charged based on the specified bandwidth. The actual outbound bandwidth does not exceed the specified bandwidth.
-   Pay-by-traffic: You are charged based on the traffic that you actually used. You can configure a peak bandwidth value for outbound traffic to avoid excess costs caused by bursts in outbound traffic.

    **Note:** When the **Pay-By-Traffic** billing method is used, the peak inbound and outbound bandwidth values are used as traffic limits instead of guaranteed performance. In scenarios where demands exceed resource supplies, the peak bandwidth values may be limited. If you need guaranteed bandwidth performance, select the **Pay-By-Bandwidth** billing method.


This topic describes how to change the billing method for network usage of an instance. For information about how to change the bandwidth size, see the following topics:

-   [Modify the bandwidth configurations of subscription instances](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Modify the bandwidth configurations of subscription instances.md)
-   [Modify the bandwidth configurations of pay-as-you-go instances](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Modify the bandwidth configurations of pay-as-you-go instances.md)

This topic describes how to change the billing method for network usage of an instance that uses a public IP address. For more information about how to change the billing method for network usage of an instance that uses an elastic IP address \(EIP\), see [Modify the bandwidth of an EIP](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Modify the bandwidth of an EIP.md).

## Change from pay-by-bandwidth to pay-by-traffic

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance for which you want to change the billing method for network usage. Then, use one of the following methods to go to the configuration page based on the billing method of the instance:

    -   Subscription

        Find the subscription instance for which you want to change the billing method for network usage. Click **Upgrade/Downgrade** in the corresponding **Actions** column. In the Upgrade/Downgrade Wizard dialog box, select **Downgrade** and **Bandwidth Configuration** and then click **Continue**.

    -   Pay-as-you-go
        -   A single instance: Find the pay-as-you-go instance for which you want to change the billing method for network usage. Choose **More** \> **Configuration Change** \> **Change Pay-as-you-go Instance Bandwidth** in the corresponding **Actions** column.
        -   Multiple instances: Select the pay-as-you-go instances for which you want to change the billing method for network usage. In the lower part of the page, choose **More** \> **Configuration Change** \> **Change Pay-as-you-go Instance Bandwidth**.
5.  On the Change Bandwidth page, find the Bandwidth section, select **Pay-By-Traffic**, and then set a peak bandwidth value.

6.  Read the notes and terms of service. If you do not have questions, select *ECS Service Terms*.

7.  Confirm the configuration costs, click Confirm in the lower part of the page, and then perform the subsequent operations as instructed on the page.

    The new configurations take effect immediately after you change the billing method.


## Change from pay-by-traffic to pay-by-bandwidth

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance for which you want to change the billing method for network usage. Then, use one of the following methods to go to the configuration page based on the billing method of the instance:

    -   Subscription
        -   A single instance: Find the subscription instance for which you want to change the billing method for network usage. Click **Upgrade/Downgrade** in the corresponding **Actions** column. In the Upgrade/Downgrade Wizard dialog box, select **Upgrade** and click **Continue**.
        -   Multiple instances: Select the subscription instances for which you want to change the billing method for network usage. In the lower part of the page, choose **More** \> **Configuration Change** \> **Change Subscription Instance Bandwidth**. In the dialog box that appears, select **Modify Peak Bandwidth Value** and click **Continue**.
    -   Pay-as-you-go
        -   A single instance: Find the pay-as-you-go instance for which you want to change the billing method for network usage. Choose **More** \> **Configuration Change** \> **Change Pay-as-you-go Instance Bandwidth** in the corresponding **Actions** column.
        -   Multiple instances: Select the pay-as-you-go instances for which you want to change the billing method for network usage. In the lower part of the page, choose **More** \> **Configuration Change** \> **Change Pay-as-you-go Instance Bandwidth**.
5.  On the Change Bandwidth page, find the Bandwidth section, select **Pay-By-Bandwidth**, and then set a bandwidth value.

6.  Read the notes and terms of service. If you do not have questions, select *ECS Service Terms*.

7.  Confirm the configuration costs, click Confirm in the lower part of the page, and then perform the subsequent operations as instructed on the page.

    The new configurations take effect immediately after you change the billing method.


