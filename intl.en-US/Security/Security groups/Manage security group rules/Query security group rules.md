---
keyword: Query security group rules
---

# Query security group rules

This topic describes how to query security group rules. After you add security group rules, you can query their details in the console.

A security group is created and security group rules are added. For more information, see [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md) and [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.

3.  In the top navigation bar, select a region.

4.  Find the security group whose rules you want to query, and then click **Add Rules** in the **Actions** column.

5.  Click a rule direction to query the corresponding security group rules.

    -   If the security group is of the VPC type, select **Inbound** or **Outbound**.
    -   If the security group is of the classic network type, select **Internal Network Ingress**, **Internal Network Egress**, **Internet Ingress**, or **Internet Egress**.

**Related topics**  


[DescribeSecurityGroupAttribute](/intl.en-US/API Reference/Security groups/DescribeSecurityGroupAttribute.md)

