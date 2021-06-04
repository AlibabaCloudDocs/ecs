---
keyword: [security group rules, access control list \(ACL\), deny access, allow access]
---

# Add security group rules

This topic describes how to add security group rules. You can use security group rules to allow or deny access to or from public or internal IP addresses for ECS instances in a security group.

Before you add security group rules, a list of public or internal IP addresses for which you want to allow or deny access to or from your instances is obtained. For information about the scenarios of adding security group rules, see [Scenarios for security groups](/intl.en-US/Security/Security groups/Scenarios for security groups.md).

Security groups control access to or from the public or internal IP addresses. For security purposes, most security groups use Forbid rules for inbound traffic. If you use the default security group, the system adds security group rules for some communication ports.

This topic is suitable for the following scenarios:

-   When an application needs to communicate with a network outside the security group but the access request remains in the wait state, you must add an Allow rule first.
-   When attacks are detected from some requests during the application operation, you can add Forbid rules to isolate those malicious requests.

Before you add security group rules, take note of the following items:

-   Before you add rules to a basic security group, all outbound traffic from the security group is allowed, and all inbound traffic to the security group is denied.
-   Before you add rules to an advanced security group, all outbound and inbound traffic of the security group is denied. For advanced security groups, you cannot set Authorization Type to Security Group in security group rules.
-   The total number of inbound and outbound rules in each security group cannot exceed 200.

For more information, see [Overview](/intl.en-US/Security/Security groups/Overview.md).

1.  Go to the Security Groups page.

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.

    3.  In the top navigation bar, select a region.

2.  Find the security group to which you want to add a rule and click **Add Rules** in the **Actions** column.

3.  Select the security group rule direction.

    |Network type|Rule direction|
    |------------|--------------|
    |Virtual private cloud \(VPC\)|    -   Inbound: controls inbound traffic from both the Internet and internal network.
    -   Outbound: controls outbound traffic to both the Internet and internal network. |
    |Classic network|    -   Internet ingress.
    -   Internet egress.
    -   Inbound: controls inbound traffic from the internal network.
    -   Outbound: controls outbound traffic to the internal network. |

4.  On the Security Group Rules page, use one of the following methods to add rules:

    -   Method 1: Quickly create security group rules

        This method is ideal for configuring common TCP forwarding rules. Click **Quick Add** and then set **Action** and **Authorization Object**. Select one or more ports.

    -   Method 2: Manually add security group rules

        You can set the Action, Priority, and Protocol Type parameters. Perform the following steps to manually add a security group rule:

    1.  Click **Add Rule**.

    2.  Configure the new security group rule by setting the parameters described in the following table.

        |Parameter|Description|
        |---------|-----------|
        |Action|        -   **Allow**: allows access requests on the specified port.
        -   **Forbid**: discards data packets and returns no messages.
If two security group rules differ only in their actions, the **Forbid** rule is used but the **Allow** rule is ignored. |
        |Priority|A smaller value indicates a higher priority. Valid values: 1 to 100.|
        |Protocol Type|The protocol type of the security group rule. Valid values:         -   **All**
        -   **Custom TCP**
        -   **Customized UDP**
        -   **All ICMP \(IPv4\)**
        -   **All GRE**
For more information about the **Protocol Type** and **Port Range** parameters, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md) and [Common ports used by applications](/intl.en-US/Security/Security groups/Typical applications of commonly used ports.md).|
        |Port Range|You can specify a custom port range when **Protocol Type** is set to **Custom TCP** or **Customized UDP**. Enter one or more port ranges. Separate multiple port ranges with commas \(,\). Example: `22/23,443/443`.|
        |Authorization Object|You can set the following authorization objects:         -   IP addresses

You can enter a single IP address. Example: 192.168.0.100.

        -   CIDR blocks

You can enter a CIDR block. Example: 192.168.0.0/24. For more information about the CIDR format, see [What is CIDR?](/intl.en-US/Network/Network FAQ.md)

        -   Security groups

This authorization type is valid only for the internal network. You can specify a security group within the current account or a different account as the authorization object to control access to or from the instances in that security group for the instances in the current security group.

**Note:** For advanced security group rules, you cannot select a security group for Authorization Object.

            -   Authorize a security group within the current account: Enter the ID of the security group that you want to authorize within the current account. If the current security group is of the VPC type, the security group that you want to authorize must reside in the same VPC as the current security group.
            -   Authorize a security group within a different account: Enter the ID of the different Alibaba Cloud account and the ID of the security group that you want to authorize in the `ID of the Alibaba Cloud account/ID of the security group` format. You can choose **Account Management** \> **Security Settings** to view your account ID.
