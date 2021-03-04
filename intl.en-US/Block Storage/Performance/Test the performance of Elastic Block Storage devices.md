---
keyword: [cloud disk performance, EBS performance, ESSD performance, performance metric, IOPS, capacity, throughput, throughput]
---

# Test the performance of Elastic Block Storage devices

This topic describes how to use the fio tool on a Linux instance to test the performance of Elastic Block Storage devices. Elastic Block Storage devices include cloud disks and local disks, and the performance metrics of these disks include IOPS, throughput, and latency.

An Elastic Block Storage device is created and attached to a Linux ECS instance.

**Note:** If you want to test only the performance of a specific category of Elastic Block Storage devices, we recommend that you use a new pay-as-you-go data disk. You can release the disk at any time after the test is complete.

You can use other tools to test the performance of Elastic Block Storage devices, but you may obtain different baseline performance. For example, tools such as dd, sysbench, and iometer may be affected by test parameters and file systems and return inaccurate results. The performance results in this topic are obtained from a fio test on a Linux instance. These results are used as performance references for Alibaba Cloud Elastic Block Storage devices. We recommend that you use the fio tool to test the performance of Elastic Block Storage devices for both Linux and Windows instances.

**Warning:** You can obtain accurate test results by testing raw disks. However, you may destroy the file system structures in a raw disk if you test the disk directly. Before you perform such a test, you must create a snapshot of the disk to back up your data. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md). To prevent data loss, we recommend that you use a new ECS instance that contains no data for the test.

## Procedure

1.  Remotely connect to an ECS instance. For more information, see [Connect to a Linux instance by using VNC](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using VNC.md).

2.  Before you test an Elastic Block Storage device, ensure that it is 4 KiB aligned.

    ```
    sudo fdisk -lu
    ```

    If the value of Start in the command output is divisible by 8, the device is 4 KiB aligned. Otherwise, perform 4 KiB alignment before you proceed with the test.

    ```
    Device     Boot Start      End  Sectors Size Id Type
    /dev/vda1  *     2048 83886046 83883999  40G 83 Linux
    ```

3.  Run the following commands in sequence to install the libaio and fio tools:

    ```
    sudo yum install libaio -y
    sudo yum install libaio-devel -y
    sudo yum install fio -y
    ```

4.  Switch the directory.

    ```
    cd /tmp
    ```

5.  Run the test commands. For more information about the commands, see the following sections.


## Commands used to test the performance of cloud disks

For more information about how to test the IOPS of an enhanced SSD \(ESSD\), see [Test the IOPS performance of an enhanced SSD](/intl.en-US/Block Storage/Performance/Test the IOPS performance of an enhanced SSD.md).

-   Command used to test the random write IOPS of a cloud disk:

    ```
    fio -direct=1 -iodepth=128 -rw=randwrite -ioengine=libaio -bs=4k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Rand_Write_Testing
    ```

-   Command used to test the random read IOPS of a cloud disk:

    ```
    fio -direct=1 -iodepth=128 -rw=randread -ioengine=libaio -bs=4k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Rand_Read_Testing
    ```

-   Command used to test the sequential write throughput \(write bandwidth\) of a cloud disk:

    ```
    fio -direct=1 -iodepth=64 -rw=write -ioengine=libaio -bs=1024k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Write_PPS_Testing
    ```

-   Command used to test the sequential read throughput \(read bandwidth\) of a cloud disk:

    ```
    fio -direct=1 -iodepth=64 -rw=read -ioengine=libaio -bs=1024k -size=1G -numjobs=1 -runtime=1000 -group_reporting -filename=iotest -name=Read_PPS_Testing
    ```

-   Command used to test the random write latency of a cloud disk:

    ```
    fio -direct=1 -iodepth=1 -rw=randwrite -ioengine=libaio -bs=4k -size=1G -numjobs=1 -group_reporting -filename=iotest -name=Rand_Write_Latency_Testing
    ```

-   Command used to test the random read latency of a cloud disk:

    ```
    fio -direct=1 -iodepth=1 -rw=randread -ioengine=libaio -bs=4k -size=1G -numjobs=1 -group_reporting -filename=iotest -name=Rand_Read_Latency_Testing
    ```


## Commands used to test the performance of local disks

The following test commands are applicable to local NVMe SSDs and local SATA HDDs.

