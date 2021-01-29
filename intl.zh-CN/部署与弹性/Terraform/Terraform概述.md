# Terraform概述

Terraform是一个开源工具，帮助您在阿里云安全高效地预配和管理云基础结构。

## 什么是Terraform

HashiCorp Terraform是一个IT基础架构自动化编排工具，可以用代码来管理维护IT资源。它编写了描述云资源拓扑的配置文件中的基础结构，例如虚拟机、存储账户和网络接口。Terraform的命令行接口（Command Line Interface，CLI）提供一种简单机制，用于将配置文件部署到阿里云或其他任意支持的云上，并对其进行版本控制。更多信息，请参见[HashiCorp Terraform](https://www.terraform.io/)。

同时，Terraform是一个高度可扩展的工具，通过Provider来支持新的基础架构。您可以使用Terraform来创建、修改、删除ECS、VPC、RDS、SLB等多种资源。

## 功能优势

-   将基础结构部署到多个云

    Terraform适用于多云方案，将相类似的基础结构部署到阿里云、其他云提供商或者本地数据中心。开发人员能够使用相同的工具和相似的配置文件同时管理不同云提供商的资源。

-   自动化管理基础结构

    Terraform能够创建配置文件的模板，以可重复、可预测的方式定义和预配ECS资源，减少人为因素导致的部署和管理错误。能够多次部署同一模板，创建相同的开发、测试和生产环境。

-   基础架构即代码（Infrastructure as Code）

    可以用代码来管理维护资源。允许保存基础设施状态，从而使您能够跟踪对系统（基础设施即代码）中不同组件所做的更改，并与其他人共享这些配置。

-   降低开发成本

    您通过按需创建开发和部署环境来降低成本。并且，您可以在系统更改之前进行评估。


## 应用场景

Terraform的应用场景，请参见[Terraform详情页](https://www.alibabacloud.com/solutions/devops/terraform)。

## 使用Terraform

Terraform能够让您在阿里云上轻松使用简单模板语言来定义、预览和部署云基础结构。更多信息，请参见 [简单模板语言](https://www.terraform.io/docs/configuration/syntax.html)。以下为Terraform在ECS中预配资源的必要步骤：

1.  安装并配置Terraform。具体操作，请参见[安装和配置Terraform](/intl.zh-CN/部署与弹性/Terraform/安装和配置Terraform.md)。
2.  使用Terraform创建一台或多台ECS实例。具体操作，请参见[创建一台ECS实例]()和[创建多台ECS实例]()。
3.  （可选）使用Terraform部署Web集群。具体操作，请参见[部署Web集群](/intl.zh-CN/部署与弹性/Terraform/部署Web集群.md)。

更多关于Terraform的使用教程，请参见[Terraform文档](https://help.aliyun.com/product/95817.html)。

## 更多信息

-   [Terraform Alibaba provider](https://www.terraform.io/docs/providers/alicloud/index.html)
-   [Terrafrom Alibaba github](https://github.com/alibaba/terraform-provider)
-   [Terraform Registry Alibaba Modules](https://registry.terraform.io/browse?provider=alicloud)

