# Configure the usage mode of persistent memory

The usage mode of persistent memory on some re6p instance types can be configured. You can use the persistent memory as memory or local SSDs. This topic describes how to configure the usage mode of persistent memory.

-   The instance type is one of the following instance types:
    -   ecs.re6p.large
    -   ecs.re6p.xlarge
    -   ecs.re6p.2xlarge
    -   ecs.re6p.13xlarge
    -   ecs.re6p.26xlarge
-   The image version meets one of the following requirements:
    -   Alibaba Cloud Linux 2
    -   CentOS 7.6 or later
    -   Ubuntu 18.10 or later
    -   SUSE Linux 12 SP4 or later

Persistent memory optimized instances are equipped with large-capacity persistent memory and provide slower access to data than instances equipped with regular memory. However, when persistent memory optimized instances are stopped or restarted, data stored in their persistent memory are not lost. The following section describes the usage modes of persistent memory:

-   Used as memory: You can move some data stored in regular memory to persistent memory, such as non-hotspot data that has lower requirements for access speed. Persistent memory offers large capacity at a low price per GiB and can help reduce the total cost of ownership \(TCO\) per GiB.
-   Used as local SSDs: Persistent memory can be used as local SSDs to provide ultra-high performance and read/write latency as low as 400 nanoseconds. Therefore, you can choose persistent memory for core application databases that require consistent response time \(RT\). You can replace cache disks with persistent memory to obtain higher IOPS, higher bandwidth, and lower latency. This can improve the business performance of the entire cluster.

**Note:** The reliability of data stored in persistent memory depends on the reliability of persistent memory devices and the physical servers to which these devices are attached. This increases risks of single points of failure. To ensure the reliability of application data, we recommend that you implement data redundancy at the application layer and use cloud disks for long-term data storage.

The following configurations are used in this example:

-   Instance type: ecs.re6p.2xlarge
-   Image: Alibaba Cloud Linux 2.1903 LTS 64-bit

## Use persistent memory as memory

When persistent memory is used as memory, its core capability is to support character addressing. The space of persistent memory and regular memory is independent of each other and is not merged. You can also use memkind to allocate memory space. For more information about how to use memkind, visit [memkind](https://github.com/memkind/memkind).

1.  Log on to the instance.

    For more information, see [Overview of instance connection](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Install the persistent memory management tool.

    ```
    yum install -y ndctl daxctl
    ```

3.  Set the usage mode to devdax.

    ```
    ndctl create-namespace -f -e namespace0.0 --mode=devdax
    ```

4.  Check the memory size.

    -   Check the size of the persistent memory.

        ```
        ndctl list -R
        ```

        ![pmem-size](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1555376061/p179060.png)

    -   Check the size of the regular memory.

        ```
        cat /proc/meminfo
        ```


## Use persistent memory as local SSDs

1.  Log on to the instance.

    For more information, see [Overview of instance connection](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Install the persistent memory management tool.

    ```
    yum install -y ndctl daxctl
    ```

3.  Set the usage mode to fsdax.

    ```
    ndctl create-namespace -f -e namespace0.0 --mode=fsdax
    ```

4.  Format the local SSDs as which the persistent memory is used.

    ```
    mkfs -t ext4 /dev/pmem0
    ```

5.  Attach the local SSDs to the instance.

    ```
    mkdir /mnt/sdb
    mount -o dax,noatime /dev/pmem0 /mnt/sdb
    ```

6.  View the attached local SSDs.

    ```
    df -h
    ```

    ![pmem-as-ssd](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1555376061/p179010.png)

    After the disks are attached, you can use disk performance test tools to test the performance of the disks. For more information about how to use fio to test disk performance in Linux, see the "Commands used to test the performance of cloud disks" section in [Test the performance of Elastic Block Storage devices](/intl.en-US/Block Storage/Performance/Test the performance of Elastic Block Storage devices.md).

    The following table describes the performance comparison between local NVMe SSDs, enhanced SSDs \(ESSDs\), and persistent memory that is used as local SSDs.

    **Note:** The performance levels \(PLs\) in the following table are only for reference. If you want to obtain details of a single test, the results of your own tests prevail.

    |Item|Persistent memory of 128 GiB|NVMe SSD of 1,788 GiB|PL1 ESSD of 800 GiB|
    |----|----------------------------|---------------------|-------------------|
    |Read bandwidth|8-10 GB/s|2-3 GB/s|0.2-0.3 GB/s|
    |Read/write bandwidth|8-10 GB/s|1-2 GB/s|0.2-0.3 GB/s|
    |Write bandwidth|4-6 GB/s|1-2 GB/s|0.2-0.3 GB/s|
    |Read IOPS|1,000,000|500,000|20,000-30,000|
    |Read/write IOPS|1,000,000|300,000|20,000-30,000|
    |Write IOPS|1,000,000|300,000|20,000-30,000|
    |Read latency|300-400 nanoseconds|100,000 nanoseconds|250,000 nanoseconds|
    |Write latency|300-400 nanoseconds|20,000 nanoseconds|150,000 nanoseconds|


