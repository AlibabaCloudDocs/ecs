# Create an ECS bare metal instance

The procedure to create an ECS bare metal instance is similar to the procedure to create a regular ECS instance.

For information about how to create a regular ECS instance, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  Click **Create Instance**.

4.  In the Basic Configurations step, configure the parameters and click **Next: Networking**.

    Take note of the following parameters:

    -   **Region**: ECS Bare Metal Instance families and types are available in specific regions and zones. For the regions and zones where ECS Bare Metal Instance families and types are available, see the [ECS Instance Types Available for Each Region](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) page. Select a billing method and enter an instance type name to search for the instance type.
    -   **Instance Type**: Set Architecture to **ECS Bare Metal Instance**, set Category to **CPU Type** or **GPU Type**, and then select an instance type. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).
    -   **Image**: All available images are displayed in the Image section of the buy page.
5.  In the Networking step, configure parameters for the network and security group, and click **Next: System Configurations**.

    **Network Type**: Only **VPC** is available.

6.  In the System Configurations \(Optional\) step, configure the parameters and click **Next: Grouping**.

7.  In the Grouping \(Optional\) step, configure the parameters and click **Next: Preview**.

8.  Check your configurations, read and select *ECS Terms of Service*, and then click Create Order.


**Related topics**  


[RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md)

