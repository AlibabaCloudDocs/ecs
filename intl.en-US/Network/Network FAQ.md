---
keyword: [outbound bandwidth, website access failure, IP address query, traffic monitoring]
---

# Network FAQ

This topic provides answers to frequently asked questions about networks used by Elastic Compute Service \(ECS\) instances.

-   FAQ about network performance
    -   [What is the packet loss rate when instances within different regions communicate over the Internet?](#section_t34_uni_zg6)
    -   [How is the network latency for instances within the same region that communicate over the internal network?](#section_vjv_lqq_ymq)
    -   [How is the performance of connections guaranteed for instances for which the maximum number of connections is not specified?](#section_sw7_2hi_kcv)
    -   [What do I do if the performance of an ECS instance is unstable when a UDP PPS test or TCP bandwidth test is performed on the instance?](#section_g5u_a6e_dwa)
-   FAQ about public bandwidth
    -   [What are the inbound and outbound bandwidths of ECS instances?](#section_pv3_qbl_qgb)
    -   [I purchased a public bandwidth of 5 Mbit/s for an ECS instance. How is this bandwidth applied to the inbound and outbound bandwidths of the instance?](#section_v44_ona_zjq)
    -   [Is public bandwidth exclusive to each ECS instance, or is public bandwidth shared among multiple instances?](#section_sp8_7jn_p3g)
    -   [How am I billed for the network usage of ECS instances?](#section_hex_69p_rar)
    -   [Why is 200 Kbit/s of inbound traffic already consumed on a newly created ECS instance?](#section_duq_s7w_t96)
    -   [How do I view the Internet traffic bills of an ECS instance?](#section_r5a_u6t_chb)
    -   [Why is the bandwidth usage of my ECS instance displayed in the CloudMonitor console different from that displayed in the ECS console?](#section_tsb_lpy_gvz)
    -   [My ECS instance has been stopped. Why am I still being charged for its outbound traffic on a pay-as-you-go basis?](#section_d7h_fs2_xu8)
-   FAQ about IP addresses
    -   [How do I query the IP addresses of ECS instances?](#section_vpl_qbg_qgb)
    -   [How do I disable the public NIC of an ECS instance?](#section_bxf_ywf_qgb)
-   FAQ about network access and traffic direction
    -   [When I attempt to access a website on an ECS instance, a message similar to "Sorry, your access has been blocked because the requested URL may pose a security threat to the website" appears. Why?](#section_cwr_y3g_4gb)
    -   [After I configure a secondary private IP address for a Windows instance, the instance cannot connect to the Internet. Why?](#section_y1b_2ys_lcb)
    -   [An exceptional logon has been detected on one of my ECS instances. What do I do?](#section_mgg_dhg_4gb)
    -   [What is traffic scrubbing?](#section_4xo_and_tfv)
    -   [How do I cancel traffic scrubbing for an ECS instance?](#section_r2g_vg8_gtv)
    -   [How do I request reverse lookup for an ECS instance?](#section_24x_y33_pml)
    -   [Can an IP address point to multiple reverse lookup domain names?](#section_0u1_fng_nzy)
-   FAQ about public IP addresses
    -   [Can I change the public IPv4 address of an instance after the instance has been created?](#section_c7c_7n5_fae)
    -   [Why am I unable to find the option to change the public IP address of an ECS instance in the ECS console?](#section_y27_eqe_lgp)
    -   [Can I change the private IP address of an instance?](#section_q67_0xd_eps)
    -   [If no public IPv4 address was assigned to an ECS instance when the instance was being created, how do I assign a public IP address to the instance?](#section_9rr_e3x_ks1)
-   FAQ about network basics
    -   [What is a BGP data center?](#section_hmd_spf_qgb)
    -   [What are WAN and LAN?](#section_o52_nlg_4gb)
    -   [What is CIDR?](#section_jua_0tj_q5m)
    -   [How do I express a subnet mask?](#section_nw6_q4l_pdt)
    -   [How do I plan subnets?](#section_g8p_l4s_2e8)
-   FAQ about quotas
    -   [How do I view resource quotas?](#section_ubf_rd5_utp)

## What is the packet loss rate when instances within different regions communicate over the Internet?

When instances within different regions communicate by using Cloud Enterprise Network \(CEN\), these instances use Alibaba Cloud backbone networks to transmit data. Alibaba Cloud aims to provide network services with an hourly packet loss rate at the 99th percentile of less than 0.0001%.

## How is the network latency for instances within the same region that communicate over the internal network?

You can achieve minimal latency when instances within the same zone and region communicate with each other over the internal network. The one-way latency at the 99th percentile is less than 180 µs for communication between instances within the same zone.

## How is the performance of connections guaranteed for instances for which the maximum number of connections is not specified?

If an instance family does not have the maximum number of connections specified, this instance family does not have a specified maximum number of connections. We recommend that you perform business stress tests on instances to choose appropriate instance types.

**Note:** After a connection is established, the connection counts towards the number of connections before its aging period ends. The displayed number of connections may be greater than the number of connections actually in use.

## What do I do if the performance of an ECS instance is unstable when a UDP PPS test or TCP bandwidth test is performed on the instance?

When a network performance test is performed on an ECS instance, the test result may be affected by a number of factors. These factors include the common performance tuning methods such as non-uniform memory access \(NUMA\) topology adaptation, binding vCPUs for tasks, and binding vCPUs for interrupts.

For example, during a single-stream TCP bandwidth test, if a receive task such as a netserver process and a network interface controller \(NIC\) receive queue interrupt are bound to the same vCPU, the NIC triggers an interrupt to interrupt the receive task when the NIC receives data frames. If the receive task is frequently interrupted, the test result may fail to meet your expectations. In this case, you can bind the receive task and the NIC receive queue interrupt to different vCPUs and obtain a better test result by using the performance advantages of multiple vCPUs.

## What are the inbound and outbound bandwidths of ECS instances?

|Bandwidth type|Description|
|:-------------|:----------|
|Inbound bandwidth|The bandwidth for inbound traffic for an ECS instance, including the following traffic: -   Traffic generated when you download external resources to the ECS instance
-   Traffic generated when you upload resources to the ECS instance by using an FTP client |
|Outbound bandwidth|The bandwidth for outbound traffic for an ECS instance, including the following traffic: -   Traffic generated when the ECS instance provides external access
-   Traffic generated when you download resources from the ECS instance by using an FTP client |

## I purchased a public bandwidth of 5 Mbit/s for an ECS instance. How is this bandwidth applied to the inbound and outbound bandwidths of the instance?

The 5 Mbit/s that you purchased is used as the outbound bandwidth for the instance. The inbound bandwidth of this instance is capped at 10 Mbit/s.

-   Outbound bandwidth is consumed when data is transferred from the ECS instance. The maximum outbound bandwidth of an ECS instance is capped at 100 Mbit/s or 200 Mbit/s regardless of whether the instance resides in a virtual private cloud \(VPC\) or the classic network. The maximum available outbound bandwidth depends on the billing method of the instance.
-   Inbound bandwidth is consumed when data is transferred to the ECS instance. The maximum inbound bandwidth is determined by the outbound bandwidth:
    -   If the outbound bandwidth is less than 10 Mbit/s, the maximum inbound bandwidth is 10 Mbit/s.
    -   If the outbound bandwidth is greater than 10 Mbit/s, the maximum inbound bandwidth is the same as the purchased outbound bandwidth.

**Note:** When the **pay-by-traffic** billing method is used, the maximum inbound and outbound bandwidth values are used as traffic limits instead of guaranteed performance. In scenarios where demands exceed resource supplies, the peak bandwidth values may be limited. If you require guaranteed bandwidth performance, use the **pay-by-bandwidth** billing method.

## Is public bandwidth exclusive to each ECS instance, or is public bandwidth shared among multiple instances?

The public bandwidth of each instance is exclusive to the instance.

## How am I billed for the network usage of ECS instances?

For more information about billing for the network usage of ECS instances, see [Public bandwidth](/intl.en-US/Pricing/Billing items/Public bandwidth.md).

## Why is 200 Kbit/s of inbound traffic already consumed on a newly created ECS instance?

This traffic was generated by Address Resolution Protocol \(ARP\) broadcast packets. Each ECS instance is assigned to a large CIDR block. When the gateway receives an ARP request packet for an ECS instance, the gateway broadcasts this packet to all ECS instances within the same CIDR block. The new instance also receives the packet. If the request is not destined for the new instance, the instance does not reply with an ARP reply packet.

## How do I view the Internet traffic bills of an ECS instance?

To view the Internet traffic bills of an ECS instance, perform the following steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).
2.  In the top navigation bar, choose **Expenses** \> **User Center**.
3.  In the left-side navigation pane, choose **Spending Summary** \> **Spending Summary**.
4.  Click the **Bills** tab. Specify a billing cycle. Set **Product Name** to **Elastic Compute Service**, **Product Detail** to **Elastic Computing \(Pay-As-You-Go\)**, and **Subscription Type** to **Pay-As-You-Go**.
5.  Click **Export Billing Overview \(CSV\)**. In the Export Billing Overview \(CSV\) dialog box, enter the CAPTCHA and click **OK**.
6.  On the Export Record page, wait until the status of the exported file changes to **Exported** and click **Download** in the Actions column.
7.  Open the exported CSV file to view the Internet traffic bills of the ECS instance.

## Why is the bandwidth usage of my ECS instance displayed in the CloudMonitor console different from that displayed in the ECS console?

ECS instances function as backend servers of Server Load Balancer \(SLB\) instances and use the Layer 7 HTTP forwarding model. In this forwarding model, SLB instances forward client requests to ECS instances, and the ECS instances use their own outbound bandwidth to return responses to the corresponding users. The bandwidth consumed by these responses is not displayed in the ECS console, but the traffic generated by the responses counts towards the outbound traffic of the SLB instances and is displayed in the CloudMonitor console. Therefore, the bandwidth usage of your ECS instance displayed in the CloudMonitor console is different from that displayed in the ECS console.

## My ECS instance has been stopped. Why am I still being charged for its outbound traffic on a pay-as-you-go basis?

-   Problem description: Your instance is in the **Stopped** state in the ECS console, but is in the **Cleaning** state in the Anti-DDoS Basic console. You are charged for outbound traffic from the instance on a pay-as-you-go basis every hour.
-   Cause: HTTP flood protection is enabled for the ECS instance. When HTTP flood protection is enabled, the security mechanism sends probe packets to potential attack sources. Therefore, a large volume of outbound traffic is generated.
-   Solution: Disable HTTP flood protection for the ECS instance.

## How do I query the IP addresses of ECS instances?

-   Linux instance

    Run the `ifconfig` command to view NIC information. You can view the IP addresses, subnet masks, gateways, DNS servers, and MAC addresses in the command output.

-   Windows instance

    In Command Prompt, run the `ipconfig /all` command to view NIC information. You can view the IP addresses, subnet masks, gateways, DNS servers, and MAC addresses in the command output.


## How do I disable the public NIC of an ECS instance?

-   Linux instance
    1.  Run the `ifconfig` command to view the name of the public NIC of the instance.
    2.  Run the `ifdown` command to disable the public NIC. For example, if the name of the public NIC is `eth1`, enter `ifdown eth1`.

        **Note:** You can run the ifup command to re-enable the NIC. For example, if the name of the public NIC is `eth1`, enter `ifup eth1`.

-   Windows instance
    1.  In Command Prompt, run the `ipconfig` command to view information about the public NIC.
    2.  Open the **Control Panel** and click View network status and tasks in the Network and Internet section. In the Network and Sharing Center window, click Change adapter settings in the left-side navigation pane to disable the public NIC.

## When I attempt to access a website on an ECS instance, a message similar to "Sorry, your access has been blocked because the requested URL may pose a security threat to the website" appears. Why?

-   Problem description: When you attempt to access a website built on an ECS instance, you are prompted with a message similar to "Sorry, your access has been blocked because the requested URL may pose a security threat to the website."
-   Cause: Web Application Firewall \(WAF\) has identified your access request to the URL as an attack and blocked your access.
-   Solution: Add the source public IP address that you use to access the website to the WAF whitelist. For more information, see [Avoid Anti-DDoS Basic false positives by using a whitelist]().

## After I configure a secondary private IP address for a Windows instance, the instance cannot connect to the Internet. Why?

-   Problem description: After you configure a secondary private IP address for a Windows instance, the instance cannot connect to the Internet.
-   Cause: In Windows 2008 and later, the rule that the longest matching prefix with the next hop IP address is used is applied to select source IP addresses. This may lead to network connection failures.
-   Solution: Run the Netsh command with skipassource set to true to configure a secondary private IP address for the Windows instance.

    Netsh command:

    ```
    Netsh int ipv4 add address <Interface> <IP Addr> [<Netmask>] [skipassource=true]
    ```

    The following table describes the parameters in the Netsh command.

    |Parameter|Description|Example value|
    |---------|-----------|-------------|
    |<Interface\>|The network interface with which to associate the secondary private IP address|'Ethernet'|
    |<IP Addr\>|The secondary private IP address|192.168.0.100|
    |<Netmask\>|The mask of the secondary private IP address|255.255.255.0|

    Sample command:

    ```
    Netsh int ipv4 add address 'Ethernet' 192.168.0.100 255.255.255.0 skipassource=true
    ```


## An exceptional logon has been detected on one of my ECS instances. What do I do?

Perform the following operations to solve the problem:

1.  Check the logon time to see whether the logon was performed by yourself or another administrator.
2.  If the logon was not performed by yourself or another administrator, it is an unauthorized logon. Perform the following steps:
    1.  Reset the password. For more information, see [Reset the logon password of an instance](/intl.en-US/Instance/Manage instances/Reset the logon password of an instance.md).
    2.  Check whether the ECS instance is infected.
    3.  Configure security groups to allow access only from specific IP addresses. For more information, see [Scenarios for security groups](/intl.en-US/Security/Security groups/Scenarios for security groups.md).

## What is traffic scrubbing?

The traffic scrubbing service monitors inbound traffic to ECS instances in real time and identifies exceptional traffic such as DDoS attacks. By default, Anti-DDoS Basic is enabled on ECS instances to provide traffic scrubbing. When ECS instances are under attack, the traffic scrubbing service automatically detects the attack and scrubs malicious traffic without affecting ECS instance services. When exceptional traffic is detected, suspicious traffic is redirected from the destination network to a scrubbing device. The device identifies and removes malicious traffic and then returns legitimate traffic to the network to be forwarded to the ECS instances.

## How do I cancel traffic scrubbing for an ECS instance?

1.  Log on to the [Alibaba Cloud Security Anti-DDoS Basic console](https://yundun.console.aliyun.com/?p=ddosnext).
2.  Click the ECS tab. In the ECS instance list, find the IP address of an ECS instance that is in the Cleaning state and click **View Details**.
3.  Click **Cancel cleaning**.

    ![Cancel traffic scrubbing](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6357298951/p50257.png)


## How do I request reverse lookup for an ECS instance?

Reverse lookup is used in mail services to reject mail from IP addresses mapped to unregistered domain names. Most spammers use dynamic IP addresses or IP addresses mapped to unregistered domain names to send unwanted mail and avoid being tracked. When reverse lookup is enabled on a mail server, the server rejects mail sent from dynamic IP addresses or unregistered domain names to reduce the amount of spams received.

You can [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to request reverse lookup for your ECS instance. To make your ticket easier to process, we recommend that you specify the region, public IP address, and registered domain name of your ECS instance in the ticket.

After your request is approved, you can run the dig command to check whether reverse lookup has taken effect on your instance. Example:

```
dig -x 121.196.255.** +trace +nodnssec
```

If information similar to the following line is displayed in the command output, reverse lookup has taken effect on your instance.

```
1.255.196.121.in-addr.arpa. 3600 IN PTR ops.alidns.com.
```

## Can an IP address point to multiple reverse lookup domain names?

No, each IP address can point only to a single reverse lookup domain name. For example, you cannot configure the IP address 121.196.255.\*\*to resolve to multiple domain names such as mail.abc.com, mail.ospf.com, and mail.zebra.com.

## Can I change the public IPv4 address of an instance after the instance has been created?

You can change the public IPv4 address of an instance within 6 hours after the instance is created. For more information, see [Change the public IP address of an ECS instance](/intl.en-US/Network/Change IPv4 addresses/Change the public IP address of an ECS instance.md).

After 6 hours, the instance network type determines whether the public IP address of the instance can be changed.

-   For an instance in a VPC, you can change the public IP address of the instance by converting the IP address into an elastic IP address \(EIP\). Then, to assign a new public IP address, you can disassociate the EIP from the instance and associate a new EIP with the instance or upgrade the public bandwidth of the instance. For more information, see [Convert the public IP address of a VPC-type instance to an Elastic IP address](/intl.en-US/Network/Change IPv4 addresses/Convert the public IP address of a VPC-type instance to an Elastic IP address.md).
-   The public IP addresses of instances in the classic network cannot be changed. However, you can convert the public IP address of an instance into an EIP when you release the instance. For more information, see [Convert a public IP address in a classic network to an Elastic IP address](/intl.en-US/Network/Change IPv4 addresses/Convert the public IP address of a classic network-type instance to an Elastic IP address.md).

## Why am I unable to find the option to change the public IP address of an ECS instance in the ECS console?

-   Within 6 hours after a pay-as-you-go instance is created: If No Fees for Stopped Instances \(VPC-Connected\) is enabled for your account, you must select Retain Instance and Continue Charging After Instance Is Stopped when you stop the pay-as-you-go instance. Otherwise, the option to change the public IP address is not displayed in the ECS console after the instance is stopped.
-   More than 6 hours after the instance is created: You cannot change the public IP address, and the option is not displayed.

## Can I change the private IP address of an instance?

-   You can change the private IP addresses of instances in VPCs. For more information, see [Modify a private IP address](/intl.en-US/Network/Change IPv4 addresses/Modify a private IP address.md).
-   You cannot change the private IP addresses of instances in the classic network.

## If no public IPv4 address was assigned to an ECS instance when the instance was being created, how do I assign a public IP address to the instance?

-   Apply for and bind an Elastic IP Address \(EIP\) to the ECS instance. For more information, see the following topic of *EIP documentation:* [Apply for new EIPs](/intl.en-US/User Guide/Create an EIP/Apply for new EIPs.md).
-   Modify the public bandwidth of the ECS instance to allocate a fixed public IP address. For more information about modifying the public bandwidth of a subscription ECS instance, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md). For more information about modifying the public bandwidth of a pay-as-you-go ECS instance, see [Modify the bandwidth configurations of pay-as-you-go instances](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Modify the bandwidth configurations of pay-as-you-go instances.md).

## What is a BGP data center?

Border Gateway Protocol \(BGP\) is used to connect autonomous systems \(AS\) over the Internet. The main purpose of BGP is to control route propagation and select the optimal routes.

China Netcom, China Telecom, China Railcom, and some large privately owned IDC service providers all have autonomous system numbers \(ASNs\). Most major network carriers in China use BGP to implement multi-line connections between their ASNs.

To implement multi-line interconnection in this manner, an IDC must obtain a CIDR block and an ASN from the China Internet Network Information Center \(CNNIC\) or Asia-Pacific Network Information Center \(APNIC\), and then broadcast this CIDR block to the networks of other carriers by using BGP. After BGP is used to connect different networks, the backbone routers of the network carriers determine the optimal routes to the CIDR block of the IDC to ensure high-speed access for users of different network carriers.

## What are WAN and LAN?

-   A wide area network \(WAN\) is also known as an external or public network. A WAN is a telecommunications network that connects smaller networks such as local area networks \(LANs\) and metro area networks \(MANs\). Each WAN extends over a large geographical area that can range in size from as small as a city or as large as an entire continent to provide telecommunications services and form an international telecommunications network. WAN is not the same as the Internet.
-   A LAN is also known as an internal network. A LAN is a network that interconnects computers within a small area. Users can manage files, share application software and printers, schedule work for work groups, and communicate with each other such as by sending emails or faxes within a LAN. A LAN is a closed network that can be as small as consisting of two computers in an office or as large as consisting of thousands of computers in a company. In Alibaba Cloud, ECS instances of the same network type within the same region can communicate with each other over the internal network. ECS instances within different regions are isolated from each other.

## What is CIDR?

Classless Inter-Domain Routing \(CIDR\) is an addressing scheme for the Internet that allows for IP addresses to be assigned in a more efficient manner than the traditional scheme based on classes A, B, and C. CIDR notation is used to denote IP addresses and IP ranges. It consists of an IP address and a forward slash followed by a decimal number that denotes how many bits are in the network prefix.

-   Example 1: Convert a CIDR block into an IP address range

    For example, you can convert the 10.0.0.0/8 CIDR block into a 32-bit binary IP address of 00001010.00000000.00000000.00000000. In this CIDR block, /8 represents an 8-bit network ID. The first 8 bits of the 32-bit binary IP address are fixed, and the corresponding IP addresses are from 00001010.00000000.00000000.00000000 to 00001010.11111111.11111111.11111111. After you convert the preceding IP addresses into IP addresses in the decimal format, the 10.0.0.0/8 CIDR block indicates the IP addresses from 10.0.0.0 to 10.255.255.255 with a subnet mask of 255.0.0.0.

-   Example 2: Convert an IP address range into a CIDR block

    For example, you have a range of IP addresses from 192.168.0.0 to 192.168.31.255. You can convert the last two parts of the first and last IP addresses to binary numbers from 00000000.00000000 to 00011111.11111111. The first 19 \(8 × 2 + 3\) bits are fixed. After you convert the IP addresses to IP addresses in the CIDR format, the corresponding CIDR block is 192.168.0.0/19.


## How do I express a subnet mask?

You can use one of the following methods to express a subnet mask:

-   Use dotted decimal notation.

    The default subnet mask of a Class A network is 255.0.0.0.

-   Append a forward slash \(/\) and a number ranging from 1 to 32 to the end of an IP address to define a subnet mask. This number indicates the length of the network identification bit in the subnet mask.

    Example: 192.168.0.3/24.


## How do I plan subnets?

For more information about the best practices for planning subnets, see [Plan and design a VPC](/intl.en-US/Quick Start/Plan and design a VPC.md).

## How can I view the resource quota?

For more information about how to view the limits and quotas of resources, see [Limits](/intl.en-US/Product Introduction/Limits.md).

