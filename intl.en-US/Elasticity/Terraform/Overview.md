# Overview

Terraform is an open source tool that you can use to provision and manage your cloud infrastructure in Alibaba Cloud.

## Introduction

HashiCorp Terraform is a tool for automated IT infrastructure orchestration. HashiCorp Terraform can use code to manage and maintain IT resources. HashiCorp Terraform provides code for infrastructure resources such as VMs, storage accounts, and network interfaces defined in the configuration files that describe the cloud resource topology. The command line interface \(CLI\) of Terraform provides a simple mechanism to deploy configuration files to Alibaba Cloud or other clouds and control the versions of the configuration files. For more information, visit [HashiCorp Terraform](https://www.terraform.io/).

Terraform is a scalable tool that relies on plug-ins called "providers" to support new infrastructure. You can use Terraform to create, modify, and delete cloud resources, such as ECS instances, VPCs, ApsaraDB RDS instances, and SLB instances.

## Benefits

-   Multi-cloud infrastructure deployment

    Terraform is suitable for multi-cloud scenarios, in which similar infrastructure is deployed to Alibaba Cloud, clouds of other providers, or data centers. Terraform allows developers to use identical tools and similar configuration files to manage infrastructure resources that are built on clouds of different providers.

-   Automated infrastructure management

    Terraform can create configuration file templates to define and provision ECS resources in a repeatable and predictable manner. This reduces human errors during deployment and management. Terraform can deploy the same template multiple times to create identical development, test, and production environments.

-   Infrastructure as code

    In Terraform, you can use code to manage and maintain resources. Terraform stores its own copy of the current state of your infrastructure. This way, you can track changes made to components in the system \(infrastructure as code\) and share infrastructure configurations with other users.

-   Reduced development costs

    You can use Terraform to create development and deployment environments based on your needs to reduce costs. In addition, you can evaluate development costs before you make changes to the system.


## Scenarios

For information about the scenarios of Terraform, see [Terraform details page](https://www.alibabacloud.com/solutions/devops/terraform).

## Use of Terraform

Terraform allows you to use a simple template language to define, preview, and deploy cloud infrastructure in Alibaba Cloud. For more information, visit [Terraform language](https://www.terraform.io/docs/configuration/syntax.html). Before you use Terraform to provision resources in ECS, complete the following steps:

1.  Install and configure Terraform. For more information, see [Install and configure Terraform](/intl.en-US/Elasticity/Terraform/Install and configure Terraform.md).
2.  Use Terraform to create one or more ECS instances. For more information, see [Create an ECS instance]() and [Create multiple ECS instances]().
3.  Optional. Use Terraform to deploy a web cluster. For more information, see [Deploy a web cluster](/intl.en-US/Elasticity/Terraform/Deploy a web cluster.md).

For more information about how to use Terraform, visit [Documents on Terraform](https://help.aliyun.com/product/95817.html).

## References

-   [Terraform Alibaba provider](https://www.terraform.io/docs/providers/alicloud/index.html)
-   [Terrafrom Alibaba github](https://github.com/alibaba/terraform-provider)
-   [Terraform Registry Alibaba Modules](https://registry.terraform.io/browse?provider=alicloud)

