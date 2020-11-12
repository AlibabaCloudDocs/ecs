# Memcg global minimum watermark rating

This topic describes the memcg global minimum watermark rating feature provided by Alibaba Cloud Linux 2 kernel version `4.19.91-18.al7` and later.

Global memory reclaim has a great impact on system performance in Linux kernels. When latency-sensitive tasks and resource-consuming tasks are deployed together, resource-consuming tasks request a large amount of memory instantly, which causes the free memory of the system to reach the global minimum watermark \(global wmark\_min\). As a result, direct memory reclaim is enabled for all system tasks, which causes performance jitters for latency-sensitive tasks. Both global kswapd backend reclaim and memcg backend reclaim cannot resolve this problem.

In this case, Alibaba Cloud Linux 2 provides the memcg global minimum watermark rating feature. The global minimum watermark of resource-consuming tasks is increased to trigger direct memory reclaim. The global minimum watermark of latency-sensitive tasks is decreased to avoid direct memory reclaim. When a resource-consuming task requests a large amount of memory, an increase in the global minimum watermark throttles the resources used by the task for a short period to avoid direct memory reclaim for latency-sensitive tasks. After a certain amount of memory is reclaimed through global kswapd backend reclaim, the resource-consuming task is not throttled.

## Interface description

The interface that implements the memcg global minimum watermark rating feature is memory.wmark\_min\_adj. The value of this interface indicates the percent of adjustment over the global minimum watermark. Valid values: -25 to 50.

-   This interface inherits a value of 0 from its parent group when the interface is created. Therefore, the default value is 0.
-   A negative value is a percent of adjustment over the `[0, WMARK_MIN]` range, where `WMARK_MIN` is the value of global wmark\_min. Example:

    ```
    memory.wmark_min_adj=-25, memcg WMARK_MIN is "WMARK_MIN + (WMARK_MIN - 0) * (-25%)"
    ```

    **Note:** A negative value also indicates a decrease of the global minimum watermark. This can increase the memcg quality of service \(QoS\) of latency-sensitive tasks.

-   A positive value is a percent of adjustment over the `[WMARK_MIN, WMARK_LOW]` range, where `WMARK_MIN` and `WMARK_LOW` are values of global wmark\_min and global wmark\_low. Example:

    ```
    memory.wmark_min_adj=50, memcg WMARK_MIN is "WMARK_MIN + (WMARK_LOW - WMARK_MIN) * 50%"
    ```

    **Note:** A positive value also indicates an increase of the global minimum watermark. This can decrease the memcg QoS of resource-consuming tasks.

-   When the offset global minimum watermark is triggered, throttling is performed, and the throttling time is linearly proportional to the excessive memory usage. Valid values of the throttling time: 1 to 1000. Unit: ms.

**Note:** This interface file is not stored in the memcg root directory.

## Precautions

A multi-level memcg contains `effective memory.wmark_min_adj`, which is the final effective value of memory.wmark\_min\_adj. The values of memory.wmark\_min\_adj at all levels are traversed to obtain the maximum value. Intermediate nodes that have 0 as the default value are excluded. The following hierarchy provides an example:

```
         root
         / \
        A   D
       / \
      B   C
     / \
    E   F
```

The following table describes the mapping between the values of memory.wmark\_min\_adj at each level and the final effective value.

|Level|Value at each level|Final effective value|
|-----|-------------------|---------------------|
|A|-10|-10|
|B|-25|-10|
|C|0|0|
|D|50|50|
|E|-25|-10|
|F|50|50|

**Note:**

-   The value displayed in the output of the `cat /sys/fs/cgroup/memory/<Memcg path>/memory.wmark_min_adj` command is the final effective value. In the command, `<Memcg path>` indicates the root path of the memcg.
-   We recommend that you use the global minimum watermark rating feature together with global wmark\_min. For example, you can set global wmark\_min to 2 GB or more in /proc/sys/vm/min\_free\_kbytes.

## Configuration examples

Example 1: Configure global minimum watermark rating for the memcg of latency-sensitive tasks.

1.  Run the `mkdir /sys/fs/cgroup/memory/test-lc` command to create a test file.

2.  Run the `echo -25 > /sys/fs/cgroup/memory/test-lc/memory.wmark_min_adj` command to write the value of `-25` to the interface to increase the memcg QoS of latency-sensitive tasks.


Example 2: Configure global minimum watermark rating for the memcg of resource-consuming tasks.

1.  Run the `mkdir /sys/fs/cgroup/memory/test-be` command to create a test file.

2.  Run the `echo 25 > /sys/fs/cgroup/memory/test-be/memory.wmark_min_adj` command to write the value of `25` to the interface to decrease the memcg QoS of resource-consuming tasks.


