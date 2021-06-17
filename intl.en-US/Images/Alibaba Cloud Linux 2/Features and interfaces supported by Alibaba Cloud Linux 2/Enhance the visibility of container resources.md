# Enhance the visibility of container resources

Alibaba Cloud Linux 2 provides kernel interfaces for the container resource visualization feature to enhance the visibility of container resources. This topic describes these interfaces and their sample scenarios.

By default, the container resource visualization feature provided by Alibaba Cloud Linux 2 is disabled. After you enable this feature, you can run commands such as top and free in a container to read data of the following interfaces. When you run these commands, the resource information of the container rather than the Elastic Compute Service \(ECS\) instance on which the container resides.

-   /proc/cpuinfo
-   /proc/meminfo
-   /sys/devices/system/cpu/online

## Interface description

|Interface|Description|
|---------|-----------|
|/proc/sys/kernel/rich\_container\_enable|Specifies whether the container resource visualization feature is enabled. Valid values:-   0: The container resource visualization feature is disabled.
-   1: The container resource visualization feature is enabled.

Default value: 0.|
|/proc/sys/kernel/rich\_container\_source|Specifies the data source of the cgroup interface. Valid values:-   0: uses the cgroup in which the current pointer resides as a data source.
-   1: uses the cgroup in which the child reaper \(Process 1 of the current PID namespace\) resides as a data source.

Default value: 0.|
|/proc/sys/kernel/rich\_container\_cpuinfo\_source|Specifies the number of CPUs that are displayed in the /proc/cpuinfo and /sys/devices/system/cpu/online interfaces. Valid values:-   0: uses the ratio of the value of Request to that of Limit \(`Request/Limit`\) in Kubernetes. This value equals the ratio of the value of the CPU parameter `quota` to that of `period` \(`quota/period`\).
-   1: uses the CPU data source in the cpuset.cpus interface.
-   2: uses the value obtained by dividing `cpu.shares` by `/proc/sys/kernel/rich_container_cpuinfo_sharesbase`. This value is rounded up to the nearest integer. If the obtained value contains a decimal, add the integer digit by 1. Only the integer digit is used as the final value. For example, if the obtained value is 1.1, 2 is used as the final value. The final value cannot exceed the number of available CPUs.

Default value: 0.|
|/proc/sys/kernel/rich\_container\_cpuinfo\_sharesbase|When the value of the /proc/sys/kernel/rich\_container\_cpuinfo\_source interface is set to 2, you must use this interface as a part of the formula to obtain the final value. The value must be an integer greater than or equal to 2. Default value: 1024. |

## Examples

In the examples, Docker is deployed in a Linux instance, and a container with 1 GB memory is created.

-   If the container resource visualization feature is disabled, the value of the /proc/sys/kernel/rich\_container\_enable interface is set to 0. When you run the free -m command in the container, you can view the following resource information, which indicates the resource information of the Linux instance on which the container resides.

    ![free](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0983812261/p269174.png)

-   If you run the echo 1 \> /proc/sys/kernel/rich\_container\_enable command on the Linux instance, the container resource visualization feature is enabled. When you run the free -m command in the container, you can view the following resource information, which indicates the resource information of the container.

    ![free](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1983812261/p269181.png)


## Special scenarios

In most cases, after the container resource visualization feature is enabled, the default value of the interface can meet your requirements. However, you must take note of the interface configurations in the following special scenarios:

For a pod in which the PID namespace is not shared, each container is an independent PID namespace. If you run the systemd command to start a privileged container and if the container process is Process 1, the task of collecting monitoring data is run in a child cgroup instead of the root cgroup of the container.

For example, when you log on to the container by using an SSH key pair and run the cat /proc/cpuinfo command, one of the following situations may occur:

-   If the value of the /proc/sys/kernel/rich\_container\_source interface is set to 0 when you run the command, the current pointer resides in the child cgroup that is created by sshd.service in the container. In this case, error data is returned.
-   If you run the echo 1 \> /proc/sys/kernel/rich\_container\_source command, the cgroup in which the child reaper resides is used as a data source. In this case, valid data is returned.

