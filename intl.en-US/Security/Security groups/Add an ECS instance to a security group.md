---
keyword: add an instance to a security group
---

# Add an ECS instance to a security group

You can add an ECS instance to one or more security groups based on your business needs. By default, an ECS instance can be added to a maximum of five security groups.

Before you add an ECS instance to a security group, make sure that the following requirements are met:

-   An instance is created. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).
-   The ECS instance and the security group to which you want to add the instance are of the same network type.
-   If the ECS instance already belongs to a security group, this new security group must be of the same type as the security group to which the ECS instance already belongs. For more information, see [Overview](/intl.en-US/Security/Security groups/Overview.md) and [Advanced security groups](/intl.en-US/Security/Security groups/Advanced security groups.md).

Security groups are an important means for security isolation. A security group can control access to or from the one or more ECS instances in it. An ECS instance must belong to one to five security groups.

The following list describes how to add an ECS instance to a security group on the Instances page. You can also choose **Network & Security** \> **Security Groups** in the left-side navigation pane of the Overview page to add an ECS instance to a security group.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  On the **Instances** page, find the ECS instance and click **Manage** in the **Actions** column.

5.  On the **Instance Details** page, click the **Security Groups** tab.

6.  Click **Add to Security Group**.

7.  In the Add to Security Group dialog box, select a security group from the drop-down list. To add the ECS instance to multiple security groups, select a security group and click **Join Multiple Security Groups**. The selected security group is automatically added to the selection box that appears. Repeat this operation to add more security groups to the selection box.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7138203261/p48434.png)

8.  Click **OK**.

    After the ECS instance is added to a security group, the security group rules in the security group automatically apply to the instance.


-   You can view all security groups that you create within a region. For more information, see [Query security groups](/intl.en-US/Security/Security groups/Manage security groups/Query security groups.md).
-   You can remove an instance from one or more security groups. After an ECS instance is removed from a security group, the instance is isolated from the other ECS instances in the security group. To ensure that services can run properly after an ECS instance is removed, we recommend that you perform sufficient tests before you remove the ECS instance. For more information, see [Remove an instance from a security group](/intl.en-US/Security/Security groups/Manage security groups/Remove an instance from a security group.md).
-   You can delete one or more security groups that are no longer needed. When a security group is deleted, its rules are also deleted. For more information, see [Delete security groups](/intl.en-US/Security/Security groups/Manage security groups/Delete security groups.md).
-   If you want to check whether a common port is enabled by a security group rule or whether one-way access is enabled between a specific IP address and a network interface controller \(NIC\), choose **Maintenance & Monitoring** \> **Troubleshooting** in the left-side navigation pane and click the **Check Security Group Rules** tab.

**Related topics**  


[ModifyInstanceAttribute](/intl.en-US/API Reference/Instances/ModifyInstanceAttribute.md)

[ModifyNetworkInterfaceAttribute](/intl.en-US/API Reference/Elastic network interfaces/ModifyNetworkInterfaceAttribute.md)

