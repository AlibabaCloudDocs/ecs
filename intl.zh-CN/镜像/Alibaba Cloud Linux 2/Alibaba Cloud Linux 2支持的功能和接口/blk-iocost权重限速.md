# blk-iocost权重限速

Alibaba Cloud Linux 2在内核版本4.19.81-17.al7.x86\_64开始支持基于成本模型（cost model）的权重限速功能，即blk-iocost功能。该功能是对内核中IO子系统（blkcg）基于权重的磁盘限速功能的进一步完善，在Alibaba Cloud Linux 2内核中，该功能同时支持cgroup v1和v2接口。本文主要介绍实现该功能的接口。

## 接口说明

|接口|描述|配置项说明|
|--|--|-----|
|cost.qos|可读可写接口，接口文件只存在于blkcg根组。在cgroup v1中，该接口文件完整名称为`blkio.cost.qos`，在cgroup v2中，该接口文件完整名称为`io.cost.qos`。该接口主要实现blk-iocost功能以及基于延迟（latency）权重限制I/O服务质量（Qos）的速率。

当实现blk-iocost功能之后，内核按延迟数值统计以下比例：超过读写延迟`rlat|wlat`的请求占所有请求的比例。当该比例超过读写延迟百分比`rpct|wpct`时，内核认为设备达到饱和状态，会降低往磁盘发送请求的速率。默认情况下，`rlat|wlat`的值为0，表示该功能未启用。

|每行配置以设备的Major号和Minor号开头（格式为`MAJ:MIN`），后边衔接其他配置项，说明如下。 -   enable：是否开启blk-iocost controller，即开启blk-iocost功能。默认值0为关闭状态，修改值为1时开启功能。
-   ctrl：控制模式，可选值为`auto`或者`user`。使用`auto`时，内核自动探测设备类型并使用内置参数；使用`user`，则需要输入以下QoS控制参数。
-   rpct：读延迟百分比，取值范围为\[0,100\]。
-   rlat：读延迟，单位为us。
-   wpct：写延迟百分比，取值范围为\[0,100\]。
-   wlat：写延迟，单位为us。
-   min：最小速率调整比例，取值范围为\[1,10000\]。
-   max：最大速率调整比例，取值范围为\[1,10000\]。 |
|cost.model|可读可写接口，只存在于blkcg根组。在cgroup v1中，该接口文件完整名称为`blkio.cost.model`，在cgroup v2中，该接口文件完整名称为`io.cost.model`。该接口用于设置成本模型（cost model）。|每行配置以设备的Major号和Minor号开头（格式为`MAJ:MIN`），后边衔接其他配置项，说明如下。 -   ctrl：控制模式，可选值为`auto`或`user`，表示是否使用用户输入模型参数。
-   model：模型参数，当前只实现了一种模型`linear`。当模型参数为`linear`时，定义如下建模参数。

    -   \[r\|w\]bps：最大顺序IO带宽。
    -   \[r\|w\]seqiops：顺序 IOPS（Input/Output Operations Per Second）。
    -   \[r\|w\]randiops：随机 IOPS（Input/Output Operations Per Second）。
**说明：** 以上参数可以使用内核源码中的tools/cgroup/iocost\_coef\_gen.py脚本来生成，然后写入cost.model接口文件内设置成本模型。 |
|cost.weight|可读可写接口，只存在blkcg的子组中。在cgroup v1中，该接口文件完整名称为`blkio.cost.weight`，在cgroup v2中，该接口文件完整名称为`io.cost.weight`。该接口用于配置子组的权重，范围为\[1,10000\]，默认值为100。该接口可以为每个设备配置权重，也可以修改该整个子组的默认权重。|-   为接口设置权重值`<weight>`：表示修改blkcg的默认权重。
-   为接口设置端口号和权重值`MAJ:MIN <weight>`：表示修改设备上的blkcg的权重。 |

## 注意事项

在ECS实例中使用blk-iocost功能启动`ctrl=auto`配置项时，如果对应的云盘为高效云盘、SSD云盘、ESSD云盘或NVMe SSD本地盘类型时，需要手动将对应磁盘的`rotational`属性设置为0。

```
echo 0 > /sys/block/[$DISK_NAME]/queue/rotational    #[$DISK_NAME]为磁盘名称
```

## 示例一

使用cost.qos接口为设备`254：48`开启blk-iocost功能，并且当读写延迟`rlat|wlat`的请求有95%超过5 ms时，认为磁盘饱和。内核将进行磁盘发送请求速率的调整，调整区间为最低降至原速率的50%，最高升至原速率的150%。cgroup v1接口和cgroup v2接口命令分别如下。

-   cgroup v1 接口。

    ```
    echo "254:48 enable=1 ctrl=user rpct=95.00 rlat=5000 wpct=95.00 wlat=5000 min=50.00 max=150.00" > /sys/fs/cgroup/blkio/blkio.cost.qos
    ```

-   cgroup v2接口。

    ```
    echo "254:48 enable=1 ctrl=user rpct=95.00 rlat=5000 wpct=95.00 wlat=5000 min=50.00 max=150.00" > /sys/fs/cgroup/io.cost.qos
    ```


## 示例二

使用`cost.model`在设备`254：48`上使用用户输入的`linear`建模参数设置模型。cgroup v1接口和cgroup v2接口命令分别如下。

