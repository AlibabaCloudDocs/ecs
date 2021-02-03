# Create an f3 instance

This topic describes how to create an f3 instance.

This topic describes the parameters for creating an f3 instance. For more information about other common parameters, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

To facilitate testing, Alibaba Cloud provides an image pre-installed with the Xilinx development environment. The image is available only as a shared image. To obtain the image, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  Click **Create Instance**.

4.  In the Basic Configurations step, configure the parameters and click **Next: Networking**.

    When you configure the parameters, take note of the following items:

    -   **Region**: Select a region from the following regions where f3 instance types are available. Note that the instance buy page shows the instance types available for your purchase in each zone and region.

        -   China \(Shanghai\)
        -   China \(Beijing\)
        -   China \(Zhangjiakou\)
        You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.

        **Note:** If you can view subscription resources but not pay-as-you-go resources when you purchase an instance, see the "Why are some instance types not available on the instance buy page when I attempt to purchase a pay-as-you-go instance?" section in [Why are some instance types not available on the instance buy page when I attempt to purchase a pay-as-you-go instance?](/intl.en-US/Instance/Instance FAQ.md).

    -   **Instance Type**: Set Architecture to **Heterogeneous Computing** and Category to **Compute Optimized Type with FPGA**.
    -   **Image**: Click **Shared Image** and select an image that is pre-installed with the Xilinx development environment.
    -   **Storage**: Images that are pre-installed with the Xilinx development environment occupy some storage space. We recommend that you select an ultra disk of 200 GiB as the system disk.
5.  In the Networking step, configure the parameters and click **Next: System Configurations**.

    Only the network type of VPC is supported.

6.  In the System Configurations \(Optional\) step, configure the parameters and click **Next: Grouping**.

7.  In the Grouping \(Optional\) step, configure the parameters and click **Next: Preview**.

8.  Confirm the order and click **Create Order**.


**References**  


[Use OpenCL on an f3 instance](/intl.en-US/Best Practices/FaaS instances best practices/Use OpenCL on an f3 instance.md)

[Use the RTL design on an f3 instance](/intl.en-US/Best Practices/FaaS instances best practices/Use the RTL design on an f3 instance.md)

