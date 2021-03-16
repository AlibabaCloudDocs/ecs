# Best practices for cost management

This topic describes the cost components and benefits of ECS and the recommended cost management solutions. These solutions can maximize cost effectiveness while ensuring rapid business development.

## Cost components

The cost of using ECS consists of the following components:

-   Ownership cost: the costs of resources and resource plans.
-   O&M cost: the labor costs incurred when you use ECS.

![Cost components of ECS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6904488951/p86306.png)

## Cost benefits of data migration to cloud

To build an Internet data center \(IDC\), you must consider direct costs such as hardware, network, electricity, and O&M. You must also consider scaling costs from upgrades and capacity increase, and the risk costs from the implementation of data backup and high availability. When you scale out your IDC to meet business needs, the unit cost of resources increases, and the IDC becomes more complex while the fault tolerance of the IDC decreases. Additional costs occur if you select improper models.

Compared with operating your own IDCs, cloud resources do not require investments such as hardware, physical environments, and labors. The unit cost of cloud resources is relatively linear and all resources allow on-demand access and delivery. Cloud resources also support multiple billing methods to further optimize costs.

## Cost optimization suggestions

We recommend that you manage ECS costs from the following aspects:

-   [Classify costs](#section_wpf_36j_l9m)
-   [Optimize resources](#section_omh_7fk_5vu)
-   [Upgrade instance families](#section_y21_qer_zzz)
-   [Regular cost saving measures](#section_tt0_yel_0fs)
-   [Implement automated O&M](#section_xkf_kuw_xxe)

## Classify costs

In the ECS console, choose Billing \> User Center from the top navigation bar. Then you can view your bills to learn about consumption details, track costs, and determine what needs to be optimized.

1.  In the ECS console, choose Billing \> User Center from the top navigation bar. On the Bills page, click the Overview tab. You can view the cost trend of your account and the cost distribution by product to learn the overall consumption status.
2.  Use resource groups and tags to categorize resources by business, department, and project and calculate corresponding costs.
3.  On the Bills page, click the Details tab to view resource consumption details. You can manage costs of various resource types in a more fine-grained manner based on resource groups and tags configured.

For example, you can create tags `department:R&D`, `department:Finance`, and `department:IT`, and bind these tags to your ECS instances. When you view bill details, you can filter the departments by tag and view resources consumed by each department to determine which departments need to optimize their costs.

## Optimize resources

If you find resources with high costs, you can monitor the resources from multiple aspects, determine the reasons for the high costs, and then take targeted optimization measures.

1.  Monitor resource usage.
    1.  Monitor the usage of resources such as CPU, memory, disks, and bandwidth. Assess whether the current configuration is higher than required.
    2.  Monitor idle resources to avoid waste. Idle resources include instances that are upgraded but not restarted, reserved instances that do not match pay-as-you-go instances, disks that are not attached to instances, and EIPs that are not associated with instances.
    3.  Monitor resource usage periods. If you use resources such as pay-as-you-go instances and disks for an extended period of time, we recommend that you use subscription resources or resource plans to reduce cost.
    4.  Monitor the lifecycle of resources. Pay attention to the expiration dates of subscription resources such as subscription instances, reserved instances, and storage capacity units. Renew the resources in a timely manner.
2.  Select appropriate instance types.

    Instance types have significant impacts on ECS costs. You need to select the most cost-effective instance type and adjust the instance quantity based on business scenarios. This way, you can maximize resource utilization and reduce costs while meeting business needs.

    For example, you are using 60 d1ne.14xlarge instances for short videos. The instance monitoring result shows that the memory usage is reasonable but the CPU utilization is relatively low. The specifications of instance families show that the CPU-to-memory ratio is 1:4 for d1ne and 1:5.5 for d2.

    To reduce the CPU-to-memory ratio to increase CPU utilization, you can use 85 d2s.8xlarge instances to replace 60 d1ne.14xlarge instances. The instance type is downgraded from 14xlarge to 8xlarge, reducing costs by about 23%.

    For more information about instance configurations, see [Best practices for instance type selection](/intl.en-US/Best Practices/Best practices for instance type selection.md).

3.  Combine multiple billing methods.

    Different types of business have different requirements for the resource usage cycle. Select an appropriate billing method for each type of business and combine billing methods to optimize costs.

    -   Subscription and reserved instances are used for stable business workloads.
    -   Pay-as-you-go instances are used for stateful and dynamic business workloads.
    -   Preemptible instances are used for stateless and fault-tolerant business workloads.
4.  Use dedicated hosts to reuse ECS instance resources.

    For scenarios that have minimal requirements for CPU stability, such as development and test environments, you can use CPU overprovisioned dedicated hosts to deploy more ECS instances of the same specifications and reduce the unit deployment cost.

    Stopped ECS instances that are deployed on dedicated hosts do not occupy resources. Therefore, you can stop some ECS instances during off-peak hours of the production environment. Then you can use other resources in the production environment to run test tasks whose periods are predictable, such as offline computing and automated tests.


## Upgrade instance families

Hardware such as processors is continuously updated to improve performance while reducing costs. ECS is also updated to provide you with more cost-effective services.

Later instance types are more cost-effective than earlier instance types. For example, the following table describes the difference between g5.2xlarge and g6.2xlarge in performance and price.

|Performance|Price|
|-----------|-----|
|-   The integer computing performance is improved by 40%.
-   The floating-point computing performance is improved by 30%.
-   The memory bandwidth is increased by 15%.
-   The memory idle latency is decreased by 40%.
-   The internal bandwidth is increased by 220%.

|-   The cost of annual subscription ECS resources is reduced by 6%.
-   The cost of pay-as-you-go ECS resources is reduced by 43%. |

To ensure that you can use the next-generation instance types in time, we recommend that you:

-   Design robust applications that can run on different instance types.
-   Assess whether to upgrade instance types based on the updates in the official website of Alibaba Cloud.

Examples of instance family upgrade

By using the following upgrade scheme, you can improve business performance while ensuring same CPU and memory configurations and save at least 15% of instance costs.

|Current instance families|Preferred target instance family|Alternative target instance family|
|-------------------------|--------------------------------|----------------------------------|
|sn1 and sn2|-   c6
-   g6
-   r6

|-   c5 and sn1ne
-   g5 and sn2ne
-   r5 and se1ne |
|c4|hfc6 and c6|hfc5 and c5|
|ce4|r6|r5 and se1ne|
|cm4|hfc6|hfc5 and g5|
|n1, n2, and e3|-   c6
-   g6
-   r6

|-   c5 and sn1ne
-   g5 and sn2ne
-   r5 and se1ne |
|-   t1
-   s1, s2, and s3
-   m1 and m2
-   c1 and c2

|-   c6
-   g6
-   r6

|-   c5 and sn1ne
-   g5 and sn2ne
-   r5 and se1ne |

## Regular cost saving measures

Cloud resources are on-demand and save you the investment and cost of operating your own IDC. However, you need to constantly optimize costs in your daily work to obtain the ideal results. You can refine the following typical operations to make a practical scheme.

-   Hold regular cost meetings. Review budget implementation with cost-related parties such as finance and R&D teams, evaluate optimization results, and improve optimization strategies on a regular basis.
-   Enforce the use of tags. Mark resources with tags of business, environment, and owners to track daily costs.
-   Classify resources and select appropriate usage methods. For example, pay-as-you-go instances are preferred for the deployment of the development and testing environments for short-term projects, and the instances are released in a timely manner after the projects are complete.
-   Avoid idle resources. Check resource usage on a regular basis and determine the notification and disposal workflows of idle resources.
-   Renew resources in a timely manner. Apply for a budget for subscription resources in advance to avoid the additional cost of purchasing and deploying new resources after existing resources are released upon expiration.

## Implement automated O&M

Alibaba Cloud provides a variety of O&M services to help you improve O&M efficiency and reduce O&M labor costs. For example:

-   [Auto Scaling](/intl.en-US/Product Introduction/What is Auto Scaling?.md): constantly maintains instance clusters of different billing methods and instance types in different zones. This service is ideal for the scenarios where business workloads fluctuate from time to time.
-   [Auto Provisioning](/intl.en-US/Elasticity/Manage auto provisioning groups/Auto Provisioning overview.md): quickly deploys instance clusters of different billing methods and instance types in different zones. This service is ideal for the scenarios where stable computing power needs to be provisioned quickly and preemptible instances are needed to reduce costs.
-   [Operation Orchestration Service](https://help.aliyun.com/document_detail/120556.html)[Operation Orchestration Service](https://www.alibabacloud.com/help/doc-detail/120556.htm): defines a series of O&M operations in a template to efficiently perform O&M tasks. This service is ideal for the scenarios where event-driven O&M, scheduled O&M, batch O&M, or cross-region O&M is needed.
-   [Resource Orchestration Service](/intl.en-US/Product Introduction/What is ROS?.md): Deploys and maintains stacks that contain multiple cloud resources and dependencies. This service is ideal for the scenarios where delivery of an integrated system or environment clone is required.

