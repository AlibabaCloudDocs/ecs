# Memcg QoS feature of the cgroup v1 interface

The memory control group \(memcg\) quality of service \(QoS\) feature can be used to control locks and limits on memory usage in a memcg. In community versions of the Linux kernel, this feature is supported by only the `cgroup v2` interface. In Alibaba Cloud Linux 2 kernel version `4.19.91-18.al7` and later, this feature is also supported by the `cgroup v1` interface.

## Background

In the Alibaba Cloud Linux 2 kernel, the `memcg QoS` feature is enabled in the `cgroup v1` interface by default. For more information about `memcg QoS`, visit `Documentation/admin-guide/cgroup-v2.rst`. You can obtain the kernel document from the Debuginfo package and source code package of Alibaba Cloud Linux 2. For more information, see [Use Alibaba Cloud Linux 2](/intl.en-US/Images/Alibaba Cloud Linux 2/Overview of Alibaba Cloud Linux 2.md).

## Precautions

When you use the memcg QoS feature of the `cgroup v1` interface, we recommend that you place your tasks in a memcg leaf node such as /sys/fs/cgroup/memory/<intermediate node\>/<leaf node\>/tasks.

## Interface description

This section describes the interfaces that implement the memcg QoS feature of the `cgroup v1` interface in the Alibaba Cloud Linux 2 kernel.

|Interface|Description|
|---------|-----------|
|memory.min|Absolutely locks the memory. Memory locked by this interface cannot be reclaimed. You can perform the following read and write operations on this interface: -   Read the size of locked memory from this interface.
-   Write the size of locked memory to this interface. |
|memory.low|Relatively locks the memory. Memory locked by this interface may be partially reclaimed if the system has no other memory to reclaim. You can perform the following read and write operations on this interface: -   Read the size of locked memory from this interface.
-   Write the size of locked memory to this interface. |
|memory.high|Limits the memory usage. You can perform the following read and write operations on this interface: -   Read the usage limits on the memory from this interface.
-   Write the usage limits on the memory to this interface. |

## Examples

Create a test memcg in the memcg mount directory such as /sys/fs/cgroup/memory/. Make sure that the memcg contains the memory.min, memory.low, and memory.high interfaces.

Example command:

```
mkdir /sys/fs/cgroup/memory/test
ls /sys/fs/cgroup/memory/test | grep -E "memory.(min|low|high)"
```

Example output:

```
memory.high
memory.low
memory.min
```

