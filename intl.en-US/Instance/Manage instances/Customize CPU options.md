---
keyword: [CPU, number of cores, number of CPUs, ECS, thread]
---

# Customize CPU options

The CPU options of an Elastic Compute Service \(ECS\) instance include the number of physical CPU cores and the number of threads per core. For some ECS instance types, you can customize these options when you use the RunInstances operation to create an instance.

## CPU and vCPU

CPUs are central processing units. A single CPU can contain several physical cores. Hyper-Threading \(HT\) Technology can be used to create two virtual processing cores for each physical core that is present in a CPU. Virtual CPUs \(vCPUs\) are virtual processing cores of ECS instances.

Alibaba Cloud ECS supports multi-threading based on Intel® HT Technology. HT Technology enables two threads to run concurrently on a single physical core. Each thread can be considered as a vCPU. For more information, visit [Intel® Hyper-Threading Technology](https://www.intel.com/content/www/us/en/architecture-and-technology/hyper-threading/hyper-threading-technology.html).

The following table describes the CPU options for ECS instances.

|CPU option|API parameter|Function|Scenario|Applicable instance type|
|----------|-------------|--------|--------|------------------------|
|Number of physical CPU cores|CpuOptions.Core|Determines the number of physical CPU cores to use.|You can use a smaller number of physical CPU cores to improve the CPU-to-memory ratio of the instance. This reduces the number of chargeable items and software licensing costs.|For more information, see [Valid values for the number of physical CPU cores and the number of threads per core](#section_wtd_72a_dsc).|
|Number of threads per core|CpuOptions.ThreadsPerCore|Determines whether to enable Hyper-Threading on the CPU. Number of vCPUs = Number of physical CPU cores × Number of threads per core.

|In most cases, the default configuration of an ECS instance type provides sufficient performance. You can disable Hyper-Threading in the following scenarios: -   High-performance computing \(HPC\) scenarios. In these scenarios, you can improve the performance of instances by disabling Hyper-Threading.
-   Memory intensive business scenarios. You can disable Hyper-Threading to reduce the number of vCPUs and increase the CPU-to-memory ratio. This can also decrease the number of chargeable items and reduce software licensing costs. |

## Billing methods

You can customize CPU options at no additional costs.

## Limits

-   The following instance families support custom CPU options. For more information about the CPU options of each instance family, see [Valid values for the number of physical CPU cores and the number of threads per core](#section_wtd_72a_dsc).
    -   hfg7, hfc7, and hfr7
    -   g6t and c6t
    -   g6e, c6e, and r6e
    -   g6, c6, and r6
    -   hfg6, hfc6, and hfr6
-   CPU options can be customized only when you create an ECS instance. You cannot modify CPU options after the instance is created.
-   If you upgrade or downgrade the configurations of an instance, the custom CPU options are changed to the default CPU options of the new instance type.
-   The instance type of an instance determines the number of physical cores available in the instance. You can specify the number of physical CPU cores to be enabled within the defined range.

## Enable or disable Hyper-Threading

You can call the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) operation to customize the CPU options of an ECS instance. If you want to use an Alibaba Cloud ECS SDK, upgrade the SDK to the latest version.

-   By default, Hyper-Threading is enabled on ECS instances. You can enable Hyper-Threading in Alibaba Cloud CLI. The following code shows the sample request:

    ```
    aliyun ecs RunInstances --RegionId cn-hangzhou --CpuOptions.Core 2 --CpuOptions.ThreadsPerCore 2 --ImageId ubuntu_18_04_64_20G_alibase_20190624.vhd --InstanceType ecs.g6.6xlarge --SecurityGroupId sg-bp67acfmxazb4ph*** --VSwitchId vsw-bp1s5fnvk4gn2tws03*** --Amount 1 --SystemDisk.AutoSnapshotPolicyId sp-bp67acfmxazb4ph***
    ```

-   To disable Hyper-Threading, set the CpuOptions. ThreadsPerCore parameter to 1 in Alibaba Cloud CLI. The following code shows the sample request:

    ```
    aliyun ecs RunInstances --RegionId cn-hangzhou --CpuOptions.Core 2 --CpuOptions.ThreadsPerCore 1 --ImageId ubuntu_18_04_64_20G_alibase_20190624.vhd --InstanceType ecs.g6.6xlarge --SecurityGroupId sg-bp67acfmxazb4ph*** --VSwitchId vsw-bp1s5fnvk4gn2tws03*** --Amount 1 --SystemDisk.AutoSnapshotPolicyId sp-bp67acfmxazb4ph***
    ```


For example, the ecs.g6.xlarge instance type provides two physical CPU cores by default.

-   To enable Hyper-Threading, you can set the number of threads per core to 2. Then, the number of vCPUs is 4, which is the product of the number of CPU cores and the number of threads per core. Hyper-Threading is enabled by default for this instance type.
-   To disable Hyper-Threading, you can set the number of threads per core to 1. Then, the number of vCPUs is 2.

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

-   Sample code by using the shell command lscpu:

    ```
    shell@ecshost:~$ lscpu
    Architecture:        x86_64
    Byte Order:          Little Endian
    CPU(s):              1   # Indicates the number of physical CPU cores.
    On-line CPU(s) list: 0
    Thread(s) per core:  2   # Indicates the number of threads per core.
    Core(s) per socket:  1
    Socket(s):           1
    Vendor ID:           GenuineIntel
    CPU family:          6
    Model:               85
    Model name:          Intel(R) Xeon(R) Platinum 8163 CPU @ 2.50GHz
    ......
    ```


## Valid values for the number of physical CPU cores and the number of threads per core

The following tables list the default values and valid values for the number of physical CPU cores \(CpuOptions.Core\) and the number of threads per core \(CpuOptions.ThreadsPerCore\). Instance types that are not listed in the tables do not support custom CPU options.

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.hfg7.large|2|1|2|1, 2|
|ecs.hfg7.xlarge|4|2|2|1, 2|
|ecs.hfg7.2xlarge|8|2, 4|2|1, 2|
|ecs.hfg7.3xlarge|12|2, 4, 6|2|1, 2|
|ecs.hfg7.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.hfg7.6xlarge|24|2, 4, 6, 8, 10, 12|2|1, 2|
|ecs.hfg7.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.hfg7.12xlarge|48|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24|2|1, 2|
|ecs.hfg7.24xlarge|96|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.hfc7.large|2|1|2|1, 2|
|ecs.hfc7.xlarge|4|2|2|1, 2|
|ecs.hfc7.2xlarge|8|2, 4|2|1, 2|
|ecs.hfc7.3xlarge|12|2, 4, 6|2|1, 2|
|ecs.hfc7.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.hfc7.6xlarge|24|2, 4, 6, 8, 10, 12|2|1, 2|
|ecs.hfc7.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.hfc7.12xlarge|48|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24|2|1, 2|
|ecs.hfc7.24xlarge|96|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.hfr7.large|2|1|2|1, 2|
|ecs.hfr7.xlarge|4|2|2|1, 2|
|ecs.hfr7.2xlarge|8|2, 4|2|1, 2|
|ecs.hfr7.3xlarge|12|2, 4, 6|2|1, 2|
|ecs.hfr7.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.hfr7.6xlarge|24|2, 4, 6, 8, 10, 12|2|1, 2|
|ecs.hfr7.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.hfr7.12xlarge|48|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24|2|1, 2|
|ecs.hfr7.24xlarge|96|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.g6t.large|2|1|2|1, 2|
|ecs.g6t.xlarge|4|2|2|1, 2|
|ecs.g6t.2xlarge|8|2, 4|2|1, 2|
|ecs.g6t.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.g6t.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.g6t.13xlarge|52|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26|2|1, 2|
|ecs.g6t.26xlarge|104|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.c6t.large|2|1|2|1, 2|
|ecs.c6t.xlarge|4|2|2|1, 2|
|ecs.c6t.2xlarge|8|2, 4|2|1, 2|
|ecs.c6t.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.c6t.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.c6t.13xlarge|52|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26|2|1, 2|
|ecs.c6t.26xlarge|104|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.g6e.large|2|1|2|1, 2|
|ecs.g6e.xlarge|4|2|2|1, 2|
|ecs.g6e.2xlarge|8|2, 4|2|1, 2|
|ecs.g6e.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.g6e.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.g6e.13xlarge|52|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26|2|1, 2|
|ecs.g6e.26xlarge|104|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.c6e.large|2|1|2|1, 2|
|ecs.c6e.xlarge|4|2|2|1, 2|
|ecs.c6e.2xlarge|8|2, 4|2|1, 2|
|ecs.c6e.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.c6e.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.c6e.13xlarge|52|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26|2|1, 2|
|ecs.c6e.26xlarge|104|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.r6e.large|2|1|2|1, 2|
|ecs.r6e.xlarge|4|2|2|1, 2|
|ecs.r6e.2xlarge|8|2, 4|2|1, 2|
|ecs.r6e.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.r6e.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.r6e.13xlarge|52|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26|2|1, 2|
|ecs.r6e.26xlarge|104|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.g6.large|2|1|2|1, 2|
|ecs.g6.xlarge|4|2|2|1, 2|
|ecs.g6.2xlarge|8|2, 4|2|1, 2|
|ecs.g6.3xlarge|12|2, 4, 6|2|1, 2|
|ecs.g6.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.g6.6xlarge|24|2, 4, 6, 8, 10, 12|2|1, 2|
|ecs.g6.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.g6.13xlarge|52|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26|2|1, 2|
|ecs.g6.26xlarge|104|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.c6.large|2|1|2|1, 2|
|ecs.c6.xlarge|4|2|2|1, 2|
|ecs.c6.2xlarge|8|2, 4|2|1, 2|
|ecs.c6.3xlarge|12|2, 4, 6|2|1, 2|
|ecs.c6.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.c6.6xlarge|24|2, 4, 6, 8, 10, 12|2|1, 2|
|ecs.c6.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.c6.13xlarge|52|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26|2|1, 2|
|ecs.c6.26xlarge|104|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.r6.large|2|1|2|1, 2|
|ecs.r6.xlarge|4|2|2|1, 2|
|ecs.r6.2xlarge|8|2, 4|2|1, 2|
|ecs.r6.3xlarge|12|2, 4, 6|2|1, 2|
|ecs.r6.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.r6.6xlarge|24|2, 4, 6, 8, 10, 12|2|1, 2|
|ecs.r6.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.r6.13xlarge|52|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26|2|1, 2|
|ecs.r6.26xlarge|104|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.hfg6.large|2|1|2|1, 2|
|ecs.hfg6.xlarge|4|2|2|1, 2|
|ecs.hfg6.2xlarge|8|2, 4|2|1, 2|
|ecs.hfg6.3xlarge|12|2, 4, 6|2|1, 2|
|ecs.hfg6.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.hfg6.6xlarge|24|2, 4, 6, 8, 10, 12|2|1, 2|
|ecs.hfg6.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.hfg6.10xlarge|40|2, 4, 6, 8, 10, 12, 14, 16, 18, 20|2|1, 2|
|ecs.hfg6.16xlarge|64|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32|2|1, 2|
|ecs.hfg6.20xlarge|80|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.hfc6.large|2|1|2|1, 2|
|ecs.hfc6.xlarge|4|2|2|1, 2|
|ecs.hfc6.2xlarge|8|2, 4|2|1, 2|
|ecs.hfc6.3xlarge|12|2, 4, 6|2|1, 2|
|ecs.hfc6.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.hfc6.6xlarge|24|2, 4, 6, 8, 10, 12|2|1, 2|
|ecs.hfc6.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.hfc6.10xlarge|40|2, 4, 6, 8, 10, 12, 14, 16, 18, 20|2|1, 2|
|ecs.hfc6.16xlarge|64|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32|2|1, 2|
|ecs.hfc6.20xlarge|80|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40|2|1, 2|

|Instance type|Default value for the number of vCPUs|Valid values for the number of physical CPU cores|Default value for the number of threads per core|Valid values for the number of threads per core|
|-------------|-------------------------------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------|
|ecs.hfr6.large|2|1|2|1, 2|
|ecs.hfr6.xlarge|4|2|2|1, 2|
|ecs.hfr6.2xlarge|8|2, 4|2|1, 2|
|ecs.hfr6.3xlarge|12|2, 4, 6|2|1, 2|
|ecs.hfr6.4xlarge|16|2, 4, 6, 8|2|1, 2|
|ecs.hfr6.6xlarge|24|2, 4, 6, 8, 10, 12|2|1, 2|
|ecs.hfr6.8xlarge|32|2, 4, 6, 8, 10, 12, 14, 16|2|1, 2|
|ecs.hfr6.10xlarge|40|2, 4, 6, 8, 10, 12, 14, 16, 18, 20|2|1, 2|
|ecs.hfr6.16xlarge|64|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32|2|1, 2|
|ecs.hfr6.20xlarge|80|2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40|2|1, 2|

