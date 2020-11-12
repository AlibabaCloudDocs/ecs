# Use the JBD2 optimization interface

JBD2 is the kernel thread of the ext4 file system. It often experiences the shadow \(BH\_Shadow\) state during its use, which can affect the system performance. To solve this problem, Alibaba Cloud Linux 2 provides an interface in the 4.19.81-17.al7 kernel version and later to optimize JBD2. This topic describes the interface.

ext4 is one of the most common journaling file systems. JBD2 is the kernel thread of ext4 for updating journals and a global resource for the ext4 file system. When the JBD2 kernel thread attempts to obtain access permissions from the cache, the cache page may be in the BH\_Shadow state. In this case, JBD2 waits an extended period of time for the cache page to write back to the disk, which can affect the system performance. To solve this problem, Alibaba Cloud Linux 2 provides the `force_copy` kernel interface to optimize JBD2. The system force copies the cache page to reduce the amount of time that JBD2 waits for the cache page in the BH\_Shadow state to write back to the disk. In addition, Alibaba Cloud Linux 2 provides the `stats` interface to help analyze quality of service \(QoS\) issues related to the file system.

## Interface description

|Interface|Description|
|---------|-----------|
|force\_copy|The interface file is stored in /proc/fs/jbd2/<device\>-8/force\_copy, where the `device` variable specifies the name of the block storage device. After you enable the force\_copy interface, the system force copies data, which reduces the waiting time of JBD2. **Note:** The interface consumes memory to run. |
|stats|The interface file is stored in /proc/fs/jbd2/<device\>-8/stats. The interface helps determine whether QoS issues in the file system are caused by JBD2.|

## Examples

The following examples demonstrate how to implement the `force_copy` and `stats` interfaces:

-   By default, the `force_copy` interface is disabled. You can set the value of the interface to 1 to enable the interface or set the value to 0 to disable the interface.

    ```
    echo 1 > /proc/fs/jbd2/nvme0n1-8/force_copy    # Call the interface.
    ```

-   Run the following command to query the `stats` interface:

    ```
    cat /proc/fs/jbd2/nvme0n1-8/stats
    ```

    A command output similar to the following one is returned:

    ```
    337 336 65536 0 14837 1701504 16 0 20058 5 33082732 605 942 1000 1000
    ```

    The following table describes the fields in the preceding sample output.

    |Field|Description|
    |-----|-----------|
    |The first field|The ID of the transaction.|
    |The second field|The number of transactions requested.|
    |The third field|The maximum number of cached transactions.|
    |The fourth field|The transaction wait time.|
    |The fifth field|The latency of the transaction request.|
    |The sixth field|The amount of time that the transaction ran.|
    |The seventh field|The amount of time that the transaction was locked.|
    |The eighth field|The amount of time that it took to refresh the transaction.|
    |The ninth field|The transaction logging time.|
    |The tenth field|The average transaction commit time.|
    |The eleventh field|The number of handles contained in the transaction.|
    |The twelfth field|The number of blocks contained in the transaction.|
    |The thirteenth field|The number of blocks recorded for the transaction.|
    |The fourteenth field|The time constant of the kernel configuration, in Hertz.|
    |The fifteenth field|The period of the time constant of the kernel configuration in milliseconds.|


