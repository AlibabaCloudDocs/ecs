# Track I/O latency

Alibaba Cloud Linux 2 optimizes the `/proc/diskstats` raw data source interface of the I/O latency analysis tool iostat. Alibaba Cloud Linux 2 can calculate the amount of time taken by read, write, and special I/O \(discard\) operations on devices. In addition, Alibaba Cloud Linux 2 provides the bcc tool to track I/O latency. This topic describes the optimized `/proc/diskstats` interface and the bcc tool.

## Interface description

The /proc/diskstats interface in Alibaba Cloud Linux 2 allows you to query the I/O information on a disk and the amount of time taken by read, write, and discard operations on a device.

Example: Query the /proc/diskstats interface by using the root account.

```
cat /proc/diskstats
```

Example output:

```
254       0 vda 6328 3156 565378 2223 1610 424 25160 4366 0 1358 5332 0 0 0 0 2205 3347 0
```

In the output, the last three domains are new domains added in Alibaba Cloud Linux 2. The following table describes the three domains.

|Domain|Description|
|------|-----------|
|The sixteenth domain|The amount of time taken by read operations on the device. Unit: ms.|
|The seventeenth domain|The amount of time taken by write operations on the device. Unit: ms.|
|The eighteenth domain|The amount of time taken by discard operations on the device. Unit: ms.|

**Note:** For information about other domains, visit the kernel document `Documentation/iostats.txt`. You can obtain the kernel document from the Debuginfo package and source code package of Alibaba Cloud Linux 2. For more information, see [Use Alibaba Cloud Linux 2](/intl.en-US/Images/Alibaba Cloud Linux 2/Overview of Alibaba Cloud Linux 2.md).

## bcc

Alibaba Cloud Linux 2 provides the bcc tool to track I/O latency. You must download the tool before you can use it. Run the following command to download the tool:

```
yum install -y bcc-tools
```

You can run one of the following commands to query the description of the bcc tool:

-   Run the following command to query the description of the bcc tool:

    ```
    /usr/share/bcc/tools/alibiolatency -h
    ```

    Sample description:

    ```
    usage: alibiolatency [-h] [-d DEVICE] [-i [DIS_INTERVAL]]
                         [-t [AVG_THRESHOLD_TIME]] [-T [THRESHOLD_TIME]] [-r]
    
    Summarize block device I/O latency
    
    optional arguments:
      -h, --help            show this help message and exit
      -d DEVICE, --device DEVICE
                            inspect specified device
      -i [DIS_INTERVAL], --dis_interval [DIS_INTERVAL]
                            specify display interval
      -t [AVG_THRESHOLD_TIME], --avg_threshold_time [AVG_THRESHOLD_TIME]
                            display only when average request process time is
                            greater than this value
      -T [THRESHOLD_TIME], --threshold_time [THRESHOLD_TIME]
                            dump request life cycle when single request process
                            time is greater than this value
      -r, --dump_raw        dump every io request life cycle
    
    examples:
        ./alibiolatency          # summarize block I/O latency(default display interval is 2s)
        ./alibiolatency -d sda3  # inspect specified device /dev/sda3
        ./alibiolatency -i 2     # specify display interval, 2s
        ./alibiolatency -t 10    # display only when average request process time is greater than 10ms
        ./alibiolatency -T 20    # dump request life cycle when single request process time is greater than 20ms
        ./alibiolatency -r       # dump every io request life cycle
    ```

-   Run the `man` command to query the description of the bcc tool:

    ```
    man bcc-alibiolatency
    ```