Take note of the following items:

        -   You can enter up to 10 authorization objects at a time. Separate multiple objects with commas \(,\).
        -   If you enter 0.0.0.0/0 as an authorization object, all IP addresses are allowed or denied based on the Action parameter. Evaluate the network risks before you specify 0.0.0.0/0.
        -   For security reasons, we recommend that you select a security group for Authorization Object when you add an internal inbound rule to a security group of the classic network type. If you want to authorize IP addresses, you can enter only a single IP address. You cannot enter CIDR blocks. |
        |Description|The description of the security group rule.|

    3.  Click **Save** in the **Actions** column.


After the security group rule is added, you can view it in the security group rule list. Changes to a security group rule are automatically applied to the ECS instances in the security group. We recommend that you immediately check whether the changes are applied.

## FAQ

-   **Why am I unable to access services after I configure a security group?**

    When the traffic on a port is allowed by a security group rule in the console, access to and from the port is not limited but this does not indicate that this port is enabled. To allow Internet access to a port of an ECS instance, the following requirements must be met:

    -   Traffic on the port is allowed by a security group rule.
    -   The corresponding application software is in the running state, and the listening address is 0.0.0.0. You can run the netstat -ano \|findstr <Port number\> command to check whether the port is a listening port.
    -   The internal firewall of the instance is disabled, or traffic on the port is allowed by the firewall.
-   **Why am I unable to use SMTP port 25 to create an email server?**

    The default SMTP port for outbound Internet traffic is port 25, which is disabled by default. It cannot be enabled by security group rules. To use SMTP port 25, take preventive measures to minimize security risks and then request to enable the port. For more information, see [Request to enable TCP port 25](https://www.alibabacloud.com/help/doc-detail/56130.htm).

-   **What is the relationship between protocol types and port ranges in security groups?**

    The following table describes the relationship between protocol types and port ranges in security groups. For more information about commonly used ports, see [Common ports used by applications](/intl.en-US/Security/Security groups/Typical applications of commonly used ports.md).

    |Protocol type|Port range|Scenario|
    |:------------|:---------|:-------|
    |All|-1/-1 is displayed, which indicates all ports. You cannot configure a port range for this protocol type.|It can be used in all trusted scenarios.|
    |All ICMP \(IPv4\)|-1/-1 is displayed, which indicates all ports. You cannot configure a port range for this protocol type.|It can be used when you run the `ping` command to check the status of network connections between ECS instances.|
    |All GRE|-1/-1 is displayed, which indicates all ports. You cannot configure a port range for this protocol type.|It can be used for VPN.|
    |Custom TCP|A custom port range. Valid values of port numbers: 1 to 65535. You must use the <start port\>/<end port\> format. For example, 80/80 indicates port 80, and 1/22 indicates ports 1 to 22.

|It can be used to allow or deny traffic on one or more successive ports.|
    |Customized UDP|A custom port range. Valid values of port numbers: 1 to 65535. You must use the <start port\>/<end port\> format. For example, 80/80 indicates port 80, and 1/22 indicates ports 1 to 22.

|It can be used to allow or deny traffic on one or more successive ports.|

    The following table describes TCP ports used by common Internet applications.

    |Scenario|Protocol type|Port range|Description|
    |--------|:------------|:---------|:----------|
    |Connection to a server|SSH|22/22|It can be used to connect to a Linux instance. After you connect to the instance, you can modify the port number. For more information, see [Modify the default remote port of an instance](/intl.en-US/Best Practices/Security/Modify the default remote port of an instance.md).|
    |TELNET|23/23|It can be used to connect to an instance.|
    |RDP|3389/3389|It can be used to connect to a Windows instance. After you connect to the instance, you can modify the port number. For more information, see [Modify the default remote port of an instance](/intl.en-US/Best Practices/Security/Modify the default remote port of an instance.md).|
    |Website service|HTTP|80/80|It can be used when an instance serves as a website or web application server.|
    |HTTPS|443/443|It can be used when an instance serves as a website or web application server that supports the HTTPS protocol.|
    |Database|MS SQL|1433/1433|It can be used when an instance serves as an MS SQL server.|
    |Oracle|1521/1521|It can be used when an instance serves as an Oracle SQL server.|
    |MySQL|3306/3306|It can be used when an instance serves as a MySQL server.|
    |PostgreSQL|5432/5432|It can be used when an instance serves as a PostgreSQL server.|
    |Redis|6379/6379|It can be used when an instance serves as a Redis server.|


**Related topics**  


[AuthorizeSecurityGroup](/intl.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md)

[AuthorizeSecurityGroupEgress](/intl.en-US/API Reference/Security groups/AuthorizeSecurityGroupEgress.md)

