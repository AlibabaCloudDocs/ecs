---
keyword: [security group rule, security group, ECS security group rule]
---

# Add security group rules

This topic describes how to add security group rules. You can use security group rules to allow or deny access to or from the Internet or internal networks for ECS instances in a security group.

Before you add security group rules, make sure that the following requirements are met:

-   A security group is created. For more information, see [Create a security group](/intl.en-US/Security/Security groups/Create a security group.md).
-   A list of Internet or internal networks for which you want to allow or deny access to or from your instances is obtained. For information about scenarios of adding security group rules, see [Scenarios for security groups](/intl.en-US/Security/Security groups/Scenarios for security groups.md).

Security groups control access to or from the Internet or internal networks. For security reasons, most security groups use Forbid rules for inbound traffic. If you use the default security group, security group rules are automatically added for some communication ports.

This topic is suitable for the following scenarios:

-   When an application needs to communicate with a network outside the security group but the access request stays in the wait state, you must add an Allow rule first.
-   When you detect attacks from some request sources during the application operation, you can add Forbid rules to isolate those malicious request sources.

Before you add security group rules, take note of the following items:

-   Before you add rules to a basic security group, all outbound traffic from the security group is allowed and all inbound traffic to the security group is denied.
-   Before you add rules to an advanced security group, all outbound and inbound traffic of the security group is denied. For advanced security groups, you cannot specify the Priority parameter, set Authorization Type to Security Group, or set Action to Forbid in security group rules.
-   The total number of inbound and outbound rules in each security group cannot exceed 200.

