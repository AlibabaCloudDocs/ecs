# ECS实例交付（创建）方式

云服务器ECS提供单台交付、批量交付、高可用部署、自动化创建集群等多种ECS实例交付（创建）方式，支持控制台操作和API调用，满足您在不同场景下的ECS实例创建需求。

## 手动创建单台或多台实例

适用场景：批量创建具有相同实例规格、可用区、付费模式等配置的ECS实例。

创建方式：

-   使用控制台：
    -   [使用向导创建实例](/intl.zh-CN/实例/创建实例/使用向导创建实例.md)

        在向导页面选择配置，可视化界面，操作简单。

    -   [使用自定义镜像创建实例](/intl.zh-CN/实例/创建实例/使用自定义镜像创建实例.md)

        使用账号中的自定义镜像创建实例，在向导页面中选择其它配置。

    -   [购买相同配置的实例](/intl.zh-CN/实例/创建实例/购买相同配置的实例.md)

        使用已有实例的配置创建实例，在向导页面中确认配置。

    -   [使用实例启动模板创建实例](/intl.zh-CN/实例/创建实例/使用实例启动模板创建实例.md)

        使用启动模板创建实例，在向导页面中确认配置。

-   使用API RunInstances：
    -   [RunInstances](/intl.zh-CN/API参考/实例/RunInstances.md)
    -   [批量创建ECS实例](/intl.zh-CN/SDK示例/Java示例/创建ECS实例/批量创建ECS实例.md)

创建数量：控制台根据您的云服务器使用情况而定，RunInstances单次1~100台。

使用控制台和RunInstances创建ECS实例时，实例生命周期如下：

![RunInstances状态图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0075688951/p81974.png)

您也可以使用[CreateInstance](/intl.zh-CN/API参考/实例/CreateInstance.md)创建一台ECS实例，但创建完成后进入已停止（Stopped）状态，您必须手动启动ECS实例。

## 高可用打散部署实例（部署集）

适用场景：将ECS实例分散部署到不同的物理机上，适合为具有高可用和底层容灾要求的应用提供算力。

创建方式：先创建部署集，然后在创建ECS实例时指定部署集。创建ECS实例时可通过控制台、RunInstances或CreateInstance。

创建数量：视创建方式而定，控制台和RunInstances单次1～7台，CreateInstance单次1台。

使用限制：

-   每个部署集在单个可用区下最多创建7台ECS实例。
-   仅支持特定的ECS实例规格，具体说明请参见[部署集概述](/intl.zh-CN/部署与弹性/部署集/部署集概述.md)。
-   付费模式支持包年包月和按量付费，不支持抢占式实例。

详细操作：

-   使用控制台：
    1.  [创建部署集](/intl.zh-CN/部署与弹性/部署集/创建部署集.md)
    2.  [在部署集内创建ECS实例](/intl.zh-CN/部署与弹性/部署集/在部署集内创建ECS实例.md)
-   使用API：
    1.  [CreateDeploymentSet](/intl.zh-CN/API参考/部署集/CreateDeploymentSet.md)
    2.  [RunInstances](/intl.zh-CN/API参考/实例/RunInstances.md)或者[CreateInstance](/intl.zh-CN/API参考/实例/CreateInstance.md)

## 自动化低成本弹性创建实例集群（弹性供应）

适用场景：一键部署跨付费模式、跨可用区和跨实例规格的实例集群。适合需要快速交付稳定算力，同时使用抢占式实例降低成本的场景。

创建方式：创建弹性供应组，由弹性供应组自动批量创建ECS实例。

创建数量：单个弹性供应组1~1000台ECS实例。

使用限制：付费模式支持按量付费和抢占式实例，不支持包年包月。

详细操作：

-   使用控制台：[创建弹性供应组](/intl.zh-CN/部署与弹性/管理弹性供应组/创建弹性供应组.md)
-   使用API：[CreateAutoProvisioningGroup](/intl.zh-CN/API参考/弹性供应组/CreateAutoProvisioningGroup.md)
-   使用API批量创建的最佳实践：[使用弹性供应组API批量创建ECS实例](/intl.zh-CN/最佳实践/使用弹性供应组API批量创建ECS实例.md)

## 自动化弹性创建和释放实例（弹性伸缩）

适用场景：持续维护跨付费模式、跨可用区、跨实例规格的实例集群。适合业务负载存在峰谷波动的场景。

创建方式：创建伸缩组和触发任务，由伸缩组自动批量创建或释放ECS实例。

创建数量：

-   单次伸缩活动最多创建1000台ECS实例。
-   单个伸缩组最多支持1000台ECS实例。

使用限制：自动创建ECS实例的付费模式支持按量付费和抢占式实例。支持将已有包年包月实例手动添加至伸缩组，但不支持在伸缩组内自动创建包年包月实例。

详细操作：

-   使用控制台：
    1.  [创建伸缩组和伸缩配置](/intl.zh-CN/快速入门/创建伸缩组和伸缩配置.md)
    2.  [实现自动扩张](/intl.zh-CN/快速入门/实现自动扩张.md)或者[实现自动收缩](/intl.zh-CN/快速入门/实现自动收缩.md)
-   使用API：
    1.  [CreateScalingGroup](/intl.zh-CN/API参考/伸缩组/CreateScalingGroup.md)
    2.  [CreateScalingConfiguration](/intl.zh-CN/API参考/伸缩配置/CreateScalingConfiguration.md)
    3.  [CreateScalingRule](/intl.zh-CN/API参考/伸缩规则/CreateScalingRule.md)
    4.  [CreateScheduledTask](/intl.zh-CN/API参考/定时任务/CreateScheduledTask.md)

弹性伸缩还支持更多便捷功能，提高交付效率，缩短算力需求出现和算力投入使用之间的流程。例如为ECS实例自动关联SLB实例和RDS实例，配置生命周期挂钩用于对ECS实例进行自定义操作等。您可以基于弹性伸缩实现贴合您业务需求的极致弹性，最佳实践示例请参见：

-   [搭建可自动伸缩的Web应用](/intl.zh-CN/最佳实践/搭建可自动伸缩的Web应用.md)
-   [利用弹性伸缩降低成本](/intl.zh-CN/最佳实践/利用弹性伸缩降低成本.md)
-   [部署高可用计算集群](/intl.zh-CN/最佳实践/部署高可用计算集群.md)

