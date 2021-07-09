---
keyword: [ECS, metadata, ]
---

# Instance metadata items

This topic describes the basic and dynamic metadata items that you can obtain from an Elastic Compute Service \(ECS\) instance.

## Basic metadata items

|Item|Description|Example|
|:---|:----------|-------|
|/meta-data/dns-conf/nameservers|The Domain Name System \(DNS\) configurations of the instance.|100.100.XX.XX|
|/meta-data/hostname|The hostname of the instance.|iZbp13znx0m0me8cquu\*\*\*\*|
|/meta-data/instance/instance-type|The instance type of the instance.|ecs.g6e.large|
|/meta-data/image-id|The ID of the image used to create the instance.|aliyun\_3\_x64\_20G\_alibase\_20210425.vhd|
|/meta-data/image/market-place/product-code|The product code of the Alibaba Cloud Marketplace image.|cmjj01\*\*\*\*|
|/meta-data/image/market-place/charge-type|The billing method of the Alibaba Cloud Marketplace image.|PrePaid|
|/meta-data/instance-id|The ID of the instance.|iZbp13znx0m0me8cquu\*\*\*\*|
|/meta-data/mac|The media access control \(MAC\) address of the instance. If the instance is bound with multiple network interface controllers \(NICs\), only the MAC address of eth0 is displayed.|00:16:3e:0f:XX:XX|
|/meta-data/network-type|The network type of the instance. Only instances that reside in virtual private clouds \(VPCs\) are supported.|vpc|
|/meta-data/network/interfaces/macs/|The list of MAC addresses of the NICs.|00:16:3e:0f:XX:XX|
|/meta-data/network/interfaces/macs/\[mac\]/network-interface-id|The identifier of the NIC. Replace \[mac\] with the MAC address of the instance.|eni-bp1b2c0jvnj0g17b\*\*\*\*|
|/meta-data/network/interfaces/macs/\[mac\]/netmask|The subnet mask of the NIC.|255.255.XX.XX|
|/meta-data/network/interfaces/macs/\[mac\]/vswitch-cidr-block|The IPv4 CIDR block of the vSwitch to which the NIC is connected.|192.168.XX.XX/24|
|/meta-data/network/interfaces/macs/\[mac\]/vpc-cidr-block|The IPv4 CIDR block of the VPC to which the NIC belongs.|192.168.XX.XX/16|
|/meta-data/network/interfaces/macs/\[mac\]/private-ipv4s|The private IPv4 addresses assigned to the NIC.|\["192.168.XX.XX"\]|
|/meta-data/network/interfaces/macs/\[mac\]/vswitch-id|The ID of the vSwitch that resides within the same VPC as the security group of the NIC.|vsw-bp1ygryo03m39xhsy\*\*\*\*|
|/meta-data/network/interfaces/macs/\[mac\]/vpc-id|The ID of the VPC to which the security group of the NIC belongs.|vpc-bp1e0g399hkd7c8q3\*\*\*\*|
|/meta-data/network/interfaces/macs/\[mac\]/primary-ip-address|The primary private IP address of the NIC.|192.168.XX.XX|
|/meta-data/network/interfaces/macs/\[mac\]/gateway|The IPv4 gateway address of the VPC to which the NIC belongs.|192.168.XX.XX|
|/meta-data/instance/max-netbw-egress|The maximum outbound internal bandwidth of the instance. Unit: Kbit/s.|1228800|
|/meta-data/instance/max-netbw-ingress|The maximum inbound internal bandwidth of the instance. Unit: Kbit/s.|1228800|
|/meta-data/private-ipv4|The private IPv4 address of the primary NIC.|192.168.XX.XX|
|/meta-data/eipv4|This metadata item is used to obtain the following information:-   The public IPv4 address of the instance
-   The elastic public IPv4 address associated with the primary NIC

