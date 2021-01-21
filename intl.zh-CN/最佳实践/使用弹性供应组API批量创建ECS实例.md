# 使用弹性供应组API批量创建ECS实例

在需要大批量创建按量付费实例的场景中，通过API完成创建操作更加高效。其中，使用RunInstances完成该需求较为复杂，本文将推荐您使用交付过程更加方便稳定的CreateAutoProvisioningGroup。

在业务需要使用按量付费ECS实例的场景下，RunInstances是使用最频繁的API。RunInstances拥有一次调用能够最多创建100台ECS实例的能力，但是在实际的生产环境中，如果需要超过100台的大批量创建ECS实例场景，直接使用RunInstances会存在一定的技术瓶颈。更多信息，请参见[RunInstances创建实例时存在的问题](#section_6v8_ugx_6ro)。

**说明：** 如果您已了解RunInstances批量创建实例过程中存在的技术瓶颈，可以跳过该章节。

为了解决大批量创建ECS实例的需求场景，阿里云提供了弹性供应组，您可以通过CreateAutoProvisioningGroup创建弹性供应组，一键式的部署跨计费方式、跨可用区、跨实例规格族的实例集群。相较于RunInstances，CreateAutoProvisioningGroup更适合大批量创建ECS实例的业务场景。两者的功能对比与优势分析，请参见[RunInstances与CreateAutoProvisioningGroup功能对比](#section_xtx_q9a_5s3)以及[弹性供应组的优势](#section_1j8_ea0_iyf)。

## RunInstances与CreateAutoProvisioningGroup功能对比

本章节对比[RunInstances](/intl.zh-CN/API参考/实例/RunInstances.md)与[CreateAutoProvisioningGroup](/intl.zh-CN/API参考/弹性供应组/CreateAutoProvisioningGroup.md)两接口的部分功能，使您可以快速了解两者的差异，选择合适的创建实例方式。

|对比项|RunInstances|CreateAutoProvisioningGroup|
|---|------------|---------------------------|
|单次批量创建实例的数量上限|100台|1000台（vCPU上限为10000）|
|容量交付方式|实例数量|实例数量、vCPU核数、实例规格的权重等|
|是否支持多可用区|否|是|
|是否支持多个实例规格|否|是|
|是否支持多种磁盘规格|否|是|
|是否提供了创建实例的策略|否|是。提供了如下策略：-   按量付费实例
    -   成本优化策略：从备选实例规格中选取成本最低的实例规格，创建实例。
    -   优先级策略：按照备选实例规格设置的优先级，依次尝试创建实例。
-   抢占式实例
    -   成本优化策略：从备选实例规格中选取成本最低的实例规格，创建实例。
    -   可用区均衡分布策略：在备选的可用区之间，数量均匀的创建实例。
    -   容量优化分布策略：根据抢占式实例的库存情况，选择最优的实例规格及可用区进行创建实例。 |
|交付稳定性|受资源库存影响较大|多可用区、多实例规格的配置组合有效降低了资源库存造成的影响|
|API响应格式|同步返回创建结果|同步返回创建结果|

创建实例的方式由RunInstances更换为CreateAutoProvisioningGroup的部分示例场景：

-   如果您之前使用RunInstances在单可用区、单实例规格的配置下批量创建实例，更换为CreateAutoProvisioningGroup后，您只需配置一组实例规格与可用区的组合，即可实现批量创建实例。
-   如果您之前使用RunInstances时手动设置了业务部署方案，更换为CreateAutoProvisioningGroup后，将由系统为您提供一键式的多可用区、多实例规格、多磁盘配置的部署能力，并且系统提供了多种创建实例的策略供您选择。

    例如：您之前手动设置了遍历多个实例规格及可用区的方案进行RunInstances调用，以提高实例创建的成功率。更换为CreateAutoProvisioningGroup后，您只需要通过参数配置多个实例规格及可用区的组合，选择合适的创建策略，系统将自动完成批量创建实例的操作。


**说明：** 弹性供应组的创建策略存在使用限制，单次最大可创建1000台实例，如果指定了实例规格的权重（`WeightedCapacity`），则单次创建的最大加权容量为10000。

## RunInstances创建实例时存在的问题

基于RunInstances功能的限制，您在大批量创建实例时，可能遇到下表所示的问题。

|问题|说明|解决方案|
|--|--|----|
|批量创建的能力有限|调用一次RunInstances最多可以创建100台ECS实例。|当您需要创建大于100台ECS实例时，需要通过循环或并发的方式多次调用该接口，以完成业务需求。|
|批量创建的稳定性不足|调用RunInstances只支持设置单可用区、单实例规格。因此您在批量创建ECS实例的过程中，可能因为实例规格的库存不足、停止售卖或使用限制等问题。引发以下情况：-   在某一时间段，实例规格的库存不足导致批量创建失败。
-   在某一时间段，无法再创建指定的实例规格。
-   指定的实例规格只在部分可用区售卖。
-   指定的实例规格只能搭配指定的磁盘类型。

|-   库存问题是导致批量创建ECS实例失败的主要原因。因此阿里云会推荐您在批量创建ECS实例之前，先调用[DescribeAvailableResource](/intl.zh-CN/API参考/地域/DescribeAvailableResource.md)查询实例规格与可用区下资源的库存情况，手动确认多个库存充足的可用区与实例规格的组合后，再批量创建ECS实例。通过复杂的创建方式，换来了较高的业务交付稳定性。

示例场景：当您确认多个库存充足的可用区与实例规格的组合后，您还需要构建合适的创建ECS实例的策略。例如，您可以根据手动确认的多个组合顺序，依次创建100台ECS实例，如果第一个组合的资源库存只支持创建50台ECS实例，那么您需要使用第二个组合尝试创建其余50台ECS实例。

-   实例规格存在使用限制。您可以通过[DescribeAvailableResource](/intl.zh-CN/API参考/地域/DescribeAvailableResource.md)查询限制，并自行建立容错方案，避免因使用限制变更带来的影响。

**说明：** 您也可以根据文档提供的实例规格特点确定相关限制。更多信息，请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。

示例场景：`ecs.g6e.large`实例规格只支持ESSD云盘类型、`cn-beijing-x`可用区下不支持选择ESSD云盘类型等。 |
|创建策略过于单一|RunInstances仅支持设置单可用区、单实例规格。如果您的业务需要多可用区部署实现异地容灾、需要按照最低成本创建ECS实例等，则需要您自行构建业务部署方案，以保障实例的成功部署。自行构建的业务部署方案存在以下问题：-   开发成本高。自行构建的业务部署方案需要处理一系列的问题。例如，库存不足时如何顺利的创建ECS实例、扩容服务器时如何在获取抢占式实例最低成本的同时保证计算能力等
-   稳定性与专业性不足。对于阿里云提供的资源，您难以用专业的方式自行构建业务部署方案，并无法对方案进行测试，进而将对生产环境造成一定的风险。

|自行解决或联系阿里云提供帮助。|

## 弹性供应组的优势

针对RunInstances批量创建ECS实例存在的问题，阿里云提供了弹性供应组，解决了大批量创建ECS实例的场景下存在的问题。弹性供应组支持一键部署跨计费方式、跨可用区、跨实例规格族的实例集群。您可以通过弹性供应组稳定提供计算力，缓解抢占式实例的回收机制带来的不稳定因素，免去重复手动创建实例的繁琐操作。本章节主要介绍弹性供应组的优势。

|优势|说明|
|--|--|
|批量创建ECS实例的数量上限更高|弹性供应组支持单次创建最多1000台ECS实例。|
|支持设置多可用区、多实例规格、多种磁盘类型|弹性供应组支持您配置最多10种实例规格或可用区的组合、最多5种磁盘类型的选择，帮助您实现高可用的批量创建ECS实例。示例场景：

当您通过弹性供应组提供的均衡可用区分布策略创建ECS实例时，可以配置多个可用区和多个实例规格。按照策略的要求，多个可用区下，创建实例的数量应相对平均，但如果其中某个可用区无法完成创建，弹性供应组会尝试将该可用区待创建的实例数量，转移到其他可用区进行创建。

如果您指定了多种磁盘规格，弹性供应组将按照指定顺序作为各磁盘类型的优先级顺序，当某一种磁盘不可用时，自动更换磁盘类型。

**说明：** 当所有磁盘类型都不可用时，系统将会自动更换其它创建方式，不再尝试该种创建方式。 |
|支持多种创建实例的策略|针对按量付费实例和抢占式实例，分别提供了以下创建策略：-   按量付费实例
    -   成本优化策略：从备选实例规格中选取成本最低的实例规格，创建实例。
    -   优先级策略：按照备选实例规格设置的优先级，依次尝试创建实例。
-   抢占式实例
    -   成本优化策略：从备选实例规格中选取成本最低的实例规格，创建实例。
    -   可用区均衡分布策略：在备选的可用区之间，数量均匀的创建实例。
    -   容量优化分布策略：根据抢占式实例的库存情况，选择最优的实例规格及可用区进行创建实例。 |
|可提高抢占式实例的可用性|抢占式实例因其价格优势使用量越来越高，但是其价格的不稳定性与系统回收的特性，造成管理抢占式实例存在一定的难度。您可以通过弹性供应组，实现在低成本的前提下，提高抢占式实例的可用性。具体方式如下：-   创建策略选择默认的成本优化策略，每次的扩容策略将按照实例规格价格从低到高的顺序尝试创建。
-   抢占式实例对应的不同实例规格与可用区的资源库存情况互相隔离。多个实例规格与多个可用区的配置组合，可以有效降低所有组合都无库存的概率。
-   创建弹性供应组时，配置多种备选的磁盘类型，保证创建实例的过程中，系统能够自动选取合适的磁盘类型。
-   配置`SpotInstancePoolsToUseCount`参数，指定抢占式实例在多个最低价格的实例规格及可用区的组合中创建。避免某一种实例规格对应的实例回收，造成计算能力产生雪崩效应。 |

## CreateAutoProvisioningGroup最佳实践

本章节提供CreateAutoProvisioningGroup接口对应的Java代码示例，使您快速了解该接口的使用方式。

1.  安装ECS Java SDK以及阿里云核心库。

    具体操作，请参见[安装Java SDK](/intl.zh-CN/SDK示例/Java示例/安装Java SDK.md)。

2.  编写调用CreateAutoProvisioningGroup接口的Java代码。

    代码示例如下：

    ```
    CreateAutoProvisioningGroupRequest request = new CreateAutoProvisioningGroupRequest();
    request.setRegionId(regionId);
    request.setLaunchConfigurationImageId(RequestHelper.IMAGE_ID);
    request.setLaunchConfigurationSecurityGroupId(securityGroupId);
    
    request.setTotalTargetCapacity(totalTargetCapacity);
    request.setPayAsYouGoTargetCapacity(payAsYouGoTargetCapacity);
    request.setSpotTargetCapacity(spotTargetCapacity);
    request.setLaunchConfigurationSystemDiskCategory("cloud_ssd");
    request.setLaunchConfigurationSystemDiskSize(40);
    request.setAutoProvisioningGroupType("instant");
    // 设置抢占式实例的创建策略
    request.setSpotAllocationStrategy("lowest-price");
    request.setSpotInstancePoolsToUseCount(spotInstancePoolsToUseCount);
    // 设置按量付费实例的创建策略
    request.setPayAsYouGoAllocationStrategy("prioritized");
    request.setMaxSpotPrice(maxSpotPrice);
    // 多实例规格，多可用区配置信息，最大支持10种
    request.setLaunchTemplateConfigs(launchTemplateConfigs);
    request.setClientToken(clientToken);
    CreateAutoProvisioningGroupResponse response = client.getAcsResponse(request);
    ```

    JSON返回值示例如下：

    ```
    {
        "autoProvisioningGroupId":"apg-****",
        "launchResults":[
            {
                "instanceIds":[
                    "i-****"
                ],
                "instanceType":"ecs.c5.large",
                "spotStrategy":"NoSpot",
                "zoneId":"cn-shanghai-b"
            },
           {
                "instanceIds":[],
                "instanceType":"ecs.c5.large",
                "spotStrategy":"NoSpot",
                "zoneId":"cn-shanghai-b",
                "errorCode" : "Invalid.Parameter",
                "errorMsg" : "Specific Parameter 'imageId' is not valid"
            }
        ],
        "requestId":"20DA1E9F-BF7F-4BE7-8204-E4DE58E4FC7B"
    }
    ```

    通过CreateAutoProvisioningGroup创建弹性供应组时，您只需要设置批量创建实例的相关配置项，无需关心创建过程，弹性供应组将以尽力交付的方式，完成创建。

    **说明：** 尽力交付的方式是指，当您配置的某些资源组合无法创建实例时，将自动切换到其他可用的资源组合继续进行创建。该方式创建实例需要一定的时间，并且可能导致实际创建结果与创建策略存在一定的偏差。


**相关文档**  


[弹性供应概述](/intl.zh-CN/部署与弹性/管理弹性供应组/弹性供应概述.md)

[弹性供应组设置示例](/intl.zh-CN/部署与弹性/管理弹性供应组/弹性供应组设置示例.md)

