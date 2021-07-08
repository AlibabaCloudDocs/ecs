---
keyword: [CPU, number of cores, number of CPUs, ECS, thread]
---

# Customize and view CPU options

The CPU options of an Elastic Compute Service \(ECS\) instance include the number of physical CPU cores and the number of threads per core. For some ECS instance types, you can customize these options when you call the RunInstances operation to create an instance.

## CPU and vCPU

CPUs are central processing units. A single CPU can contain several physical cores. Hyper-Threading \(HT\) Technology can be used to create two virtual processing cores for each physical core that is present in a CPU. Virtual CPUs \(vCPUs\) are virtual processing cores of ECS instances.

Alibaba Cloud ECS supports multi-threading based on HT Technology of the x86 architecture. HT Technology enables two threads to concurrently run on a single physical core. Each thread can be considered as a vCPU.

The following table describes the CPU options for ECS instances.

|CPU option|API parameter|Description|Scenario|Applicable instance type|
|----------|-------------|-----------|--------|------------------------|
|Number of physical CPU cores|CpuOptions.Core|Specifies the number of physical CPU cores to use.|You can use a smaller number of physical CPU cores to improve the CPU-to-memory ratio of an instance. This can decrease the number of chargeable items and reduce software licensing costs.|For more information, see [Limits](#section_f4c_fvs_984).|
|Number of threads per core|CpuOptions.ThreadsPerCore|Specifies whether to enable HT on the CPU. Number of vCPUs = Number of physical CPU cores × Number of threads per core.

|In most cases, the default configuration of an ECS instance type provides sufficient performance. You can disable HT in the following scenarios: -   High-performance computing \(HPC\) scenarios. In these scenarios, you can disable HT to improve the performance of instances.
-   Memory-intensive business scenarios. You can disable HT to reduce the number of vCPUs and increase the CPU-to-memory ratio. This can also decrease the number of chargeable items and reduce software licensing costs.

|For more information, see [Limits](#section_f4c_fvs_984).|

## Billing methods

You can customize CPU options at no additional costs.

## Limits

-   The following instance families support custom CPU options.

    **Note:** Click the following links to check the default and valid values for the number of physical CPU cores \(CpuOptions.Core\) and the number of threads per core \(CpuOptions.ThreadsPerCore\). Instance types that are not listed do not support custom CPU options.

    -   General purpose instance families: [g7a](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of general purpose instance families.md), [g7](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of general purpose instance families.md), [g7t](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of general purpose instance families.mdt), [g7ne](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of general purpose instance families.md), [g6t](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of general purpose instance families.md), [g6se](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of general purpose instance families.md), [g6a](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of general purpose instance families.md), [g6e](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of general purpose instance families.mde), and [g6](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of general purpose instance families.md)
    -   Compute optimized instance families: [c7a](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of compute optimized instance families.mda), [c7](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of compute optimized instance families.md), [c7t](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of compute optimized instance families.mdt), [c6t](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of compute optimized instance families.mdt), [c6a](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of compute optimized instance families.mda), [c6e](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of compute optimized instance families.md), and [c6](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of compute optimized instance families.md)
    -   Memory optimized instance families: [r7a](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of memory optimized instance families.mda), [r7](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of memory optimized instance families.md), [r7t](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of memory optimized instance families.md), [re6p](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of memory optimized instance families.md), [r6a](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of memory optimized instance families.md),[r6e](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of memory optimized instance families.mde), and [r6](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of memory optimized instance families.md)
    -   Instance families with high clock speeds: [hfg7](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of instance families with high clock speeds.md), [hfc7](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of instance families with high clock speeds.md), [hfr7](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of instance families with high clock speeds.md), [hfg6](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of instance families with high clock speeds.md), [hfc6](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of instance families with high clock speeds.md), and [hfr6](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of instance families with high clock speeds.md)
    -   Instance families with local SSDs: [i3g](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of instance families with local SSDs.mdg) and [i3](/intl.en-US/Instance/Manage instance attributes/Customize CPU options/CPU options of instance families with local SSDs.md)
-   CPU options can be customized only when you create an ECS instance. You cannot modify CPU options after the instance is created.
-   If you upgrade or downgrade the configurations of an instance, the custom CPU options are changed to the default CPU options of the new instance type.
-   The instance type of an instance determines the number of physical cores available in the instance. You can specify the number of physical CPU cores to be enabled within the specified value range.

## Enable or disable HT

You can call the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) operation to customize the CPU options of an ECS instance. If you want to use an Alibaba Cloud ECS SDK, upgrade the SDK to the latest version.

-   By default, HT is enabled on ECS instances. You can enable HT in Alibaba Cloud CLI. The following code shows a sample request:

    ```
    aliyun ecs RunInstances --RegionId cn-hangzhou --CpuOptions.Core 2 --CpuOptions.ThreadsPerCore 2 --ImageId ubuntu_18_04_64_20G_alibase_20190624.vhd --InstanceType ecs.g6.xlarge --SecurityGroupId sg-bp67acfmxazb4ph*** --VSwitchId vsw-bp1s5fnvk4gn2tws03*** --Amount 1 --SystemDisk.AutoSnapshotPolicyId sp-bp67acfmxazb4ph***
    ```

-   To disable HT, set the CpuOptions.ThreadsPerCore parameter to 1 in Alibaba Cloud CLI. The following code shows a sample request:

    ```
    aliyun ecs RunInstances --RegionId cn-hangzhou --CpuOptions.Core 2 --CpuOptions.ThreadsPerCore 1 --ImageId ubuntu_18_04_64_20G_alibase_20190624.vhd --InstanceType ecs.g6.xlarge --SecurityGroupId sg-bp67acfmxazb4ph*** --VSwitchId vsw-bp1s5fnvk4gn2tws03*** --Amount 1 --SystemDisk.AutoSnapshotPolicyId sp-bp67acfmxazb4ph***
    ```


For example, the ecs.g6.xlarge instance type provides two physical CPU cores by default.

-   To enable HT, you can set the number of threads per core to 2. Then, the number of vCPUs is 4, which is the product of the number of CPU cores and the number of threads per core. HT is enabled by default for this instance type.
-   To disable HT, you can set the number of threads per core to 1. Then, the number of vCPUs is 2.

## View CPU options

You can call the [DescribeInstances](/intl.en-US/API Reference/Instances/DescribeInstances.md) operation to view the CPU options of an ECS instance. If you want to use an Alibaba Cloud ECS SDK, upgrade the SDK to the latest version.

-   Sample request in Alibaba Cloud CLI:

    ```
    aliyun ecs DescribeInstances --InstanceIds '["i-bp19rxmzeocge2z57***"]' --output cols=CpuOptions rows=Instances.Instance[]
    ```

    Sample response:

    ```
    CpuOptions
    ----------
    map[CoreCount:1 ThreadsPerCore:2]
    ```

-   Sample code of running the shell command lscpu:

    ```
    shell@ecshost:~$ lscpu
    Architecture:        x86_64
    Byte Order:          Little Endian
    CPU(s):              1   # the number of physical CPU cores.
    On-line CPU(s) list: 0
    Thread(s) per core:  2   # the number of threads per core.
    Core(s) per socket:  1
    Socket(s):           1
    Vendor ID:           GenuineIntel
    CPU family:          6
    Model:               85
    Model name:          Intel(R) Xeon(R) Platinum 8163 CPU @ 2.50GHz
    ......
    ```


