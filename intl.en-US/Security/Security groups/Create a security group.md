---
keyword: [security group, security group rules, virtual firewall, network access control, trituple, quintuple]
---

# Create a security group

A security group functions as a virtual firewall to control network access of Elastic Compute Service \(ECS\) instances. Each instance must belong to at least one security group. This topic describes how to create a security group and configure security group rules in the ECS console.

A virtual private cloud \(VPC\) and a vSwitch are created if you want to create a VPC-type security group. For more information, see [Work with VPCs](/intl.en-US/VPCs and vSwitchs/Work with VPCs.md).

If no security groups have been created when you create an ECS instance, a default security group is created. The default security group has the following default rules:

-   A default rule that supports the ICMP protocol for operations such as pinging the ECS instance.
-   A default inbound rule that allows traffic on SSH port 22 and RDP port 3389 to access the ECS instance.
-   An optional inbound rule that allows traffic on HTTP port 80 and HTTPS port 443. If you want to build websites by using ECS instances, you must enable HTTP port 80 and HTTPS port 443.

If you want the ECS instance to be added to a custom security group, you can perform the following operations to create a security group. For more information, see [Overview](/intl.en-US/Security/Security groups/Overview.md).

1.  Go to the Security Groups page.

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

    2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.

    3.  In the top navigation bar, select a region.

2.  Click **Create Security Group**.

3.  In the **Basic Information** section, set the parameters for the security group.

    |Parameter|Description|
    |---------|-----------|
    |Security Group Name|Specify a security group name.|
    |Description|Enter a brief description of the security group for future management.|
    |Network|Set the network type of the security group.     -   To create a VPC-type security group, select an existing VPC.
    -   To create a classic network-type security group, select **Classic Network**. |
    |Security Group Type|Select a security group type.     -   Basic Security Group: applicable to scenarios with small-scale clusters and moderate network connections.
    -   Advanced Security Group: applicable to scenarios with large-scale clusters that require highly efficient O&M.
For other functional differences between basic and advanced security groups, see [Overview](/intl.en-US/Security/Security groups/Overview.md). |
    |Resource Group|Select a resource group to which to assign the security group to facilitate subsequent O&M.|
    |Tags|Configure tags for the security group to facilitate subsequent O&M.|

4.  In the **Access Rule** section, configure the security group rule.

    The system configures a default security group rule that has the basic configurations. If you want to make custom configurations, you can perform the following operations. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    1.  Click the **Inbound** or **Outbound** tab to select the security group rule direction.

        |Network type|Rule direction|
        |------------|--------------|
        |VPC|        -   Inbound: controls inbound traffic from both the Internet and internal network.

By default, the inbound rules are configured for the ICMP protocol, SSH port 22, RDP port 3389, HTTP port 80, and HTTPS port 443.

        -   Outbound: controls outbound traffic to both the Internet and internal network.

By default, all ports are enabled to allow outbound access of basic security groups, and all ports are disabled to deny outbound access of advanced security groups. |
        |Classic network|        -   Internet Ingress: By default, the inbound rules are configured for the ICMP protocol, SSH port 22, RDP port 3389, HTTP port 80, and HTTPS port 443.
        -   Internet Egress: By default, all ports are enabled.
        -   Inbound: By default, all ports are disabled to deny inbound access over the internal network.
        -   Outbound: By default, all ports are enabled to allow outbound access over the internal network. |

    2.  Click **Add Rule**.

    3.  Configure custom security group rules.

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

5.  Click **Create Security Group**.


After the security group is created, it is displayed in the security group list.

![Creation result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3541472061/p96162.png)

-   You can configure security group rules to allow or deny access to or from the Internet or internal network for ECS instances in a security group. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).
-   Each ECS instance must belong to at least one security group. You can add an instance to one or more security groups. For more information, see [Add an ECS instance to a security group](/intl.en-US/Security/Security groups/Add an ECS instance to a security group.md).

**Related topics**  


[CreateSecurityGroup](/intl.en-US/API Reference/Security groups/CreateSecurityGroup.md)

