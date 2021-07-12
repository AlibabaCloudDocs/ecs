---
keyword: [release note, released updates, ECS, Linux, Windows]
---

# Release notes

This topic describes the updates to Elastic Compute Service \(ECS\) public images. The release notes are ordered by release date, from the latest to the earliest.

## Background information

-   Unless otherwise stated, the released updates apply to all Alibaba Cloud regions where ECS is available.
-   Public images are applicable to most instance families. Some instance families can use only specific public images. For more information, see the following sections:
    -   [UEFI images](#section_5m3_jo1_1sl)
    -   [Trusted images](#section_ta4_ich_flj)
    -   [AMD images](#section_in3_bba_8af)

## Anolis OS

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Anolis OS 8.2 RHCK|anolisos\_8\_2\_x64\_20G\_rhck\_alibase\_20210529.vhd|2021-05-29|-   New release.
-   Provided 100% compatibility with the CentOS 8 software ecosystem and other mainstream Linux distributions.
-   Provided a migration tool to migrate CentOS operating systems and applications to Anolis OS.
-   Applicable regions: China \(Hangzhou\), China \(Beijing\), China \(Heyuan\), China \(Chengdu\), UK \(London\), Germany \(Frankfurt\), Singapore \(Singapore\), Indonesia \(Jakarta\), Malaysia \(Kuala Lumpur\), Australia \(Sydney\), and UAE \(Dubai\). |

## CentOS

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|CentOS 8.3|centos\_8\_3\_x64\_20G\_alibase\_20210521.vhd|2021-05-21|-   Kernel version: 4.18.0-240.22.1.el8\_3.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 7.9|centos\_7\_9\_x64\_20G\_alibase\_20210521.vhd|2021-05-21|-   Kernel version: 3.10.0-1160.25.1.el7.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 8.3|centos\_8\_3\_x64\_20G\_alibase\_20210420.vhd|2021-04-20|-   Kernel version: 4.18.0-240.22.1.el8\_3.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 7.9|centos\_7\_9\_x64\_20G\_alibase\_20210420.vhd|2021-04-20|-   Kernel version: 3.10.0-1160.24.1.el7.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 8.3|centos\_8\_3\_x64\_20G\_alibase\_20210318.vhd|2021-03-18|-   Kernel version: 4.18.0-240.15.1.el8\_3.x86\_64.
-   Changes:
    -   Updated to include the latest patches.
    -   Supported NVME drivers. |
|CentOS 7.9|centos\_7\_9\_x64\_20G\_alibase\_20210318.vhd|2021-03-18|-   Kernel version: 3.10.0-1160.15.2.el7.x86\_64.
-   Changes:
    -   Updated to include the latest patches.
    -   Supported NVME drivers. |
|CentOS 7.9|centos\_7\_9\_x64\_20G\_alibase\_20210128.vhd|2021-01-28|-   Kernel version: 3.10.0-1160.11.1.el7.x86\_64.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2021-3156 vulnerability. |
|CentOS 7.9|centos\_7\_9\_x64\_20G\_alibase\_20201228.vhd|2020-12-28|-   Kernel version: 3.10.0-1160.11.1.el7.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 8.2|centos\_8\_2\_x64\_20G\_alibase\_20201120.vhd|2020-11-20|-   Kernel version: 4.18.0-193.28.1.el8\_2.x86\_64.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2020-14386 vulnerability in the Linux kernel. |
|CentOS 7.9|centos\_7\_9\_x64\_20G\_alibase\_20201120.vhd|2020-11-20|-   Kernel version: 3.10.0-1160.6.1.el7.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 6.10|centos\_6\_10\_x64\_20G\_alibase\_20201120.vhd|2020-11-20|-   Kernel version: 2.6.32-754.35.1.el6.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 8.2|centos\_8\_2\_x64\_20G\_alibase\_20200914.vhd|2020-09-14|-   Kernel version: 4.18.0-193.14.2.el8\_2.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 7.8|centos\_7\_8\_x64\_20G\_alibase\_20200914.vhd|2020-09-14|-   Kernel version: 3.10.0-1127.19.1.el7.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 6.10|centos\_6\_10\_x64\_20G\_alibase\_20200914.vhd|2020-09-14|-   Kernel version: 2.6.32-754.33.1.el6.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 8.2|centos\_8\_2\_x64\_20G\_alibase\_20200824.vhd|2020-08-24|-   Kernel version: 4.18.0-193.14.2.el8\_2.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 7.8|centos\_7\_8\_x64\_20G\_alibase\_20200817.vhd|2020-08-17|-   Kernel version: 3.10.0-1127.18.2.el7.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 6.10|centos\_6\_10\_x64\_20G\_alibase\_20200817.vhd|2020-08-17|-   Kernel version: 2.6.32-754.31.1.el6.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 8.2|centos\_8\_2\_x64\_20G\_alibase\_20200717.vhd|2020-07-17|-   Kernel version: 4.18.0-193.6.3.el8\_2.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 7.8|centos\_7\_8\_x64\_20G\_alibase\_20200717.vhd|2020-07-17|-   Kernel version: 3.10.0-1127.13.1.el7.x86\_64.
-   Changes: enabled IPv6 by default. |
|CentOS 6.10|centos\_6\_10\_x64\_20G\_alibase\_20200717.vhd|2020-07-17|-   Kernel version: 2.6.32-754.30.2.el6.x86\_64.
-   Changes: enabled IPv6 by default. |
|CentOS 7.8|centos\_7\_8\_x64\_20G\_alibase\_20200622.vhd|2020-06-22|-   Kernel version: 3.10.0-1127.10.1.el7.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 8.2|centos\_8\_2\_x64\_20G\_alibase\_20200616.vhd|2020-06-16|-   Kernel version: 4.18.0-193.el8.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 6.10|centos\_6\_10\_x64\_20G\_alibase\_20200616.vhd|2020-06-16|-   Kernel version: 2.6.32-754.30.2.el6.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 8.1|centos\_8\_1\_x64\_20G\_alibase\_20200519.vhd|2020-05-19|-   Kernel version: 4.18.0-147.8.1.el8\_1.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 7.8|centos\_7\_8\_x64\_20G\_alibase\_20200519.vhd|2020-05-19|-   Kernel version: 3.10.0-1127.8.2.el7.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 6.10|centos\_6\_10\_x64\_20G\_alibase\_20200519.vhd|2020-05-19|-   Kernel version: 2.6.32-754.29.2.el6.x86\_64.
-   Changes: updated to include the latest patches. |
|CentOS 8.1|centos\_8\_1\_x64\_20G\_alibase\_20200426.vhd|2020-04-26|-   Kernel version: 4.18.0-147.8.1.el8\_1.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 7.7|centos\_7\_7\_x64\_20G\_alibase\_20200426.vhd|2020-04-26|-   Kernel version: 3.10.0-1062.18.1.el7.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 6.10|centos\_6\_10\_x64\_20G\_alibase\_20200426.vhd|2020-04-26|-   Kernel version: 2.6.32-754.28.1.el6.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 8.1|centos\_8\_1\_x64\_20G\_alibase\_20200329.vhd|2020-03-29|-   Kernel version: 4.18.0-147.5.1.el8\_1.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 7.7|centos\_7\_7\_x64\_20G\_alibase\_20200329.vhd|2020-03-29|-   Kernel version: 3.10.0-1062.18.1.el7.x86\_64.
-   Changes:
    -   Updated to include the latest operating system patches.
    -   Upgraded cloud-init to version 19.1.

**Note:** cloud-init dynamically generates network configurations. For more information about custom network configurations, see the "\(Optional\) Customize network configuration" section in [Install cloud-init](/intl.en-US/Images/Custom image/Import images/Install cloud-init.md). |
|CentOS 6.10|centos\_6\_10\_x64\_20G\_alibase\_20200319.vhd|2020-03-19|-   Kernel version: 2.6.32-754.28.1.el6.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 8.0|centos\_8\_0\_x64\_20G\_alibase\_20200218.vhd|2020-02-18|-   Kernel version: 4.18.0-147.5.1.el8\_1.x86\_64.
-   Changes:
    -   Updated to include the latest operating system patches.
    -   Added the EPEL repository and Chinese Simplified \(zh-CN\) language pack.
    -   Enabled IPv6 by default.
-   Known issue: The system version of ECS instances created from the centos\_8\_0\_x64\_20G\_alibase\_20200218.vhd public image is CentOS 8.1. For more information about this issue, see [CentOS 8.0: The version update of the public image leads to the change of image version number of created instances](/intl.en-US/Images/Public image/Known issues.md). |
|CentOS 7.7|centos\_7\_7\_x64\_20G\_alibase\_20200220.vhd|2020-02-20|-   Kernel version: 3.10.0-1062.12.1.el7.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 6.10|centos\_6\_10\_x64\_20G\_alibase\_20200214.vhd|2020-02-14|-   Kernel version: 2.6.32-754.27.1.el6.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 6.10|centos\_6\_10\_x64\_20G\_alibase\_20200103.vhd|2020-01-03|-   Kernel version: 2.6.32-754.25.1.el6.x86\_64.
-   Changes: updated to include the latest operating system patches.
-   Applicable regions: China \(Beijing\), US \(Virginia\), China \(Hong Kong\), China \(Zhangjiakou\), China \(Hohhot\), China \(Hangzhou\), China \(Qingdao\), China \(Chengdu\), and Singapore \(Singapore\). |
|CentOS 7.7|centos\_7\_7\_x64\_20G\_alibase\_20191225.vhd|2019-12-25|-   Kernel version: 3.10.0-1062.9.1.el7.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 8.0|centos\_8\_0\_x64\_20G\_alibase\_20191225.vhd|2019-12-25|-   Kernel version: 4.18.0-80.11.2.el8\_0.x86\_64.
-   Changes:
    -   Updated to include the latest operating system patches.
    -   Upgraded cloud-init to version 19.1.

**Note:** cloud-init dynamically generates network configurations. For more information about custom network configurations, see the "\(Optional\) Customize network configuration" section in [Install cloud-init](/intl.en-US/Images/Custom image/Import images/Install cloud-init.md). |
|CentOS 6.10|centos\_6\_10\_x64\_20G\_alibase\_20191223.vhd|2019-12-25|-   Kernel version: 2.6.32-754.24.3.el6.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 7.7|centos\_7\_7\_64\_20G\_alibase\_20191008.vhd|2019-10-8|-   Kernel version: 3.10.0-1062.1.2.el7.x86\_64.
-   Changes: new release. |
|CentOS 7.6|centos\_7\_06\_64\_20G\_alibase\_20190711.vhd|2019-7-11|-   Kernel version: 3.10.0-957.21.3.el7.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 6.10|centos\_6\_10\_64\_20G\_alibase\_20190709.vhd|2019-7-9|-   Kernel version: 2.6.32-754.17.1.el6.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 6.10|centos\_6\_10\_64\_20G\_alibase\_20190621.vhd|2019-6-21|-   Kernel version: 2.6.32-754.15.3.el6.x86\_64.
-   Changes: updated to include the latest operating system patches and fixed the CVE-2019-11477 vulnerability. |
|CentOS 7.6|centos\_7\_06\_64\_20G\_alibase\_20190619.vhd|2019-6-19|-   Kernel version: 3.10.0-957.21.3.el7.x86\_64.
-   Changes:
    -   Updated to include the latest patches and fixed the CVE-2019-11477 vulnerability.
    -   Set the default CPU mode to performance. |
|CentOS 7.6|centos\_7\_06\_64\_20G\_alibase\_20190218.vhd|2019-2-18|-   Kernel version: 3.10.0-957.5.1.el7.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 7.6|centos\_7\_05\_64\_20G\_alibase\_20181212.vhd|2018-12-12|-   Kernel version: 3.10.0-957.1.3.el7.x86\_64.
-   Changes: updated to include the latest operating system patches. |
|CentOS 7.5|centos\_7\_05\_64\_20G\_alibase\_20181210.vhd|2018-12-10|-   Kernel version: 3.10.0-862.3.3.el7.x86\_64.
-   Changes:
    -   Updated to include the latest operating system patches.
    -   Upgraded the cloud-init version.
    -   Enabled the chrony \(time synchronization\) service.
    -   Disabled password authentication by default.
    -   Set GRUB\_TIMEOUT to 1. |

## Debian

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Debian 10.9|debian\_10\_9\_x64\_20G\_alibase\_20210521.vhd|2021-05-21|-   Kernel version: 4.19.0-16-amd64.
-   Changes: updated to include the latest patches. |
|Debian 9.13|debian\_9\_13\_x64\_20G\_alibase\_20210521.vhd|2021-05-21|-   Kernel version: 4.9.0-15-amd64.
-   Changes: updated to include the latest patches. |
|Debian 10.9|debian\_10\_9\_x86\_20G\_alibase\_20210420.vhd|2021-04-20|-   Kernel version: 4.19.0-16-amd64.
-   Changes: updated to include the latest patches. |
|Debian 9.13|debian\_9\_13\_x64\_20G\_alibase\_20210420.vhd|2021-04-20|-   Kernel version: 4.9.0-15-amd64.
-   Changes: updated to include the latest patches. |
|Debian 10.9|debian\_10\_9\_x86\_20G\_alibase\_20210318.vhd|2021-03-18|-   Kernel version: 4.19.0-16-amd64.
-   Changes: updated to include the latest patches. |
|Debian 9.13|debian\_9\_13\_x64\_20G\_alibase\_20210318.vhd|2021-03-18|-   Kernel version: 4.9.0-15-amd64.
-   Changes: updated to include the latest patches. |
|Debian 10.7|debian\_10\_7\_x64\_20G\_alibase\_20210128.vhd|2021-01-28|-   Kernel version: 4.19.0-13-amd64.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2021-3156 vulnerability in the Linux kernel. |
|Debian 9.13|debian\_9\_13\_x64\_20G\_alibase\_20210128.vhd|2021-01-28|-   Kernel version: 4.9.0-14-amd64.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2021-3156 vulnerability in the Linux kernel. |
|Debian 10.7|debian\_10\_7\_x64\_20G\_alibase\_20201228.vhd|2020-12-28|-   Kernel version: 4.19.0-13-amd64.
-   Changes: updated to include the latest patches. |
|Debian 9.13|debian\_9\_13\_x64\_20G\_alibase\_20201228.vhd|2020-12-28|-   Kernel version: 4.9.0-14-amd64.
-   Changes: updated to include the latest patches. |
|Debian 10.6|debian\_10\_6\_x64\_20G\_alibase\_20201120.vhd|2020-11-20|-   Kernel version: 4.19.0-12-amd64.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2020-14386 vulnerability in the Linux kernel. |
|Debian 9.13|debian\_9\_13\_x64\_20G\_alibase\_20201120.vhd|2020-11-20|-   Kernel version: 4.9.0-14-amd64.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2020-14386 vulnerability in the Linux kernel. |
|Debian 10.5|debian\_10\_5\_x64\_20G\_alibase\_20200914.vhd|2020-09-14|-   Kernel version: 4.19.0-10-amd64.
-   Changes: updated to include the latest patches. |
|Debian 9.13|debian\_9\_13\_x64\_20G\_alibase\_20200914.vhd|2020-09-14|-   Kernel version: 4.9.0-13-amd64.
-   Changes: updated to include the latest patches. |
|Debian 10.5|debian\_10\_5\_x64\_20G\_alibase\_20200819.vhd|2020-08-19|-   Kernel version: 4.19.0-10-amd64.
-   Changes:
    -   Updated to include the latest patches.
    -   Updated NIC configurations and configured DHCP for eight NICs by default. |
|Debian 9.13|debian\_9\_13\_x64\_20G\_alibase\_20200819.vhd|2020-08-19|-   Kernel version: 4.9.0-13-amd64.
-   Changes:
    -   Updated to include the latest patches.
    -   Updated NIC configurations and configured DHCP for eight NICs by default. |
|Debian 9.13|debian\_9\_13\_x64\_20G\_alibase\_20200730.vhd|2020-07-30|-   Kernel version: 4.9.0-13-amd64.
-   Changes:
    -   Updated to include the latest patches.
    -   Enabled IPv6 by default. |
|Debian 10.4|debian\_10\_4\_x64\_20G\_alibase\_20200717.vhd|2020-07-17|-   Kernel version: 4.19.0-10-amd64.
-   Changes: updated to include the latest patches. |
|Debian 10.4|debian\_10\_4\_x64\_20G\_alibase\_20200622.vhd|2020-06-22|-   Kernel version: 4.19.0-9-amd64.
-   Changes: updated to include the latest patches. |
|Debian 9.12|debian\_9\_12\_x64\_20G\_alibase\_20200622.vhd|2020-06-22|-   Kernel version: 4.9.0-12-amd64.
-   Changes: updated to include the latest patches. |
|Debian 10.4|debian\_10\_4\_x64\_20G\_alibase\_20200519.vhd|2020-05-19|-   Kernel version: 4.19.0-9-amd64.
-   Changes: updated to include the latest patches. |
|Debian 9.12|debian\_9\_12\_x64\_20G\_alibase\_20200519.vhd|2020-05-19|-   Kernel version: 4.9.0-12-amd64.
-   Changes: updated to include the latest patches. |
|Debian 10.3|debian\_10\_3\_x64\_20G\_alibase\_20200426.vhd|2020-04-26|-   Kernel version: 4.19.0-8-amd64.
-   Changes: updated to include the latest operating system patches. |
|Debian 9.12|debian\_9\_12\_x64\_20G\_alibase\_20200426.vhd|2020-04-26|-   Kernel version: 4.9.0-12-amd64.
-   Changes: updated to include the latest operating system patches. |
|Debian 10.3|debian\_10\_3\_x64\_20G\_alibase\_20200329.vhd|2020-03-29|-   Kernel version: 4.19.0-8-amd64.
-   Changes:
    -   Updated to include the latest operating system patches.
    -   Enabled IPv6 by default. |
|Debian 9.12|debian\_9\_12\_x64\_20G\_alibase\_20200324.vhd|2020-03-24|-   Kernel version: 4.9.0-12-amd64.
-   Changes: updated to include the latest operating system patches. |
|Debian 9.12|debian\_9\_12\_x64\_20G\_alibase\_20200220.vhd|2020-02-20|-   Kernel version: 4.9.0-12-amd64.
-   Changes: updated to include the latest operating system patches. |
|Debian 10.3|debian\_10\_3\_x64\_20G\_alibase\_20200218.vhd|2020-02-18|-   Kernel version: 4.19.0-8-amd64.
-   Changes: updated to include the latest operating system patches. |
|Debian 9.11|debian\_9\_11\_x64\_20G\_alibase\_20191225.vhd|2019-12-25|-   Kernel version: 4.9.0-11-amd64.
-   Changes: updated to include the latest operating system patches. |
|Debian 10.2|debian\_10\_2\_x64\_20G\_alibase\_20191223.vhd|2019-12-24|-   Kernel version: 4.19.0-6-amd64.
-   Changes:
    -   Updated to include the latest operating system patches.
    -   Upgraded cloud-init to version 19.1.

**Note:** cloud-init dynamically generates network configurations. For more information about custom network configurations, see the "\(Optional\) Customize network configuration" section in [Install cloud-init](/intl.en-US/Images/Custom image/Import images/Install cloud-init.md). |
|Debian 9.9|debian\_9\_09\_64\_20G\_alibase\_20190702.vhd|2019-7-2|-   Kernel version: 4.9.0-9-amd64.
-   Changes: updated to include the latest operating system patches. |
|Debian 9.9|debian\_9\_09\_64\_20G\_alibase\_20190510.vhd|2019-5-10|-   Kernel version: 4.9.0-9-amd64.
-   Changes: updated to include the latest operating system patches. |
|Debian 8.11|11\_64\_20G\_alibase\_20190311.vhd|2019-3-11|-   Kernel version: 3.16.0-7-amd64.
-   Changes:
    -   Updated to include the latest operating system patches.
    -   Fixed invalid APT repository configurations in Debian 8.9. |
|Debian 9.8|debian\_9\_08\_64\_20G\_alibase\_20190225.vhd|2019-2-25|-   Kernel version: 4.9.0-8-amd64.
-   Changes: updated to include the latest operating system patches. |
|Debian 9.6|debian\_9\_06\_64\_20G\_alibase\_20190103.vhd|2019-1-3|-   Kernel version: 4.9.0-8-amd64.
-   Changes: enabled the systemd-networkd service. |
|Debian 9.6|debian\_9\_06\_64\_20G\_alibase\_20181212.vhd|2018-12-12|-   Kernel version: 4.9.0-8-amd64.
-   Changes:
    -   Updated to include the latest operating system patches.
    -   Upgraded the cloud-init version.
    -   Enabled the chrony \(time synchronization\) service.
    -   Set GRUB\_TIMEOUT to 1.
-   Known issues: [classic network configuration issues](/intl.en-US/Images/Public image/Known issues.md). |

## FreeBSD

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|FreeBSD 11.4|freebsd\_11\_4\_x64\_30G\_alibase\_20210319.vhd|2021-03-19|-   Kernel version: 11.4-RELEASE.
-   Changes: updated to include the latest patches. |
|FreeBSD 12.1|freebsd\_12\_1\_x64\_30G\_alibase\_20201022.vhd|2020-10-22|-   Kernel version: 12.1-RELEASE.
-   Changes: updated to include the latest patches. |
|FreeBSD 11.3|freebsd\_11\_3\_x64\_30G\_alibase\_20200803.vhd|2020-08-03|-   Kernel version: 11.3-RELEASE.
-   Changes: updated to include the latest patches. |
|FreeBSD 11.3|freebsd\_11\_3\_x64\_20G\_alibase\_20200420.vhd|2020-04-20|-   Kernel version: 11.3-RELEASE.
-   Changes: updated to include the latest patches. |
|FreeBSD 11.2|freebsd\_11\_02\_64\_30G\_alibase\_20190806.vhd|2019-8-6|-   Kernel version: 11.2-RELEASE.
-   Changes:
    -   Fixed the clock offset issue.
    -   Fixed the error that causes the failure to create a 30 GiB system disk. |

## Ubuntu

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Ubuntu20.04|ubuntu\_20\_04\_x64\_20G\_alibase\_20210521.vhd|2021-05-21|-   Kernel version: 5.4.0-74-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20210521.vhd|2021-05-21|-   Kernel version: 4.15.0-144-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20210521.vhd|2021-05-21|-   Kernel version: 4.4.0-210-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu20.04|ubuntu\_20\_04\_x64\_20G\_alibase\_20210420.vhd|2021-04-20|-   Kernel version: 5.4.0-73-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20210420.vhd|2021-04-20|-   Kernel version: 4.15.0-143-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20210420.vhd|2021-04-20|-   Kernel version: 4.4.0-210-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu20.04|ubuntu\_20\_04\_x64\_20G\_alibase\_20210318.vhd|2021-03-18|-   Kernel version: 5.4.0-67-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20210318.vhd|2021-03-18|-   Kernel version: 4.15.0-139-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20210318.vhd|2021-03-18|-   Kernel version: 4.4.0-206-generic.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2021-3156 vulnerability in the Linux kernel. |
|Ubuntu20.04|ubuntu\_20\_04\_x64\_20G\_alibase\_20210128.vhd|2021-01-28|-   Kernel version: 5.4.0-65-generic.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2021-3156 vulnerability in the Linux kernel. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20210128.vhd|2021-01-28|-   Kernel version: 4.15.0-135-generic.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2021-3156 vulnerability in the Linux kernel. |
|Ubuntu20.04|ubuntu\_20\_04\_x64\_20G\_alibase\_20201228.vhd|2020-12-28|-   Kernel version: 5.4.0-58-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20201228.vhd|2020-12-28|-   Kernel version: 4.15.0-128-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20201228.vhd|2020-12-28|-   Kernel version: 4.4.0-198-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu20.04|ubuntu\_20\_04\_x64\_20G\_alibase\_20201120.vhd|2020-11-20|-   Kernel version: 5.4.0-54-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20201120.vhd|2020-11-20|-   Kernel version: 4.15.0-124-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20201120.vhd|2020-11-20|-   Kernel version: 4.4.0-194-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu20.04|ubuntu\_20\_04\_x64\_20G\_alibase\_20200914.vhd|2020-09-14|-   Kernel version: 5.4.0-47-generic.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2020-14386 vulnerability in the Linux kernel. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20200914.vhd|2020-09-14|-   Kernel version: 4.15.0-117-generic.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2020-14386 vulnerability in the Linux kernel. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20200914.vhd|2020-09-14|-   Kernel version: 4.4.0-189-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20200817.vhd|2020-08-17|-   Kernel version: 4.15.0-112-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20200817.vhd|2020-08-17|-   Kernel version: 4.4.0-187-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20200717.vhd|2020-07-17|-   Kernel version: 4.15.0-111-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20200717.vhd|2020-07-17|-   Kernel version: 4.4.0-185-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20200618.vhd|2020-06-18|-   Kernel version: 4.15.0-106-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20200618.vhd|2020-06-18|-   Kernel version: 4.4.0-184-generic.
-   Changes: updated to include the latest patches. |
|Ubuntu20.04|ubuntu\_20\_04\_x64\_20G\_alibase\_20200522.vhd|2020-05-22|-   New release.
-   Kernel version: 5.4.0-31-generic. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20200522.vhd|2020-05-22|-   Kernel version: 4.4.0-179-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20200521.vhd|2020-05-21|-   Kernel version: 4.15.0-101-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20200426.vhd|2020-04-26|-   Kernel version: 4.15.0-96-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20200426.vhd|2020-04-26|-   Kernel version: 4.4.0-177-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20200329.vhd|2020-03-29|-   Kernel version: 4.15.0-91-generic.
-   Changes:
    -   Updated to include the latest operating system patches.
    -   Enabled IPv6 by default. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20200319.vhd|2020-03-19|-   Kernel version: 4.4.0-176-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20200220.vhd|2020-02-20|-   Kernel version: 4.15.0-88-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20200220.vhd|2020-02-20|-   Kernel version: 4.4.0-174-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu18.04|ubuntu\_18\_04\_x64\_20G\_alibase\_20191225.vhd|2019-12-25|-   Kernel version: 4.15.0-72-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu16.04|ubuntu\_16\_04\_x64\_20G\_alibase\_20191225.vhd|2019-12-25|-   Kernel version: 4.4.0-170-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu 18.04|ubuntu\_18\_04\_64\_20G\_alibase\_20190624.vhd|2019-6-24|-   Kernel version: 4.15.0-52-generic.
-   Changes: updated to include the latest operating system patches and fixed the CVE-2019-11477 vulnerability. |
|Ubuntu 16.04|ubuntu\_16\_04\_64\_20G\_alibase\_20190620.vhd|2019-6-20|-   Kernel version: 4.4.0-151-generic.
-   Changes: updated to include the latest operating system patches and fixed the CVE-2019-11477 vulnerability. |
|Ubuntu 16.04|ubuntu\_16\_04\_64\_20G\_alibase\_20190513.vhd|2019-5-13|-   Kernel version: 4.4.0-146-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu 18.04|ubuntu\_18\_04\_64\_20G\_alibase\_20190509.vhd|2019-5-9|-   Kernel version: 4.15.0-48-generic.
-   Changes:
    -   Upgraded cloud-init to speed up system boot.
    -   Updated to include the latest operating system patches. |
|Ubuntu 16.04|ubuntu\_16\_04\_64\_20G\_alibase\_20190301.vhd|2019-3-1|-   Kernel version: 4.4.0-142-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu 18.04|ubuntu\_18\_04\_64\_20G\_alibase\_20190223.vhd|2019-2-23|-   Kernel version: 4.15.0-45-generic.
-   Changes: updated to include the latest operating system patches. |
|Ubuntu 18.04|ubuntu\_18\_04\_64\_20G\_alibase\_20181212.vhd|2018-12-12|-   Kernel version: 4.15.0-42-generic.
-   Changes:
    -   Updated to include the latest operating system patches.
    -   Upgraded the cloud-init version.
    -   Enabled the chrony \(time synchronization\) service.
    -   Set GRUB\_TIMEOUT to 1. |

## CoreOS

**Note:** Based on the end-of-life announcement from the Fedora CoreOS community, updates are no longer provided for CoreOS Container Linux as of May 26, 2020. In light of this, Alibaba Cloud has issued the following announcements:

-   As of May 26, 2020, Alibaba Cloud no longer provides technical support for ECS instances that use the CoreOS Container Linux operating system. However, you can still use existing ECS instances that run this operating system.
-   You can still obtain CoreOS Container Linux images from Alibaba Cloud before September 30, 2020. After September 30, 2020, you will be unable to use CoreOS Container Linux public images provided by Alibaba Cloud to create ECS instances.
-   As of May 26, 2020, CoreOS Container Linux can continue to be used on instances on which it is already installed. However, no security patches are available because the operating system has reached its end of life. For security concerns, we recommend that you no longer use CoreOS Container Linux images.
-   The Fedora CoreOS community recommends that you use Fedora CoreOS in place of CoreOS Container Linux. Alibaba Cloud will bring Fedora CoreOS public images online soon.

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|CoreOS 2345\_3.0|coreos\_2345\_3.0\_x64\_30G\_alibase\_20200519.vhd|2020-05-19|-   Kernel version: 4.19.106-coreos.
-   Changes: updated to include the latest patches. |
|CoreOS 2345\_3.0|coreos\_2345\_3.0\_x64\_30G\_alibase\_20200423.vhd|2020-04-23|-   Kernel version: 4.19.106-coreos.
-   Changes: updated to include the latest operating system patches. |
|CoreOS 2345\_3.0|coreos\_2345\_3.0\_x64\_30G\_alibase\_20200325.vhd|2020-03-25|-   Kernel version: 4.19.106-coreos.
-   Changes: updated to include the latest operating system patches. |
|CoreOS 2303\_4.0|coreos\_2303\_4.0\_x64\_30G\_alibase\_20200217.vhd|2020-02-17|-   Kernel version: 4.19.95-coreos.
-   Changes: updated to include the latest operating system patches. |
|CoreOS 2303\_3.0|coreos\_2303\_3\_x64\_30G\_alibase\_20191223.vhd|2019-12-23|-   Kernel version: 4.19.86-coreos.
-   Changes: updated to include the latest operating system patches. |

## OpenSUSE

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Opensuse 15.2|opensuse\_15\_2\_x64\_20G\_alibase\_20210521.vhd|2021-05-21|-   Kernel version: 5.3.18-lp152.75-default.
-   Updated to include the latest patches. |
|Opensuse 15.2|opensuse\_15\_2\_x64\_20G\_alibase\_20210420.vhd|2021-04-20|-   Kernel version: 5.3.18-lp152.69-default.
-   Updated to include the latest patches. |
|Opensuse 15.2|opensuse\_15\_2\_x64\_20G\_alibase\_20210318.vhd|2021-03-18|-   Kernel version: 5.3.18-lp152.66-default.
-   Changes:
    -   Updated to include the latest patches.
    -   Supported NVME drivers. |
|Opensuse 15.2|opensuse\_15\_2\_x64\_20G\_alibase\_20210128.vhd|2021-01-28|-   Kernel version: 5.3.18-lp152.60-default.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2021-3156 vulnerability. |
|Opensuse 15.2|opensuse\_15\_2\_x64\_20G\_alibase\_20201228.vhd|2020-12-28|-   Kernel version: 5.3.18-lp152.57-default.
-   Updated to include the latest patches. |
|Opensuse 15.2|opensuse\_15\_2\_x64\_20G\_alibase\_20201120.vhd|2020-11-20|-   Kernel version: 5.3.18-lp152.50-default.
-   Updated to include the latest patches.
-   Fixed the CVE-2020-14386 vulnerability in the Linux kernel. |
|Opensuse 15.2|opensuse\_15\_2\_x64\_20G\_alibase\_20200914.vhd|2020-09-14|-   Kernel version: 5.3.18-lp152.41-default.
-   Updated to include the latest patches. |
|Opensuse 15.2|opensuse\_15\_2\_x64\_20G\_alibase\_20200818.vhd|2020-08-18|-   Kernel version: 5.3.18-lp152.33-default.
-   Updated to include the latest patches. |
|Opensuse 15.2|opensuse\_15\_2\_x64\_20G\_alibase\_20200717.vhd|2020-07-17|-   Kernel version: 5.3.18-lp152.20.7-default.
-   Updated to include the latest patches. |
|Opensuse 15.1|opensuse\_15\_1\_x64\_20G\_alibase\_20200623.vhd|2020-06-23|-   Kernel version: 4.12.14-lp151.28.52-default.
-   Updated to include the latest patches. |
|Opensuse 15.1|opensuse\_15\_1\_x64\_20G\_alibase\_20200520.vhd|2020-05-20|-   Kernel version: 4.12.14-lp151.28.48-default.
-   Updated to include the latest patches. |
|Opensuse 15.1|opensuse\_15\_1\_x64\_20G\_alibase\_20200426.vhd|2020-04-26|-   Kernel version: 4.12.14-lp151.28.48-default.
-   Changes:
    -   Enabled IPv6 by default.
    -   Updated to include the latest operating system patches. |
|Opensuse 15.1|opensuse\_15\_1\_x64\_20G\_alibase\_20200331.vhd|2020-03-31|-   Kernel version: 4.12.14-lp151.28.44-default.
-   Changes: updated to include the latest operating system patches. |
|Opensuse 15.1|opensuse\_15\_1\_x64\_20G\_alibase\_20200222.vhd|2020-02-22|-   Kernel version: 4.12.14-lp151.28.36-default.
-   Changes: updated to include the latest operating system patches. |
|Opensuse 15.1|opensuse\_15\_1\_x64\_20G\_alibase\_20191219.vhd|2019-12-19|-   Kernel version: 4.12.14-lp151.28.36-default.
-   Changes:
    -   Updated to include the latest operating system patches.
    -   Upgraded cloud-init to version 19.1. |

## SUSE Linux Enterprise Server

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|SUSE Linux Enterprise Server 15 SP2|sles\_15\_sp2\_x64\_20G\_alibase\_20201228.vhd|2020-12-28|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 15 SP2|sles\_15\_sp2\_x64\_20G\_alibase\_20201120.vhd|2020-11-20|-   Updated to include the latest patches.
-   Fixed the CVE-2020-14386 vulnerability in the Linux kernel.
-   Fixed the bsc\#1176925 vulnerability in the Linux kernel and the issue of failed startup for hfg6 instances. |
|SUSE Linux Enterprise Server 12 SP5|sles\_12\_sp5\_x64\_20G\_alibase\_20201120.vhd|2020-11-20|-   Updated to include the latest patches.
-   Fixed the CVE-2020-14386 vulnerability in the Linux kernel. |
|SUSE Linux Enterprise Server 15 SP2|sles\_15\_sp2\_x64\_20G\_alibase\_20200914.vhd|2020-09-14|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 12 SP5|sles\_12\_sp5\_x64\_20G\_alibase\_20200914.vhd|2020-09-14|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 15 SP2|sles\_15\_sp2\_x64\_20G\_alibase\_20200820.vhd|2020-08-20|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 12 SP5|sles\_12\_sp5\_x64\_20G\_alibase\_20200819.vhd|2020-08-19|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 15 SP1|sles\_15\_sp1\_x64\_20G\_alibase\_20200717.vhd|2020-07-17|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 12 SP5|sles\_12\_sp5\_x64\_20G\_alibase\_20200717.vhd|2020-07-17|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 15 SP1|sles\_15\_sp1\_x64\_20G\_alibase\_20200617.vhd|2020-06-17|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 12 SP5|sles\_12\_sp5\_x64\_20G\_alibase\_20200617.vhd|2020-06-17|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 15 SP1|sles\_15\_sp1\_x64\_20G\_alibase\_20200520.vhd|2020-05-20|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 12 SP5|sles\_12\_sp5\_x64\_20G\_alibase\_20200520.vhd|2020-05-20|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 15 SP1|sles\_15\_sp1\_x64\_20G\_alibase\_20200426.vhd|2020-04-26|-   Enabled IPv6 by default.
-   Updated to include the latest patches. |
|SUSE Linux Enterprise Server 12 SP5|sles\_12\_sp5\_x64\_20G\_alibase\_20200426.vhd|2020-04-26|-   Enabled IPv6 by default.
-   Updated to include the latest patches. |
|SUSE Linux Enterprise Server 15 SP1|sles\_15\_sp1\_x64\_20G\_alibase\_20200329.vhd|2020-03-29|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 12 SP4|sles\_12\_sp4\_x64\_20G\_alibase\_20200319.vhd|2020-03-19|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 12 SP4|sles\_12\_sp4\_x64\_20G\_alibase\_20200227.vhd|2020-02-27|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 15 SP1|sles\_15\_sp1\_x64\_20G\_alibase\_20200218.vhd|2020-02-18|Updated to include the latest patches.|
|SUSE Linux Enterprise Server 15 SP1|sles\_15\_sp1\_x64\_20G\_alibase\_20200107.vhd|2020-01-07|New release.|

## Fedora CoreOS

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Fedora CoreOS 33.20210217.3.0\_3|fcos\_33.20210217.3.0\_3\_x86\_20G\_alibase\_20210331.vhd|2021-03-31|-   New release.
-   Kernel version: 5.10.12--200.fc33.x86\_64.
-   When you use this image, take note of the following items:
    -   When you create an instance or replace the system disk for an instance, you can use only a key pair as your logon credential. You can use only the key pair that you initially configured for your instance to log on to the instance. You cannot change or unbind the key pair.
    -   When you have created an instance or replaced the system disk for an instance, you cannot change the password for the instance. |

## Fedora

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Fedora 33 64-bit|fedora\_33\_0\_x64\_20G\_alibase\_20210318.vhd|2021-03-18|-   Kernel version: 5.11.7-200.fc33.x86\_64.
-   Changes:
    -   Updated to include the latest patches.
    -   Supported NVME drivers. |
|Fedora 33 64-bit|fedora\_33\_0\_x64\_20G\_alibase\_20210128.vhd|2021-01-28|-   New release.
-   Kernel version: 5.10.10-200.fc33.x86\_64.
-   Changes:
    -   Updated to include the latest patches.
    -   Fixed the CVE-2021-3156 vulnerability. |

## UEFI images

Unified Extensible Firmware Interface \(UEFI\) images are applicable only to ecs.g7, ecs.r7, ecs.c7, ecs.g7t, ecs.r7t, and ecs.c7t instance families.

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|CentOS 8.4|centos\_8\_4\_uefi\_x64\_20G\_alibase\_20210611.vhd|2021-06-11|New release.|
|CentOS 8.3|centos\_8\_3\_uefi\_x64\_20G\_alibase\_20210611.vhd|2021-06-11|New release.|
|Ubuntu 20.04|ubuntu\_20\_04\_uefi\_x64\_20G\_alibase\_20210609.vhd|2021-06-09|-   New release.
-   Applicable regions: China \(Beijing\), China \(Hangzhou\), China \(Shanghai\), China \(Chengdu\), China \(Hong Kong\), and Singapore \(Singapore\). |
|Ubuntu 18.04|ubuntu\_18\_04\_uefi\_x64\_20G\_alibase\_20210609.vhd|2021-06-09|-   New release.
-   Applicable regions: China \(Beijing\), China \(Hangzhou\), China \(Shanghai\), China \(Chengdu\), China \(Hong Kong\), and Singapore \(Singapore\). |

## Trusted images

Trusted images are applicable only to the following instance families and dedicated host types:

-   Instance families: ecs.g6t and ecs.c6t
-   Dedicated host types: ddh.g6t and ddh.c6t

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|CentOS 7.8|centos\_7\_8\_tpm\_x64\_20G\_alibase\_20200810.vhd|2020-08-10|-   New release.
-   Installed with GRUB 2 and TPM, to which the following RPM packages are related:
    -   grub2 \(trusted customized version\)
    -   tpm2-abrmd
    -   tpm2-tss
    -   tpm2-tools
-   GRUB 2 packages are trusted and customized. To enable trusted boot, we recommend that you do not upgrade GRUB 2 on your own. |

## AMD images

AMD images are applicable only to the ecs.ebmg6a, ecs.ebmc6a, and ecs.ebmr6a instance families.

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Debian 10.7|debian\_10\_7\_amd\_x64\_20G\_alibase\_20201231.vhd|2020-12-31|-   New release.
-   Applicable regions: China \(Qingdao\), China \(Beijing\), China \(Zhangjiakou\), China \(Hohhot\), China \(Chengdu\), Singapore \(Singapore\), and US \(Virginia\). |
|Ubuntu 20.04|ubuntu\_20\_04\_amd\_x64\_20G\_alibase\_20200820.vhd|2020-08-20|-   New release.
-   Applicable regions: China \(Beijing\), China \(Ulanqab\), China \(Shenzhen\), China \(Guangzhou\), Singapore \(Singapore\), China \(Hangzhou\), and China \(Chengdu\). |
|CentOS 7.8|centos\_7\_8\_amd\_x64\_20G\_alibase\_20200806.vhd|2020-08-06|-   New release.
-   Applicable regions: China \(Hangzhou\), China \(Shanghai\), China \(Beijing\), China \(Ulanqab\), and China \(Shenzhen\). |
|CentOS 8.2|centos\_8\_2\_amd\_x64\_20G\_alibase\_20200804.vhd|2020-08-04|-   New release.
-   Applicable regions: China \(Hangzhou\), China \(Shanghai\), China \(Beijing\), China \(Ulanqab\), and China \(Shenzhen\). |
|Ubuntu 18.04|ubuntu\_18\_04\_amd\_x64\_20G\_alibase\_20200804.vhd|2020-08-04|-   New release.
-   Applicable regions: China \(Beijing\), China \(Ulanqab\), China \(Shenzhen\), China \(Shanghai\), China \(Hangzhou\), and China \(Chengdu\). |

## Windows Server 2012

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20210516.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20210516.vhd

|2021-05-16|-   Updated to include the KB5003209 operating system patch released in May 2021.
-   Fixed the CVE-2020-24587, CVE-2021-31186, and CVE-2021-28479 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20210416.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20210416.vhd

|2021-04-16|-   Updated to include the KB5001382 and KB5001403 operating system patches released in April 2021.
-   Fixed the CVE-2021-28325 vulnerability. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20210316.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20210316.vhd

|2021-03-16|-   Updated to include the KB5000848 operating system patch released in March 2021.
-   Fixed the CVE-2021-26877 and CVE-2021-26897 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20210220.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20210220.vhd

|2021-02-20|-   Updated to include the KB4601384 and KB4601058 operating system patches released in February 2021.
-   Fixed the CVE-2021-24074, CVE-2021-24078, and CVE-2021-24086 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20210114.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20210114.vhd

|2021-01-14|-   Updated to include the KB4597253 and KB4598285 operating system patches released in January 2021.
-   Fixed the CVE-2021-1673, CVE-2021-1648, CVE-2021-1674, and CVE-2021-1665 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20201217.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20201217.vhd

|2020-12-17|-   Updated to include the KB4592484 operating system patch released in December 2020.
-   Fixed the CVE-2020-17096 and CVE-2020-16996 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20201120.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20201120.vhd

|2020-11-20|-   Updated to include the KB4586845, KB4585212, and KB4566425 operating system patches released in November 2020.
-   Fixed the CVE-2020-17051, CVE-2020-17087, and CVE-2020-17042 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20201015.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20201015.vhd

|2020-10-15|-   Updated to include the KB4580347 and KB4578976 operating system patches released in October 2020.
-   Fixed the CVE-2020-16911 and CVE-2020-16891 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20200914.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20200914.vhd

|2020-09-14|-   Updated to include the KB4577066, KB4576486, and KB4566425 operating system patches released in September 2020.
-   Fixed the CVE-2020-0718, CVE-2020-0922, CVE-2020-1319, CVE-2020-1285, CVE-2020-1508, CVE-2020-0836, CVE-2020-1012, and CVE-2020-0878 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20200814.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20200814.vhd

|2020-08-14|-   Updated to include the KB4571703 and KB4569753 operating system patches released in August 2020.
-   Fixed the CVE-2020-1472, CVE-2020-1464, CVE-2020-1554, CVE-2020-1509, CVE-2020-1567, and CVE-2020-1380 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20200723.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20200723.vhd

|2020-07-23|Updated to include the KB4566425, KB4565541, and KB4565635 operating system patches released in July 2020.|
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20200615.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20200615.vhd

|2020-06-15|-   Updated to include the KB4561666 operating system patch released in June 2020.
-   Fixed the CVE-2020-1301, CVE-2020-1239, CVE-2020-1300, CVE-2020-1281, and CVE-2020-1260 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20200516.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20200516.vhd

|2020-05-16|-   Updated to include the KB4556846 operating system patch released in May 2020.
-   Fixed the CVE-2020-1153, CVE-2020-1112, CVE-2020-1174, and CVE-2020-1062 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20200416.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20200416.vhd

|2020-04-16|-   Updated to include the KB4550961 operating system patch released in April 2020.
-   Added disk drives for Windows Recovery mode.
-   Fixed the CVE-2020-1020, CVE-2020-0687, CVE-2020-0938, CVE-2020-0965, and CVE-2020-0968 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20200314.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20200314.vhd

|2020-03-14|-   Updated to include the operating system patches released in March 2020.
-   Fixed the CVE-2020-0684, CVE-2020-0881, and CVE-2020-0787 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20200213.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20200213.vhd

|2020-02-13|-   Updated to include the operating system patches released in February 2020.
-   Fixed the CVE-2020-0738, CVE-2020-0689, CVE-2020-0681, CVE-2020-0683, CVE-2020-0686, CVE-2020-0674, and CVE-2020-0706 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win201202r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20200116.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20200116.vhd

|2020-01-16|-   Updated to include the operating system patches released in January 2020.
-   Fixed the CVE-2020-0609, CVE-2020-0625, CVE-2020-0611, and CVE-2020-0640 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_9600\_x64\_dtc\_zh-cn\_40G\_alibase\_20191218.vhd
-   English version: win2012r2\_9600\_x64\_dtc\_en-us\_40G\_alibase\_20191218.vhd

|2019-12-18|Updated to include the security patches released in December 2019.|
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_64\_dtc\_9600\_zh-cn\_40G\_alibase\_20191012.vhd
-   English version: win2012r2\_64\_dtc\_9600\_en-us\_40G\_alibase\_20191012.vhd

|2019-10-12|Updated to include the security patches released in October 2019.|
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_64\_dtc\_9600\_zh-cn\_40G\_alibase\_20190816.vhd
-   English version: win2012r2\_64\_dtc\_9600\_en-us\_40G\_alibase\_20190816.vhd

|2019-8-16|-   Updated to include the operating system patches released in August 2019.
-   Fixed the CVE-2019-1181 and CVE-2019-1182 vulnerabilities. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_64\_dtc\_9600\_zh-cn\_40G\_alibase\_20190718.vhd
-   English Edition: win2012r2\_64\_dtc\_9600\_en-us\_40G\_alibase\_20190718.vhd

|2019-7-18|-   Updated to include the operating system patches released in July 2019.
-   Upgraded .NET Framework to version 4.8. |
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_64\_dtc\_9600\_zh-cn\_40G\_alibase\_20190523.vhd
-   English version: win2012r2\_64\_dtc\_9600\_en-us\_40G\_alibase\_20190523.vhd

|2019-5-23|Updated to include the operating system patches released in May 2019.|
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_64\_dtc\_9600\_zh-cn\_40G\_alibase\_20190318.vhd
-   English version: win2012r2\_64\_dtc\_9600\_en-us\_40G\_alibase\_20190318.vhd

|2019-3-18|Updated to include the operating system patches released in March 2019.|
|Windows Server 2012 R2 Datacenter|-   Chinese version: win2012r2\_64\_dtc\_9600\_zh-cn\_40G\_alibase\_20181220.vhd
-   English version: win2012r2\_64\_dtc\_9600\_en-us\_40G\_alibase\_20181220.vhd

|2018-12-20|-   Updated to include the KB4471320 security patch released in December 2018. You must update Windows clients by using the latest patch to establish Remote Desktop Protocol \(RDP\) connections.
-   Upgraded .NET Framework to version 4.7.2.
-   Used the Sysprep tool to generalize the image. |

## Windows Server 2016

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20210516.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20210516.vhd

|2021-05-16|-   Updated to include the KB5003197 operating system patch released in May 2021.
-   Fixed the CVE-2020-24587, CVE-2021-31186, and CVE-2021-28479 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20210416.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20210416.vhd

|2021-04-16|-   Updated to include the KB5001347 and KB5001402 operating system patches released in April 2021.
-   Fixed the CVE-2021-28325 vulnerability. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20210316.vhd
-   Chinese version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20210316.vhd

|2021-03-16|-   Updated to include the KB5000803 operating system patch released in March 2021.
-   Fixed the CVE-2021-26877 and CVE-2021-26897 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20210220.vhd
-   Chinese version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20210220.vhd

|2021-02-20|-   Updated to include the KB5001078, KB4601318, and KB4601051 operating system patches released in February 2021.
-   Fixed the CVE-2021-24074, CVE-2021-24078, and CVE-2021-24086 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20210114.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20210114.vhd

|2021-01-14|-   Updated to include the KB4597247 and KB4598243 operating system patches released in January 2021.
-   Fixed the CVE-2021-1673, CVE-2021-1648, CVE-2021-1674, and CVE-2021-1665 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20201217.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20201217.vhd

|2020-12-17|-   Updated to include the KB4592440 operating system patch released in December 2020.
-   Fixed the CVE-2020-17096, CVE-2020-16996, and CVE-2020-17095 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20201120.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20201120.vhd

|2020-11-20|-   Updated to include the KB4586830, KB4585207, and KB4576750 operating system patches released in November 2020.
-   Fixed the CVE-2020-17051, CVE-2020-17087, CVE-2020-17042, and CVE-2020-17058 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20201015.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20201015.vhd

|2020-10-15|-   Updated to include the KB4580346 and KB4578969 operating system patches released in October 2020.
-   Fixed the CVE-2020-16911, CVE-2020-16891, CVE-2020-16909, and CVE-2020-16885 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20200914.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20200914.vhd

|2020-09-14|-   Updated to include the KB4577015, KB4576479, and KB4576750 operating system patches released in September 2020.
-   Fixed the CVE-2020-0718, CVE-2020-0922, CVE-2020-1319, CVE-2020-1285, CVE-2020-1508, CVE-2020-0836, CVE-2020-1012, CVE-2020-0878, CVE-2020-1129, and CVE-2020-0908 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20200814.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20200814.vhd

|2020-08-14|-   Updated to include the KB4571694 and KB4569746 operating system patches released in August 2020.
-   Fixed the CVE-2020-1472, CVE-2020-1464, CVE-2020-1554, CVE-2020-1509, CVE-2020-1567, and CVE-2020-1380 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20200723.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20200723.vhd

|2020-07-23|Updated to include the KB4565628, KB4486129, KB4565912, and KB4565511 operating system patches released in July 2020.|
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20200615.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20200615.vhd

|2020-06-15|-   Updated to include the KB4561616 operating system patch released in June 2020.
-   Fixed the CVE-2020-1301, CVE-2020-1239, CVE-2020-1300, CVE-2020-1281, and CVE-2020-1260 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20200516.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20200516.vhd

|2020-05-16|-   Updated to include the KB4556813 operating system patch released in May 2020.
-   Fixed the CVE-2020-1153, CVE-2020-1112, CVE-2020-1174, CVE-2020-1126, and CVE-2020-1062 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20200416.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20200416.vhd

|2020-04-16|-   Updated to include the KB4550929 and KB4550994 operating system patches released in April 2020.
-   Added disk drives for Windows Recovery mode.
-   Fixed the CVE-2020-1020, CVE-2020-0687, CVE-2020-0938, CVE-2020-0965, and CVE-2020-0968 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20200314.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20200314.vhd

|2020-03-14|-   Updated to include the operating system patches released in March 2020.
-   Fixed the CVE-2020-0684, CVE-2020-0801, CVE-2020-0881, and CVE-2020-0787 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20200213.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20200213.vhd

|2020-02-13|-   Updated to include the operating system patches released in February 2020.
-   Fixed the CVE-2020-0738, CVE-2020-0689, CVE-2020-0681, CVE-2020-0683, CVE-2020-0686, CVE-2020-0674, and CVE-2020-0706 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20200116.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20200116.vhd

|2020-01-16|-   Updated to include the operating system patches released in January 2020.
-   Fixed the CVE-2020-0609, CVE-2020-0601, CVE-2020-0625, CVE-2020-0611, and CVE-2020-0640 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_1607\_x64\_dtc\_zh-cn\_40G\_alibase\_20191220.vhd
-   English version: win2016\_1607\_x64\_dtc\_en-us\_40G\_alibase\_20191224.vhd

|2019-12-24|Updated to include the security patches released in December 2019.|
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_64\_dtc\_1607\_zh-cn\_40G\_alibase\_20191012.vhd
-   English version: win2016\_64\_dtc\_1607\_en-us\_40G\_alibase\_20191012.vhd

|2019-10-12|Updated to include the security patches released in October 2019.|
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_64\_dtc\_1607\_zh-cn\_40G\_alibase\_20190816.vhd
-   English version: win2016\_64\_dtc\_1607\_en-us\_40G\_alibase\_20190816.vhd

|2019-8-16|-   Updated to include the operating system patches released in August 2019.
-   Fixed the CVE-2019-1181 and CVE-2019-1182 vulnerabilities. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_64\_dtc\_1607\_zh-cn\_40G\_alibase\_20190718.vhd
-   English version: win2016\_64\_dtc\_1607\_en-us\_40G\_alibase\_20190718.vhd

|2019-7-18|-   Updated to include the operating system patches released in July 2019.
-   Upgraded .NET Framework to version 4.8. |
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_64\_dtc\_1607\_zh-cn\_40G\_alibase\_20190523.vhd
-   English version: win2016\_64\_dtc\_1607\_en-us\_40G\_alibase\_20190523.vhd

|2019-5-23|Updated to include the operating system patches released in May 2019.|
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_64\_dtc\_1607\_zh-cn\_40G\_alibase\_20190318.vhd
-   English version: win2016\_64\_dtc\_1607\_en-us\_40G\_alibase\_20190318.vhd

|2019-3-18|Updated to include the operating system patches released in March 2019.|
|Windows Server 2016 Datacenter|-   Chinese version: win2016\_64\_dtc\_1607\_zh-cn\_40G\_alibase\_20181220.vhd
-   English version: win2016\_64\_dtc\_1607\_en-us\_40G\_alibase\_20181220.vhd

|2018-12-20|-   Updated to include the KB4471321 security patch released in December 2018. You must update Windows clients by using the latest patch to establish RDP connections.
-   Upgraded .NET Framework to version 4.7.2.
-   Used the Sysprep tool to generalize the image. |

## Windows Server 2019

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20210516.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20210516.vhd

|2021-05-16|-   Updated to include the KB5003171 operating system patch released in May 2021.
-   Fixed the CVE-2020-24587, CVE-2021-31186, and CVE-2021-28479 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20210516.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20210516.vhd

|2021-05-16|-   Updated to include the KB5003171 operating system patch released in May 2021.
-   Fixed the CVE-2020-24587, CVE-2021-31186, and CVE-2021-28479 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20210416.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20210416.vhd

|2021-04-16|-   Updated to include the KB5001342 and KB5001404 operating system patches released in April 2021.
-   Fixed the CVE-2021-28325 and CVE-2021-28442 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20210416.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20210416.vhd

|2021-04-16|-   Updated to include the KB5001342 and KB5001404 operating system patches released in April 2021.
-   Fixed the CVE-2021-28325 and CVE-2021-28442 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20210316.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20210316.vhd

|2021-03-16|-   Updated to include the KB5000822 and KB5000859 operating system patches released in March 2021.
-   Fixed the CVE-2021-26877 and CVE-2021-26897 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20210316.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20210316.vhd

|2021-03-16|-   Updated to include the KB5000822 and KB5000859 operating system patches released in March 2021.
-   Fixed the CVE-2021-26877 and CVE-2021-26897 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20210220.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20210220.vhd

|2021-02-20|-   Updated to include the KB4601393, KB4601055, and KB4601383 operating system patches released in February 2021.
-   Fixed the CVE-2021-24074, CVE-2021-24078, and CVE-2021-24086 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20210220.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20210220.vhd

|2021-02-20|-   Updated to include the KB4601393, KB4601055, and KB4601383 operating system patches released in February 2021.
-   Fixed the CVE-2021-24074, CVE-2021-24078, and CVE-2021-24086 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20210114.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20210114.vhd

|2021-01-14|-   Updated to include the KB4586877, KB4598230, and KB4598480 operating system patches released in January 2021.
-   Fixed the CVE-2021-1673, CVE-2021-1648, CVE-2021-1674, and CVE-2021-1665 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20210114.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20210114.vhd

|2021-01-14|-   Updated to include the KB4586877, KB4598230, and KB4598480 operating system patches released in January 2021.
-   Fixed the CVE-2021-1673, CVE-2021-1648, CVE-2021-1674, and CVE-2021-1665 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20201217.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20201217.vhd

|2020-12-17|-   Updated to include the KB4592440 operating system patch released in December 2020.
-   Fixed the CVE-2020-17096, CVE-2020-16996, and CVE-2020-17095 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20201217.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20201217.vhd

|2020-12-17|-   Updated to include the KB4592440 operating system patch released in December 2020.
-   Fixed the CVE-2020-17096, CVE-2020-16996, and CVE-2020-17095 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20201120.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20201120.vhd

|2020-11-20|-   Updated to include the KB4586793, KB4580979, and KB4587735 operating system patches released in November 2020.
-   Fixed the CVE-2020-17051, CVE-2020-17087, CVE-2020-17042, and CVE-2020-17058 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20201120.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20201120.vhd

|2020-11-20|-   Updated to include the KB4586793, KB4580979, and KB4587735 operating system patches released in November 2020.
-   Fixed the CVE-2020-17051, CVE-2020-17087, CVE-2020-17042, and CVE-2020-17058 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20201015.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20201015.vhd

|2020-10-15|-   Updated to include the KB4577668, KB4577667, and KB4578973 operating system patches released in October 2020.
-   Fixed the CVE-2020-16911, CVE-2020-16891, CVE-2020-16909, CVE-2020-16885, and CVE-2020-16898 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20201015.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20201015.vhd

|2020-10-15|-   Updated to include the KB4577668, KB4577667, and KB4578973 operating system patches released in October 2020.
-   Fixed the CVE-2020-16911, CVE-2020-16891, CVE-2020-16909, CVE-2020-16885, and CVE-2020-16898 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200914.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200914.vhd

|2020-09-14|-   Updated to include the KB4570333, KB4576483, and KB4570332 operating system patches released in September 2020.
-   Fixed the CVE-2020-0718, CVE-2020-0922, CVE-2020-1319, CVE-2020-1285, CVE-2020-1508, CVE-2020-0836, CVE-2020-1012, CVE-2020-0878, CVE-2020-1129, and CVE-2020-0908 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20200914.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20200914.vhd

|2020-09-14|-   Updated to include the KB4570333, KB4576483, and KB4570332 operating system patches released in September 2020.
-   Fixed the CVE-2020-0718, CVE-2020-0922, CVE-2020-1319, CVE-2020-1285, CVE-2020-1508, CVE-2020-0836, CVE-2020-1012, CVE-2020-0878, CVE-2020-1129, and CVE-2020-0908 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200814.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200814.vhd

|2020-08-14|-   Updated to include the KB4565349, KB4566424, and KB4569750 operating system patches released in August 2020.
-   Fixed the CVE-2020-1472, CVE-2020-1464, CVE-2020-1554, CVE-2020-1509, CVE-2020-1567, and CVE-2020-1380 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20200814.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20200814.vhd

|2020-08-14|-   Updated to include the KB4565349, KB4566424, and KB4569750 operating system patches released in August 2020.
-   Fixed the CVE-2020-1472, CVE-2020-1464, CVE-2020-1554, CVE-2020-1509, CVE-2020-1567, and CVE-2020-1380 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200723.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200723.vhd

|2020-07-23|Updated to include the KB4558998, KB4558997, and KB4565632 operating system patches released in July 2020.|
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20200723.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20200723.vhd

|2020-07-23|Updated to include the KB4558998, KB4558997, and KB4565632 operating system patches released in July 2020.|
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200615.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200615.vhd

|2020-06-15|-   Updated to include the KB4561608 operating system patch released in June 2020.
-   Fixed the CVE-2020-1301, CVE-2020-1286, CVE-2020-1292, CVE-2020-1239, CVE-2020-1300, CVE-2020-1281, and CVE-2020-1260 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20200615.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20200615.vhd

|2020-06-15|-   Updated to include the KB4561608 operating system patch released in June 2020.
-   Fixed the CVE-2020-1301, CVE-2020-1286, CVE-2020-1292, CVE-2020-1239, CVE-2020-1300, CVE-2020-1281, and CVE-2020-1260 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200516.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200516.vhd

|2020-05-16|-   Updated to include the KB4551853 operating system patch released in May 2020.
-   Added the Docker runtime environment. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20200516.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20200516.vhd

|2020-05-16|-   Updated to include the KB4551853 operating system patch released in May 2020.
-   Fixed the CVE-2020-1153, CVE-2020-1112, CVE-2020-1174, CVE-2020-1126, CVE-2020-1118, and CVE-2020-1062 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200416.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200416.vhd

|2020-04-16|-   Updated to include the KB4549947 and KB4549949 operating system patches released in April 2020.
-   Added the Docker runtime environment.
-   Added disk drives for Windows Recovery mode.
-   Fixed the CVE-2020-1020, CVE-2020-0687, CVE-2020-0910, CVE-2020-0938, CVE-2020-0965, and CVE-2020-0968 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20200416.vhd
-   English version: none

|2020-04-16|-   Updated to include the KB4549947 and KB4549949 operating system patches released in April 2020.
-   Added disk drives for Windows Recovery mode.
-   Fixed the CVE-2020-1020, CVE-2020-0687, CVE-2020-0910, CVE-2020-0938, CVE-2020-0965, and CVE-2020-0968 vulnerabilities. |
|Windows Server 2019 Datacenter with Containers|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200314.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200314.vhd

|2020-03-14|-   Updated to include the operating system patches released in March 2020.
-   Added the Docker runtime environment.
-   Fixed the CVE-2020-0684, CVE-2020-0801, CVE-2020-0881, and CVE-2020-0787 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20200314.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20200314.vhd

|2020-03-14|-   Updated to include the operating system patches released in March 2020.
-   Fixed the CVE-2020-0684, CVE-2020-0801, CVE-2020-0881, and CVE-2020-0787 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alidocker\_20200225.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alidocker\_20200225.vhd

|2020-02-25|-   Updated to include the operating system patches released in February 2020.
-   Added the Docker runtime environment.
-   Fixed the CVE-2020-0738, CVE-2020-0689, CVE-2020-0681, CVE-2020-0683, CVE-2020-0686, CVE-2020-0674, and CVE-2020-0706 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20200213.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20200213.vhd

|2020-02-13|-   Updated to include the operating system patches released in February 2020.
-   Fixed the CVE-2020-0738, CVE-2020-0689, CVE-2020-0681, CVE-2020-0683, CVE-2020-0686, CVE-2020-0674, and CVE-2020-0706 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20200116.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20200116.vhd

|2020-01-16|-   Updated to include the operating system patches released in January 2020.
-   Fixed the CVE-2020-0609, CVE-2020-0601, CVE-2020-0625, CVE-2020-0611, and CVE-2020-0640 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_1809\_x64\_dtc\_zh-cn\_40G\_alibase\_20191220.vhd
-   English version: win2019\_1809\_x64\_dtc\_en-us\_40G\_alibase\_20191220.vhd

|2019-12-20|Updated to include the security patches released in December 2019.|
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_64\_dtc\_1809\_zh-cn\_40G\_alibase\_20191012.vhd
-   English version: win2019\_64\_dtc\_1809\_en-us\_40G\_alibase\_20191012.vhd

|2019-10-12|Updated to include the security patches released in October 2019.|
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_64\_dtc\_1809\_zh-cn\_40G\_alibase\_20190816.vhd
-   English version: win2019\_64\_dtc\_1809\_en-us\_40G\_alibase\_20190816.vhd

|2019-8-16|-   Updated to include the operating system patches released in August 2019.
-   Fixed the CVE-2019-1181 and CVE-2019-1182 vulnerabilities. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_64\_dtc\_1809\_zh-cn\_40G\_alibase\_20190718.vhd
-   English version: win2019\_64\_dtc\_1809\_en-us\_40G\_alibase\_20190718.vhd

|2019-7-18|-   Updated to include the operating system patches released in July 2019.
-   Upgraded .NET Framework to version 4.8. |
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_64\_dtc\_1809\_zh-cn\_40G\_alibase\_20190528.vhd
-   English version: win2019\_64\_dtc\_1809\_en-us\_40G\_alibase\_20190528.vhd

|2019-5-28|Updated to include the operating system patches released in May 2019.|
|Windows Server 2019 Datacenter|-   Chinese version: win2019\_64\_dtc\_1809\_zh-cn\_40G\_alibase\_20190318.vhd
-   English version: win2019\_64\_dtc\_1809\_en-us\_40G\_alibase\_20190318.vhd

|2019-3-18|New release.|

## Windows Server Version 1809

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Windows Server Version 1809 Datacenter|-   Chinese version: winsvr\_64\_dtcC\_1809\_zh-cn\_40G\_alibase\_20190528.vhd
-   English version: winsvr\_64\_dtcC\_1809\_en-us\_40G\_alibase\_20190528.vhd

|2019-5-28|Updated to include the operating system patches released in May 2019.|
|Windows Server Version 1809 Datacenter|-   Chinese version: winsvr\_64\_dtcC\_1809\_zh-cn\_40G\_alibase\_20190318.vhd
-   English version: winsvr\_64\_dtcC\_1809\_en-us\_40G\_alibase\_20190318.vhd

|2019-3-18|Updated to include the operating system patches released in March 2019.|
|Windows Server Version 1809 Datacenter|-   Chinese version: winsvr\_64\_dtcC\_1809\_zh-cn\_40G\_alibase\_20181222.vhd
-   English version: winsvr\_64\_dtcC\_1809\_en-us\_40G\_alibase\_20181222.vhd

|2018-12-22|-   Updated to include the KB4483235 patch released in December 2018.
-   Used the Sysprep tool to generalize the image. |

## Windows Server Version 1903

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Windows Server Version 1903 Datacenter|-   Chinese version: winsvr\_64\_dtcC\_1903\_zh-cn\_40G\_alibase\_20191012.vhd
-   English version: winsvr\_64\_dtcC\_1903\_en-us\_40G\_alibase\_20191012.vhd

|2019-10-12|Updated to include the security patches released in October 2019.|
|Windows Server Version 1903 Datacenter|-   Chinese version: winsvr\_64\_dtcC\_1903\_zh-cn\_40G\_alibase\_20190816.vhd
-   English version: winsvr\_64\_dtcC\_1903\_en-us\_40G\_alibase\_20190816.vhd

|2019-8-16|-   Updated to include the operating system patches released in August 2019.
-   Fixed the CVE-2019-1181 and CVE-2019-1182 vulnerabilities. |
|Windows Server Version 1903 Datacenter|-   Chinese version: winsvr\_64\_dtcC\_1903\_zh-cn\_40G\_alibase\_20190718.vhd
-   English version: winsvr\_64\_dtcC\_1903\_en-us\_40G\_alibase\_20190718.vhd

|2019-7-18|-   Updated to include the operating system patches released in July 2019.
-   Upgraded .NET Framework to version 4.8. |

## Windows Server Version 1909

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Windows Server Version 1909 Datacenter with Containers|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200723.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200723.vhd

|2020-07-23|Updated to include the KB4565483, KB4565554, and KB4565633 operating system patches released in July 2020.|
|Windows Server Version 1909 Datacenter|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_alibase\_20200723.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_alibase\_20200723.vhd

|2020-07-23|Updated to include the KB4565483, KB4565554, and KB4565633 operating system patches released in July 2020.|
|Windows Server Version 1909 Datacenter with Containers|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200615.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200615.vhd

|2020-06-15|-   Updated to include the KB4560960 operating system patch released in June 2020.
-   Fixed the CVE-2020-1301, CVE-2020-1286, CVE-2020-1292, CVE-2020-1248, CVE-2020-1239, CVE-2020-1300, and CVE-2020-1281 vulnerabilities. |
|Windows Server Version 1909 Datacenter|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_alibase\_20200615.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_alibase\_20200615.vhd

|2020-06-15|-   Updated to include the KB4560960 operating system patch released in June 2020.
-   Fixed the CVE-2020-1301, CVE-2020-1286, CVE-2020-1292, CVE-2020-1248, CVE-2020-1239, CVE-2020-1300, and CVE-2020-1281 vulnerabilities. |
|Windows Server Version 1909 Datacenter|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_alibase\_20200516.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_alibase\_20200516.vhd

|2020-05-16|-   Updated to include the KB4556799 operating system patch released in May 2020.
-   Fixed the CVE-2020-1153, CVE-2020-1112, CVE-2020-1174, CVE-2020-1126, and CVE-2020-1118 vulnerabilities. |
|Windows Server Version 1909 Datacenter with Containers|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200516.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200516.vhd

|2020-05-16|-   Updated to include the KB4556799 operating system patch released in May 2020.
-   Added the Docker runtime environment. |
|Windows Server Version 1909 Datacenter|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_alibase\_20200416.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_alibase\_20200416.vhd

|2020-04-16|-   Updated to include the KB4549951 and KB4552152 operating system patches released in April 2020.
-   Added disk drives for Windows Recovery mode.
-   Fixed the CVE-2020-1020, CVE-2020-0687, CVE-2020-0910, CVE-2020-0938, CVE-2020-0965, and CVE-2020-0968 vulnerabilities. |
|Windows Server Version 1909 Datacenter with Containers|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200416.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200416.vhd

|2020-04-16|-   Updated to include the KB4549951 and KB4552152 operating system patches released in April 2020.
-   Added the Docker runtime environment.
-   Added disk drives for Windows Recovery mode.
-   Fixed the CVE-2020-1020, CVE-2020-0687, CVE-2020-0910, CVE-2020-0938, CVE-2020-0965, and CVE-2020-0968 vulnerabilities. |
|Windows Server Version 1909 Datacenter|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_alibase\_20200315.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_alibase\_20200315.vhd

|2020-03-15|-   Updated to include the operating system patches released in March 2020.
-   Fixed the CVE-2020-0684, CVE-2020-0801, CVE-2020-0881, CVE-2020-0787, and CVE-2020-0796 vulnerabilities. |
|Windows Server Version 1909 Datacenter|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_alibase\_20200213.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_alibase\_20200213.vhd

|2020-02-13|-   Updated to include the operating system patches released in February 2020.
-   Fixed the CVE-2020-0738, CVE-2020-0689, CVE-2020-0681, CVE-2020-0683, CVE-2020-0686, CVE-2020-0674, and CVE-2020-0706 vulnerabilities. |
|Windows Server Version 1909 Datacenter|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_alibase\_20200116.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_alibase\_20200116.vhd

|2020-01-16|-   Updated to include the operating system patches released in January 2020.
-   Fixed the CVE-2020-0601, CVE-2020-0625, and CVE-2020-0611 vulnerabilities. |
|Windows Server Version 1909 Datacenter|-   Chinese version: wincore\_1909\_x64\_dtc\_zh-cn\_40G\_alibase\_20191219.vhd
-   English version: wincore\_1909\_x64\_dtc\_en-us\_40G\_alibase\_20191219.vhd

|2019-12-19|Updated to include the security patches released in December 2019.|

## Windows Server Version 2004

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Windows Server Version 2004 Datacenter with Containers|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20210516.vhd
-   English version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20210516.vhd

|2021-05-16|-   Updated to include the KB5003173 operating system patch released in May 2021.
-   Fixed the CVE-2020-24587, CVE-2021-31186, CVE-2021-28479, CVE-2021-31205, and CVE-2021-31166 vulnerabilities. |
|Windows Server Version 2004 Datacenter|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_alibase\_20210516.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_alibase\_20210516.vhd

|2021-05-16|-   Updated to include the KB5003173 operating system patch released in May 2021.
-   Fixed the CVE-2020-24587, CVE-2021-31186, CVE-2021-28479, CVE-2021-31205, and CVE-2021-31166 vulnerabilities. |
|Windows Server Version 2004 Datacenter with Containers|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20210416.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_container\_alibase\_20210416.vhd

|2021-04-16|-   Updated to include the KB5001330 operating system patch released in April 2021.
-   Fixed the CVE-2021-28325, CVE-2021-28324 and CVE-2021-28442 vulnerabilities. |
|Windows Server Version 2004 Datacenter|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_alibase\_20210416.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_alibase\_20210416.vhd

|2021-04-16|-   Updated to include the KB5001330 operating system patch released in April 2021.
-   Fixed the CVE-2021-28325, CVE-2021-28324 and CVE-2021-28442 vulnerabilities. |
|Windows Server Version 2004 Datacenter with Containers|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20210316.vhd
-   English version wincore\_2004\_x64\_dtc\_en-us\_40G\_container\_alibase\_20210316.vhd

|2021-03-16|-   Updated to include the KB5000802 operating system patch released in March 2021.
-   Fixed the CVE-2021-26877 and CVE-2021-26897 vulnerabilities. |
|Windows Server Version 2004 Datacenter|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_alibase\_20210316.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_alibase\_20210316.vhd

|2021-03-16|-   Updated to include the KB5000802 operating system patch released in March 2021.
-   Fixed the CVE-2021-26877 and CVE-2021-26897 vulnerabilities. |
|Windows Server Version 2004 Datacenter with Containers|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20210220.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_container\_alibase\_20210220.vhd

|2021-02-20|-   Updated to include the KB4601319 and KB4601050 operating system patches released in February 2021.
-   Fixed the CVE-2021-24074, CVE-2021-24078, and CVE-2021-24086 vulnerabilities. |
|Windows Server Version 2004 Datacenter|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_alibase\_20210220.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_alibase\_20210220.vhd

|2021-02-20|-   Updated to include the KB4601319 and KB4601050 operating system patches released in February 2021.
-   Fixed the CVE-2021-24074, CVE-2021-24078, and CVE-2021-24086 vulnerabilities. |
|Windows Server Version 2004 Datacenter with Containers|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20210114.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_container\_alibase\_20210114.vhd

|2021-01-14|-   Updated to include the KB4586876, KB4598242, and KB4598481 operating system patches released in January 2021.
-   Fixed the CVE-2021-1673, CVE-2021-1648, CVE-2021-1674, and CVE-2021-1665 vulnerabilities. |
|Windows Server Version 2004 Datacenter|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_alibase\_20210114.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_alibase\_20210114.vhd

|2021-01-14|-   Updated to include the KB4586876, KB4598242, and KB4598481 operating system patches released in January 2021.
-   Fixed the CVE-2021-1673, CVE-2021-1648, CVE-2021-1674, and CVE-2021-1665 vulnerabilities. |
|Windows Server Version 2004 Datacenter with Containers|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20201217.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_container\_alibase\_20201217.vhd

|2020-12-17|-   Updated to include the KB4592438 and KB4593175 operating system patches released in December 2020.
-   Fixed the CVE-2020-17096, CVE-2020-16996, and CVE-2020-17095 vulnerabilities. |
|Windows Server Version 2004 Datacenter|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_alibase\_20201217.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_alibase\_20201217.vhd

|2020-12-17|-   Updated to include the KB4592438 and KB4593175 operating system patches released in December 2020.
-   Fixed the CVE-2020-17096, CVE-2020-16996, and CVE-2020-17095 vulnerabilities. |
|Windows Server Version 2004 Datacenter with Containers|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20201120.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_container\_alibase\_20201120.vhd

|2020-11-20|-   Updated to include the KB4586781, KB4580419, and KB4586864 operating system patches released in November 2020.
-   Fixed the CVE-2020-17051, CVE-2020-17087, CVE-2020-17042, and CVE-2020-17058 vulnerabilities. |
|Windows Server Version 2004 Datacenter|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_alibase\_20201120.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_alibase\_20201120.vhd

|2020-11-20|-   Updated to include the KB4586781, KB4580419, and KB4586864 operating system patches released in November 2020.
-   Fixed the CVE-2020-17051, CVE-2020-17087, CVE-2020-17042, and CVE-2020-17058 vulnerabilities. |
|Windows Server Version 2004 Datacenter with Containers|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20201015.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_container\_alibase\_20201015.vhd

|2020-10-15|-   Updated to include the KB4579311 and KB4578968 operating system patches released in October 2020.
-   Fixed the CVE-2020-16911, CVE-2020-16891, CVE-2020-16909, CVE-2020-16885, and CVE-2020-16898 vulnerabilities. |
|Windows Server Version 2004 Datacenter|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_alibase\_20201015.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_alibase\_20201015.vhd

|2020-10-15|-   Updated to include the KB4579311 and KB4578968 operating system patches released in October 2020.
-   Fixed the CVE-2020-16911, CVE-2020-16891, CVE-2020-16909, CVE-2020-16885, and CVE-2020-16898 vulnerabilities. |
|Windows Server Version 2004 Datacenter with Containers|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200914.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200914.vhd

|2020-09-14|-   Updated to include the KB4571756, KB4576478, and KB4577266 operating system patches released in September 2020.
-   Fixed the CVE-2020-0718, CVE-2020-0922, CVE-2020-1319, CVE-2020-1285, CVE-2020-1508, CVE-2020-0836, CVE-2020-1012, CVE-2020-0878, CVE-2020-1129, and CVE-2020-0908 vulnerabilities. |
|Windows Server Version 2004 Datacenter|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_alibase\_20200914.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_alibase\_20200914.vhd

|2020-09-14|-   Updated to include the KB4571756, KB4576478, and KB4577266 operating system patches released in September 2020.
-   Fixed the CVE-2020-0718, CVE-2020-0922, CVE-2020-1319, CVE-2020-1285, CVE-2020-1508, CVE-2020-0836, CVE-2020-1012, CVE-2020-0878, CVE-2020-1129, and CVE-2020-0908 vulnerabilities. |
|Windows Server Version 2004 Datacenter with Containers|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_container\_alibase\_20200814.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_container\_alibase\_20200814.vhd

|2020-08-14|-   Updated to include the KB4566782, KB4570334, and KB4569745 operating system patches released in August 2020.
-   Fixed the CVE-2020-1472, CVE-2020-1464, CVE-2020-1554, CVE-2020-1509, CVE-2020-1567, and CVE-2020-1380 vulnerabilities. |
|Windows Server Version 2004 Datacenter|-   Chinese version: wincore\_2004\_x64\_dtc\_zh-cn\_40G\_alibase\_20200814.vhd
-   English version: wincore\_2004\_x64\_dtc\_en-us\_40G\_alibase\_20200814.vhd

|2020-08-14|-   Updated to include the KB4566782, KB4570334, and KB4569745 operating system patches released in August 2020.
-   Fixed the CVE-2020-1472, CVE-2020-1464, CVE-2020-1554, CVE-2020-1509, CVE-2020-1567, and CVE-2020-1380 vulnerabilities. |

## Windows Server 2008

**Note:** On January 14, 2020, Microsoft stopped providing support for Windows Server 2008 and Windows Server 2008 R2 operating systems. In light of this, Alibaba Cloud no longer provides technical support for ECS instances that use these operating systems. If you have ECS instances that use these operating systems, upgrade them to Windows Server 2012 or later at your earliest opportunity.

|Release|Image ID|Release date|Description|
|:------|--------|------------|:----------|
|Windows Server 2008 R2 Enterprise|-   Chinese version: win2008r2\_sp1\_x64\_ent\_zh-cn\_40G\_alibase\_20200116.vhd
-   English version: win2008r2\_sp1\_x64\_ent\_en-us\_40G\_alibase\_20200116.vhd

|2020-01-16|-   Updated to include the operating system patches released in January 2020.
-   Fixed the CVE-2020-0625, CVE-2020-0611, and CVE-2020-0640 vulnerabilities. |
|Windows Server 2008 R2 Enterprise|-   Chinese version: win2008r2\_sp1\_x64\_ent\_zh-cn\_40G\_alibase\_20191218.vhd
-   English version: win2008r2\_sp1\_x64\_ent\_en-us\_40G\_alibase\_20191220.vhd

|2019-12-20|Updated to include the security patches released in December 2019.|
|Windows Server 2008 R2 Enterprise|-   Chinese version: win2008r2\_64\_ent\_sp1\_zh-cn\_40G\_alibase\_20191012.vhd
-   English version: win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20191012.vhd

|2019-10-12|Updated to include the security patches released in October 2019.|
|Windows Server 2008 R2 Enterprise|-   Chinese version: win2008r2\_64\_ent\_sp1\_zh-cn\_40G\_alibase\_20190816.vhd
-   English version: win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20190816.vhd

|2019-8-16|-   Updated to include the operating system patches released in August 2019.
-   Fixed the CVE-2019-1181 and CVE-2019-1182 vulnerabilities. |
|Windows Server 2008 R2 Enterprise|-   Chinese version: win2008r2\_64\_ent\_sp1\_zh-cn\_40G\_alibase\_20190816.vhd
-   English version: win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20190816.vhd

|2019-8-16|-   Updated to include the operating system patches released in August 2019.
-   Fixed the CVE-2019-1181 and CVE-2019-1182 vulnerabilities. |
|Windows Server 2008 R2 Enterprise|-   Chinese version: win2008r2\_64\_ent\_sp1\_zh-cn\_40G\_alibase\_20190718.vhd
-   English version: win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20190718.vhd

|2019-7-18|-   Updated to include the operating system patches released in July 2019.
-   Upgraded .NET Framework to version 4.8. |
|Windows Server 2008 Standard Edition SP2|-   Chinese version: win2008\_32\_std\_sp2\_zh-cn\_40G\_alibase\_20190517.vhd
-   English version: none

|2019-5-17|-   Updated to include the operating system patches released in May 2019.
-   Fixed the CVE-2019-0708 remote code execution vulnerability in Microsoft Windows Remote Desktop Services. |
|Windows Server 2008 R2 Enterprise|-   Chinese version: win2008r2\_64\_ent\_sp1\_zh-cn\_40G\_alibase\_20190515.vhd
-   English version: win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20190515.vhd

|2019-5-15|-   Updated to include the operating system patches released in May 2019.
-   Fixed the CVE-2019-0708 remote code execution vulnerability in Microsoft Windows Remote Desktop Services. |
|Windows Server 2008 R2 Enterprise|-   Chinese version: win2008r2\_64\_ent\_sp1\_zh-cn\_40G\_alibase\_20190318.vhd
-   English version: win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20190318.vhd

|2019-3-18|Updated to include the operating system patches released in March 2019.|
|Windows Server 2008 R2 Enterprise|-   Chinese version: win2008r2\_64\_ent\_sp1\_zh-cn\_40G\_alibase\_20181220.vhd
-   English version: none

|2018-12-20|-   Updated to include the KB4471318 security patch released in December 2018. You must update Windows clients by using the latest patch to establish RDP connections.
-   Upgraded .NET Framework to version 4.7.2.
-   Used the Sysprep tool to generalize the image. |

