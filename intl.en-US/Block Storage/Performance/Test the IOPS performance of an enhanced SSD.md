---
keyword: [select an ESSD, select an ESSD, high-performance disks used for databases, ECS]
---

# Test the IOPS performance of an enhanced SSD

This topic describes how to test the IOPS performance of an enhanced SSD \(ESSD\). The specifications of the disk and the test conditions affect the test results. If you configure the test conditions as in the following example, you can achieve an IOPS of one million when you perform a performance stress test on the ESSD.

Test conditions:

-   Sample operation: random write \(randwrite\).
-   Image: We recommend that you use a later version of a Linux public image provided by Alibaba Cloud, such as CentOS 7.4 64-bit, CentOS 7.3 64-bit, CentOS 7.2 64-bit, or Alibaba Cloud Linux 2.1903 64-bit.
-   Tool: We recommend that you use [fio](https://linux.die.net/man/1/fio).
-   Instance type: We recommend that you use ecs.g5se.18xlarge.
-   ESSD: We recommend that you use a PL3 ESSD. In this example, the device name of the ESSD is /dev/vdb. For more information, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).

    **Warning:** You can obtain accurate test results by testing raw disk partitions. However, you may destroy the file system structure in a raw disk partition if you test the partition directly. Before you test a raw disk, we recommend that you create a snapshot of the disk to back up your data. For more information about how to create a snapshot, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md). To prevent data loss, we recommend that you use a new ECS instance that contains no data for the test.


## Procedure

1.  Remotely connect to an ECS instance. For more information, see [Connect to a Linux instance by using VNC](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using VNC.md).

2.  Run the following commands in sequence to install the libaio and fio tools:

    ```
    sudo yum install libaio -y
    sudo yum install libaio-devel -y
    sudo yum install fio -y
    ```

3.  Switch the directory.

    ```
    cd /tmp
    ```

4.  Create the test100w.sh script.

    ```
    vim test100w.sh
    ```

5.  Paste the following snippet of code to the test100w.sh script:

    ```
    function RunFio
    {
     numjobs=$1   # The number of test threads. In this example, the value is 10.
     iodepth=$2   # The maximum number of concurrent I/O requests. In this example, the value is 64.
     bs=$3        # The size of the data block per I/O. In this example, the value is 4k.
     rw=$4        # The read and write policy. In this example, the value is randwrite.
     filename=$5  # The name of the file to be tested. In this example, the value is /dev/vdb.
     nr_cpus=`cat /proc/cpuinfo |grep "processor" |wc -l`
     if [ $nr_cpus -lt $numjobs ];then
         echo "Numjobs is more than cpu cores, exit!"
         exit -1
     fi
     let nu=$numjobs+1
     cpulist=""
     for ((i=1;i<10;i++))
     do
         list=`cat /sys/block/vdb/mq/*/cpu_list | awk '{if(i<=NF) print $i;}' i="$i" | tr -d ',' | tr '\n' ','`
         if [ -z $list ];then
             break
         fi
         cpulist=${cpulist}${list}
     done
     spincpu=`echo $cpulist | cut -d ',' -f 2-${nu}`
     echo $spincpu
     fio --ioengine=libaio --runtime=30s --numjobs=${numjobs} --iodepth=${iodepth} --bs=${bs} --rw=${rw} --filename=${filename} --time_based=1 --direct=1 --name=test --group_reporting --cpus_allowed=$spincpu --cpus_allowed_policy=split
    }
    echo 2 > /sys/block/vdb/queue/rq_affinity
    sleep 5
    RunFio 10 64 4k randwrite /dev/vdb
    ```

6.  Modify the parameter settings in the test100w.sh script based on your actual environment.

    -   Modify `vdb` based on the actual device name of the ESSD.
    -   Modify 10, 64, 4k, randwrite, and /dev/vdb in `RunFio 10 64 4k randwrite /dev/vdb`.
    -   If you want to proceed with this operation, set `filename` to a device name such as \[/dev/vdb\]. If you do not want to risk data loss, set `filename` to a file path such as \[/mnt/test.image\].
7.  Test the performance of the ESSD.

    ```
    sh test100w.sh
    ```

    If the `IOPS=***` result appears, the performance stress test for the ESSD is complete.

    ![Test the performance of the ESSD](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4182909951/p42181.png)


## Details of the test100w.sh script

-   In the script, the following command sets the `rq_affinity` parameter to 2:

    ```
    echo 2 > /sys/block/vdb/queue/rq_affinity
    ```

    |Value of rq\_affinity|Description|
    |---------------------|-----------|
    |1|Indicates that the block device delivers the received I/O completion events to the group of vCPUs that submit the corresponding I/O requests. In scenarios where multiple threads run concurrently, I/O completion events may be delivered only to one vCPU and cause a performance bottleneck.|
    |2|Indicates that the block device delivers the received I/O completion events to the vCPU that submits the corresponding I/O requests. In scenarios where multiple threads run concurrently, each vCPU can deliver its maximum performance.|

-   The following command runs `jobs` to bind queues to different CPU cores:

    ```
    fio -ioengine=libaio -runtime=30s -numjobs=${numjobs} -iodepth=${iodepth} -bs=${bs} -rw=${rw} -filename=${filename} -time_based=1 -direct=1 -name=test -group_reporting -cpus_allowed=$spincpu -cpus_allowed_policy=split
    ```

    **Note:** In normal mode, a device has a single request queue. This request queue becomes a performance bottleneck when multiple threads run concurrently to process I/O. In multi-queue mode, a device can have multiple request queues to process I/O and deliver the maximum backend storage performance. Assume that you have four I/O threads. To make full use of the multi-queue mode and improve storage performance, you must bind these threads to the CPU cores that correspond to different request queues.

    |Parameter|Description|Example|
    |---------|-----------|-------|
    |`numjobs`|The number of I/O threads.|10|
    |`/dev/vdb`|The device name of the ESSD.|/dev/vdb|
    |`cpus_allowed_policy`|The `cpus_allowed_policy` and `cpus_allowed` parameters provided by fio to bind vCPUs.|split|

    The preceding command runs `jobs` to bind queues to CPU cores. To view the ID of the CPU core to which a queue is bound, perform the following steps:

    -   Run the `ls /sys/block/vd*/mq/` command to view the ID of the queue for an ESSD whose device name is in the /dev/vd\* format.
    -   Run the `cat /sys/block/vd*/mq//cpu_list` command to view the ID of the CPU core to which the queue returned in the previous step is bound.

