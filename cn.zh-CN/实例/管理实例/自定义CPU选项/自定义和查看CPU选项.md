---
keyword: [cpu, 核心数, 核数, ecs, 线程]
---

# 自定义和查看CPU选项

一台ECS实例的CPU选项由CPU物理核心数和每核线程数决定，部分ECS实例规格支持通过API RunInstances购买实例时自定义设置CPU选项。

## CPU与vCPU

CPU是中央处理器，一个CPU可以包含若干个物理核，通过超线程HT（Hyper-Threading）技术可以将一个物理核变成两个逻辑处理核。vCPU（virtual CPU）是ECS实例的虚拟处理核。

阿里云ECS的超线程的实现基于x86平台架构HT技术，允许在一个物理核上并发地运行两个线程（Thread），一个线程可以视为一个vCPU。

下表从多个维度对比了ECS实例的CPU选项参数。

|CPU选项|API参数|作用|适用场景|适用的实例规格|
|-----|-----|--|----|-------|
|CPU物理核心数|CpuOptions.Core|决定启用的CPU物理核心数。|减少启用的CPU物理核心数，提高内存配比，收费对象减少也可以降低软件许可费支出。|请参见[使用限制](#section_f4c_fvs_984)。|
|每核线程数|CpuOptions.ThreadsPerCore|决定CPU是否开启超线程。 vCPU数量=CPU物理核心数\*每核线程数。

|通常，ECS实例规格能应对常见的工作负载。在以下场景中，您可以考虑关闭超线程： -   部分HPC场景，关闭超线程可能获得更好的性能表现。
-   在内存密集型业务场景中，通过关闭超线程减少vCPU数，提高内存配比，收费对象减少也可以降低软件许可费支出。

|请参见[使用限制](#section_f4c_fvs_984)。|

## 计费

自定义CPU选项不会产生额外计费。

## 使用限制

-   支持自定义CPU选项的实例规格族如下：

    **说明：** 单击下方链接查看各实例规格CPU物理核心数（CpuOptions.Core）与每核线程数（CpuOptions.ThreadsPerCore）的默认值和取值范围，未列出的实例规格不支持自定义CPU选项。

    -   通用型：[g7a](/cn.zh-CN/实例/管理实例/自定义CPU选项/通用型实例规格族取值表.md)、[g7](/cn.zh-CN/实例/管理实例/自定义CPU选项/通用型实例规格族取值表.md)、[g7t](/cn.zh-CN/实例/管理实例/自定义CPU选项/通用型实例规格族取值表.mdt)、[g7ne](/cn.zh-CN/实例/管理实例/自定义CPU选项/通用型实例规格族取值表.md)、[g6t](/cn.zh-CN/实例/管理实例/自定义CPU选项/通用型实例规格族取值表.md)、[g6se](/cn.zh-CN/实例/管理实例/自定义CPU选项/通用型实例规格族取值表.md)、[g6a](/cn.zh-CN/实例/管理实例/自定义CPU选项/通用型实例规格族取值表.md)、[g6e](/cn.zh-CN/实例/管理实例/自定义CPU选项/通用型实例规格族取值表.mde)、[g6](/cn.zh-CN/实例/管理实例/自定义CPU选项/通用型实例规格族取值表.md)
    -   计算型：[c7a](/cn.zh-CN/实例/管理实例/自定义CPU选项/计算型实例规格族取值表.mda)、[c7](/cn.zh-CN/实例/管理实例/自定义CPU选项/计算型实例规格族取值表.md)、[c7t](/cn.zh-CN/实例/管理实例/自定义CPU选项/计算型实例规格族取值表.mdt)、[c6t](/cn.zh-CN/实例/管理实例/自定义CPU选项/计算型实例规格族取值表.mdt)、[c6a](/cn.zh-CN/实例/管理实例/自定义CPU选项/计算型实例规格族取值表.mda)、[c6e](/cn.zh-CN/实例/管理实例/自定义CPU选项/计算型实例规格族取值表.md)、[c6](/cn.zh-CN/实例/管理实例/自定义CPU选项/计算型实例规格族取值表.md)
    -   内存型：[r7a](/cn.zh-CN/实例/管理实例/自定义CPU选项/内存型实例规格族取值表.mda)、[r7](/cn.zh-CN/实例/管理实例/自定义CPU选项/内存型实例规格族取值表.md)、[r7t](/cn.zh-CN/实例/管理实例/自定义CPU选项/内存型实例规格族取值表.md)、[re6p](/cn.zh-CN/实例/管理实例/自定义CPU选项/内存型实例规格族取值表.md)、[r6a](/cn.zh-CN/实例/管理实例/自定义CPU选项/内存型实例规格族取值表.md)、[r6e](/cn.zh-CN/实例/管理实例/自定义CPU选项/内存型实例规格族取值表.mde)、[r6](/cn.zh-CN/实例/管理实例/自定义CPU选项/内存型实例规格族取值表.md)
    -   高主频型：[hfg7](/cn.zh-CN/实例/管理实例/自定义CPU选项/高主频型实例规格族取值表.md)、[hfc7](/cn.zh-CN/实例/管理实例/自定义CPU选项/高主频型实例规格族取值表.md)、[hfr7](/cn.zh-CN/实例/管理实例/自定义CPU选项/高主频型实例规格族取值表.md)、[hfg6](/cn.zh-CN/实例/管理实例/自定义CPU选项/高主频型实例规格族取值表.md)、[hfc6](/cn.zh-CN/实例/管理实例/自定义CPU选项/高主频型实例规格族取值表.md)、[hfr6](/cn.zh-CN/实例/管理实例/自定义CPU选项/高主频型实例规格族取值表.md)
    -   本地SSD型：[i3g](/cn.zh-CN/实例/管理实例/自定义CPU选项/本地SSD型实例规格族取值表.mdg)、[i3](/cn.zh-CN/实例/管理实例/自定义CPU选项/本地SSD型实例规格族取值表.md)
-   您只能在创建ECS实例时自定义CPU选项，成功创建实例后不允许修改。
-   一台ECS实例如果已经自定义了CPU选项，操作了升降配后，这台ECS实例的CPU选项会被置为默认的CPU选项。
-   一台ECS实例可提供的物理核由实例规格决定，您可以在取值范围内设置启用的CPU物理核心数，但不支持自定义取值范围外的数值。

## 开启或关闭超线程配置

您可以通过[RunInstances](/cn.zh-CN/API参考/实例/RunInstances.md)自定义ECS实例的CPU选项。如果您使用的是SDK，请更新至最新版本。

-   ECS实例默认开启超线程配置，开启CPU超线程配置的阿里云CLI请求示例：

    ```
    aliyun ecs RunInstances --RegionId cn-hangzhou --CpuOptions.Core 2 --CpuOptions.ThreadsPerCore 2 --ImageId ubuntu_18_04_64_20G_alibase_20190624.vhd --InstanceType ecs.g6.xlarge --SecurityGroupId sg-bp67acfmxazb4ph*** --VSwitchId vsw-bp1s5fnvk4gn2tws03*** --Amount 1 --SystemDisk.AutoSnapshotPolicyId sp-bp67acfmxazb4ph***
    ```

-   通过将参数CpuOptions.ThreadsPerCore置为1可以关闭CPU超线程配置，阿里云CLI请求示例：

    ```
    aliyun ecs RunInstances --RegionId cn-hangzhou --CpuOptions.Core 2 --CpuOptions.ThreadsPerCore 1 --ImageId ubuntu_18_04_64_20G_alibase_20190624.vhd --InstanceType ecs.g6.xlarge --SecurityGroupId sg-bp67acfmxazb4ph*** --VSwitchId vsw-bp1s5fnvk4gn2tws03*** --Amount 1 --SystemDisk.AutoSnapshotPolicyId sp-bp67acfmxazb4ph***
    ```


例如，ecs.g6.xlarge默认提供2个物理核：

-   开启超线程：如果您将每核线程数置为2，则该实例规格有2\*2=4个vCPU。默认情况下该实例规格开启超线程配置。
-   关闭超线程：如果您选择关闭超线程配置，则1个物理核只能运行1个线程，实例的vCPU数量等于物理核数，为2。

## 查看CPU选项

您可以通过[DescribeInstances](/cn.zh-CN/API参考/实例/DescribeInstances.md)查看ECS实例的已经设定的CPU选项。如果您使用的是SDK，请更新至最新版本。

-   阿里云CLI请求示例：

    ```
    aliyun ecs DescribeInstances --InstanceIds '["i-bp19rxmzeocge2z57***"]' --output cols=CpuOptions rows=Instances.Instance[]
    ```

    返回示例：

    ```
    CpuOptions
    ----------
    map[CoreCount:1 ThreadsPerCore:2]
    ```

-   Shell命令lscpu示例：

    ```
    shell@ecshost:~$ lscpu
    Architecture:        x86_64
    Byte Order:          Little Endian
    CPU(s):              1   # CPU物理核心数
    On-line CPU(s) list: 0
    Thread(s) per core:  2   # 每核线程数
    Core(s) per socket:  1
    Socket(s):           1
    Vendor ID:           GenuineIntel
    CPU family:          6
    Model:               85
    Model name:          Intel(R) Xeon(R) Platinum 8163 CPU @ 2.50GHz
    ......
    ```