For more information, see [Overview](/intl.en-US/Security/Security groups/Overview.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.

3.  In the top navigation bar, select a region.

4.  Find the security group to which you want to add rules. Click **Add Rules** in the **Actions** column.

5.  On the Security Group Rules page, use one of the following methods to add rules:

    -   Method 1: Quickly create security group rules

        This method is applicable when ICMP and GRE are not required and you can select multiple ports. In the **Quick Rule Creation** dialog box, the following application ports are provided: SSH 22, Telnet 23, HTTP 80, HTTPS 443, MS SQL 1433, Oracle 1521, MySQL 3306, RDP 3389, PostgreSQL 5432, and Redis 6379. You can select one or more ports.

        Click **Quick Rule Creation**. In the Quick Rule Creation dialog box, configure parameters such as **NIC Type**, **Rule Direction**, and **Custom Port Range**. For more information about how to configure parameters for a security group rule, see Method 2: **Manually add security group rules**.

    -   Method 2. Manually add security group rules
        1.  Click **Add Security Group Rule**.
        2.  Add a security group rule in the rule list.

            |Parameter|Description|
            |---------|-----------|
            |NIC Type|The **NIC Type** parameter is required only for security group rules of the classic network type.            -   **Internal**: adds an internal security group rule of the classic network type.
            -   **Public**: adds a public security group rule of the classic network type. |
            |Rule Direction|The direction in which the security group rule is applied.            -   **Outbound**: Select this value if the ECS instances in the current security group need to access other ECS instances in an internal network or resources in the Internet.
            -   **Inbound**: Select this value if other ECS instances in an internal network or resources in the Internet need to access the ECS instances in the current security group. |
            |Action|            -   **Allow**: allows access requests on the specified port.
            -   **Forbid**: discards data packets and returns no messages. If two security group rules differ only in their actions, the **Forbid** rule is used while the **Allow** rule is ignored.
**Note:** Only **Allow** rules can be created for advanced security groups. |
            |Protocol Type|The protocol type of the security group rule.For the relationship between **Protocol Type** and **Port Range**, see [Table 2](#table_igi_6jy_v9s). For more information about common ports, see [Common ports used by applications](/intl.en-US/Security/Security groups/Typical applications of commonly used ports.md). |
            |Port Range|The port range depends on the protocol type. You can specify a custom port range when **Protocol Type** is set to **Custom TCP** or **Customized UDP**. Enter a port range manually. Example: `22/23,443/443`.|
            |Priority|A smaller value indicates a higher priority. Valid values: 1 to 100. **Note:** The Priority value of each rule in advanced security groups is fixed to 1. You cannot set Priority values for rules in advanced security groups. |
            |Authorization Type|Valid values: IPv4 CIDR Block and Security Group.**Note:** For advanced security group rules, you cannot set Authorization Type to Security Group. |
            |Authorization Object|Supported authorization objects include:             -   IPv4 CIDR block
                -   Enter IPv4 addresses or IPv4 CIDR blocks. Example: 12.1.1.1 or 13.1.1.1/25.

For more information about the CIDR format, see [Network FAQ](/intl.en-US/Network/Network FAQ.md).

                -   You can enter up to 10 authorization objects at a time. Separate multiple objects with commas \(,\).
                -   If you enter 0.0.0.0/0 as an authorization object, all IPv4 addresses are allowed or denied based on the Action parameter. Evaluate the network risks before you specify 0.0.0.0/0.
            -   Security group

**Note:** For advanced security group rules, you cannot set Authorization Type to Security Group.

This authorization type is valid only for internal networks. Specify a security group in your or another account as the authorization object to control to or from the instances in that security group for the instances in the current security group. For access to or from the Internet, you must specify CIDR blocks.

                -   Select Authorize Current Account and then select the ID of another security group in your account. If the current security group is of the VPC type, the selected security group must be in the same VPC as the current security group.
                -   Select Authorize Another Account and then enter a security group ID and the ID of another account to which the security group belongs. Choose **Account Management** \> **Security Settings** in the Account Center to view your account ID.
**Note:** For security reasons, we recommend that you set Authorization Object to Security Group when you add an internal inbound rule to a security group of the classic network type. If you set Authorization Object to CIDR blocks, you can specify only single IP addresses in CIDR notation in the a.b.c.d/32 format. Only IPv4 is supported, and the subnet mask must be /32. |
            |Description|The description of the security group rule.|

            |Protocol Type|Port Range|Scenario|
            |:------------|:---------|:-------|
            |All|-1/-1 is displayed, which indicates all ports. You cannot configure a port range for this protocol type.|It can be used in all trusted scenarios.|
            |All ICMP \(IPv4\)|-1/-1 is displayed, which indicates all ports. You cannot configure a port range for this protocol type.|It can be used when you run the `ping` command to check the status of network connections between ECS instances.|
            |All GRE|-1/-1 is displayed, which indicates all ports. You cannot configure a port range for this protocol type.|It can be used for VPN.|
            |Custom TCP|Specify a custom port range. Valid values of port numbers: 1 to 65535. You must use the <start port\>/<end port\> format. For example, 80/80 indicates port 80, and 1/22 indicates port 1 to port 22.

|It can be used to allow or deny traffic on one or more successive ports.|
            |Custom UDP|
            |SSH|22/22|It can be used to connect to a Linux instance. After you are connected to the instance, you can modify the port number. For more information, see [Modify the default remote port of an instance](/intl.en-US/Best Practices/Security/Modify the default remote port of an instance.md).|
            |TELNET|23/23|It is used to connect to an instance.|
            |HTTP|80/80|It is used when an instance serves as a website or web application server.|
            |HTTPS|443/443|It can be used when an instance serves as a website or web application server that supports the HTTPS protocol.|
            |MS SQL|1433/1433|It is used when an instance serves as an MS SQL server.|
            |Oracle|1521/1521|It is used when an instance serves as an Oracle SQL server.|
            |MySQL|3306/3306|It is used when an instance serves as a MySQL server.|
            |RDP|3389/3389|It can be used to connect to a Windows instance. After you are connected to the instance, you can modify the port number. For more information, see [Modify the default remote port of an instance](/intl.en-US/Best Practices/Security/Modify the default remote port of an instance.md).|
            |PostgreSQL|5432/5432|It is used when an instance serves as a PostgreSQL server.|
            |Redis|6379/6379|It can be used when an instance serves as a Redis server.|

            **Note:** The default SMTP port for outbound Internet traffic is port 25, which is disabled by default. It cannot be enabled by security group rules. To use SMTP port 25, take preventive measures to minimize security risks and then apply to enable the port. For more information,see [Apply to enable TCP port 25](https://www.alibabacloud.com/help/doc-detail/56130.htm).

        3.  Click **OK**.

After the security group rule is added, you can view it in the security group rule list. Changes to a security group rule are automatically applied to the ECS instances in the security group. We recommend that you immediately check whether the changes take effect.

An ECS instance must belong to at least one security group. You can add an instance to one or more security groups. For more information, see [Add an ECS instance to a security group](/intl.en-US/Security/Security groups/Add an ECS instances to a security group.md).

**Related topics**  


[AuthorizeSecurityGroup](/intl.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md)

[AuthorizeSecurityGroupEgress](/intl.en-US/API Reference/Security groups/AuthorizeSecurityGroupEgress.md)

