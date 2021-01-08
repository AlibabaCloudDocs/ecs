# Best practices of the security group \(part 3\)

In practice, all instances may be placed in the same security group, thus reducing the configuration workload in the initial period. In the long run, however, interactions of the business systems will become complicated and uncontrollable. When you modify a security group, you will be unable to clearly identify the impact scope of adding or removing a rule.

Rational planning and differentiation of security groups makes it easy to adjust your systems, sort out the services provided by the applications, and arrange applications at different layers. We recommend that you plan different security groups and set different security group rules for different businesses.

## Distinguish between different security groups

-   **Use different security groups for ECS instances on the Internet and those on the intranet**

    ECS instances that provide Internet services, either through exposure of some ports for external access \(such as 80 and 443\) or through provision of port forwarding rules \(for example, instances configured with forwarding rules for Internet IP address, EIP address or NAT ports\), will expose their applications to the Internet.

    For the two scenarios above, the relevant security groups should adopt the strictest rules. We recommend that Internet access should be rejected first. Specifically, all ports and protocols should be disabled by default except the ports needed to provide external services, such as 80 and 443. As the security group only contains the ECS instances that provide Internet access, it is easier to adjust the security group rules.

    For a group of ECS instances that provide Internet access, their responsibilities should be clear and simple, avoiding offering other external services on the same instances. For MySQL, Redis, and more, for example, it is recommended to install such services on ECS instances that disable Internet access, and then enable access to them through security group authorization.

    Assume you have an ECS instance that provides Internet access, which is in the security group SG\_CURRENT as the instances of other applications. You can make changes by performing the steps below.

    1.  Sort out the ports and protocols exposed by the current Internet services, such as 80 and 443.
    2.  Create a new security group such as SG\_WEB and add corresponding ports and rules.

        **Note:** Action: Allow; Protocol Type: All; Port Range: 80/80; Authorization Objects: 0.0.0.0/0; Action: Allow; Protocol Type: All; Port Range: 443/443; Authorization Objects: 0.0.0.0/0.

    3.  Select the security group SG\_CURRENT and add a rule for security group authorization, that is, allowing the resources in SG\_WEB to access the resources in SG\_CURRENT.

        **Note:** Action: Allow; Protocol Type: All; Port Range: -1/-1; Authorization Objects: SG\_WEB; Priority: Choose from \[1-100\] according to actual conditions.

    4.  Add ECS\_WEB\_1 to the new security group. It is an instance that needs to switch its security group.
        1.  In the ECS console, select **Security groups**.
        2.  Select **SG\_WEB** \> **Manage Instances** \> **Add Instance**. Add the instance ECS\_WEB\_1 to the new security group SG\_WEB. Make sure ECS\_WEB\_1 works normally.
    5.  Remove the instance ECS\_WEB\_1 from the original security group.
        1.  In the ECS console, select **Security Groups**.
        2.  Select **SG\_WEB** \> **Manage Instances** \> **Add Instance**. Select ECS\_WEB\_1 and remove it from SG\_CURRENT. Verify that the traffic and network are in normal condition.
        3.  If errors occur, add ECS\_WEB\_1 back to the security group SG\_CURRENT. Check whether the ports of SG\_WEB are exposed as expected, and then make adjustments accordingly.
    6.  Make other changes to the security group.
-   **Use different security groups for different applications**

    In production environments, different operating systems generally do not belong to the same application group to provide load balancing services. Providing different services means that exposed ports are different from rejected ports. Therefore, it is recommended that instances with different operating systems belong to different security groups.

    For example, TCP port 22 may be exposed for implementing SSH in Linux, while TCP port 3389 may be exposed for implementing remote desktop connection in Windows.

    In addition, for instances that have the same type of images but provide different services, it is recommended to put them into different security groups if they do not need to access each other over the intranet. This facilitates decoupling and future changes to security group rules as the rules can be as simple as possible.

    When planning and adding new applications, you should reasonably organize the security groups apart from dividing different VSwitches to configure subnets. You can use network segments and security groups to distinguish yourself as the service provider or consumer.

    For specific change procedures, see the operations above.

-   **Use different security groups for production environments and testing environments**

    To better isolate systems, you may build multiple testing environments and one online environment during actual development. For better network isolation, you need to configure different security policies for different environments, preventing changes to the testing environment from being synchronized to the online environment, which may affect the stability of online services.

    By creating different security groups, you can restrict the access domains of applications and avoid interoperability between the production environment and testing environment. Also, you can create different security groups for different test environments, thus avoiding interference between test environments and improving development efficiency.


## Only assign Internet addresses to subnets or instances that require Internet access

Whether it is a classic network or a VPC, rational allocation of Internet addresses facilitates Internet management of the system and reduces the risk of attack. For VPCs, we recommend that you place the IP segments of instances requiring Internet access onto several dedicated VSwitches \(subnet CIDR\) when creating a VSwitch. This facilitates auditing and differentiation and helps avoid accidental Internet access.

Most distributed applications have different layers and groups. For ECS instances that offer no Internet access, try your best not to provide Internet addresses for them. If there are multiple instances that provide Internet access, we recommend you to configure the [Server Load Balancer](/intl.en-US/Classic Load Balancer/Product Introduction/What is SLB?.md) to distribute traffic of Internet services, thus improving system availability and avoiding a single point of failure.

For ECS instances that require no Internet access, try your best not to assign Internet addresses to them. In VPCs, when your ECS instances need to access the Internet, we recommend you to use the [NAT gateway](/intl.en-US/Product Introduction/What is NAT Gateway?.md) to provide Internet proxy services for ECS instances without Internet addresses in the VPC. By simply configuring the corresponding SNAT rules, you can enable a specific CIDR segment or subnet to access the Internet. For specific configurations, see [Create a SNAT entry to access the Internet](/intl.en-US/User Guide/Create a SNAT entry to access the Internet.md). In this way, exposure of services to the Internet can be avoided after Elastic IP \(EIP\) addresses are allocated when only outbound access is required.

## Minimum principle

A security group should work as a whitelist. Therefore, try your best to open and expose as few ports as possible, and allocate as few Internet addresses as possible. Although allocating Internet addresses or binding EIPs makes it easy to access online instances for troubleshooting, it exposes the entire instance to the Internet after all. A safer policy is to manage IP addresses by using the Jump Server.

## Use the Jump Server

As the Jump Server has much higher permissions, relevant operations should be well recorded and audited through tools. In addition, it is recommended to choose a dedicated VSwitch for the Jump Server in VPCs, providing the corresponding EIP or NAT port forwarding tables to it.

First, create a dedicated security group SG\_BRIDGE by enabling the corresponding port such as TCP 22 in Linux or RDP 3389 in Windows. To restrict the inbound access, you can limit the authorization objects to the Internet egress ports of your company, lowering the probability of being scanned and accessed.

After that, you can add the Jumper Server instance to that security group. In order for that Jumper Server to access other appropriate instances, you can configure appropriate group authorization. For example, add a rule for SG\_CURRENT, allowing SG\_BRIDGE to access certain ports and protocols.

When you use the Jumper Server for SSH communication, it is recommended to use the [SSH key pair](/intl.en-US/Security/Key pairs/Overview.md) for logon, instead of the password.

In summary, reasonable planning of security groups makes it easy for you to expand the applications and makes your system more secure.

