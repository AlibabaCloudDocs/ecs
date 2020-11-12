# Enable the PSI feature for cgroup v1

In the Linux kernel, only the cgroup v2 interface supports the Pressure Stall Information \(PSI\) feature. Alibaba Cloud Linux 2 supports the PSI feature for the cgroup v1 interface in the 4.19.81-17.al7 kernel version and later to allow you to monitor the CPU, memory, and I/O performance. This topic describes how to enable the PSI feature for the cgroup v1 interface and query relevant information.

PSI is a kernel feature that can be used to monitor the CPU, memory, and I/O performance. For more information about the PSI feature, see the `Documentation/accounting/psi.txt` kernel document. This kernel document is contained in the Debuginfo package and source code package of Alibaba CloudLinux 2. For information about how to download the Debuginfo package and source code package, see [Use Alibaba Cloud Linux 2](/intl.en-US/Images/Alibaba Cloud Linux 2/Overview.md).

## Enable the PSI feature for the cgroup v1 interface

By default, the PSI feature is disabled for the cgroup v1 interface. You can perform the following steps to enable the PSI feature:

1.  Run the `grubby` command to modify the startup parameter.

    The default value of the `args` parameter is `"psi=1"`, which indicates that the PSI feature is enabled for the cgroup v2 interface. Change the value of the parameter to `"psi=1 psi_v1=1"` to enable the PSI feature for the cgroup v1 interface. In this example, the kernel version is `4.19.81-17.al7.x86_64`. You must use your actual kernel version when you the operation. To query the kernel version, run the `uname -a` command.

    ```
    sudo grubby --update-kernel="/boot/vmlinuz-4.19.81-17.al7.x86_64" --args="psi=1 psi_v1=1"
    ```

2.  Restart the system to apply the change.

    ```
    sudo reboot
    ```


## Check whether the PSI feature is enabled for cgroup v1

After the system restarts, you can run the following command to check whether the PSI feature is enabled for the cgroup v1 interface in `/proc/cmdline` of the kernel:

```
cat /proc/cmdline | grep "psi=1 psi_v1=1"
```

## Query the monitoring data of the CPU, memory, and I/O performance

After the PSI feature is enabled for the cgroup v1 interface, this feature monitors the CPU, memory, and I/O performance and transmits all the monitoring data to the cpuacct controller. You can query detailed monitoring data by running the following commands:

```
cat /sys/fs/cgroup/cpuacct/cpu.pressure
cat /sys/fs/cgroup/cpuacct/memory.pressure
cat /sys/fs/cgroup/cpuacct/io.pressure
```

