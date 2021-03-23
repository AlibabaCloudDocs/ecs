# Make ECS instances more secure

An ECS instance serves as a virtual machine. Typically, on-premises virtual machines are protected against attacks and intrusions. ECS instances also need security protection. You must implement effective security measures in conjunction with the inherent protection of Alibaba Cloud.

An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).

Lack of security protection for ECS instances may cause adverse effects. For example:

-   DDoS attacks interrupt your business.
-   Trojans tamper with or attack your web pages.
-   Data leak caused by injection affects the normal operation of ECS.

You can use the following methods to improve the security of your ECS instances:

-   [Configure security groups](#section_bp7_wr3_8nr)
-   [Enable Anti-DDoS Basic](#section_xyh_fkq_gfb)
-   [Access Security Center](#section_ezh_fkq_gfb)
-   [Access Web Application Firewall](#section_9b9_grv_99n)

## Configure security groups

A security group is a virtual firewall that provides stateful packet inspection \(SPI\). Security groups can serve the following purposes:

-   Control access to one or more ECS instances. Security group rules can allow or deny inbound or outbound Internet and internal network traffic for ECS instances associated with security groups.
-   If security groups are not planned properly or do not contain strict enough rules, they will be at a much greater risk of attack.

To add a rule to the security group associated with the ECS instance, perform the following operations:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.

3.  In the top navigation bar, select a region.

4.  Find the security group to which to add a rule. Click **Add Rules** in the **Actions** column.

5.  Click **Add Security Group Rule**.

6.  In the dialog box that appears, configure the parameters.

    For example, to allow a specific IP address to access the ECS instance, configure an inbound rule for Internet traffic. Assume that the instance runs the Linux operating system and you want to allow only the specific IP address to access the instance over port 22.

    1.  Add the following inbound rule for Internet traffic:

        -   Set **Action** to **Allow**.
        -   Set **Protocol Type** to **Custom TCP**.
        -   Set **Port Range** to 22/22.
        -   Set **Authorization Type** to **IPv4 CIDR Block**.
        -   Set **Authorization Object** to the CIDR block that is allowed to access to the ECS instance, in the format of x.x.x.x/xx \(IP address/subnet mask\). In this example, the CIDR block is 10.x.x.x/32. The priority is 1.
    2.  Add another inbound rule for Internet traffic:

        -   Set **Action** to **Forbid**.
        -   Set **Protocol Type** to **Custom TCP**.
        -   Set **Port Range** to 22/22.
        -   Set **Authorization Type** to **IPv4 CIDR Block**.
        -   Set **Authorization Object** to 0.0.0.0/0. The priority is 2.
7.  Click **OK**.

    After the two rules are created, they can implement the following effects:

    -   The allow rule with a priority of 1 takes precedence for traffic from 10.x.x.x to port 22.
    -   The deny rule with a priority of 2 takes precedence for traffic from other IP addresses to port 22.

## Enable Anti-DDoS Basic

Distributed denial of service \(DDoS\) attacks use client and server technologies to combine multiple computers into an attack platform and attack one or more targets simultaneously so that the impact of the denial-of-service \(DoS\) attack is multiplied.

Alibaba Cloud Security can defend against Layer 3 to Layer 7 DDoS attacks, including SYN Flood, UDP Flood, ACK Flood, ICMP Flood, DNS Flood, and HTTP Flood attacks. Anti-DDoS Basic provides up to 5 Gbit/s default DDoS protection free of charge. By default, Anti-DDoS Basic is enabled on ECS instances. Anti-DDoS eliminates the need to purchase expensive traffic scrubbing devices and allows you to maintain the access speed during DDoS attacks. Anti-DDoS help ensure your bandwidth regardless of the usage of other users. This ensures the availability and stability of your business. After an ECS instance is created, you can set the scrubbing thresholds. For more information, see [Configure a cleaning threshold](/intl.en-US/Anti-DDoS Origin User Guide/Cleaning settings/Configure a cleaning threshold.md).

Alibaba Cloud has also launched the Security Credibility program, which provides improved DDoS protection based on a security credit score. Users that meet the criteria can obtain free protection against DDoS attacks up to 100 Gbit/s. In the Anti-DDoS Basic console, you can check your current security credibility score and details, as well as scoring criteria. For more information, see [Security Credibility](/intl.en-US/Legal Terms/Anti-DDoS Origin/Security Credibility.md).

## Access Security Center

Security Center is a unified security management system that recognizes, analyzes, and warns of security threats in real time. With security capabilities such as ransomware protection, anti-virus protection, web tamper protection, and compliance assessments, users can automate security operations, responses, and threat tracing to secure cloud and local servers and meet regulatory compliance requirements.

The Security Center agent is a security plug-in installed on your local servers. You must install this agent on your servers before you can enable Security Center features. For more information about how to install the Security Center agent, see [Install the Security Center agent](/intl.en-US/Access Cloud Security Center/Install the Security Center agent.md).

**Note:** When you purchase an ECS instance, you can select the **Security Enhancement** check box to automatically install the agent and activate Security Center Basic edition.

The Basic edition of Security Center is available by default. The Basic edition only scans for the following risks: unusual logons to servers, vulnerabilities, and configuration risks in cloud services. To use advanced features such as vulnerability fixing and virus detection and removal, you must log on to the [Security Center console](https://yundunnext.console.aliyun.com/?p=sas).

## Access Web Application Firewall

Web Application Firewall \(WAF\) is implemented based on the big data capabilities of Apsara Stack Security. This module protects web applications against common attacks reported by OWASP, such as SQL injections, XSS, vulnerability exploits in web server plugins, trojan attacks, and unauthorized access. WAF blocks malicious visits to avoid data from being compromised and ensure the security and availability of your websites.

WAF has the following benefits:

-   WAF can handle various web application attacks to ensure web security and availability of a website without installing software or hardware or modifying website configuration and code. In addition to powerful web protection capabilities, WAF can customize protection for specific websites. WAF is used to protect web applications in fields such as finance, e-commerce, O2O, Internet Plus, gaming, governments, and insurance.
-   Without WAF, you may be vulnerable to web intrusions such as data leaks, HTTP floods, and trojans.

For more information about how to access WAF, see [Deploy WAF](/intl.en-US/Quick Start/Quick start.md).

Alibaba Cloud provides multiple security services to safeguard ECS instances. You can choose appropriate methods to enhance systems and data protection, prevent intrusion into ECS instances, and ensure stability and reliability.

