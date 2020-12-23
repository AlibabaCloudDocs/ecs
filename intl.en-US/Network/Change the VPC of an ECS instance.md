# Change the VPC of an ECS instance

This topic describes how to migrate a VPC-type ECS instance from the current VPC to another. If you select a VPC that does not meet your business needs when you create an ECS instance or if you want to replan the network of an instance, you can use this feature to change the VPC of the instance.

-   The instance is in the Stopped state. For more information, see [Stop an instance](/intl.en-US/Instance/Manage instances/Stop an instance.md).

    **Note:** If the instance has not been restarted after it is created, you must restart it before you stop it.

-   The instance is not added as a backend server of a Server Load Balancer \(SLB\) instance. For more information, see [Remove a backend server](/intl.en-US/User Guide/Backend servers/Default server groups/Remove a backend server.md).
-   Secondary elastic network interfaces \(ENIs\) bound to the instance are unbound. Multiple secondary private IP addresses assigned to the ENIs are revoked. For more information, see [Unbind an ENI](/intl.en-US/Network/Elastic Network Interfaces/Unbind an ENI.md) and [Revoke secondary private IP addresses](/intl.en-US/Network/Elastic Network Interfaces/Revoke secondary private IP addresses.md).
-   The destination VPC, vSwitch, and security groups are created and available.

## Scenarios

-   You want to replan the VPCs of your ECS instances because the original VPCs are unable to keep up with the growing needs of your business.
-   In the early business stage, only one VPC is planned. Risks in data operations exist because different projects and usage environments share this VPC. You want to use different VPCs for different projects and environments.
-   Your ECS instances are deployed in the default VPCs of different accounts. Connections between instances across Alibaba Cloud accounts cannot be implemented due to IP address conflicts. In this case, you must change the VPCs of the ECS instances and resolve the address conflicts before you can interconnect the instances across Alibaba Cloud accounts.

## Limits

-   The instance cannot be used in other cloud services. For example, the instance cannot be in the process of being migrated or having its VPC changed, or the databases deployed in the instance cannot be managed by Data Transmission Service \(DTS\).
-   After the VPC is changed, the new vSwitch of the instance must be in the same zone as the original vSwitch.
-   You must select one to five security groups for an instance and the security groups must be of the same type \(basic security group or advanced security group\).
-   Instances of some instance families cannot be migrated to a VPC if advanced VPC features are enabled on the VPC. For more information, see [Instance families that do not support advanced VPC features](/intl.en-US/Instance/Instance families that do not support advanced VPC features.md).
-   You can change the VPCs of up to 20 instances at a time.
-   After you change the VPC of an instance, the instance can no longer communicate with other instances in the original VPC. For information about how to communicate with other instances, see [What is Express Connect?](/intl.en-US/Product Introduction/What is Express Connect?.md)
-   The cut-through mode or multi-EIP to ENI mode cannot be enabled for the instance.
-   The instance cannot be associated with a high-availability virtual IP address \(HAVIP\).
-   The vSwitch of the instance cannot be associated with a custom route table.
-   Global Accelerator \(GA\) cannot be activated for the instance.

## Procedure

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Change the VPC of one or more ECS instances at a time.

    -   Change the VPC of a single instance

        Find the instance for which you want to change the VPC, and choose **More** \> **Network and Security Group** \> **Change VPC** in the **Actions** column.

    -   Change the VPCs of multiple ECS instances at a time

        Select the instances for which you want to change the VPCs, and choose **More** \> **Network and Security Group** \> **Change VPC** in the lower part of the page.

5.  In the **Change VPC** wizard, follow the instructions to change the VPC of the ECS instance.

    ![Change VPC](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3357298951/p120673.png)

    1.  In the **Prepare** step, check the network information and precautions and click **Next**.

    2.  In the **Select VPC** step, configure the **Destination VPC**, **Destination VSwitch**, and **Destination Security Group** parameters and click **Next**.

    3.  In the **Configure Primary Private IP Address** step, specify a primary private IP address for the selected instance to use in the destination VPC.

        -   The primary private IP address must be within the CIDR block of the destination vSwitch.
        -   If you do not manually set the primary private IP address, the system assigns one.
    4.  Click **OK**.


After you change the VPC of the instance, you can click the instance ID to view the new VPC and vSwitch in the **Network Information** section on the **Instance Details** page.

**Related topics**  


[ModifyInstanceVpcAttribute](/intl.en-US/API Reference/Networks/ModifyInstanceVpcAttribute.md)