-   Command used to test the random write IOPS of a local disk:

    ```
    fio -direct=1 -iodepth=32 -rw=randwrite -ioengine=libaio -bs=4k -numjobs=4 -time_based=1 -runtime=1000 -group_reporting -filename=/dev/vdx -name=test
    ```

-   Command used to test the random read IOPS of a local disk:

    ```
    fio -direct=1 -iodepth=32 -rw=randread -ioengine=libaio -bs=4k -numjobs=4 -time_based=1 -runtime=1000 -group_reporting -filename=/dev/vdx -name=test
    ```

-   Command used to test the sequential write throughput \(write bandwidth\) of a local disk:

    ```
    fio -direct=1 -iodepth=128 -rw=write -ioengine=libaio -bs=128k -numjobs=1 -time_based=1 -runtime=1000 -group_reporting -filename=/dev/vdx -name=test
    ```

-   Command used to test the sequential read throughput \(read bandwidth\) of a local disk:

    ```
    fio -direct=1 -iodepth=128 -rw=read -ioengine=libaio -bs=128k -numjobs=1 -time_based=1 -runtime=1000 -group_reporting -filename=/dev/vdx -name=test
    ```

-   Command used to test the random write latency of a local disk:

    ```
    fio -direct=1 -iodepth=1 -rw=randwrite -ioengine=libaio -bs=4k -numjobs=1 -time_based=1 -runtime=1000 -group_reporting -filename=/dev/vdx -name=test
    ```

-   Command used to test the random read latency of a local disk:

    ```
    fio -direct=1 -iodepth=1 -rw=randread -ioengine=libaio -bs=4k -numjobs=1 -time_based=1 -runtime=1000 -group_reporting -filename=/dev/vdx -name=test
    ```

-   Command used to test the sequential write latency of a local disk:

    ```
    fio -direct=1 -iodepth=1 -rw=write -ioengine=libaio -bs=4k -numjobs=1 -time_based=1 -runtime=1000 -group_reporting -filename=/dev/vdx -name=test
    ```

-   Command used to test the sequential read latency of a local disk:

    ```
    fio -direct=1 -iodepth=1 -rw=read -ioengine=libaio -bs=4k -numjobs=1 -time_based=1 -runtime=1000 -group_reporting -filename=/dev/vdx -name=test
    ```


## fio parameter settings

The following table describes the parameter settings in fio commands. In this example, the command used to test the random write IOPS \(randwrite\) of a cloud disk is used.

|Parameter setting|Description|
|:----------------|:----------|
|-direct=1|Indicates that the I/O buffer is ignored during the test and data is written directly.|
|-iodepth=128|Indicates that when asynchronous I/O is used, up to 128 I/O requests can be made concurrently.|
|-rw=randwrite|Indicates that the read/write policy is random writes. Other valid values for rw: -   randread \(random reads\)
-   read \(sequential reads\)
-   write \(sequential writes\)
-   randrw \(random reads and writes\) |
|-ioengine=libaio|Indicates that libaio \(the Linux-native asynchronous I/O facility\) is used for the test. An application can use I/O in the following ways: -   Synchronous

In synchronous I/O mode, a thread sends a single I/O request at a time and waits for the request be to complete. In this case, the iodepth value is always less than 1 for a single thread. You can increase the iodepth value by using multiple concurrent threads. The iodepth value reaches its upper limit when 16 to 32 threads are running concurrently.

-   Asynchronous

In asynchronous I/O mode, a thread uses libaio to send multiple I/O requests at a time and waits for all these requests to be complete. Asynchronous I/O helps reduce the number of interactions and make the interactions more efficient. |
|-bs=4k|Indicates that the size of each block for one I/O is 4 KiB. The default value is also 4 KiB. -   When IOPS is tested, we recommend that you set bs to a small value such as 4k.
-   When throughput is tested, we recommend that you set bs to a large value such as 1024k. |
|-size=1G|Indicates that the size of the test file is 1 GiB.|
|-numjobs=1|Indicates that the number of test threads is 1.|
|-runtime=1000|Indicates that the test duration is 1,000 seconds. If this parameter is not specified, the file of the size specified by -size is written in blocks of the size specified by -bs.|
|-group\_reporting|Indicates that in the test results, statistics are displayed for a group of threads, not for each individual thread.|
|-filename=iotest|Indicates that the name of the test file is iotest.|
|-name=Rand\_Write\_Testing|Indicates that the name of the test task is Rand\_Write\_Testing. You can specify a name.|