|120.55.XX.XX|
|/meta-data/ntp-conf/ntp-servers|The IP address of the Network Time Protocol \(NTP\) server.|ntp1.aliyun.com|
|/meta-data/owner-account-id|The ID of the Alibaba Cloud account to which the instance belongs.|1609\*\*\*\*|
|/meta-data/public-keys/|The list of all public keys of the instance.|skp-bp1brtqj5sw1vq\*\*\*\*/|
|/meta-data/region-id|The region ID of the instance.|cn-hangzhou|
|/meta-data/zone-id|The zone ID of the instance.|cn-hangzhou-i|
|/meta-data/serial-number|The serial number of the instance.|4acd2b47-b328-4762-852f-998\*\*\*\*|
|/meta-data/source-address|The address of the YUM or APT image repository. The package management software of a Linux instance can obtain updates from the image repository.|http://mirrors.cloud.aliyuncs.com|
|/meta-data/kms-server|The server that activates Key Management Service \(KMS\) for a Windows instance.|kms.cloud.aliyuncs.com|
|/meta-data/wsus-server/wu-server|The server that updates a Windows instance.|http://update.cloud.aliyuncs.com|
|/meta-data/wsus-server/wu-status-server|The server that monitors the update status of a Windows instance.|http://update.cloud.aliyuncs.com|
|/meta-data/vpc-id|The ID of the VPC to which the instance belongs.|vpc-bp1e0g399hkd7c8q\*\*\*\*|
|/meta-data/vpc-cidr-block|The CIDR block of the VPC to which the instance belongs.|192.168.XX.XX/16|
|/meta-data/vswitch-cidr-block|The CIDR block of the vSwitch to which the instance is connected.|192.168.XX.XX/24|
|/meta-data/vswitch-id|The ID of the vSwitch to which the instance is connected.|vsw-bp1ygryo03m39xhsy\*\*\*\*|
|-   /meta-data/ram/security-credentials/\[role-name\]
-   /meta-data/ram/security-credentials/

|The temporary Security Token Service \(STS\) credentials generated for the Resource Access Management \(RAM\) role of the instance. You can obtain the STS credentials only after the instance assumes a RAM role. Replace \[role-name\] with the name of the RAM role. If the \[role-name\] parameter is not specified, the name of the RAM role is returned. **Note:** A new STS credential is available 30 minutes prior to the expiration time of the previous one. During this period, both STS credentials can be used.

|AliyunECSImageExportDefaultRole|
|/meta-data/instance/spot/termination-time|The stop and release time specified in the operating system of a preemptible instance. The time is in the yyyy-MM-ddThh:mm:ssZ format \(UTC+0\).|2020-04-07T17:03:00Z|
|/meta-data/instance/virtualization-solution|The ECS virtualization solution. Virt 1.0 and Virt 2.0 are supported.|ECS Virt|
|/meta-data/instance/virtualization-solution-version|The version of the ECS virtualization solution.|2.0|
|/maintenance/active-system-events|The active system events of the instance.|None|

## Dynamic metadata items

|Item|Description|Example|
|----|-----------|-------|
|/dynamic/instance-identity/document|The instance identity document that provides the identity information of the instance. The instance identity document contains information such as the ID and IP address of the instance.|\{"zone-id":"cn-hangzhou-i","serial-number":"4acd2b47-b328-4762-852f-99\*\*\*\*","instance-id":"i-bp13znx0m0me8cq\*\*\*\*","region-id":"cn-hangzhou","private-ipv4":"192.168.XX.XX","owner-account-id":"1609\*\*\*\*","mac":"00:16:3e:0f:XX:XX","image-id":"aliyun\_3\_x64\_20G\_alibase\_20210425.vhd","instance-type":"ecs.g6e.large"\}|
|/dynamic/instance-identity/pkcs7|The instance identity signature that is used to verify the authenticity and content of the instance identity document.|MIIDJwYJKoZIhvcNAQcCoIIDGDCCAxQCAQExCzAJBgUrDgMCGgUAMIIBYQYJKoZIhvcNAQcBoIIBUgSCAU57InpvbmUtaWQiOiJjbi1oYW5nemhvdS1oIiwic2VyaWFsLW\*\*\*\*|

