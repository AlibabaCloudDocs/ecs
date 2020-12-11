---
keyword: [security group, virtual firewall, network access control]
---

# Create a security group

A security group functions as a virtual firewall to control network access of ECS instances. This topic describes how to create a security group in the ECS console.

A VPC and a vSwitch are created if you want to create a VPC-type security group. For more information, see [Create a VPC](/intl.en-US/VPCs and VSwitches/VPC management/Create a VPC.md).

Each ECS instance must belong to at least one security group. If no security groups have been created when you create an ECS instance, a default security group is created. The default security group has only inbound rules configured for the ICMP protocol, SSH port 22, RDP port 3389, HTTP port 80, and HTTPS port 443. For more information, see [Overview](/intl.en-US/Security/Security groups/Overview.md). If you do not want the ECS instance to be added to the default security group, you can create a security group as described in this topic.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.

3.  In the top navigation bar, select a region.

4.  Click **Create Security Group**.

5.  In the **Create Security Group** dialog box, configure the parameters for the security group.

    |Parameter|Description|
    |---------|-----------|
    |Template|Select a suitable template based on the services to be deployed on the ECS instances to make it easy to configure security group rules. Valid values:    -   Web Server Linux: applicable to Linux instances where web services need to be deployed.
    -   Web Server Windows: applicable to Windows instances where web services need to be deployed.
    -   Custom: You must add security group rules to the security group after it is created. |
    |Security Group Name|Specify a security group name.|
    |Description|Enter a brief description of the security group for future management.|
    |Security Group Type|Select a security group type.     -   Basic security group: applicable to scenarios with small-scale clusters and moderate network connections.
    -   Advanced security group: applicable to scenarios with large-scale clusters that require highly efficient O&M.
For other functional differences between basic and advanced security groups, see [Overview](/intl.en-US/Security/Security groups/Overview.md). |
    |Network Type|Set the network type of the security group.     -   To create a VPC-type security group, select **VPC**.
    -   To create a classic network-type security group, select **Classic**. |
    |VPC|Select the VPC in which your ECS instances reside. This parameter is required only when you set **Network Type** to **VPC**.|
    |Resource Group|Select a resource group to which to assign the security group to facilitate subsequent O&M.|
    |Tag|Configure tags for the security group to facilitate subsequent O&M.|

6.  Click **OK**.


After the security group is created, it is displayed in the security group list.

![Creation result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3541472061/p96162.png)

-   You can configure security group rules to allow or deny access to or from the Internet or internal network for ECS instances in a security group. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).
-   Each ECS instance must belong to at least one security group. You can add an instance to one or more security groups. For more information, see [Add an ECS instance to a security group](/intl.en-US/Security/Security groups/Add an ECS instances to a security group.md).

**Related topics**  


[CreateSecurityGroup](/intl.en-US/API Reference/Security groups/CreateSecurityGroup.md)

