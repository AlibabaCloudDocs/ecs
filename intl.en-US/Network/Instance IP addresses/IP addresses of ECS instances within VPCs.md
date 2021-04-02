---
keyword: [Alibaba Cloud, elastic IP address \(EIP\), ECS, public bandwidth]
---

# IP addresses of ECS instances within VPCs

IP addresses are used to connect to ECS instances or their deployed services. ECS instances within VPCs can be assigned two types of IP addresses: private IP addresses and public IP addresses.

## Private IP addresses

Each new ECS instance within a VPC is assigned a private IP address based on the VPC and CIDR block of the vSwitch to which the instance is connected. Private IP addresses can be used in the following scenarios:

-   Load balancing
-   Communication over the internal network between ECS instances within the same LAN
-   Communication over the internal network between an ECS instance and other cloud services such as OSS and ApsaraDB RDS within the same LAN

You can use the ECS console to modify the private IP addresses of ECS instances within VPCs. For more information, see [Modify a private IP address](/intl.en-US/Network/Change IPv4 addresses/Modify a private IP address.md). For more information about internal network communication, see [Internal network](/intl.en-US/Network/Instance IP addresses/Internal network.md).

## Public IP addresses

ECS instances within VPCs support the following types of public IP addresses:

-   PublicIP addresses: the public IP addresses assigned by the ECS system.
-   Elastic IP address \(EIPs\). For more information, see [What is an EIP?](/intl.en-US/.md).

The following table lists the major differences between the two types of public IP addresses.

|Item|PublicIP address|EIP|
|----|----------------|---|
|Scenario|You may want the system to automatically assign a public IP address to an ECS instance when you create the instance. However, you do not want to retain the public IP address when the instance is released. In this case, use a PublicIP address.|If you want to retain a public IP address to use with other ECS instances deployed within the same region, use an EIP. Each EIP can be associated with or disassociated from different ECS instances. After an instance is released, its associated EIP is retained.|
|Method to obtain an address|If you select **Assign Public IP Address** when you create an ECS instance within a VPC, a PublicIP address is assigned to the instance.|An EIP is created and associated with an ECS instance that is not assigned a PublicIP address. For more information, see [Apply for new EIPs](/intl.en-US/User Guide/Create an EIP/Apply for new EIPs.md) and [Associate an EIP with an ECS instance](/intl.en-US/User Guide/Associate an EIP with a cloud instance/Associate an EIP with an ECS instance.md).|
|Maximum number of public IP addresses that can be assigned to or associated with a single ECS instance|An ECS instance can only be assigned a single PublicIP address.|Multiple EIPs can be associated with a single ECS instance in multi-EIP to ENI mode. For more information, see [Associate EIPs with secondary ENIs in multi-EIP-to-ENI mode](/intl.en-US/User Guide/Associate an EIP with a cloud instance/Bind an EIP to a secondary ENI/Associate EIPs with secondary ENIs in multi-EIP-to-ENI mode.md).|
|Method to disassociate an address|After a PublicIP address is assigned to an ECS instance, the address can be only released and cannot be disassociated from the instance.|See [Disassociate an EIP from a cloud resource](/intl.en-US/User Guide/Disassociate an EIP from a cloud resource.md).|
|Method to release an address|-   When ECS instances are released, their assigned PublicIP addresses are also released.
-   During the lifecycle of an ECS instance, you can release its PublicIP address by setting the public bandwidth of the instance to 0 Mbit/s. For more information about how to modify the public bandwidth of a subscription ECS instance, see [Modify the bandwidth configurations of subscription instances](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Modify the bandwidth configurations of subscription instances.md). For more information about how to modify the public bandwidth of a pay-as-you-go ECS instance, see [Modify the bandwidth configurations of pay-as-you-go instances](/intl.en-US/Instance/Change configurations/Modify bandwidth configurations/Modify the bandwidth configurations of pay-as-you-go instances.md).

|See [Release an EIP](/intl.en-US/User Guide/Manage Pay-As-You-Go-billed EIPs/Release an EIP.md).|
|Method to view the MAC address|ECS instances within VPCs are connected to the Internet by using the mapping of public IP addresses to internal network interface controllers \(NICs\). Therefore, the public NICs of ECS instances within VPCs cannot be located regardless of whether the instances are assigned PublicIP addresses or associated with EIPs.|

## Billing

You are billed only for outbound Internet traffic. For more information, see [Public bandwidth](/intl.en-US/Pricing/Billing items/Public bandwidth.md).

