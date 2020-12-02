---
keyword: [multi-queue, network bandwidth bottleneck, NIC queue, pps, bandwidth performance]
---

# Configure NIC multi-queue

Network interface controller \(NIC\) multi-queue enables an ECS instance to use more than one NIC queues to improve network performance. Performance bottlenecks may occur when a single vCPU of an instance is used to process NIC interrupts. To solve this issue, you can use NIC multi-queue to distribute NIC interrupts to different vCPUs for processing. This way, you can achieve higher network performance.

Before you configure NIC multi-queue, make sure that the following requirements are met:

-   The instance type of your instance supports the NIC multi-queue feature. For more information about instance types that support NIC multi-queue, see [Instance families](/intl.en-US/Instance/Instance families.md). If the number of NIC queues is greater than 1, the NIC multi-queue feature is supported.

    **Note:** In an instance of the re6p persistent memory optimized instance family, if NIC interrupts are not distributed to different vCPUs, we recommend that you upgrade the `ecs_mq` configuration script to the latest version.

-   Your image supports the NIC multi-queue feature and has the feature disabled by default. Your instance uses one of the following images. The following public images provided by Alibaba Cloud support the NIC multi-queue feature. Whether images support this feature is irrelevant to the bit sizes of the operating systems.

    **Note:**

    -   Even if your operating system is included in the list, public images of earlier versions may not support the NIC multi-queue feature. We recommend that you use the latest public images. If your image has the NIC multi-queue feature enabled by default, skip this topic.
    -   The following procedure applies only to Linux instances. You do not need to configure the NIC multi-queue feature for ECS instances that run Windows 2012 or later because this feature is automatically configured.
    |Public image|NIC multi-queue supported|NIC multi-queue enabled|
    |:-----------|:------------------------|:----------------------|
    |CentOS 6.8/6.9/7.2/7.3/7.4/8. \*|Yes|Yes|
    |Ubuntu 14.04/16.04/18.04/20.04|Yes|Yes|
    |Debian 8.9/9.2/10. \*|Yes|Yes|
    |SUSE Linux Enterprise Server 12 SP1/12 SP2/15 SP1/15 SP2|Yes|Yes|
    |Red Hat Enterprise Linux 6.9/7.4/7.5|Yes|No|
    |OpenSUSE 42.3/15. \*|Yes|No|
    |Alibaba Cloud Linux 2.1903|Yes|Yes|
    |Windows 2012 or later|Yes|Yes|


NIC multi-queue is a technology that can fix Quality of Service \(QoS\) issues of I/O bandwidth. The NIC multi-queue driver binds NIC queues to different vCPUs by using interrupts. This solves processing bottlenecks of single vCPU when network I/O bandwidth increases, and improves the packet forwarding rate and bandwidth performance. Under identical packet forwarding rate and network bandwidth conditions, the performance of two queues can be 50% to 100% higher than that of a single queue, and the performance of four queues can be even higher.

## Automatic configuration

1.  Remotely connect to an ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Download the `ecs_mq` automatic configuration script.

    ```
    wget https://ecs-image-tools.oss-cn-hangzhou.aliyuncs.com/ecs_mq/ecs_mq_latest.tgz
    ```

3.  Decompress the script package.

    ```
    tar -xzf ecs_mq_latest.tgz
    ```

4.  Change the working path.

    ```
    cd ecs_mq/
    ```

5.  Run the extracted script file.

    The script format varies with image versions. For example, `bash install.sh centos 7` is suitable for CentOS 7.6 images.

    ```
    bash install.sh <System name> <Major version number of the system>
    ```

6.  Start the service.

    ```
    systemctl start ecs_mq
    ```


## Manual configuration

CentOS 7.6 images are used in this section. The name of the primary elastic network interface \(ENI\) is eth0, and the name of the secondary ENI is eth1. This section describes how to manually configure NIC multi-queue.

1.  Run the `ethtool -l eth0` command to check whether the primary NIC supports NIC multi-queue.

    ```
    [root@localhost ~]# ethtool -l eth0
    Channel parameters for eth0:
    Pre-set maximums:
    RX: 0
    TX: 0
    Other: 0
    Combined: 2 # This value indicates that a maximum of two queues can be configured.
    Current hardware settings:
    RX: 0
    TX: 0
    Other: 0
    Combined: 1 # This value indicates that one queue is in effect.
    ```

    **Note:** If the returned values of the two Combined fields are the same, the NIC multi-queue feature is enabled.

2.  Run the `ethtool -L eth0 combined 2` command to enable the NIC multi-queue feature.

    This command configures the eth0 primary ENI to use two queues.

    ```
    [root@localhost ~]# ethtool -L eth0 combined 2
    ```

3.  Configure NIC multi-queue for the secondary ENI.

    ```
    # Check whether the eth1 secondary ENI supports NIC multi-queue.
    [root@localhost ~]# ethtool -l eth1
    Channel parameters for eth1:
    Pre-set maximums:
    RX: 0
    TX: 0
    Other: 0
    Combined: 4 # This value indicates that a maximum of four queues can be configured.
    Current hardware settings:
    RX: 0
    TX: 0
    Other: 0
    Combined: 1 # This value indicates that one queue is in effect.
    # Configure the eth1 secondary ENI to use four queues.
    [root@localhost ~]# ethtool -L eth1 combined 4
    ```


