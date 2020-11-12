# Memcg Exstat feature

This topic describes the Memcg Exstat \(Extend/Extra\) feature provided by Alibaba Cloud Linux 2 kernel version `4.19.91-18.al7` or later.

Compared with the Memcg Exstat feature provided by community versions of the Linux kernel, the Memcg Exstat feature that is available with the Alibaba Cloud Linux 2 kernel provides the following additional memcg statistical items:

-   Interfaces supported by the cgroup v1 interface: memory.events, memory.events.local, and memory.stat
-   Statistics on latency caused by changes in the global minimum watermark
-   Statistics on latency caused by backend asynchronous reclaim

## Features

Alibaba Cloud Linux 2 kernel features are implemented based on kernel interfaces. This topic describes the implementation methods for each feature.

|Feature|Description|
|-------|-----------|
|Statistics on memory events|The cgroup v2 interface of community versions of the Linux kernel supports the memory.events and memory.events.local interfaces to show the number of times that specific memory events have occurred in a memcg. For more information, visit [cgroup-v2.rst](https://www.kernel.org/doc/Documentation/admin-guide/cgroup-v2.rst).

The cgroup v1 interface of the Alibaba Cloud Linux 2 kernel supports the memory.events and memory.events.local interfaces.

**Note:** The interface files are not stored in the memcg root directory. |
|Statistics on memory workingsets|The cgroup v2 interface of community versions of the Linux kernel supports the memory.stat interface. The interface file contains the following statistical items: `workingset refault`, `workingset activate`, and `workingset nodereclaim`. For more information, visit [cgroup-v2.rst](https://www.kernel.org/doc/Documentation/admin-guide/cgroup-v2.rst).

The cgroup v1 interface of the Alibaba Cloud Linux 2 kernel supports the memory.stat interface. The interface file contains the following statistical items: `workingset refault`, `workingset activate`, `workingset nodereclaim`, and `workingset restore`. The following content is the official description of `workingset restore`:

```
+    workingset_restore
+    Number of restored pages which have been detected as an active
+    workingset before they got reclaimed.
``` |
|Statistics on latency caused by changes in the global minimum watermark|Alibaba Cloud Linux 2 provides the memcg global minimum watermark rating feature. For more information, see [Memcg global minimum watermark rating](/intl.en-US/Images/Alibaba Cloud Linux 2/Features and interfaces supported by Alibaba Cloud Linux 2/Memcg global minimum watermark rating.md).

Alibaba Cloud Linux 2 provides statistics on the time of throttling that results from the offset global minimum watermark specified in the memcg.exstat interface being exceeded. The statistical item is `wmark_min_throttled_ms`.

**Note:** This statistical item is recursive to the parent group, and the interface file is not stored in the memcg root directory.

Statistics description:

-   Interface file: memory.exstat
-   Statistical item: `wmark_min_throttled_ms`
-   Unit: ms |
|Statistics on latency caused by backend asynchronous reclaim|Alibaba Cloud Linux 2 provides the backend asynchronous reclaim feature memcg kswapd. For more information, see [Memcg backend asynchronous reclaim](/intl.en-US/Images/Alibaba Cloud Linux 2/Features and interfaces supported by Alibaba Cloud Linux 2/Memcg backend asynchronous reclaim.md).

Alibaba Cloud Linux 2 provides statistics on latency caused by backend asynchronous reclaim in the memcg.exstat interface. These statistics include the block time and actual working time of the reclaim. The statistical item is `wmark_reclaim_work_ms`.

**Note:** This statistical item is recursive to the parent group, and the interface file is not stored in the memcg root directory.

Statistics description:

-   Interface file: memory.exstat
-   Statistical item: `wmark_reclaim_work_ms`
-   Unit: ms |

## Examples

Create a test file at the /sys/fs/cgroup/memory mount point of the memcg. Make sure that the test file path contains the memory.events, memory.events.local, and memory.exstat interface files. You must also make sure that the memory.stat interface file contains the `workingset` statistical item.

1.  Run the following command to create a test file:

    ```
    mkdir /sys/fs/cgroup/memory/test
    ```

2.  Query the memory.events, memory.events.local, and memory.exstat interfaces.

    1.  Run the following command to query the memory.events interface:

        ```
        cat /sys/fs/cgroup/memory/test/memory.events
        ```

        Example output:

        ```
        low 0
        high 0
        max 0
        oom 0
        oom_kill 0
        ```

    2.  Run the following command to query the memory.events.local interface:

        ```
        cat /sys/fs/cgroup/memory/test/memory.events.local
        ```

        Example output:

        ```
        low 0
        high 0
        max 0
        oom 0
        oom_kill 0
        ```

    3.  Run the following command to query the memory.exstat interface:

        ```
        cat /sys/fs/cgroup/memory/test/memory.exstat
        ```

        Example output:

        ```
        wmark_min_throttled_ms 0
        wmark_reclaim_work_ms 0
        ```

3.  Run the following command to check whether the memory.stat interface file contains the `workingset` statistical item:

    ```
    cat /sys/fs/cgroup/memory/test/memory.stat | grep workingset
    ```

    A command output similar to the following one indicates that the interface file contains the `workingset` statistical item:

    ```
    workingset_refault 0
    workingset_activate 0
    workingset_restore 0
    workingset_nodereclaim 0
    total_workingset_refault 0
    total_workingset_activate 0
    total_workingset_restore 0
    total_workingset_nodereclaim 0
    ```


