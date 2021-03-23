Best practices for ECS data security 
=========================================================

This topic describes the O\&M best practices for improving the data security of ECS instances.

Intended users 
-----------------------------------

This topic applies to individuals and small and medium-sized enterprises that are new to Alibaba Cloud.

Back up data regularly 
-------------------------------------------

Data backup is the foundation of disaster recovery, and can reduce the risk of data loss due to system failures, operational errors, and security problems. ECS provides the snapshot feature to meet the data backup requirements of most users. You can select a method of creating snapshots based on your business requirements. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md) and [Execute or disable an automatic snapshot policy](/intl.en-US/Snapshots/Automatic snapshot policies/Apply or disable an automatic snapshot policy.md).

We recommend that you create automatic snapshots on a daily basis and store the snapshots for at least seven days. This significantly improves disaster tolerance and minimizes potential data losses.

Design security domains 
--------------------------------------------

You can build private networks by using virtual private clouds (VPCs) to separately host servers of different security levels in your enterprise. This way, servers do not interfere each other over an interconnected network.

We recommend that you create a VPC. Then, specify a private IP address range in CIDR notation, and configure route tables and gateways of the VPC. You can store important data in the created VPC, which is logically isolated from the Internet. Then, you can use an elastic IP address (EIP) or a jumper server to manage data for daily O\&M purposes. For more information, see [Create a VPC](/intl.en-US/VPCs and vSwitchs/Create a VPC.md).

Configure security group rules 
---------------------------------------------------

Security groups are an essential tool to isolate networks. You can use security groups to configure network access control for one or more ECS instances. You can control the access to and from an ECS instance over the network by configuring security group rules. Specifically, you can restrict the inbound and outbound access on a port, and allow or deny access to and from specific IP addresses. This reduces the attack surface and makes ECS instances more secure.

Consider the following example. By default, port 22 is used as the remote access port on Linux ECS instances. Security risks arise if this port is open to external devices. You can authorize only specific local IP addresses to access the instances over port 22 when you configure security group rules. If you have higher security requirements, you can use third-party virtual private network (VPN) products to encrypt logon data.

Configure strong logon passwords 
-----------------------------------------------------

Weak passwords are one of the most common vulnerabilities and can lead to data leaks. To prevent security risks that arise from weak passwords, we recommend that you use a complex password for server access. The password must be at least eight characters in length, and contain multiple character types such as uppercase letters, lowercase letters, digits, and special characters. We also recommend that you change the password on a regular basis.

Improve the security of server ports 
---------------------------------------------------------

When ECS instances provide Internet access services, the service ports of the ECS instances are exposed. If you enable more service ports, the server is exposed to higher security risks. We recommend that you open only the required service ports, change the default service ports to high-numbered ports such as those numbers higher than 30000, and implement access control on these service ports.

For example, use internal connections for relational database service (RDS) to avoid exposing service ports to the Internet. If an external connection is necessary for RDS, change the default connection port from port 3306 to a port numbered 30001 or higher. Then, authorize client IP addresses based on your business requirements.

Install a WAF 
----------------------------------

Application vulnerabilities are security defects that can be exploited by hackers to illegally access data from web applications, cache, databases, and storage products. Common application vulnerabilities include SQL injection, XSS cross-site scripting, Webshell upload, backdoor protection, command injection, illegal HTTP requests, common vulnerabilities of web servers, unauthorized access to core files, and passthrough. Application vulnerabilities are different from system vulnerabilities, and are difficult to fix. You must consider security baseline issues before you design applications. To ensure website security and availability, we recommend that you use Web Application Firewall (WAF) to prevent various application attacks. For more information about how to deploy and use WAF, see [Quick start](/intl.en-US/Quick Start/Quick start.md).
