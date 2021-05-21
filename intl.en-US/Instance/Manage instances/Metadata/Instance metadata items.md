---
keyword: [ECS, metadata, ]
---

# Instance metadata items

This topic describes the basic and dynamic metadata items that you can obtain from an Elastic Compute Service \(ECS\) instance.

## Basic metadata items

|Item|Description|
|:---|:----------|
|/meta-data/dns-conf/nameservers|The Domain Name System \(DNS\) configurations of the instance.|
|/meta-data/hostname|The hostname of the instance.|
|/meta-data/instance/instance-type|The instance type of the instance.|
|/meta-data/image-id|The ID of the image used to create the instance.|
|/meta-data/image/market-place/product-code|The product code of the Alibaba Cloud Marketplace image.|
|/meta-data/image/market-place/charge-type|The billing method of the Alibaba Cloud Marketplace image.|
|/meta-data/instance-id|The ID of the instance.|
|/meta-data/mac|The media access control \(MAC\) address of the instance. If the instance is bound with multiple network interface controllers \(NICs\), only the MAC address of eth0 is displayed.|
|/meta-data/network-type|The network type of the instance. Only instances that reside in virtual private clouds \(VPCs\) are supported.|
|/meta-data/network/interfaces/macs|The list of MAC addresses of the NICs.|
|/meta-data/network/interfaces/macs/\[mac\]/network-interface-id|The identifier of the NIC. Replace \[mac\] with the MAC address of the instance.|
|/meta-data/network/interfaces/macs/\[mac\]/netmask|The subnet mask of the NIC.|
|/meta-data/network/interfaces/macs/\[mac\]/vswitch-cidr-block|The IPv4 Classless Inter-Domain Routing \(CIDR\) block of the vSwitch to which the NIC is connected.|
|/meta-data/network/interfaces/macs/\[mac\]/vpc-cidr-block|The IPv4 CIDR block of the VPC to which the NIC belongs.|
|/meta-data/network/interfaces/macs/\[mac\]/private-ipv4s|The private IPv4 addresses assigned to the NIC.|
|/meta-data/network/interfaces/macs/\[mac\]/vswitch-id|The ID of the vSwitch that is in the same VPC as the security group of the NIC.|
|/meta-data/network/interfaces/macs/\[mac\]/vpc-id|The ID of the VPC to which the security group of the NIC belongs.|
|/meta-data/network/interfaces/macs/\[mac\]/primary-ip-address|The primary private IP address of the NIC.|
|/meta-data/network/interfaces/macs/\[mac\]/gateway|The IPv4 gateway address of the VPC to which the NIC belongs.|
|/meta-data/instance/max-netbw-egress|The maximum outbound internal bandwidth of the instance. Unit: Kbit/s.|
|/meta-data/instance/max-netbw-ingress|The maximum inbound internal bandwidth of the instance. Unit: Kbit/s.|
|/meta-data/private-ipv4|The private IPv4 address of the primary NIC.|
|/meta-data/eipv4|This metadata item is used to obtain the following information:-   The public IPv4 address of the instance
-   The elastic public IPv4 address associated with the primary NIC |
|/meta-data/ntp-conf/ntp-servers|The IP address of the Network Time Protocol \(NTP\) server.|
|/meta-data/owner-account-id|The ID of the Alibaba Cloud account to which the instance belongs.|
|/meta-data/public-keys|All the public keys of the instance.|
|/meta-data/region-id|The region ID of the instance.|
|/meta-data/zone-id|The zone ID of the instance.|
|/meta-data/serial-number|The serial number of the instance.|
|/meta-data/source-address|The image library from which the package management software of a Linux instance obtains updates. The source of the package management software is the YUM or APT repository.|
|/meta-data/kms-server|The server that activates the Key Management Service \(KMS\) for a Windows instance.|
|/meta-data/wsus-server/wu-server|The server that updates a Windows instance.|
|/meta-data/wsus-server/wu-status-server|The server that monitors the update status of a Windows instance.|
|/meta-data/vpc-id|The ID of the VPC to which the instance belongs.|
|/meta-data/vpc-cidr-block|The CIDR block of the VPC to which the instance belongs.|
|/meta-data/vswitch-cidr-block|The CIDR block of the vSwitch to which the instance is connected.|
|/meta-data/vswitch-id|The ID of the vSwitch to which the instance is connected.|
|/meta-data/ram/security-credentials/\[role-name\]|The temporary Security Token Service \(STS\) credentials generated for the RAM role of the instance. You can obtain the STS credentials only after the instance assumes a RAM role. Replace \[role-name\] with the name of the RAM role. If the \[role-name\] parameter is not specified, the name of the RAM role is returned. **Note:** A new STS credential is available 30 minutes prior to the expiration of the old one. During this period, both STS credentials can be used. |
|/meta-data/instance/spot/termination-time|The stop and release time specified in the operating system of a preemptible instance. The time is in the yyyy-MM-ddThh:mm:ssZ format \(UTC+0\). Example: 2018-04-07T17:03:00Z.|
|/meta-data/instance/virtualization-solution|The ECS virtualization solution. Virt 1.0 and Virt 2.0 are supported.|
|/meta-data/instance/virtualization-solution-version|The version of the ECS virtualization solution.|
|/maintenance/active-system-events|The active system events of the instance.|

## Dynamic metadata items

|Item|Description|
|----|-----------|
|/dynamic/instance-identity/document|The instance identity document that provides the identity information of the instance. The instance identity document contains information such as the ID and IP address of the instance.|
|/dynamic/instance-identity/pkcs7|The instance identity signature that is used to verify the authenticity and content of the instance identity document.|

