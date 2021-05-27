---
keyword: [Alibaba Cloud, ECS, time calibration, time zone]
---

# Alibaba Cloud NTP server

This topic describes Alibaba Cloud Network Time Protocol \(NTP\) servers. Alibaba Cloud provides internal and public NTP servers to synchronize the local time of Elastic Compute Service \(ECS\) instances in networks.

## Internal and public NTP servers

NTP is used to synchronize computer time in a network.

The consistency of time and time zones in ECS is crucial because it can affect task execution results. For example, when you update a database or analyze logs, the time sequence has a significant impact on the results. When you run business on ECS instances, you must standardize the time zones of all involved instances to avoid problems such as logical confusions and network request errors. You can use NTP servers to synchronize the local time of all ECS instances within a network.

ECS provides a high-precision NTP server for your convenience. The `ntp.cloud.aliyuncs.com` server offers a globally distributed NTP service that uses Stratum 1 servers. Stratum 1 servers are suitable for industries such as finance, communication, scientific research, and astronomy that require precise timing. The NTP service is also used to synchronize the local time between ECS instances and other cloud services. The following table describes the domain names of Alibaba Cloud NTP servers in various networks.

|Classic network \(internal network\)|VPC \(internal network\)|Internet|
|:-----------------------------------|:-----------------------|:-------|
|-|ntp.cloud.aliyuncs.com|ntp.aliyun.com|
|ntp1.cloud.aliyuncs.com|ntp7.cloud.aliyuncs.com|ntp1.aliyun.com|
|ntp2.cloud.aliyuncs.com|ntp8.cloud.aliyuncs.com|ntp2.aliyun.com|
|ntp3.cloud.aliyuncs.com|ntp9.cloud.aliyuncs.com|ntp3.aliyun.com|
|ntp4.cloud.aliyuncs.com|ntp10.cloud.aliyuncs.com|ntp4.aliyun.com|
|ntp5.cloud.aliyuncs.com|ntp11.cloud.aliyuncs.com|ntp5.aliyun.com|
|ntp6.cloud.aliyuncs.com|ntp12.cloud.aliyuncs.com|ntp6.aliyun.com|
|-|-|ntp7.aliyun.com|

## Other public services

The following table describes other public services provided by Alibaba Cloud.

|Public service|Description|
|--------------|-----------|
|Public Domain Name System \(DNS\): 223.5.5.5/223.6.6.6|Domain name: `http://www.alidns.com`|
|Website of public images: `https://developer.aliyun.com/mirror`|Update frequency: Images are updated from 02:00 to 04:00 every day \(UTC+8\). The images contain a wide collection of Linux distributions and open source software. **Note:** The website of public images is being upgraded and maintained. The features of some image repositories are available. You can manually add software repositories. For more information, see [Add a software repository](/intl.en-US/Instance/Manage instances/Manage software on Linux instances/Add a software repository.md). |

## References

-   [Configure the NTP service for Windows instances](/intl.en-US/Instance/Manage instances/Configure time/Configure the NTP service for Windows instances.md)
-   [Configure the NTP service for ECS instances that run CentOS 6](/intl.en-US/Instance/Manage instances/Configure time/Configure the NTP service for ECS instances that run CentOS 6.md)