-   cgroup v1接口。

    ```
    echo "254:48 ctrl=user model=linear rbps=2706339840 rseqiops=89698 rrandiops=110036 wbps=1063126016 wseqiops=135560 wrandiops=130734" > /sys/fs/cgroup/blkio/blkio.cost.model
    ```

-   cgroup v2接口。

    ```
    echo "254:48 ctrl=user model=linear rbps=2706339840 rseqiops=89698 rrandiops=110036 wbps=1063126016 wseqiops=135560 wrandiops=130734" > /sys/fs/cgroup/io.cost.model
    ```


## 示例三

使用`cost.weight`接口将blkcg1的默认权重修改为50，然后设置blkcg1在设备`254:48`上的权重为50，cgroup v1接口和cgroup v2接口命令分别如下。

-   cgroup v1接口。

    ```
    echo "50" > /sys/fs/cgroup/blkio/blkcg1/blkio.cost.weight    # 将默认权重修改为50
    echo "254:48 50" > /sys/fs/cgroup/blkio/blkcg1/blkio.cost.weight    #将设备上的权重设置为50
    ```

-   cgroup v2接口。

    ```
    echo "50" > /sys/fs/cgroup/cg1/io.cost.weight    # 将默认权重修改为50
    echo "254:48 50" > /sys/fs/cgroup/cg1/io.cost.weight    #将设备上的权重设置为50
    ```


## 常用监测工具

-   iocost monitor脚本

    内核源码中的`tools/cgroup/iocost_monitor.py`脚本基于drgn调试器直接获取内核参数进行IO性能数据的监控输出。关于drgn的详情请参见[drgn](https://github.com/osandov/drgn)。脚本使用方式如下。

    执行以下命令监测磁盘vdd的IO性能数据。

    ```
    ./iocost_monitor.py vdd
    ```

    返回结果示例如下。

    ```
    vdd RUN  per=500.0ms cur_per=3930.839:v14620.321 busy= +1 vrate=6136.22% params=hdd
                              active    weight      hweight% inflt% dbt  delay usages%
    blkcg1                       *    50/   50   9.09/  9.09   0.00   0  0*000 009:009:009
    blkcg2                       *   500/  500  90.91/ 90.91   0.00   0  0*000 089:091:092
    ```

-   cgroup v1接口下的blkio.cost.statcost.stat接口

    Alibaba Cloud Linux 2内核提供了在cgroup v1接口下的blk-iocost统计接口，该接口文件中记录了每个受控制的设备的QoS数据。查看该接口文档的命令如下。

    ```
    cat /sys/fs/cgroup/blkio/blkcg1/blkio.cost.stat
    ```

    返回结果示例如下。

    ```
    254:48 is_active=1 active=50 inuse=50 hweight_active=5957 hweight_inuse=5957 vrate=159571
    ```

-   ftrace监测工具

    Alibaba Cloud Linux 2内核提供了blk-iocost相关的ftrace工具，您可以进行内核侧的分析。使用方式如下。

    1.  将`enable`属性设置为1，开启ftrace工具。

        ```
        echo 1 > /sys/kernel/debug/tracing/events/iocost/enable
        ```

    2.  查看信息输出接口。

        ```
        cat /sys/kernel/debug/tracing/trace_pipe
        ```

        返回结果示例如下。

        ```
            dd-1593  [008] d...   688.565349: iocost_iocg_activate: [vdd:/blkcg1] now=689065289:57986587662878 vrate=137438 period=22->22 vtime=0->57986365150756 weight=50/50 hweight=65536/65536
            dd-1593  [008] d.s.   688.575374: iocost_ioc_vrate_adj: [vdd] vrate=137438->137438 busy=0 missed_ppm=0:0 rq_wait_pct=0 lagging=1 shortages=0 surpluses=1
        <idle>-0     [008] d.s.   688.608369: iocost_ioc_vrate_adj: [vdd] vrate=137438->137438 busy=0 missed_ppm=0:0 rq_wait_pct=0 lagging=1 shortages=0 surpluses=1
            dd-1594  [006] d...   688.620002: iocost_iocg_activate: [vdd:/blkcg2] now=689119946:57994099611644 vrate=137438 period=22->26 vtime=0->57993412421644 weight=250/250 hweight=65536/65536
        <idle>-0     [008] d.s.   688.631367: iocost_ioc_vrate_adj: [vdd] vrate=137438->137438 busy=0 missed_ppm=0:0 rq_wait_pct=0 lagging=1 shortages=0 surpluses=1
        <idle>-0     [008] d.s.   688.642368: iocost_ioc_vrate_adj: [vdd] vrate=137438->137438 busy=0 missed_ppm=0:0 rq_wait_pct=0 lagging=1 shortages=0 surpluses=1
        <idle>-0     [008] d.s.   688.653366: iocost_ioc_vrate_adj: [vdd] vrate=137438->137438 busy=0 missed_ppm=0:0 rq_wait_pct=0 lagging=1 shortages=0 surpluses=1
        <idle>-0     [008] d.s.   688.664366: iocost_ioc_vrate_adj: [vdd] vrate=137438->137438 busy=0 missed_ppm=0:0 rq_wait_pct=0 lagging=1 shortages=0 surpluses=1
        ```


