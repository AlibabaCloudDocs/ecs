# Enable the cgroup writeback feature

Alibaba Cloud Linux 2 supports the cgroup writeback feature for the cgroup v1 kernel interface in the 4.19.36-12.al7 kernel version and later. This feature allows you to limit the buffered I/O rate when you use the cgroup v1 kernel interface.

cgroups \(abbreviated from control groups\) are a Linux kernel mechanism that organizes processes hierarchically and distributes system resources along the hierarchy in a controlled and configurable manner. Two versions of cgroups are available: cgroup v1 and cgroup v2. For more information, visit [What are control groups](https://access.redhat.com/documentation/zh-cn/red_hat_enterprise_linux/7/html-single/resource_management_guide/index#sec-What_are_Control_Groups). This topic describes how to enable the cgroup writeback feature for cgroup v1 to limit the buffered I/O rate of processes.

## Limits

After you enable the cgroup writeback feature, check whether the mappings between memory subsystems \(memcgs\) and I/O subsystems \(blkcgs\) conform to the following rule. If the mappings conform to the rule, limit the buffered I/O rate of processes.

The cgroup writeback feature requires cooperation between memcgs and blkcgs to limit the buffered I/O rate. However, by default, the control subsystems of cgroup v1 do not work together. Memcgs and blkcgs must be associated based on the rule that each memcg is mapped to a unique blkcg. The mappings from memcgs to blkcgs can be one-to-one or many-to-one, but cannot be one-to-many or many-to-many.

For example, to limit the buffered I/O rate of Processes A and B, you must take note of the following items:

-   When A and B belong to two different memcgs, each of the memcgs can be mapped to a unique blkcg. For example, A belongs to `memcg1` and `blkcg1`, and B belongs to `memcg2` and `blkcg0`.
-   When A and B belong to two different memcgs, these memcgs can also be mapped to the same blkcg. For example, A belongs to `memcg1` and B belongs to `memcg2`, and both A and B belong to `blkcg2`.
-   When A and B belong to the same memcg, the memcg can be mapped only to one blkcg. For example, both A and B belong to `memcg0` and `blkcg3`.

To avoid exceptions, we recommend that you perform the following operations after you enable the cgroup writeback feature but before you limit the buffered I/O rate of a process: Configure the `cgroup.procs` interface for the corresponding blkcg, and write the ID of the process to the interface to ensure that the memcgs mapped to this blkcg are not mapped to any other blkcgs. You can also use a tool to view the mappings between memcgs and blkcgs. For more information, see [Verify the mappings from memcgs to blkcgs](#section_dm0_iub_dvr).

During O&M, processes may move to different cgroups. Based on the preceding rule, no exceptions occur if processes move between memcgs. However, If processes move between blkcgs, exceptions may occur. The following rule is defined in the code of the cgroup writeback feature to avoid exceptions: If a process in a running blkcg moves to a different blkcg, the memcg to which the process belongs is mapped to the root blkcg. Typically, no throttling threshold is set for the root blkcg. When the memcg is mapped to the root blkcg, the throttling feature no longer takes effect.

**Note:** Although the preceding rule is defined in the kernel code, we recommend that you do not move processes between blkcgs.

## Enable cgroup writeback

By default, the cgroup writeback feature is disabled for the cgroup v1 interface. To enable this feature, perform the following steps:

1.  Add the `cgwb_v1` field to the `grubby` command and run the command to enable the cgroup writeback feature.

    In this example, the kernel version is `4.19.36-12.al7.x86_64`. You must enter your actual kernel version during the operation. To query your kernel version, run the `uname -a` command.

    ```
    sudo grubby --update-kernel="/boot/vmlinuz-4.19.36-12.al7.x86_64" --args="cgwb_v1"
    ```

2.  Restart the system for the cgroup writeback feature to take effect.

    ```
    sudo reboot
    ```

3.  Run the following command to read the `/proc/cmdline` kernel file. Ensure that the parameters of the command include the `cgwb_v1` field. This way, the `blkio.throttle.write_bps_device` and `blkio.throttle.write_iops_device` interfaces in the corresponding blkcgs can limit the buffered I/O rate.

    ```
    cat /proc/cmdline | grep cgwb_v1
    ```


## Verify the mappings from memcgs to blkcgs

Before you limit the buffered I/O rate of processes, you can use one of the following methods to check whether the mappings from memcgs to blkcgs are one-to-one or many-to-one.

-   Run the following command to view the mappings from memcgs to blkcgs:

    ```
    sudo cat /sys/kernel/debug/bdi/bdi_wb_link
    ```

    The following sample response shows that the mapping from the memcg to the blkcg is one-to-one.

    ```
    memory     <--->     blkio
    memcg1:   35 <---> blkcg1:   48
    ```

-   Use the ftrace kernel monitoring tool.
    1.  Use the ftrace tool.

        ```
        sudo bash -c "echo 1 > /sys/kernel/debug/tracing/events/writeback/insert_memcg_blkcg_link/enable"
        ```

    2.  View the output information.

        ```
        sudo cat /sys/kernel/debug/tracing/trace_pipe
        ```

        The following sample response contains `memcg_ino=35 blkcg_ino=48`, which indicates that the mapping from the memcg to the blkcg is one-to-one.

        ```
        <... >-1537  [006] ....    99.511327: insert_memcg_blkcg_link: memcg_ino=35 blkcg_ino=48 old_blkcg_ino=0
        ```


## Check whether cgroup writeback takes effect

In this example, two processes that generate I/O are simulated to check whether the cgroup writeback feature takes effect.

**Note:**

-   The `dd` command responds quickly and the screen rolls too fast to be viewed. Run the `iostat` command to view the dd command output.
-   The `dd` command writes data in sequence. The system performs sequential I/O refreshing every time 1 MB of output data is generated. Therefore, you must set the threshold for `blkio.throttle.write_bps_device` to a value of no less than 1 MB \(1,048,576 bytes\). If you set the threshold for blkio.throttle.write\_bps\_device to a value of less than 1 MB, I/O hangs may occur.

1.  Simulate two processes that generate I/O, and set the `cgroup.procs` interface of the blkcg based on the preceding limits.

    ```
    sudo mkdir /sys/fs/cgroup/blkio/blkcg1
    sudo mkdir /sys/fs/cgroup/memory/memcg1
    sudo bash -c "echo $$ > /sys/fs/cgroup/blkio/blkcg1/cgroup.procs"    # $$ specifies the process ID.
    sudo bash -c "echo $$ > /sys/fs/cgroup/memory/memcg1/cgroup.procs"    # $$ specifies the process ID.
    ```

2.  Use the `blkio.throttle.write_bps_device` interface in the blkcg to limit the buffered I/O rate.

    ```
    sudo bash -c "echo 254:48 10485760 > /sys/fs/cgroup/blkio/blkcg1/blkio.throttle.write_bps_device"    # Set the writeback throttling threshold for the disk to 10 MB/s based on the device number.
    ```

3.  Use the `dd` command that does not have `oflag` set to sync to generate buffered I/O.

    ```
    sudo dd if=/dev/zero of=/mnt/vdd/testfile bs=4k count=10000
    ```

4.  Use the iostat tool to query the results. View the `wMB/s` column in the command output. If the value is 10 MB/s, the cgroup writeback feature takes effect.

    ```
    iostat -xdm 1 vdd
    ```


