# Detect I/O hangs of file systems and block layers

An I/O hang occurs when the system becomes unstable or even goes down due to time-consuming I/O requests. To accurately detect I/O hangs, Alibaba Cloud Linux 2 extends the core data structure and provides a feature to locate and detect I/O hangs at low system overheads. This topic describes the interfaces for this feature and the usage examples of these interfaces.

## Interface description

|Interface|Description|
|---------|-----------|
|/sys/block/<device\>/queue/hang\_threshold|The interface allows you to query and modify the threshold for I/O hangs. Unit of the threshold: ms. Default value: 5000.|
|/sys/block/<device\>/hang|The interface allows you to query the number of I/O operations that exceed the threshold for I/O hangs on the device.|
|/sys/kernel/debug/block/<device\>/rq\_hang|The interface allows you to query details about I/O hangs.|
|/proc/<pid\>/wait\_res|The interface allows you to query information about the resources for which the process is waiting.|
|/proc/<pid\>/task/<tid\>/wait\_res|The interface allows you to query information about the resources for which the thread is waiting.|

The following table describes variables in the preceding interfaces.

|Variable|Description|
|--------|-----------|
|<device\>|The name of the Elastic Block Storage \(EBS\) device.|
|<pid\>|The ID of the process.|
|<tid\>|The ID of the thread.|

## Example 1

You can call the `/sys/block/<device>/queue/hang_threshold` interface to modify the threshold for I/O hangs. In this example, the threshold is changed from 5,000 ms to 10,000 ms.

1.  Change the threshold for I/O hangs of the vdb disk to 10,000 ms.

    ```
    echo 10000 > /sys/block/vdb/queue/hang_threshold
    ```

2.  View the change result.

    ```
    cat /sys/block/vdb/queue/hang_threshold
    ```

    Example output:

    ```
    10000
    ```


## Example 2

You can call the `/sys/block/<device>/hang` interface to query the number of I/O operations that have I/O hangs on a disk. The vdb disk is used in this example.

The following command is used:

```
cat /sys/block/vdb/hang
```

Example output:

```
0        1     # The value on the left indicates the number of read operations that have I/O hangs. The value on the right indicates the number of write operations that have I/O hangs.
```

## Example 3

You can call the `/sys/kernel/debug/block/<device>/rq_hang` interface to query the details of I/O hangs. The vdb disk is used in this example.

The following command is used:

```
cat /sys/kernel/debug/block/vdb/rq_hang
```

Example output:

```
ffff9e50162fc600 {.op=WRITE, .cmd_flags=SYNC, .rq_flags=STARTED|ELVPRIV|IO_STAT|STATS, .state=in_flight, .tag=118, .internal_tag=67, .start_time_ns=1260981417094, .io_start_time_ns=1260981436160, .current_time=1268458297417, .bio = ffff9e4907c31c00, .bio_pages = { ffffc85960686740 }, .bio = ffff9e4907c31500, .bio_pages = { ffffc85960639000 }, .bio = ffff9e4907c30300, .bio_pages = { ffffc85960651700 }, .bio = ffff9e4907c31900, .bio_pages = { ffffc85960608b00 }}
```

The preceding output shows the details of an I/O operation. `io_start_time_ns` indicates the start time of the I/O request and this parameter has an assigned value. This indicates that the I/O request was not processed in a timely manner, which leads to prolonged I/O time.

## Example 4

You can call the `/proc/<pid>/wait_res` interface to query information about the resources for which a process is waiting. In this example, the `577` process is used.

The following command is used:

```
cat /proc/577/wait_res
```

Example output:

```
1 0000000000000000 4310058496 4310061448    # 1 is the value of Field 1, 0000000000000000 is the value of Field 2, 4310058496 is the value of Field 3, and 4310061448 is the value of Field 4.
```

The following table describes the parameters in the example output.

|Parameter|Description|
|---------|-----------|
|Field 1|The types of the resources for which the process is waiting. A value of 1 indicates the cache page in the file system. A value of 2 indicates the block I/O layer.|
|Field 2|The addresses of the resources \(cache page or block I/O layer\) for which the process is waiting.|
|Field 3|The time at which the process began waiting for resources.|
|Field 4|The current time when the file is being read. The difference between Field 4 and Field 3 is the amount of time taken by the process to wait for the resources.|

