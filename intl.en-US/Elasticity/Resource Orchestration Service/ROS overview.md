---
keyword: [ROS template, IaC, stack, DevOps, ]
---

# ROS overview

Resource Orchestration Service \(ROS\) is a service provided by Alibaba Cloud to simplify the management of cloud computing resources. The ROS engine automatically creates and configures all resources in a stack based on a template, making automatic delivery of ECS and ApsaraDB for RDS instances possible.

For more information, see [What is ROS?](/intl.en-US/Product Introduction/What is ROS?.md)

## Features

-   Repeated deployment

    You can use the same template to deploy resources in the development, test, or production environment by specifying different values for parameters. For example, you can set the number of ECS instances in the test environment to 2 and the number of ECS instances in the production environment to 20. You can also use the same template to deploy resources in multiple regions. This improves the efficiency of multi-region deployment.

-   Standardized deployment

    In practice, subtle differences in different environments often lead to complicated management, high costs, and prolonged troubleshooting time. By using ROS for repeated deployment, you can standardize deployment environments, minimize the differences between environments, and integrate environment configurations into templates.

-   Fully managed automation

    You do not need to purchase or maintain the resources that are used to execute templates. You only need to focus on the resources required by your business and the template specifications. If you want to create multiple projects that are distributed across multiple stacks, the fully managed automation service allows you to create tasks faster.

-   Authentication and audit

    ROS is integrated with Resource Access Management \(RAM\) to provide unified authentication. This eliminates the need to establish user authentication and permission systems. You can use ActionTrail to review all O&M operations of Alibaba Cloud services, including operations on ROS.


## Benefits

-   Infrastructure as Code

    ROS is an Infrastructure as Code \(IaC\) solution provided by Alibaba Cloud to quickly implement IaC as a key component of DevOps.

-   Efficiency improvement

    ROS provides solution templates to reduce nearly 90% of deployment time for complex solutions such as SAP deployment. You can also use templates to implement repeated deployment in a standardized manner to improve efficiency.

-   Architecture optimization

    ROS supports one-click deployment of classic cloud migration solutions, which simplifies the cloud migration process and optimizes cloud architecture.

-   Internal compliance control

    ROS templates can be used to deploy a predefined cloud environment, which simplifies financial and IT compliance audits.

-   Cost-effectiveness

    The preconfigured ROS templates can be used to deploy or release applications and cloud environments on a regular basis to implement on-demand usage and pay-as-you-go billing.


## Usage

You can create a stack template in the ROS console or by calling API operations. Then, you can use the template to quickly create and manage resources. For more information, see the following topics in the *ROS documentation*:

-   [Template structure](/intl.en-US/Template/Template syntax/Template structure.md)
-   [t23186.md\#](/intl.en-US/Stack Management/Create a stack.md)
-   [List of operations by function](/intl.en-US/API Reference/List of operations by function.md)

You can also perform the following operations:

-   Uses Git or Subversion \(SVN\) to manage template versions and then calls ROS API operations to maintain stacks.
-   Uses Alibaba Cloud command-line interface \(CLI\) to create stacks. For more information, see [Stack operations](/intl.en-US/Common Tools/Command line tools/Alibaba Cloud CLI/API operation examples/Stack operations.md).

