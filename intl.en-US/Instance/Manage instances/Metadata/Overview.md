# Overview

This topic describes instance metadata and the items that can be obtained from it. You can use instance metadata to flexibly manage or configure instances.

## Introduction

Metadata of an instance includes basic information of the instance in Alibaba Cloud, such as the instance ID, IP address, MAC addresses of network interface controllers \(NICs\) bound to the instance, and operating system type. Instance metadata also includes dynamic items generated after the instance is first started such as system events, instance identifiers, and user data.

For more information, see [Retrieve instance metadata](/intl.en-US/Instance/Manage instances/Metadata/Retrieve instance metadata.md).

## Metadata items

The following table lists basic metadata items that you can obtain from an ECS instance.

|Metadata item|Description|Version|
|:------------|:----------|:------|
|/dns-conf/nameservers|The DNS configurations of the instance.|2016-01-01|
|/eipv4|The IPv4 elastic IP address \(EIP\) that is associated with the primary NIC of the instance.|2016-01-01|
|/hostname|The hostname of the instance.|2016-01-01|
|/instance/instance-type|The instance type of the instance.|2016-01-01|
|/image-id|The ID of the image used to create the instance.|2016-01-01|
|/image/market-place/product-code|The product code of the Alibaba Cloud Marketplace image.|2016-01-01|
|/image/market-place/charge-type|The billing method of the Alibaba Cloud Marketplace image.|2016-01-01|
|/instance-id|The ID of the instance.|2016-01-01|
|/mac|The MAC address of the instance. If the instance is bound with multiple NICs, only the MAC address of eth0 is displayed.|2016-01-01|
|/network-type|The network type of the instance. Only VPC-type instances are supported.|2016-01-01|
|/network/interfaces/macs|The list of MAC addresses of the NICs.|2016-01-01|
|/network/interfaces/macs/\[mac\]/network-interface-id|The identifier of the NIC. Replace \[mac\] with the MAC address of the instance.|2016-01-01|
|/network/interfaces/macs/\[mac\]/netmask|The subnet mask of the NIC.|2016-01-01|
|/network/interfaces/macs/\[mac\]/vswitch-cidr-block|The IPv4 CIDR block of the VSwitch to which the NIC is connected.|2016-01-01|
|/network/interfaces/macs/\[mac\]/vpc-cidr-block|The IPv4 CIDR block of the VPC to which the NIC belongs.|2016-01-01|
|/network/interfaces/macs/\[mac\]/private-ipv4s|The list of private IPv4 addresses assigned to the NIC.|2016-01-01|
|/network/interfaces/macs/\[mac\]/vswitch-id|The ID of the VSwitch that is in the same VPC as the security group of the NIC.|2016-01-01|
|/network/interfaces/macs/\[mac\]/vpc-id|The ID of the VPC to which the security group of the NIC belongs.|2016-01-01|
|/network/interfaces/macs/\[mac\]/primary-ip-address|The primary private IP address of the NIC.|2016-01-01|
|/network/interfaces/macs/\[mac\]/gateway|The IPv4 gateway of the VPC to which the NIC belongs.|2016-01-01|
|/instance/max-netbw-egress|The maximum outbound internal bandwidth of the instance type. Unit: Kbit/s.|2016-01-01|
|/instance/max-netbw-ingerss|The maximum inbound internal bandwidth of the instance type. Unit: Kbit/s.|2016-01-01|
|/private-ipv4|The private IPv4 address of the primary NIC.|2016-01-01|
|/public-ipv4|The public IPv4 address of the primary NIC.|2016-01-01|
|/ntp-conf/ntp-servers|The IP address of the Network Time Protocol \(NTP\) server.|2016-01-01|
|/owner-account-id|The Alibaba Cloud account ID of the instance owner.|2016-01-01|
|/public-keys|The list of all public keys of the instance.|2016-01-01|
|/region-id|The region ID of the instance.|2016-01-01|
|/zone-id|The zone ID of the instance.|2016-01-01|
|/serial-number|The serial number of the instance.|2016-01-01|
|/source-address|The image library from which the package management software of a Linux instance obtains updates. The source of the package management software is the YUM or APT repository.|2016-01-01|
|/kms-server|The server that activates the KMS service of a Windows instance.|2016-01-01|
|/wsus-server/wu-server|The server that updates a Windows instance.|2016-01-01|
|/wsus-server/wu-status-server|The server that monitors the update status of a Windows instance.|2016-01-01|
|/vpc-id|The ID of the VPC to which the instance belongs.|2016-01-01|
|/vpc-cidr-block|The CIDR block of the VPC to which the instance belongs.|2016-01-01|
|/vswitch-cidr-block|The CIDR block of the VSwitch to which the instance is connected.|2016-01-01|
|/vswitch-id|The ID of the VSwitch to which the instance is connected.|2016-01-01|
|/ram/security-credentials/\[role-name\]|The temporary STS credentials generated for the RAM role of the instance. You can obtain the STS credentials only after the instance assumes a RAM role. Replace \[role-name\] with the RAM role name of the instance. If the \[role-name\] parameter is not specified, the name of the instance RAM role is returned.**Note:** A new STS credential is available 30 minutes prior to the expiration of the old one. During this period, both STS credentials can be used.

|2016-01-01|
|/instance/spot/termination-time|The stop and release time specified in the operating system of a preemptible instance. The time is in the yyyy-MM-ddThh:mm:ssZ format \(UTC+0\). Example: 2018-04-07T17:03:00Z.|2016-01-01|
|/instance/virtualization-solution|The ECS virtualization solution. Virt 1.0 and Virt 2.0 are supported.|2016-01-01|
|/instance/virtualization-solution-version|The internal build version.|2016-01-01|
|/instance-identity/pkcs7|The signature of the instance identifier.|2016-01-01|

## Dynamic metadata - O&M

For more information, see [Overview](/intl.en-US/Deployment & Maintenance/System events/Overview.md).

## Dynamic metadata - identity

Instance identifiers are used to identify and differentiate instances. This can provide trust foundation for application permission control and software activation. Instance identifiers consist of **instance identity documents** \(document\) and **instance identity signatures** \(signature\). For more information, see [Instance identity](/intl.en-US/Instance/Manage instances/Instance identity.md).

## Dynamic metadata - configuration

User data of an instance is implemented mainly based on different types of custom scripts and you can configure user data when you create the instance. User data allows users to customize instance startup and pass in data to the instance. For example, you can use user data to perform configuration operations such as automatically obtaining software resource packages, enabling services, printing logs, installing dependency packages, and initializing web environments. You can also pass in user data as common data to the instance and reference the data in the instance.

When the instance enters the **Running** state, the system runs the user data scripts by using the administrator or root permission. Then, the system runs the initialization information or the `/etc/init` folder.

For more information, see [Prepare user data](/intl.en-US/Instance/Manage instances/User data/Prepare user data.md).

