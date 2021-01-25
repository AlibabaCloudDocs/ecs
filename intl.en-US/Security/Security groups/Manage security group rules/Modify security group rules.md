---
keyword: Modify security group rules
---

# Modify security group rules

This topic describes how to modify security group rules. Improper configurations of security group rules may cause serious security risks. You can modify improper rules in a security group to ensure the network security of instances within the security group.

A security group is created and security group rules are added. For more information, see [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md) and [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

Security group rules that do not limit traffic on certain points may be exposed to serious security risks. You can modify security group rules to ensure the network security of instances.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.

3.  In the top navigation bar, select a region.

4.  Find the security group whose rules you want to modify, and then click **Add Rules** in the **Actions** column.

5.  Select a direction of security group rules.

    -   If the security group is of the VPC type, select **Inbound** or **Outbound**.
    -   If the security group is of the classic network type, select **Internal Network Ingress**, **Internal Network Egress**, **Internet Ingress**, or **Internet Egress**.
6.  Find the security group rules that you want to modify and click **Modify** in the **Actions** column.

    -   For information about how to configure a security group rule, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.mdul_vpc_qwz_xdb).
    -   For information about how to use security group rules, see [Typical applications of security group rules]().
7.  After you modify security group rules, click **OK**.


