# Quick start

This topic describes methods of how to build websites on ECS instances.

## Procedure

1.  Select an ECS instance.

    Different types of websites have different requirements on instance configurations. Select an appropriate instance based on the website size and the number of potential visitors. Typically, you can select instances that have basic configurations for small websites. We recommend that you select an instance in the same way as you purchase an instance. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

    The following table lists recommended instance types and disks.

    |Parameter|Recommendation|
    |---------|--------------|
    |Instance type|    -   The instance types in the s6 shared standard and t6 burstable instance families. These instance types are cost-effective and able to meet basic requirements on website building.
    -   The instance types in the c6 compute optimized and g6 general purpose instance families. These instance types are high-performance and applicable to website building scenarios that rely on the instance performance.
For more information about how to select instance families and instance types, see [Instance families](/intl.en-US/Instance/Instance families.md) and [Best practices for instance type selection](/intl.en-US/Best Practices/Best practices for instance type selection.md).

You can upgrade or downgrade an instance based on your actual needs. For more information, see [Instance families that support instance type changes](/intl.en-US/Instance/Change configurations/Change instance types/Instance families that support instance type changes.md). |
    |Disk|    -   PL0 enhanced SSDs \(ESSDs\): ultra-high performance and based on the next-generation distributed Elastic Block Storage \(EBS\) architecture. For more information, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).
    -   Ultra disks: cost-effective, medium random IOPS, and high data reliability.
For more information about the performance metrics and specifications of disks, see [EBS performance](/intl.en-US/Block Storage/Performance/EBS performance.md). |

    ECS supports the subscription and pay-as-you-go billing methods. For more information, see [Billing overview](/intl.en-US/Pricing/Billing overview.md). Price varies based on the selected configurations. For more information, see [Pricing of ECS](https://www.alibabacloud.com/product/ecs?tab=pricing).

2.  Configure security group rules.

    By default, port 22 and port 3389 that are required to connect to an instance are enabled when you create a security group. For this step, you must make sure that these ports are enabled to allow inbound traffic. If the ports are not enabled, manually configure security group rules to allow inbound traffic on these ports. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

3.  Deploy a website.

    Select a method to deploy your website. For more information, see [Summary of website building methods](/intl.en-US/Tutorials/Summary of website building methods.md).

4.  Purchase a domain name.

    Enter the domain name that you want to purchase. If the domain name is not in use, you can purchase it. For more information, see [Register a generic domain name](/intl.en-US/Quick Start/Register a generic domain name.md).

    For differences between the .com and .net suffixes, see [Domain name differences](/intl.en-US/FAQ/Concepts/Domain name differences.md).

5.  Apply for an Internet Content Provider \(ICP\) filing for the domain name.

    **Note:** If the instance that hosts your website is located in a region within mainland China, you must apply for an ICP filing for your domain name. Otherwise, you can skip this step.

    1.  Prepare for the ICP filing.

        For more information about ICP filing regulations, see [ICP filing regulations of MIIT in different regions](). For more information, see [Overview]().

    2.  Apply for an ICP filing.
6.  Resolve the domain name.

    You can resolve your domain name in Alibaba Cloud DNS. For more information, see [Configure domain name resolution](https://www.alibabacloud.com/help/faq-detail/58131.htm). After you configure the domain name resolution, users can visit your website by using the configured domain name.

    To map the domain name to an IP address, add an A record. For more information, see [Record types](https://www.alibabacloud.com/help/faq-detail/58077.htm).


Now you have built a website on your own. You can visit the website and test its service by using the domain name.

## FAQ

The following section provides answers to commonly asked questions about using ECS instances or building websites:

Security groups and snapshots

-   [Scenarios for security groups](/intl.en-US/Security/Security groups/Scenarios for security groups.md)
-   [Roll back a disk by using a snapshot](/intl.en-US/Snapshots/Use snapshots/Roll back a disk by using a snapshot.md)

Failure to visit a website that you have built

-   [What are the common causes and solutions of failures occurring when I attempt to visit my website?](https://www.alibabacloud.com/help/faq-detail/31710.htm?spm=a2c63.q38357.a3.1.68994b4dAUyfoq)
-   [How do I test the connection when the ping result shows packet loss or when the ping operation has failed?](https://www.alibabacloud.com/help/faq-detail/40573.htm)

## References

-   For information about how to select Alibaba Cloud services and configurations based on your business needs, see [Architecture Consulting Service](https://www.alibabacloud.com/services/consulting/architecture?spm=a2796.208404.1107812.2.8e1068ae2GDLmg).
-   If you want to migrate your business from a data center or a hosted data center to Alibaba Cloud, you can request technical support from Alibaba Cloud for cloud migration. For more information, see [Cloud Migration Service](https://www.alibabacloud.com/services/cloudmigration?spm=a2796.208404.1107812.6.8e1068ae2GDLmg).

