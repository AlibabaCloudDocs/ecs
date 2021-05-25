---
keyword: [选择ESSD, 选择essd, 数据库高性能云盘, ecs]
---

# 压测ESSD云盘IOPS性能

压测ESSD云盘性能时，云盘本身以及压测条件都起着重要的作用。您可以按照本示例配置ESSD云盘性能的压测条件，充分发挥出多核多并发的系统性能，压测出100万IOPS的性能指标。

压测条件：

-   示例操作：随机写（randwrite）。
-   镜像：使用公共镜像中高版本的Linux镜像。例如，CentOS 7.4/7.3/7.2 64位和Alibaba Cloud Linux 2.1903 64位操作系统。
-   工具：使用[FIO](https://linux.die.net/man/1/fio)。
-   实例规格：推荐使用ecs.g5se.18xlarge。
-   ESSD云盘：推荐使用ESSD PL3云盘。本示例中，使用的设备名为/dev/your\_device，请您根据实际情况替换。更多详情，请参见[ESSD云盘](/intl.zh-CN/块存储/块存储介绍/ESSD云盘.md)。

    **警告：** 测试裸盘可以获得真实的块存储盘性能，但会破坏文件系统结构，请在测试前提前创建快照做好数据备份。具体操作，请参见[创建一个云盘快照](/intl.zh-CN/快照/使用快照/创建一个云盘快照.md)。建议您只在新购无数据的ECS实例上使用工具测试块存储性能，避免造成数据丢失。


## 操作步骤

1.  远程连接ECS实例。连接方式请参见[通过密码认证登录Linux实例](/intl.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。

2.  依次运行以下命令安装libaio和FIO。

    ```
    sudo yum install libaio -y
    sudo yum install libaio-devel -y
    sudo yum install fio -y
    ```

3.  切换路径。

    ```
    cd /tmp
    ```

4.  新建test100w.sh脚本。

    ```
    vim test100w.sh
    ```

5.  在test100w.sh中粘贴以下内容。

    ```
    function RunFio
    {
     numjobs=$1   # 实例中的测试线程数，例如示例中的10
     iodepth=$2   # 同时发出I/O数的上限，例如示例中的64
     bs=$3        # 单次I/O的块文件大小，例如示例中的4k
     rw=$4        # 测试时的读写策略，例如示例中的randwrite
     filename=$5  # 指定测试文件的名称，例如示例中的/dev/your_device
     nr_cpus=`cat /proc/cpuinfo |grep "processor" |wc -l`
     if [ $nr_cpus -lt $numjobs ];then
         echo “Numjobs is more than cpu cores, exit!”
         exit -1
     fi
     let nu=$numjobs+1
     cpulist=""
     for ((i=1;i<10;i++))
     do
         list=`cat /sys/block/your_device/mq/*/cpu_list | awk '{if(i<=NF) print $i;}' i="$i" | tr -d ',' | tr '\n' ','`
         if [ -z $list ];then
             break
         fi
         cpulist=${cpulist}${list}
     done
     spincpu=`echo $cpulist | cut -d ',' -f 2-${nu}`
     echo $spincpu
     fio --ioengine=libaio --runtime=30s --numjobs=${numjobs} --iodepth=${iodepth} --bs=${bs} --rw=${rw} --filename=${filename} --time_based=1 --direct=1 --name=test --group_reporting --cpus_allowed=$spincpu --cpus_allowed_policy=split
    }
    echo 2 > /sys/block/your_device/queue/rq_affinity
    sleep 5
    RunFio 10 64 4k randwrite /dev/your_device
    ```

6.  因测试环境而异，根据实际情况修改test100w.sh脚本。

    -   所有`your_device`。请将该值设置成ESSD云盘实际的设备名。
    -   `RunFio 10 64 4k randwrite /dev/your_device`中的10、64、4k、randwrite和/dev/your\_device。
    -   如果云盘上的数据丢失不影响业务，可以设置`filename=[设备名，例如/dev/vdb]`；否则，请设置为`filename=[具体的文件路径，例如/mnt/test.image]`。
7.  测试ESSD云盘性能。

    ```
    sh test100w.sh
    ```

    出现`IOPS=***`的结果时，表示ESSD云盘性能测试结束。

    ![测试ESSD云盘性能](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9563359951/p42181.png)


## test100w.sh脚本解读

-   以下命令将块设备的系统参数`rq_affinity`取值修改为2。

    ```
    echo 2 > /sys/block/your_device/queue/rq_affinity
    ```

    |rq\_affinity取值|取值说明|
    |--------------|----|
    |1|表示块设备收到I/O完成（I/O Completion）的事件时，这个I/O被发送回处理这个I/O下发流程的vCPU所在Group上处理。在多线程并发的情况下，I/O Completion就可能集中在某一个vCPU上执行，造成瓶颈，导致性能无法提升。|
    |2|表示块设备收到I/O Completion的事件时，这个I/O会在当初下发的vCPU上执行。在多线程并发的情况下，就可以完全充分发挥各个vCPU的性能。|

-   以下命令分别将几个`jobs`绑定不同的CPU Core上。

    ```
    fio -ioengine=libaio -runtime=30s -numjobs=${numjobs} -iodepth=${iodepth} -bs=${bs} -rw=${rw} -filename=${filename} -time_based=1 -direct=1 -name=test -group_reporting -cpus_allowed=$spincpu -cpus_allowed_policy=split
    ```

    **说明：** 普通模式下，一个设备（Device）只有一个请求队列（Request-Queue），在多线程并发处理I/O的情况下，这个唯一的Request-Queue就是一个性能瓶颈点。多队列（Multi-Queue）模式下，一个设备（Device）可以拥有多个处理I/O的Request-Queue，充分发挥后端存储的性能。假设您有4个I/O线程，您需要将4个I/O线程分别绑定在不同的Request-Queue对应的CPU Core上，这样就可以充分利用Multi-Queue提升性能。

    |参数|说明|取值示例|
    |--|--|----|
    |`numjobs`|I/O线程。|10|
    |`/dev/your_device`|ESSD云盘设备名。|/dev/vdb|
    |`cpus_allowed_policy`|FIO提供了参数`cpus_allowed_policy`以及`cpus_allowed`来绑定vCPU。|split|

    以上命令一共运行了几个`jobs`，分别绑定在几个CPU Core上，分别对应着不同的Queue\_Id。关于如何查看Queue\_Id绑定的cpu\_core\_id，您可以运行如下命令：

    -   运行`ls /sys/block/your_device/mq/`。其中，`your_device`是您的设备名，例如vdb。运行该命令查看设备名为vd\*云盘的Queue\_Id。
    -   运行`cat /sys/block/your_device/mq//cpu_list`。其中，`your_device`是您的设备名，例如vdb。运行该命令查看对应设备名为vd\*云盘的Queue\*绑定到的cpu\_core\_id。

