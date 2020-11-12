# Enhance the monitoring of block I/O throttling

Alibaba Cloud Linux 2 provides interfaces in the 4.19.81-17.al7 kernel version and later to better monitor Linux block I/O throttling. This topic describes how to use the interfaces.

Linux block I/O throttling \(bit/s or IOPS\) is required in multiple scenarios, especially those where cgroup writeback is enabled. You can perform I/O throttling related operations in a more convenient manner if block I/O throttling is well monitored. In this context, Alibaba Cloud Linux 2 provides interfaces to enhance the monitoring of block I/O throttling.

## Interface description

|Interface|Description|
|---------|-----------|
|blkio.throttle.io\_service\_time|The total amount of time between request dispatch and request completion for I/O operations. Unit: nanoseconds.|
|blkio.throttle.io\_wait\_time|The total amount of time that the I/O operations wait in scheduler queues. Unit: nanoseconds.|
|blkio.throttle.io\_completed|The number of completed I/O operations. It is used to calculate the average latency of the block I/O throttling layer.|
|blkio.throttle.total\_io\_queued|The number of I/O operations that were throttled. The number of I/O operations that were throttled in the current cycle can be calculated based on periodic monitoring data and be used to analyze whether I/O latency is related to throttling.|
|blkio.throttle.total\_bytes\_queued|The total bytes of I/O that were throttled. Unit: bytes.|

The path of the preceding interfaces is /sys/fs/cgroup/blkio/<cgroup\>/, where `<cgroup>` is the control group.

## Example

You can obtain the average I/O latency of a disk by using the interface that enhances the monitoring of block I/O throttling. In this example, the average I/O write latency of the vdd disk is monitored at an interval of five seconds. Then, the average I/O latency of the vdd disk is calculated. The following table describes the relevant parameters.

|Parameter|Description|
|---------|-----------|
|write\_wait\_time<N\>|Obtains the duration of throttling at the block I/O throttling layer.|
|write\_service\_time<N\>|Obtains the total amount of time between request dispatch and request completion for I/O operations.|
|write\_completed<N\>|Obtains the number of completed I/O operations.|

1.  Obtain the monitoring data at the T1 time.

    ```
    write_wait_time1 = `cat /sys/fs/cgroup/blkio/blkcg1/blkio.throttle.io_wait_time | grep -w "254:48 Write" | awk '{print $3}'`
    write_service_time1 = `cat /sys/fs/cgroup/blkio/blkcg1/blkio.throttle.io_service_time | grep -w "254:48 Write" | awk '{print $3}'`
    write_completed1 = `cat /sys/fs/cgroup/blkio/blkcg1/blkio.throttle.io_completed | grep -w "254:48 Write" | awk '{print $3}'`
    ```

2.  Wait five seconds and obtain the monitoring data at the T2 \(T1 + 5s\) time.

    ```
    write_wait_time2 = `cat /sys/fs/cgroup/blkio/blkcg1/blkio.throttle.io_wait_time | grep -w "254:48 Write" | awk '{print $3}'`
    write_service_time2 = `cat /sys/fs/cgroup/blkio/blkcg1/blkio.throttle.io_service_time | grep -w "254:48 Write" | awk '{print $3}'`
    write_completed2 = `cat /sys/fs/cgroup/blkio/blkcg1/blkio.throttle.io_completed | grep -w "254:48 Write" | awk '{print $3}'`
    ```

3.  Calculate the average I/O latency during the five seconds based on the following formula:

    Average I/O latency = \(Total I/O duration at the T2 time - Total I/O duration at the T1 time\)/\(Number of completed I/O operations at the T2 time - Number of completed I/O operations at the T1 time\).

    ```
    avg_delay = `echo "((write_wait_time2 + write_service_time2) - (write_wait_time1+write_service_time1)) / (write_completed2 - write_completed1)" | bc`
    ```


